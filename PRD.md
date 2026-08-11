# **School Management SaaS – Product Requirement Document (v2 – Corrected)**

> **Version 2** incorporates corrections from `ARCHITECTURE.md` (same folder). Product behavior is unchanged; the technical architecture, data model, security, and cost plan have been corrected. Supersedes v1.

---

# **1. Product Overview**

A cloud-based, multi-tenant School Management System (LMS) designed for individual schools. It offers three portals: **Admin**, **Teacher**, and **Parent**. The system handles academic sessions, class organisation, student enrolment, staff assignment, fee management, daily attendance, marks/assessments, a student diary, and a timetable. It also provides a precise promotion/demotion/repeat workflow when a session ends.

The product is built as a **SaaS** application. Each school’s data is completely isolated using a **single shared database** with a `school_id` column and **Row-Level Security (RLS)** enforced on every table.

---

# **2. Technical Architecture (Summary)**

| Aspect | Choice | Note |
|---|---|---|
| **Frontend** | Next.js 14 (App Router), React Server Components, Client Components | RSC moves queries server-side (fewer round trips, cheaper) |
| **Styling** | Tailwind CSS – minimal white-toned design, built from scratch | Unchanged |
| **Backend** | Next.js Server Actions + Postgres RPC functions (SECURITY DEFINER) for multi-step operations | Multi-row writes are single DB transactions |
| **Database** | Supabase (PostgreSQL) – **single project**, multi-tenant via `school_id` + RLS | One shared DB = lowest cost + strongest isolation |
| **Authentication** | **Supabase Auth** (email + password) — replaces NextAuth v5 | **v2 correction:** NextAuth JWTs are incompatible with Supabase RLS; one identity source is required |
| **Login format** | `role@schoolSlug` (e.g., `admin@schoolA`, `emp@schoolA`, `reg@schoolA`) stored as the auth email; school derived from the login id itself | No subdomain required (unchanged) |
| **Hosting** | **Vercel Pro** with Supabase connection pooling (Supavisor) | v2 correction: Hobby plan is non-commercial by ToS; Pro required once schools pay |
| **Data fetching** | TanStack Query with **polling + caching** (30–60 s intervals, refetch on focus/mutation) | v2 correction: **no Supabase Realtime** (billed per message; polling is free) |
| **Server cache** | Vercel data cache (`unstable_cache`, 60 s TTL keyed by school) for dashboards/aggregates | Absorbs the evening parent/teacher burst without touching the DB |
| **Audit & Logs** | `audit_logs` table **written by DB triggers** (unskippable), exportable to Excel/CSV | v2 correction: app-level logging can be bypassed |
| **Backups** | Nightly `pg_dump` → Backblaze B2 (encrypted); Pro tier adds Supabase daily backups | v2 addition: Supabase Free tier has **no backups** |
| **Monitoring** | Sentry (errors), UptimeRobot (uptime), Supabase/Vercel usage dashboards | v2 addition |
| **CI/CD** | GitHub Actions + Vercel Git integration; SQL migrations in repo | v2 addition |

**v2 decision rationale (from ARCHITECTURE.md):** NextAuth v5 signs its own JWT, which Supabase RLS cannot read — the only safe designs are (a) Supabase Auth as the single identity source (chosen), or (b) NextAuth with all DB access via server code plus session-variable RLS (rejected: more plumbing, same result). Supabase Auth is free (50k MAU), rate-limited by default, and puts `role` + `school_id` into JWT claims that RLS reads directly.

---

# **3. Multi-Tenancy & Data Isolation**

- One database for all schools. Every table contains a `school_id` column and `school_id` is part of every relevant index.
- **RLS is enabled on every table.** Every policy begins with the school-scope clause reading the `school_id` claim from the JWT — no subquery, unspoofable.
- Role-based policy families (applied to every table):
  - **Admin** → all rows of their school.
  - **Teacher** → rows of classes they teach / are incharge of (via `teacher_assignments`, `class_incharge_teacher_id`).
  - **Parent** → rows of their own child only (via `parent_users`).
- The login ID determines the school: everything after `@` is the school slug (e.g., `schoolA`), used to look up `school_id`. Because the slug is embedded in the login id, ids are globally unique across the whole SaaS.
- The `service_role` key is **server-side only** (never in the client bundle). Browsers use only the anon key — authorization happens in RLS, so a leaked key cannot cross schools.
- RLS must never be disabled to "fix" a slow query; slow queries are fixed with indexes/caching.

---

# **4. Core Entities & Concepts**

# **4.1 Session**

- A session represents an academic year (e.g., 2025-2026).
- Created by the Admin.
- Can be **active** or **archived** (once all its classes are archived).
- Archived sessions are **read-only at the database level** (a trigger rejects any write referencing an archived session). Parents never see archived data; admins use it for record-keeping.

# **4.2 Class**

- Belongs to a session.
- Has a name and a section (e.g., 9th, A).
- Each class has a unique set of **subjects** (per class per session).
- Has one **class incharge** (a teacher), optional at creation time.
- Can be **archived** after all its active students have been promoted/demoted/repeated.
- Uniqueness per school: one class per (session, name, section).

# **4.3 Subjects**

- Defined **per class per session** (subject rows carry an explicit `session_id`). Even if two classes have a subject with the same name (e.g., "Physics"), they are separate records.
- This avoids cross-class entanglement and gives complete flexibility.

# **4.4 Students**

- Personal data in `students`; **class membership lives in `enrollments`** (student ↔ class ↔ session), so every transfer/promotion leaves a full history. **v2 correction:** the previous `current_class_id` approach destroyed history.
- Have a **roll number** (registration ID) assigned by Admin; unique per school. One parent login per child uses the roll number.
- Statuses:
  - **Active** – normal student.
  - **Left** – left the school (soft-deleted, no attendance/marks, greyed out in history).
  - **Suspended** – temporarily barred (like left).
  - **Fee Not Paid** – still active, but a pop-up reminder appears on parent login; portal fully functional.
  - **Fee Defaulter** – manually flagged by Admin; parent portal completely blocked with a warning overlay.
- A student can be **transferred** to another class within the same session (attendance carries over; marks may be updated by the new teacher). Transfer is a single transactional RPC — the DB enforces one class per student per session.

# **4.5 Teachers**

- Added by Admin with an employee ID (`emp_id`) and password.
- Assigned to teach specific subjects to specific classes in a session (`teacher_assignments`).
- Can be designated as **class incharge** of a class (one teacher per class).
- If a teacher leaves, they are soft-deleted (historical records remain untouched; new class incharge takes over future attendance).

# **4.6 Fee Management**

- **Batch Fee Voucher** – Admin issues a fee voucher for all active students of a class for a given month. Includes base tuition fee plus any class-wide extra charges.
- **Individual Edits** – After batch issuance, Admin can edit a student's voucher amount (discounts, kinship waiver, extra charges). This is the only way to apply sibling discounts or custom fines.
- **Fine Voucher** – Admin can issue an individual fine voucher to a specific student at any time. Additional voucher, unlimited.
- **Rule (DB-enforced):** only **one batch fee voucher per class per month** — enforced by a partial unique index on `(school_id, class_id, session_id, month_year) WHERE type = 'batch'`. Fine vouchers unlimited.
- **Payment Recording** – No online payment gateway. Admin manually records payments (cash/cheque/bank). A parent can pay an arbitrary amount.
  - Each payment is a row in `fee_payments`; a **DB trigger recomputes `paid_amount`** on the voucher — no race conditions, no double-counting (v2 fix).
  - Status is a **generated column**: Unpaid → Partially Paid → Fully Paid (derived from amounts; cannot drift).
- **Fee Defaulter Flag** – distinct from "Fee Not Paid". Admin must manually set a student as fee defaulter to block the parent portal; "Fee Not Paid" only shows a dismissible pop-up.

# **4.7 Attendance**

- Marked daily by the **class incharge** for their assigned class, as **one batch UPSERT** (whole class in a single statement — atomic, idempotent, no duplicates).
- Duplicate marking is impossible: `UNIQUE (student_id, session_id, date)`.
- Visible to: Admin (all classes), class incharge (own class), Parent (own child only). No other teacher can view or modify.
- Students with status Left/Suspended are excluded from the marking roster.

# **4.8 Marks (Quizzes / Assignments / Assessments)**

- Teachers create a **Marks Entry** for a subject they teach to a specific class (name + total marks), then enter marks for each active student.
- Marks can be **edited after submission**; **every change is written to `audit_logs` by a DB trigger** (unskippable — v2 fix).
- Teachers see the whole class's marks for that entry (sorted by roll number + name). Parents see **only their child's** marks.
- Left/Suspended students are not listed for new entries; historical marks remain visible (read-only) in past entries.
- Uniqueness per entry per student: `UNIQUE (marks_entry_id, student_id)`.

# **4.9 Diary**

- A teacher writes a diary entry for a **subject they teach to a specific class**, on a specific date.
- Parent portal shows diary of all subjects for the most recent date that has at least one entry, then previous dates descending. Subjects without an entry on a date are omitted; blank dates are hidden.
- Old entries can be collapsed/expanded.

# **4.10 Timetable**

- Set **per class** as a weekly schedule (Mon–Fri, optionally Saturday). Each entry: day, start time, end time, subject, teacher.
- Conflicts prevented: one slot per class per day (`UNIQUE (class_id, day_of_week, start_time)`) + app-level teacher double-booking check.
- Teacher portal shows a consolidated timetable (all classes taught). Parent portal shows the child's class timetable.

# **4.11 Promotion, Demotion, Repeat & Transfer**

- **Promotion** – move a student to a higher class in a **new** session.
- **Demotion** – move a student to a lower class in a **new** session.
- **Repeat** – move a student to the same class (or different section) in a **new** session.
- **Transfer** – move a student to a different class **within the same session** (attendance carries over; marks can be updated by the new teacher).
- All operations are **one student at a time** and run as **a single DB transaction (RPC)** — if anything fails, nothing changes (v2 fix: previously a sequence of app-level writes could partially fail and lose a student).
- The **fee check happens inside the transaction** with a row lock on the student's vouchers: promotion/demotion/repeat is only allowed if every voucher of the current session is fully paid. Outstanding fees → error.
- Left/Suspended students are ignored; they stay in the old session records.
- After all active students of a class are moved, the **class is archived**. When all classes of a session are archived, the **session is archived** (writes to archived data are rejected by a DB trigger).
- Archived session data is read-only for administrative reference; parents cannot access previous sessions.

---

# **5. Portal Descriptions**

# **5.1 Admin Portal**

**Dashboard** – Quick stats (active students, teachers, fee collection status, recent logs). Aggregates served from a 60 s server-side cache; numbers are recomputed on every mutation.

# **Sessions**
- Create / list sessions. Archive a session (only when all classes inside are archived).

# **Classes**
- Create classes under a session (name, section). Assign a class incharge later.
- Edit subjects for the class (add/remove). View students enrolled. Archive class after all active students are moved.

# **Subjects**
- Defined per class per session. No global subject pool.

# **Students**
- Enroll a student (assign roll number, class, session, parent password). View/edit profile; change status (Active, Left, Suspended, Fee Not Paid, Fee Defaulter).
- Transfer to another class in the same session.
- Promote / Demote / Repeat to a new session (fee check enforced by the DB transaction).
- Issue fee vouchers (batch per class per month — DB-enforced one-per-class-per-month), edit individual vouchers, record manual payments (cash/cheque/bank), view payment history with paid/partial/unpaid filters.

# **Teachers**
- Add teacher (emp_id, password, name). Assign teacher to subject(s) of specific classes. Mark teacher as left (soft-delete). Set class incharge.

# **Timetable**
- Create weekly schedule per class (day, time, subject, teacher). Conflict-checked.

# **Attendance** (view only) / **Marks** (view only, incl. edit logs) / **Diary** (view only, filterable)

# **Logs**
- Full audit trail of all critical actions (promotion, fee changes, marks edits, status changes, logins, etc.) — written by DB triggers.
- Export to Excel/CSV (client-side generation for < 10k rows; streaming CSV beyond).

# **Fee Defaulter Management**
- Manually flag/unflag a student as fee defaulter → blocks/restores parent portal.

# **5.2 Teacher Portal**

**Dashboard** – Today's timetable (consolidated across all classes taught), quick links to mark attendance and write diary.

# **Attendance** (only if class incharge)
- Mark attendance for their class (present/absent/late) for the current date — one batch save for the whole roster. View own class history (read-only). Cannot see other classes.

# **Marks**
- Create a marks entry (quiz/assignment) for a subject they teach, for a specific class. Enter/edit marks per active student. All edits audited automatically. Class-wide view of past entries.

# **Diary**
- Write a diary entry for a subject they teach, for a specific class and date. View/edit previous entries (with logs).

# **Timetable**
- Personal weekly teaching schedule (all classes, times, subjects).

# **5.3 Parent Portal**

**Login** – Uses student's roll number (e.g., `reg@schoolA`) and password set by Admin. **One login per child** — a parent with two children has two separate logins. No unified family account (schema allows adding it later without migration).

# **Dashboard**
- Today's diary, latest fee status, recent attendance.

# **Diary**
- Entries for the child's class, grouped by date (most recent first); only dates with entries appear; subjects without an entry are omitted.

# **Fee**
- All vouchers (batch and fines) for the current session: total, paid, remaining, status. Payment history visible.
- Fee Defaulter → entire portal blocked by overlay: "FEE DEFAULTER. CONTACT SCHOOL".

# **Attendance / Timetable**
- Own child's attendance record (monthly view). Child's class weekly timetable.

**Note:** No access to other students' marks/attendance; no diary-writing; no teacher/admin functions.

---

# **6. Business Rules Summary (DB-Enforced)**

| Rule | Enforcement level |
|---|---|
| **Class Incharge** – only the assigned class incharge can mark/see attendance for that class | RLS policy (subquery on `class_incharge_teacher_id`) |
| **Fee & Promotion** – student must have all vouchers fully paid before promote/demote/repeat; system errors otherwise | Inside the promotion RPC transaction, with row locks on vouchers |
| **One Batch Voucher/Month** – one batch fee voucher per class per month; individual/fine vouchers unlimited | Partial unique index on `fee_vouchers` |
| **Fee Defaulter vs Fee Not Paid** – "Not Paid" = dismissible pop-up; "Defaulter" = full portal block | App + RLS-driven overlay; flag stored on student |
| **Marks Editing Logs** – every marks edit recorded in `audit_logs` | DB trigger on `marks_records` (unskippable) |
| **Session Archival** – session archives only when all classes archived; class archives only when all active students moved | App workflow + DB trigger blocks writes to archived sessions |
| **Transfer (same session)** – attendance rolls over; marks optionally filled by new teacher | Transactional RPC; `UNIQUE (student_id, session_id)` guarantees one class |
| **Attendance Duplication** – impossible | `UNIQUE (student_id, session_id, date)` |
| **Parent Access** – one login per child; no "forgot password" (admin resets); parents see only their child | RLS via `parent_users`; reset via admin-only RPC (audited) |
| **Data Visibility** – teachers see only classes they teach; admin sees all (own school) | RLS policy families per role (§3) |
| **School Isolation** – no cross-school access ever | `school_id` JWT claim on every RLS policy + school-scoped indexes |
| **Soft Delete** – deleted entities remain read-only; history preserved | `status`/`is_active` flags; `enrollments` history table |

---

# **7. Database Schema (Corrected)**

Every table includes `school_id`, `created_at`, `updated_at`. Key constraints listed inline. Full DDL and RLS policies: see `ARCHITECTURE.md` §5–6.

- **schools** – `id`, `name`, `slug` (unique), `address`, `status`, timestamps
- **users** – `id` (= `auth.users.id`), `school_id`, `role` (admin/teacher/parent), `login_id` (unique, e.g. `admin@schoolA`), `is_active`. Role + school_id mirrored into `app_metadata` → JWT claims
- **teachers** – `id`, `user_id`, `name`, `emp_id` (unique per school), `status`
- **students** – `id`, `user_id`, `name`, `roll_number` (unique per school), `status` (active/left/suspended/fee_not_paid/fee_defaulter), guardian info
- **parent_users** – `id`, `user_id`, `student_id` (login = roll number). One login per child; table allows multi-child later
- **sessions** – `id`, `name` (unique per school), `status` (active/archived)
- **classes** – `id`, `session_id`, `name`, `section`, `class_incharge_teacher_id` (nullable), `status`; unique (session, name, section) per school
- **subjects** – `id`, `class_id`, `session_id`, `name` (per class per session, as per PRD)
- **enrollments** – `id`, `student_id`, `session_id`, `class_id`, `status` (active/left/transferred/promoted/demoted/repeated), `joined_on`, `left_on`; **`UNIQUE (student_id, session_id)`** — full membership history; current class = active enrollment
- **teacher_assignments** – `id`, `teacher_id`, `subject_id`, `class_id`, `session_id`
- **timetable_entries** – `id`, `class_id`, `day_of_week`, `start_time`, `end_time`, `subject_id`, `teacher_id`; `UNIQUE (class_id, day_of_week, start_time)`; teacher-conflict check
- **attendance** – `id`, `student_id`, `class_id`, `session_id`, `date`, `status` (present/absent/late), `marked_by_teacher_id`; **`UNIQUE (student_id, session_id, date)`**; index `(school_id, class_id, date)`
- **marks_entries** – `id`, `subject_id`, `class_id`, `session_id`, `name`, `total_marks`, `created_by_teacher_id`, `date`
- **marks_records** – `id`, `marks_entry_id`, `student_id`, `marks_obtained`; **`UNIQUE (marks_entry_id, student_id)`**; audit trigger on write
- **diary_entries** – `id`, `subject_id`, `class_id`, `session_id`, `teacher_id`, `date`, `content`
- **fee_vouchers** – `id`, `student_id`, `class_id` (v2 addition), `session_id`, `type` (batch/fine), `month_year`, `total_amount`, `paid_amount`, **`status` (generated column: unpaid/partial/paid)**, `issued_by`; **partial unique index `(school_id, class_id, session_id, month_year) WHERE type='batch'`**
- **fee_payments** – `id`, `voucher_id`, `amount_paid`, `payment_date`, `payment_method` (cash/cheque/bank/other), `reference_no`, `recorded_by`; balance trigger recomputes `paid_amount`
- **audit_logs** – `id`, `school_id`, `action`, `actor_user_id`, `target_type`, `target_id`, `old_values` (JSONB), `new_values` (JSONB), `occurred_at`; written by DB triggers; index `(school_id, occurred_at DESC)`

**RPC functions (single-transaction operations):** `promote_student`, `demote_student`, `repeat_student`, `transfer_student`, `record_payment`, `reset_password` (admin only) — all `SECURITY DEFINER`, all verify the caller's `school_id` + role from JWT claims, all audit themselves.

**Triggers:** audit (marks_records, fee_vouchers, fee_payments, attendance, enrollments, students, users), fee-balance recompute, archived-session write guard, `updated_at` maintenance.

---

# **8. Security Requirements**

1. **RLS on every table**, school-scope clause first; never disabled. Browsers use only the anon key; `service_role` is server-side only.
2. **Supabase Auth** (single identity source): rate-limited login, lockout after repeated failures, httpOnly+Secure session cookie, 1 h access token + refresh rotation, session revocation on password reset.
3. **No public forgot-password** (per product rule): admin-initiated reset via audited RPC.
4. **Password policy** at creation: ≥ 8 chars, mixed case + digit. Passwords hashed by the auth system; never logged.
5. **School onboarding** via single-use invite token (72 h expiry); no default passwords.
6. **Audit trail** for critical actions via DB triggers (cannot be bypassed by code); logins audited too.
7. **Archived data** write-protected at the DB; parents never see prior sessions.
8. **Headers**: CSP, X-Frame-Options DENY, nosniff, Referrer-Policy, HSTS.
9. **Secrets**: env-var only, per environment; `.env.local` gitignored; CI secret scan; Dependabot/`npm audit` weekly.
10. **Backups encrypted** (B2 server-side encryption); restore runbook in repo.

---

# **9. Cost & Hosting Plan (v2 addition)**

Target: **stay ≤ $45/month through the first ~100 schools.**

| Tier | Stack | Monthly cost | When |
|---|---|---|---|
| **0 – Dev/Pilot** | Vercel Hobby + Supabase Free + B2 backups | ~$1 | Development, staging, unpaid pilots (Hobby is non-commercial by ToS) |
| **1 – Launch** | Vercel Pro ($20) + Supabase Free ($0) + B2 backups (~$1–2) | **~$22** | From first paying school; supports ~10–15k students |
| **2 – Growth** | Vercel Pro ($20) + Supabase Pro ($25) + B2 archival (~$2) | **~$47** | When DB > 400 MB or egress > 4 GB/month (~50–80k students) |
| **3 – Cost-min hybrid** | Cloudflare Pages ($0) + self-hosted Postgres on cheap VPS (~$5) + B2 (~$2) | **~$8–10** | 100+ schools; near-unlimited DB size |

**Cost guardrails (non-negotiable):**
- No Supabase Realtime (poll with TanStack Query: 30–60 s intervals, refetch on focus/mutation).
- No per-school databases, no Redis, no read replicas, no multi-region — none needed at this scale.
- No image/file uploads in v1 (files are the #1 egress cost; revisit with Cloudflare R2 / Supabase Storage only when a school demands it).
- Server-side data cache (60 s TTL per school) for dashboards; keyset pagination on all lists; batch single-statement writes.
- Excel/CSV exports generated client-side; receipts/report cards via browser print CSS (no PDF server work).
- Monthly review of Supabase (DB size, egress, MAU) and Vercel (bandwidth, invocations) usage; upgrade before hitting caps.

---

# **10. Backup & Disaster Recovery (v2 addition)**

- **Free tier has no backups** → nightly `pg_dump` (cron / GitHub Action) to Backblaze B2: 30 days daily + 12-month monthly cold copies. RPO ≤ 24 h, RTO ~1 h.
- **Pro tier** adds Supabase daily backups (7-day) + optional PITR; B2 archival continues.
- Restore runbook in repo; **quarterly restore drill** (a backup never restored is not a backup).
- Backups encrypted; credentials in repo secrets only.

---

# **11. Development Roadmap (Phased)**

# **Phase 0 – Foundation (v2 addition)**
- Supabase Auth replaces NextAuth; JWT claims (`role`, `school_id`) configured
- RLS policies on all base tables; `users` / `parent_users` / `enrollments` schema
- CI/CD (GitHub Actions + Vercel), 3 environments, SQL migrations in repo
- Nightly backup job + B2 bucket; invite-token admin onboarding

# **Phase 1 – Foundation (PRD)**
- Project setup (Next.js, Tailwind, Supabase, Auth); Credentials login with `role@school` format
- Admin: Session & Class CRUD; Subject management per class

# **Phase 2 – Core Entities**
- Admin: Student enrollment (enrollments) & status management
- Admin: Teacher creation & assignment to subjects/classes; Timetable builder (conflict-checked)
- Teacher: Dashboard & timetable

# **Phase 3 – Daily Operations**
- Teacher: Batch attendance marking (class incharge only); Diary writing; Marks entries & editing (auto-audited)
- Parent: Diary, Attendance, Timetable viewing

# **Phase 4 – Fee Management**
- Admin: Batch fee issuance (DB-enforced one-per-class-per-month), individual edits, fine vouchers
- Admin: Payment recording (cash/cheque/bank), trigger-computed balances; Parent: fee viewing
- Fee defaulter blocking logic

# **Phase 5 – Year-End Workflow**
- One-by-one promotion/demotion/repeat (transactional RPC with fee validation)
- Class/session archival; read-only guard at DB level

# **Phase 6 – Audit & Polish**
- Audit triggers on remaining tables; Excel/CSV export
- Performance: indexes review (EXPLAIN), keyset pagination, server cache tuning
- k6 load test (1,000 concurrent users, p95 < 500 ms); security headers; restore drill #1

# **Phase 7 – Ops Hardening (v2 addition)**
- Cost budget alerts (usage API check on cron), runbook polish, quarterly restore-drill calendar, Dependabot, staging parity

---

# **12. UI/UX Philosophy**

- Minimal, white-toned design. Built entirely with Tailwind CSS; no heavy component library.
- Focus on clarity, fast navigation, and data density where needed (fee tables, marks grids).
- Parent portal extremely simple; teacher and admin portals provide richer manipulation interfaces.
- Receipts, fee slips, and report cards print cleanly via print stylesheets (no downloads needed).

---

# **13. Success Metrics**

- Each portal completes its core tasks without degradation during **bursts of 1,000+ concurrent users** (evening parent/teacher peak) — target p95 < 500 ms. Load-tested with k6.
- Data accuracy: zero fee-calculation errors (trigger-computed balances), zero attendance duplication (unique constraint), zero lost students (transactional promotion RPC).
- **Zero data leakage between schools** (validated by RLS policy tests in CI; periodic audit of policies).
- Promotion/demotion workflow is error-free and prevents any student from being lost (verified by restore-drill and test suites).
- **Infrastructure cost ≤ $45/month through ~100 schools** (Tier 1→2 ladder); monthly usage review; no surprise bills (spend guardrails in §9).
- Restore drill succeeds within RTO (≤ 1 h) every quarter.

---

# **14. Open Questions**

1. Launch scale (pilots vs 20 vs 100 schools) — determines Free vs Pro start.
2. Geography → region choice (e.g., `ap-south-1`, `us-east-1`, `eu-central-1`).
3. Future file uploads (photos, scanned receipts)? If yes, plan storage from the start.
4. Multi-child parent accounts (schema supports later; per-child logins for v1).
5. Printed receipts / report cards needed in v1? (Print CSS covers it at $0.)
6. Archived-data retention: 3 years online, then B2 cold archive — confirm.
7. Online payment gateway later? Schema allows adding without redesign.
8. Second language (e.g., Urdu)? Plan i18n early if so.
9. School onboarding: self-serve signup vs sales-assisted invite.

---

*End of PRD v2. All corrections trace to `ARCHITECTURE.md` in the same folder; keep both in sync.*

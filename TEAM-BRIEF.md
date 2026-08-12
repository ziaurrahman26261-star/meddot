# Team Brief — School SaaS: Terms, Focus & Eliminate

> One-page-per-step briefing for the build team. Read Step 6 first — it's the checklist.
> Full detail lives in: `PRD.md` (what), `ARCHITECTURE.md` (plain how), `SYSTEM-DESIGN.md` (engineering blueprint), `AUTOMATION.md` (self-acting parts).

---

## STEP 1 — Big Picture

| Term | Simple meaning | Focus | Eliminate |
|---|---|---|---|
| SaaS | One software many schools rent | One shared system | Per-school systems |
| Multi-tenant | One building, locked rooms per school | Every row tagged with `school_id` | Code assuming one school |
| Frontend/Backend/DB | Shop window / staff / storage room | Keep all three simple | Over-engineering |
| Next.js | Tool that builds the website | App Router, server-built pages | Heavy client-side apps |
| Server Actions | Buttons → small server helpers | All writes via helpers/RPC | Browser writing to DB directly |
| RPC | Asking the DB to run a prepared routine | Big jobs = ONE DB routine | Multi-step app writes |
| Vercel / serverless | Company that runs our app | Vercel Pro once schools pay | Managing own servers in v1 |
| CDN / edge | Copies of site near users | Automatic, nothing to build | — |

## STEP 2 — Security (most important)

| Term | Simple meaning | Focus | Eliminate |
|---|---|---|---|
| Auth vs Authorization | Who you are vs what you may see | Check both on every request | Trusting after login only |
| JWT / token / claims | Signed ID card (who, school, role) | `role` + `school_id` inside token | School/role in URLs or browser |
| RLS | Drawer locks inside the database | **On every table, school check first, tested in CI** | Ever disabling RLS |
| school_id | School tag on every row | Every table + every index | Tables without it |
| anon vs service_role key | Public key vs master key | anon in browser, service_role server-only | service_role in browser code |
| Rate limiting / lockout | 5 wrong tries → 15 min block | Supabase Auth built-in | Custom login systems |
| Session / cookie / refresh | Pass that expires & refreshes | httpOnly+Secure, revoke on reset | Never-expiring tokens |
| Password hashing | Passwords scrambled at rest | Let Supabase Auth do it | Plain text / second password store |
| Security headers / SSL | Browser rules + encryption | Standard headers, free SSL | Skipping "it's small" |
| Invite token | One-time 72h link for first admin | No default passwords | admin/admin accounts |

## STEP 3 — Database (the heart)

| Term | Simple meaning | Focus | Eliminate |
|---|---|---|---|
| Table / row / column | Drawer / record / field | 21 tables, all with school_id | — |
| Primary / foreign key | Row ID / pointer to other rows | Everywhere, keeps data consistent | Loose references |
| Constraint / unique / CHECK | Rules the DB enforces itself | Business rules HERE: attendance unique, one batch voucher/class/month, one class/student/session | App-code-only rules |
| Partial unique index | Uniqueness for some rows only | Batch voucher rule | App enforcement |
| Index | Book's table of contents | FK + school_id combos; attendance (school, class, date) | Full-table scans |
| Trigger | DB reflex: X happens → do Y | Audit, fee balance, archival seal | App-level logging/math |
| Generated column | DB calculates it (fee status) | Derived values | App-computed status |
| Transaction | All-or-nothing form | Promotion/transfer/payment = 1 transaction | Step-by-step writes |
| SECURITY DEFINER | Function with special powers | Re-check caller role+school inside | Trusting the caller |
| JSONB | Flexible notes (audit diffs) | Audit old/new values | Rigid audit columns |
| Migration | Versioned SQL for schema | Every change = migration file via CI | Hand-editing prod DB |
| UPSERT / ON CONFLICT | Insert-or-update in one statement | Whole-class attendance = 1 UPSERT | 40 inserts for 40 students |
| Keyset pagination | "Next 50 after last seen" | All lists | OFFSET, full-list loads |
| N+1 query | Query inside a loop (51 queries) | Joins + batching | Queries in `.map()` |
| Connection pooling | Receptionist for DB connections | Supabase pooler (port 6543) | Direct serverless connections |

## STEP 4 — App & Architecture

| Term | Simple meaning | Focus | Eliminate |
|---|---|---|---|
| Server vs client components | Built in kitchen vs built in browser | Pages on server, client minimal | Browser data fetching |
| Cache / TTL | Notice board, 60s answers | Dashboards cached per school | Re-querying every view |
| Polling vs Realtime | Check every 30–60s vs instant push | Polling + refetch on focus | Supabase Realtime (paid meter) |
| TanStack Query / staleTime | When to refetch | Timetable 5min, dashboards 60s, fees 30s | Refetching everything |
| Middleware | Checkpoint for every request | Session refresh + role redirects | Checking only some pages |
| Cron job | Alarm clock for jobs | Nightly backup, fee snapshots, usage checks | Manual routines |
| Environments | dev / staging / prod | 3 copies, never test on prod | One shared environment |
| CI/CD | Robot tests every change | Lint + tests + RLS tests + secret scan | Deploying untested |

## STEP 5 — Cost & Operations

| Term | Simple meaning | Focus | Eliminate |
|---|---|---|---|
| Egress / bandwidth | Data leaving the system (billed) | Cache + pagination + polling | Big list reloads, images in v1 |
| MAU | Logins per month | 50k free is plenty | Worrying early |
| Free tier limits | 500MB DB / 5GB egress / no backups | Upgrade at 80% (calendar) | Discovering limits at 11 PM |
| Backup / RPO / RTO | Nightly copy; lose ≤1 day; back in ~1h | Nightly encrypted → B2 + quarterly drill | Assuming host backs us up |
| B2 / object storage | Cheap safe for backups ($6/TB) | All backups there | Expensive storage |
| Monitoring | Smoke detector + alarm clock | Sentry + UptimeRobot from day one | Finding out from angry principals |
| Load test / p95 | Simulate 1,000 users; 95% < 500ms | 3 scenarios before launch | Launching blind |
| Vendor lock-in | Stuck with one company | Standard SQL, migrations in repo | Vendor-only features |

---

## STEP 6 — The Checklist (give this to the team)

### ✅ FOCUS ON (non-negotiable)
1. **RLS on every table** — school claim first, tested in CI (the #1 safety feature)
2. **Supabase Auth** — single login system (no NextAuth)
3. **`enrollments` table** — full history, one class per student per session
4. **Business rules as DB constraints** — attendance unique, one batch voucher/class/month, marks unique
5. **Triggers** — audit register book, fee balance, archived-year seal
6. **RPC transactions** — promotion/transfer/payment = one all-or-nothing form
7. **Polling + caching** — no Realtime; notice board 60s
8. **Nightly backups to B2** from day one + quarterly restore drill
9. **Batch writes** — one UPSERT per class attendance; one INSERT for batch vouchers
10. **Keyset pagination** on all lists
11. **CI robot** — tests, RLS tests, secret scan, migrations in repo
12. **Cost guardrails** — monthly meter review, upgrade before limits

### ❌ ELIMINATE (remove these problems)
1. **NextAuth** → Supabase Auth (incompatible with RLS)
2. **`parent_password_hash` on students** → one password store only
3. **`current_class_id`** → enrollments history
4. **App-level audit logging** → triggers only
5. **App-level fee balance math** → trigger only
6. **Supabase Realtime** → polling
7. **Redis, queues, replicas, multi-region** → not needed at this scale
8. **Image/file uploads in v1** → biggest cost driver; later, on demand
9. **Server-side PDF generation** → browser print CSS
10. **Vercel Hobby for paying schools** → Pro required
11. **Disabling RLS ever** → fix queries with indexes
12. **service_role key in browser** → server env only
13. **OFFSET pagination** → keyset only
14. **Per-student loops** → batch everything
15. **Hand-editing production DB** → migrations only
16. **Default passwords** → invite tokens only

---

*Companion to PRD.md, ARCHITECTURE.md, SYSTEM-DESIGN.md, AUTOMATION.md, system-diagram.html.*
# AGENTS.md

## Repo state: planning docs only

- No code exists yet: the repo is `README.md` + a Visual Studio/.NET `.gitignore` + `docs/`. There is no solution to build or test — do not expect one, and do not act as if implementation already happened. The docs are all review drafts awaiting owner approval.
- Product: a multi-page **ASP.NET Core MVC (.NET 10)** portfolio + single-admin Admin CMS for Adib Hasan Avik, backed by SQL Server. Viewer (public) and Admin areas are one application, not two deployments.
- Implementation follows phases P00–P24 in `docs/Implementation_Plan.md`, in that order. **P00 (baseline reconciliation) comes before any code** and is mandatory: resolve/record documented inconsistencies first.

## Documentation precedence

Requirements and constraints live entirely in `docs/`. On conflict, follow the precedence in `docs/Implementation_Plan.md` §3.1 and stop at the first authority:

1. Scope & behavior: `PRD.md` + `REQUIREMENTS_CATALOG.md` (canonical 112-ID baseline; 113 catalog rows minus `RE-010`, which is merged into `AD-003`)
2. Architecture boundaries: `ADD_Comprehensive.md`
3. Technical detail: `TECHNICAL_SPEC_v2.md` + `Decisions.md` (decision register D-001…D-041)
4. Release allocation: `SCOPE_AND_RELEASES_v2.md`
5. Visual/interaction rules: `DESIGN_SYSTEM.md` + `PAGE_DESIGN_SPECIFICATION_v2.0.md`
6. Verification: `TESTING_STRATEGY.md` + `REQUIREMENTS_TRACEABILITY_v2.md`
7. Sequencing: `Implementation_Plan.md`

Never resolve a conflict by picking whatever is easiest to implement — record it and surface it for a decision (see ADR rule below).

## Document status traps

- `Decisions.md` distinguishes **approved** (locked) vs **proposed** (recommended defaults) vs **open** decisions. Proposed providers (Hangfire, ClamAV, Quill, image-processing library, etc.) are **not yet approved** — verify fit and record an ADR before wiring them in.
- `Implementation_Plan.md` §3.2 baseline inconsistencies are now marked **RESOLVED** (reconciliation decisions D1–D6, 8 November 2026): the catalog grew from 78 to the canonical 112-ID baseline; the phantom `FR-I18N-001`–`FR-I18N-003` references were retired and their meaning re-pointed per decision D4; the older narrow plan revision (seeded admin credentials, Bootstrap-vs-Tailwind) was reconciled against the approved v3.0 content. Retired legacy identifiers (`FR-ADM-001`…`NFR-DATA-001`) remain readable **only** as aliases through `docs/REQUIREMENTS_ALIAS_ANNEX.md` — never use a legacy ID as an active requirement, allocation, task, or test reference; resolve it there and cite the canonical ID.
- Shelf the tempting shortcuts: spec §27 names explicit non-goals (multi-admin, public accounts, blog, ratings, speculative AI features).

## Stack and architecture (approved)

- `net10.0`, EF Core 10, SQL Server, Code First migrations, Razor views.
- Clean Architecture modular monolith: `Portfolio.Domain`, `Portfolio.Application`, `Portfolio.Infrastructure`, `Portfolio.Web` + unit/integration/architecture test projects (see TECHNICAL_SPEC §3).
- Dependency direction enforced by architecture tests: Domain depends on nothing; Application → Domain only; Infrastructure → Application/Domain; Web uses Infrastructure only at the composition root. Controllers never touch `DbContext`, `DbSet`, concrete repositories, or Identity entities; Razor views get presentation ViewModels.
- CQRS with MediatR; FluentValidation; Mapster only where mapping is explicit; Serilog structured logging.
- Bootstrap 5 is a responsive/interaction **foundation only** — the Executive Dark design system (`docs/DESIGN_SYSTEM.md`) is the visual source of truth. Do not ship default-Bootstrap-looking pages; self-host assets.
- Email is transactional-outbox based: persist the business record first, dispatch retries via background worker, idempotent — a Mailtrap outage must not lose content.

## Hard product constraints (often overlooked)

- Exactly **one** administrator: no public admin registration, no second-admin path, and the Setup Wizard is permanently disabled after first successful setup. MFA (TOTP + recovery codes) is required.
- Public pages render **published content only** — drafts, unpublished translations, and in-progress edits never leak to public pages, search, sitemap, or fallback behavior. Re-publishing is the only promotion path.
- **Never invent content**: no fabricated personal facts, project metrics, certifications, photos, or achievements. The Gallery ships as a designed empty state until the admin uploads real photographs — never pre-populate with generated/stock/placeholder images.
- Private media lives outside `wwwroot` and is served only through authorized endpoints, authorized on **every** request.
- Contact messages persist before email delivery is attempted; visitor confirmation and admin notification are independent outcomes.
- Accessibility target: WCAG 2.2 AA — verify contrast in both dark and light themes; do not assume the token palette passes.
- Do not bypass malware scanning, authorization, MFA, anti-forgery, sanitization, or private-media checks to make a demo work; do not add "tutorial-typical" bits (Autofac, Redis, separate search engine) measuring only commonality, seldom real need.

## Configuration and environment

- Deployment-dependent values (connection strings, storage roots, Mailtrap/reCAPTCHA keys, ClamAV endpoint, backup destination, Data Protection keys) must come from environment config / strongly typed options — never hard-coded (`TECHNICAL_SPEC_v2.md` §1.3). Credentials in the docs are illustrative.
- Dev host is Windows; write commands and paths PowerShell-compatible.

## Working habits specific to this repo

- Small vertical slices; keep tests + docs + traceability updated in the same change.
- Any deviation from the spec needs an **ADR** (affected requirement, reason, impact, alternatives, approval status) — no silent substitutions, and no silently dropping hard requirements; log blockers instead.
- Never claim tests, scans, deployments, or backups succeeded unless actually executed in this session.
- Verify names against the actual repo rather than doc examples before creating anything (docs are occasionally out of date with each other).

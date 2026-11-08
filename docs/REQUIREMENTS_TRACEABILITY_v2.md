# Requirements Traceability Matrix (RTM) v2.0

**Product:** Adib Hasan Avik — Personal Portfolio & Travel Gallery  
**Document status:** Comprehensive working draft — mappings prepared; implementation and verification evidence not yet populated  
**Version:** 2.0  
**Prepared:** 8 November 2026  
**Baseline source:** `REQUIREMENTS_CATALOG.md` (Draft baseline)  
**Release approach:** Option A confirmed — R1 is the first public production release; detailed allocations remain provisional until `SCOPE_AND_RELEASES_v2.md` is formally approved.

> **Important:** This document establishes traceability links and exposes delivery gaps. It does not claim that code exists, tests have passed, releases are approved, or production readiness has been achieved. Any item marked `Not assigned`, `Not run`, or `Not evidenced` is intentionally left open rather than fabricated.

## 1. Purpose and intended use

This document is the project-level Requirements Traceability Matrix. It connects each stable requirement in the Requirements Catalog to product intent, architecture, technical constraints, planned release, verification approach, implementation work, test records and evidence. It is intended for the owner, engineers, reviewers and AI coding agents.

The RTM is a control document, not a substitute for the source requirements. The Requirements Catalog remains authoritative for requirement wording and acceptance criteria; the PRD remains authoritative for product goals and user-visible scope; the approved ADD governs architecture boundaries; the Technical Specification governs technical decisions; the approved Scope and Releases document governs release commitments; and the Testing Strategy governs test methods and quality gates.

## 2. Document authority and source baseline

| Source | Role in traceability | Current treatment |
|---|---|---|
| `PRD(1).md` | Product goals, user journeys, scope, public/Admin behavior and success criteria | Reviewed baseline; owner approval status should be confirmed in document control |
| `REQUIREMENTS_CATALOG.md` | Stable requirement IDs and acceptance criteria | Draft baseline; exact ID inventory extracted for this RTM |
| `ADD_Comprehensive.md` | Clean Architecture boundaries, modules, patterns and dependency direction | Architecture reference; mappings are module-level, not invented class names |
| `TECHNICAL_SPEC_v2.md` | Platform, technical constraints, security, media, deployment and operations | v2 draft; section references below point to its current structure |
| `SCOPE_AND_RELEASES_v2.md` | R1/R2/R3 scope, release gates and sequencing | Option A confirmed; individual allocations are treated as provisional pending document approval |
| `TESTING_STRATEGY.md` | Test layers, critical scenarios, accessibility, performance and recovery | Verification strategy reference; no test execution evidence supplied |
| `implementation_plan_document.md` | Delivery sequencing and implementation tasks | Existing plan is known to be narrower than product scope; task links are intentionally unassigned pending reconciliation |
| Existing `REQUIREMENTS_TRACEABILITY(1).md` | Prior framework and change-control concepts | Superseded as the working matrix by this v2 draft; retain as historical source |

### 2.1 Conflict and precedence rules

1. Product behavior and scope: approved PRD and Requirements Catalog. 2. Architecture boundaries: approved ADD. 3. Technical choices: approved Technical Specification. 4. Release commitment: approved Scope and Releases. 5. Verification methods: Testing Strategy and approved test cases. 6. If two documents conflict, record the conflict and decision in an ADR/change record; do not silently choose one.

## 3. Traceability model

The intended end-to-end chain is:

`Requirement ID → PRD section → Architecture module/boundary → Technical Specification → Release → Implementation task/PR → Test case → Execution result → Evidence/defect`

A link is considered **defined** when a grounded source section or relevant architecture module is identified. A link is considered **implemented** only when a real task/PR and code reference exist. A link is considered **verified** only when an identified test has actually run and its result/evidence is recorded.

## 4. Status vocabulary

| Dimension | Allowed values | Meaning |
|---|---|---|
| Requirement baseline | Draft / Approved / Changed / Retired | Governance status of the requirement itself |
| Mapping | Mapped / Partial / Gap / Not applicable | Whether a traceability link has been established |
| Implementation | Not started / In progress / Implemented / Blocked / Deferred | Actual delivery state; must be supported by repository/task evidence |
| Verification | Not designed / Test designed / Not run / Pass / Fail / Blocked | Actual verification state |
| Evidence | Not evidenced / Linked | A durable test report, CI run, screenshot, log, or signed review exists |
| Release | Proposed R1 / Proposed R2 / Proposed R3 / Cross-release / Unassigned | Planning allocation only until release baseline approval |

Do not collapse these dimensions into a single `Done` status. A requirement can be implemented but not verified, or tested but blocked by a release decision.

## 5. Complete master traceability matrix

**Catalog inventory:** 78 unique requirement IDs: 65 functional and 13 non-functional. This count is derived from the current catalog text, not from the earlier estimate of 81.

### 5.1 Matrix field definitions

- **PRD:** relevant product section; exact section titles are used where known. - **Architecture:** relevant Clean Architecture module/boundary; detailed class names are intentionally deferred. - **Technical specification:** section reference in `TECHNICAL_SPEC_v2.md`. - **Release:** provisional planning classification, not a commitment. - **Implementation:** no task/PR IDs were supplied; these remain unassigned. - **Verification:** test approach derived from `TESTING_STRATEGY.md`; test case IDs/results/evidence remain unassigned until created and executed.

| Requirement ID | Requirement (catalog summary) | PRD trace | Architecture trace | Technical spec | Proposed release | Verification approach | Implementation / test / evidence |
|---|---|---|---|---|---|---|---|
| `FR-PUB-001` | Distinct public portfolio pages | §6 Public experience; §21 Success criteria | Presentation (MVC) + Application read/query services + published-content policies | §4 Frontend; §12 Publishing/localization; §17 Caching/performance | Proposed R1 — provisional | E2E + accessibility + integration | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-PUB-002` | Published-content-only public output | §6 Public experience; §21 Success criteria | Presentation (MVC) + Application read/query services + published-content policies | §4 Frontend; §12 Publishing/localization; §17 Caching/performance | Proposed R1 — provisional | E2E + accessibility + integration | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-PUB-003` | Dark and light themes | §6 Public experience; §21 Success criteria | Presentation (MVC) + Application read/query services + published-content policies | §4 Frontend; §12 Publishing/localization; §17 Caching/performance | Proposed R1 — provisional | E2E + accessibility + integration | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-PUB-004` | English and Bangla public content | §6 Public experience; §21 Success criteria | Presentation (MVC) + Application read/query services + published-content policies | §4 Frontend; §12 Publishing/localization; §17 Caching/performance | Proposed R1 — provisional | E2E + accessibility + integration | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-PUB-005` | Global search over published portfolio content | §6 Public experience; §21 Success criteria | Presentation (MVC) + Application read/query services + published-content policies | §4 Frontend; §12 Publishing/localization; §17 Caching/performance | Proposed R1 — provisional | E2E + accessibility + integration | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-PUB-006` | Responsive and accessible navigation/interactions | §6 Public experience; §21 Success criteria | Presentation (MVC) + Application read/query services + published-content policies | §4 Frontend; §12 Publishing/localization; §17 Caching/performance | Proposed R1 — provisional | E2E + accessibility + integration | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-PUB-007` | Contact form with categories and optional attachments | §6 Public experience; §21 Success criteria | Presentation (MVC) + Application read/query services + published-content policies | §4 Frontend; §12 Publishing/localization; §17 Caching/performance | Proposed R1 — provisional | E2E + accessibility + integration | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-PUB-008` | Published resume preview and download | §6 Public experience; §21 Success criteria | Presentation (MVC) + Application read/query services + published-content policies | §4 Frontend; §12 Publishing/localization; §17 Caching/performance | Proposed R1 — provisional | E2E + accessibility + integration | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-ADM-001` | Single-admin protected management area | §9 Admin Panel; §10 Publishing | Presentation Admin area + Application commands/queries + authorization + Domain | §3 Architecture; §5 Identity/authorization; §25 Operational Admin capabilities | Proposed R1 — provisional | E2E + integration + authorization/security | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-ADM-002` | CRUD for portfolio content records | §9 Admin Panel; §10 Publishing | Presentation Admin area + Application commands/queries + authorization + Domain | §3 Architecture; §5 Identity/authorization; §25 Operational Admin capabilities | Proposed R1 — provisional | E2E + integration + authorization/security | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-ADM-003` | Draft, preview, publish and unpublish workflow | §9 Admin Panel; §10 Publishing | Presentation Admin area + Application commands/queries + authorization + Domain | §3 Architecture; §5 Identity/authorization; §25 Operational Admin capabilities | Proposed R1 — provisional | E2E + integration + authorization/security | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-ADM-004` | Scheduled publishing where appropriate | §9 Admin Panel; §10 Publishing | Presentation Admin area + Application commands/queries + authorization + Domain | §3 Architecture; §5 Identity/authorization; §25 Operational Admin capabilities | Proposed R1 — provisional | E2E + integration + authorization/security | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-ADM-005` | Admin dashboard with real operational/content data | §9 Admin Panel; §10 Publishing | Presentation Admin area + Application commands/queries + authorization + Domain | §3 Architecture; §5 Identity/authorization; §25 Operational Admin capabilities | Proposed R1 — provisional | E2E + integration + authorization/security | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-ADM-006` | Website settings management | §9 Admin Panel; §10 Publishing | Presentation Admin area + Application commands/queries + authorization + Domain | §3 Architecture; §5 Identity/authorization; §25 Operational Admin capabilities | Proposed R1 — provisional | E2E + integration + authorization/security | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-ADM-007` | Admin collection search/filter/sort/pagination | §9 Admin Panel; §10 Publishing | Presentation Admin area + Application commands/queries + authorization + Domain | §3 Architecture; §5 Identity/authorization; §25 Operational Admin capabilities | Proposed R1 — provisional | E2E + integration + authorization/security | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-ADM-008` | Unsaved-change warnings and destructive-action confirmation | §9 Admin Panel; §10 Publishing | Presentation Admin area + Application commands/queries + authorization + Domain | §3 Architecture; §5 Identity/authorization; §25 Operational Admin capabilities | Proposed R1 — provisional | E2E + integration + authorization/security | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-SEC-001` | Protected atomic one-time initial admin setup | §11 Identity and administrator setup; §17 Security | Security cross-cutting policies + Identity/authorization + Infrastructure | §5 Identity/setup; §18 Security baseline; §21 Configuration/secrets | Proposed R1 — provisional | Security + integration + concurrency + E2E | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-SEC-002` | Idempotent Admin role initialization | §11 Identity and administrator setup; §17 Security | Security cross-cutting policies + Identity/authorization + Infrastructure | §5 Identity/setup; §18 Security baseline; §21 Configuration/secrets | Proposed R1 — provisional | Security + integration + concurrency + E2E | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-SEC-003` | Create initial admin through ASP.NET Core Identity | §11 Identity and administrator setup; §17 Security | Security cross-cutting policies + Identity/authorization + Infrastructure | §5 Identity/setup; §18 Security baseline; §21 Configuration/secrets | Proposed R1 — provisional | Security + integration + concurrency + E2E | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-SEC-004` | Authenticator-app MFA and recovery codes | §11 Identity and administrator setup; §17 Security | Security cross-cutting policies + Identity/authorization + Infrastructure | §5 Identity/setup; §18 Security baseline; §21 Configuration/secrets | Proposed R1 — provisional | Security + integration + concurrency + E2E | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-SEC-005` | Secure password reset | §11 Identity and administrator setup; §17 Security | Security cross-cutting policies + Identity/authorization + Infrastructure | §5 Identity/setup; §18 Security baseline; §21 Configuration/secrets | Proposed R1 — provisional | Security + integration + concurrency + E2E | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-SEC-006` | Prevent second-admin creation or assignment | §11 Identity and administrator setup; §17 Security | Security cross-cutting policies + Identity/authorization + Infrastructure | §5 Identity/setup; §18 Security baseline; §21 Configuration/secrets | Proposed R1 — provisional | Security + integration + concurrency + E2E | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-SEC-007` | Audit important security and admin actions | §11 Identity and administrator setup; §17 Security | Security cross-cutting policies + Identity/authorization + Infrastructure | §5 Identity/setup; §18 Security baseline; §21 Configuration/secrets | Proposed R1 — provisional | Security + integration + concurrency + E2E | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-MED-001` | Seven organized Media Library categories | §15 Media Library | Media module (Domain/Application) + Infrastructure storage/scanner/image-processing adapters | §10 Media Library/storage/file security; §21 Configuration/secrets | Proposed R1 foundation / R2 completion — provisional | Integration + security + file-processing tests | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-MED-002` | Single and bulk uploads with per-file progress/retry | §15 Media Library | Media module (Domain/Application) + Infrastructure storage/scanner/image-processing adapters | §10 Media Library/storage/file security; §21 Configuration/secrets | Proposed R1 foundation / R2 completion — provisional | Integration + security + file-processing tests | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-MED-003` | Server-side file validation and quarantine | §15 Media Library | Media module (Domain/Application) + Infrastructure storage/scanner/image-processing adapters | §10 Media Library/storage/file security; §21 Configuration/secrets | Proposed R1 foundation / R2 completion — provisional | Integration + security + file-processing tests | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-MED-004` | Public and private storage separation | §15 Media Library | Media module (Domain/Application) + Infrastructure storage/scanner/image-processing adapters | §10 Media Library/storage/file security; §21 Configuration/secrets | Proposed R1 foundation / R2 completion — provisional | Integration + security + file-processing tests | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-MED-005` | Media reference tracking before replacement/deletion | §15 Media Library | Media module (Domain/Application) + Infrastructure storage/scanner/image-processing adapters | §10 Media Library/storage/file security; §21 Configuration/secrets | Proposed R1 foundation / R2 completion — provisional | Integration + security + file-processing tests | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-MED-006` | Image variants/WebP while preserving originals | §15 Media Library | Media module (Domain/Application) + Infrastructure storage/scanner/image-processing adapters | §10 Media Library/storage/file security; §21 Configuration/secrets | Proposed R1 foundation / R2 completion — provisional | Integration + security + file-processing tests | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-MED-007` | Recycle bin, restore and safe permanent deletion | §15 Media Library | Media module (Domain/Application) + Infrastructure storage/scanner/image-processing adapters | §10 Media Library/storage/file security; §21 Configuration/secrets | Proposed R1 foundation / R2 completion — provisional | Integration + security + file-processing tests | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-MED-008` | SHA-256 duplicate detection | §15 Media Library | Media module (Domain/Application) + Infrastructure storage/scanner/image-processing adapters | §10 Media Library/storage/file security; §21 Configuration/secrets | Proposed R1 foundation / R2 completion — provisional | Integration + security + file-processing tests | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-MED-009` | Media metadata search and filters | §15 Media Library | Media module (Domain/Application) + Infrastructure storage/scanner/image-processing adapters | §10 Media Library/storage/file security; §21 Configuration/secrets | Proposed R1 foundation / R2 completion — provisional | Integration + security + file-processing tests | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-MED-010` | Storage quotas and usage monitoring | §15 Media Library | Media module (Domain/Application) + Infrastructure storage/scanner/image-processing adapters | §10 Media Library/storage/file security; §21 Configuration/secrets | Proposed R1 foundation / R2 completion — provisional | Integration + security + file-processing tests | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-MED-011` | Antivirus scanning through scanner abstraction | §15 Media Library | Media module (Domain/Application) + Infrastructure storage/scanner/image-processing adapters | §10 Media Library/storage/file security; §21 Configuration/secrets | Proposed R1 foundation / R2 completion — provisional | Integration + security + file-processing tests | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-MED-012` | Media and metadata backup/restore integrity | §15 Media Library | Media module (Domain/Application) + Infrastructure storage/scanner/image-processing adapters | §10 Media Library/storage/file security; §21 Configuration/secrets | Proposed R1 foundation / R2 completion — provisional | Integration + security + file-processing tests | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-GAL-001` | Dedicated public Personal/Travel Gallery | §8 Gallery; §9 Admin Panel | Gallery module + Media module + publishing/visibility policies + MVC presentation | §11 Gallery visibility/publication; §10 Media; §12 Publishing | Proposed R1 foundation / R2 completion — provisional | E2E + integration + authorization/security + accessibility | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-GAL-002` | Album/collection and unified photo browsing | §8 Gallery; §9 Admin Panel | Gallery module + Media module + publishing/visibility policies + MVC presentation | §11 Gallery visibility/publication; §10 Media; §12 Publishing | Proposed R1 foundation / R2 completion — provisional | E2E + integration + authorization/security + accessibility | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-GAL-003` | Flexible album organization and destination metadata | §8 Gallery; §9 Admin Panel | Gallery module + Media module + publishing/visibility policies + MVC presentation | §11 Gallery visibility/publication; §10 Media; §12 Publishing | Proposed R1 foundation / R2 completion — provisional | E2E + integration + authorization/security + accessibility | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-GAL-004` | Photograph metadata with public-field controls | §8 Gallery; §9 Admin Panel | Gallery module + Media module + publishing/visibility policies + MVC presentation | §11 Gallery visibility/publication; §10 Media; §12 Publishing | Proposed R1 foundation / R2 completion — provisional | E2E + integration + authorization/security + accessibility | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-GAL-005` | Independent album/photo publishing with parent safeguards | §8 Gallery; §9 Admin Panel | Gallery module + Media module + publishing/visibility policies + MVC presentation | §11 Gallery visibility/publication; §10 Media; §12 Publishing | Proposed R1 foundation / R2 completion — provisional | E2E + integration + authorization/security + accessibility | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-GAL-006` | Public, Unlisted and Private visibility | §8 Gallery; §9 Admin Panel | Gallery module + Media module + publishing/visibility policies + MVC presentation | §11 Gallery visibility/publication; §10 Media; §12 Publishing | Proposed R1 foundation / R2 completion — provisional | E2E + integration + authorization/security + accessibility | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-GAL-007` | Masonry and uniform-grid layouts | §8 Gallery; §9 Admin Panel | Gallery module + Media module + publishing/visibility policies + MVC presentation | §11 Gallery visibility/publication; §10 Media; §12 Publishing | Proposed R1 foundation / R2 completion — provisional | E2E + integration + authorization/security + accessibility | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-GAL-008` | Featured albums/photos and custom ordering | §8 Gallery; §9 Admin Panel | Gallery module + Media module + publishing/visibility policies + MVC presentation | §11 Gallery visibility/publication; §10 Media; §12 Publishing | Proposed R1 foundation / R2 completion — provisional | E2E + integration + authorization/security + accessibility | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-GAL-009` | Gallery search and filters | §8 Gallery; §9 Admin Panel | Gallery module + Media module + publishing/visibility policies + MVC presentation | §11 Gallery visibility/publication; §10 Media; §12 Publishing | Proposed R1 foundation / R2 completion — provisional | E2E + integration + authorization/security + accessibility | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-GAL-010` | Accessible full-screen photo viewer | §8 Gallery; §9 Admin Panel | Gallery module + Media module + publishing/visibility policies + MVC presentation | §11 Gallery visibility/publication; §10 Media; §12 Publishing | Proposed R1 foundation / R2 completion — provisional | E2E + integration + authorization/security + accessibility | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-GAL-011` | Related albums/photos without visibility leakage | §8 Gallery; §9 Admin Panel | Gallery module + Media module + publishing/visibility policies + MVC presentation | §11 Gallery visibility/publication; §10 Media; §12 Publishing | Proposed R1 foundation / R2 completion — provisional | E2E + integration + authorization/security + accessibility | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-GAL-012` | Shareable URLs and OpenGraph metadata | §8 Gallery; §9 Admin Panel | Gallery module + Media module + publishing/visibility policies + MVC presentation | §11 Gallery visibility/publication; §10 Media; §12 Publishing | Proposed R1 foundation / R2 completion — provisional | E2E + integration + authorization/security + accessibility | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-GAL-013` | Permission-controlled downloads | §8 Gallery; §9 Admin Panel | Gallery module + Media module + publishing/visibility policies + MVC presentation | §11 Gallery visibility/publication; §10 Media; §12 Publishing | Proposed R1 foundation / R2 completion — provisional | E2E + integration + authorization/security + accessibility | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-GAL-014` | Optional comments disabled by default | §8 Gallery; §9 Admin Panel | Gallery module + Media module + publishing/visibility policies + MVC presentation | §11 Gallery visibility/publication; §10 Media; §12 Publishing | Proposed R1 foundation / R2 completion — provisional | E2E + integration + authorization/security + accessibility | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-GAL-015` | Admin comment moderation | §8 Gallery; §9 Admin Panel | Gallery module + Media module + publishing/visibility policies + MVC presentation | §11 Gallery visibility/publication; §10 Media; §12 Publishing | Proposed R1 foundation / R2 completion — provisional | E2E + integration + authorization/security + accessibility | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-GAL-016` | Privacy-friendly aggregate Gallery analytics | §8 Gallery; §9 Admin Panel | Gallery module + Media module + publishing/visibility policies + MVC presentation | §11 Gallery visibility/publication; §10 Media; §12 Publishing | Proposed R1 foundation / R2 completion — provisional | E2E + integration + authorization/security + accessibility | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-GAL-017` | Owner-uploaded photographs only; designed empty state | §8 Gallery; §9 Admin Panel | Gallery module + Media module + publishing/visibility policies + MVC presentation | §11 Gallery visibility/publication; §10 Media; §12 Publishing | Proposed R1 foundation / R2 completion — provisional | E2E + integration + authorization/security + accessibility | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-GAL-018` | Gallery integration with Media Library and backup | §8 Gallery; §9 Admin Panel | Gallery module + Media module + publishing/visibility policies + MVC presentation | §11 Gallery visibility/publication; §10 Media; §12 Publishing | Proposed R1 foundation / R2 completion — provisional | E2E + integration + authorization/security + accessibility | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-CON-001` | Persist contact messages before email attempts | §12 Contact | Contact module + transactional persistence/outbox + email/attachment adapters | §7 Background jobs/outbox; §8 Email; §9 Abuse protection; §14 Contact | Proposed R1 — provisional | Integration + E2E + failure/retry tests | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-CON-002` | Track message and notification delivery lifecycle | §12 Contact | Contact module + transactional persistence/outbox + email/attachment adapters | §7 Background jobs/outbox; §8 Email; §9 Abuse protection; §14 Contact | Proposed R1 — provisional | Integration + E2E + failure/retry tests | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-CON-003` | Contact conversation threads, replies and internal notes | §12 Contact | Contact module + transactional persistence/outbox + email/attachment adapters | §7 Background jobs/outbox; §8 Email; §9 Abuse protection; §14 Contact | Proposed R1 — provisional | Integration + E2E + failure/retry tests | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-CON-004` | Private attachments with strict limits and access rules | §12 Contact | Contact module + transactional persistence/outbox + email/attachment adapters | §7 Background jobs/outbox; §8 Email; §9 Abuse protection; §14 Contact | Proposed R1 — provisional | Integration + E2E + failure/retry tests | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-CON-005` | Contact retention and deletion controls | §12 Contact | Contact module + transactional persistence/outbox + email/attachment adapters | §7 Background jobs/outbox; §8 Email; §9 Abuse protection; §14 Contact | Proposed R1 — provisional | Integration + E2E + failure/retry tests | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-RES-001` | Multiple language/professional resume versions | §13 Resume | Resume module + publishing + private/public media delivery | §15 Resume management; §10 Private documents/downloads | Proposed R1 — provisional | Integration + E2E + authorization tests | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-RES-002` | Only published resume versions publicly accessible | §13 Resume | Resume module + publishing + private/public media delivery | §15 Resume management; §10 Private documents/downloads | Proposed R1 — provisional | Integration + E2E + authorization tests | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-RES-003` | Aggregate resume download metrics | §13 Resume | Resume module + publishing + private/public media delivery | §15 Resume management; §10 Private documents/downloads | Proposed R1 — provisional | Integration + E2E + authorization tests | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-SEO-001` | Language-prefixed /en/ and /bn/ routes and SEO metadata | §14 Multilingual experience; §17 Security/operations | Presentation routing/metadata + localization + sitemap generation | §12 Localization; §23 SEO/HTTP behavior | Proposed R1 — provisional | Integration + E2E + SEO inspection | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-SEO-002` | Sitemap contains only eligible published/indexable content | §14 Multilingual experience; §17 Security/operations | Presentation routing/metadata + localization + sitemap generation | §12 Localization; §23 SEO/HTTP behavior | Proposed R1 — provisional | Integration + E2E + SEO inspection | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-ANA-001` | Privacy-friendly aggregate analytics | §16 Analytics and privacy | Analytics module + privacy/consent policy + reporting queries | §16 Analytics/privacy; §17 Caching/performance | Proposed R2 — provisional | Integration + privacy/consent tests | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `FR-ANA-002` | Consent and tracking preference behavior | §16 Analytics and privacy | Analytics module + privacy/consent policy + reporting queries | §16 Analytics/privacy; §17 Caching/performance | Proposed R2 — provisional | Integration + privacy/consent tests | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `NFR-SEC-001` | OWASP-aligned secure defaults | §11 Identity and administrator setup; §17 Security | Security cross-cutting policies + Identity/authorization + Infrastructure | §5 Identity/setup; §18 Security baseline; §21 Configuration/secrets | Proposed R1 — provisional | Security + integration + concurrency + E2E | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `NFR-SEC-002` | Server-side authorization for every admin operation | §11 Identity and administrator setup; §17 Security | Security cross-cutting policies + Identity/authorization + Infrastructure | §5 Identity/setup; §18 Security baseline; §21 Configuration/secrets | Proposed R1 — provisional | Security + integration + concurrency + E2E | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `NFR-SEC-003` | Secrets held in environment/deployment secret management | §11 Identity and administrator setup; §17 Security | Security cross-cutting policies + Identity/authorization + Infrastructure | §5 Identity/setup; §18 Security baseline; §21 Configuration/secrets | Proposed R1 — provisional | Security + integration + concurrency + E2E | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `NFR-PRIV-001` | Data minimization, retention and privacy controls | §16 Analytics and privacy; §18 Backup/recovery | Privacy policy + data lifecycle/retention + analytics/contact/media modules | §16 Analytics/privacy; §18 Security; §26 Legal/retention | Proposed R1 — provisional | Privacy/security review + integration tests | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `NFR-ACC-001` | WCAG 2.2 AA accessibility target | §19 Quality attributes; §21 Success criteria | Presentation design system and interaction patterns across public/Admin surfaces | §4.7 Accessibility; §24 Testing/release evidence | Proposed R1 — provisional | Automated accessibility + manual keyboard/screen-reader review | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `NFR-PERF-001` | Performance optimization and measurable budgets | §19 Quality attributes | Presentation, Application query paths, EF Core persistence, media pipeline and cache | §17 Caching/performance; §24 Testing/release evidence | Cross-release; production gate — provisional | Performance/load tests on representative Staging | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `NFR-REL-001` | Reliability, centralized errors, health checks and bounded retries | §17 Security, reliability and operations | Host/Infrastructure health, retries, background jobs and error handling | §7 Background jobs; §18 Security; §19 Logging/health | Proposed R1 — provisional | Integration + resilience/failure-injection tests | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `NFR-DR-001` | RPO <=4 hours and RTO <=4 hours demonstrated by recovery drills | §18 Backup and disaster recovery | Infrastructure backup/restore services + database/media integrity procedures | §20 Backup/restore/disaster recovery | Cross-release; production gate — provisional | Backup integrity + isolated restore drill with measured RPO/RTO | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `NFR-COMP-001` | Current/recent desktop and mobile browser compatibility | §19 Quality attributes | Presentation responsive frontend + supported runtime/browser test matrix | §4 Frontend; §22 Docker/deployment; §24 Testing | Cross-release; production gate — provisional | Cross-browser/device E2E matrix | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `NFR-MAINT-001` | Modular maintainable architecture and documented interfaces | §1 Product summary; §3 Product goals; §19 Quality attributes | Solution-wide Clean Architecture boundaries and modular interfaces | §3 Solution structure; §6 Application patterns; §7 Repository/UoW | Cross-release; production gate — provisional | Architecture tests + code review | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `NFR-DEP-001` | Docker compatibility and provider-portable deployment | §1 Product summary; §17 Operations | Host/container/deployment configuration + storage provider abstraction | §2 Platform; §10 Storage abstraction; §21 Configuration; §22 Docker | Proposed R1 — provisional | Container/deployment smoke tests | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `NFR-OBS-001` | Structured logs, health and background-job observability | §17 Security, reliability and operations | Host/Infrastructure logging, health checks, job/outbox and operational status | §19 Logging/monitoring/health; §25 Operational Admin | Proposed R1 — provisional | Operational integration + health/log/job verification | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |
| `NFR-DATA-001` | Transactional data integrity and coordinated backup/restore | §18 Backup and disaster recovery; §21 Success criteria | Domain invariants + EF Core transactions/constraints + backup/restore coordination | §6 Database/integrity; §7 Transactions/outbox; §20 Recovery | Proposed R1 — provisional | Integration + concurrency + restore-integrity tests | Task: **Not assigned**; test ID: **Not assigned**; result: **Not run**; evidence: **Not evidenced** |

## 6. Cross-cutting traceability controls

The following controls cut across multiple requirements and must be implemented and tested as coherent end-to-end behaviors.

| Control area | Requirements primarily affected | Required cross-check |
|---|---|---|
| Published-content boundary | FR-PUB-002, FR-ADM-003, FR-GAL-005/006/012, FR-RES-002, FR-SEO-002 | Draft/private/unlisted/unpublished records must not leak through pages, search, direct routes, sitemap, metadata, cache or fallback behavior |
| Single-admin security | FR-ADM-001, FR-SEC-001..007, NFR-SEC-001..003 | One-time setup is atomic; no public registration/second admin; MFA, recovery, authorization and audit are enforced |
| Media safety and privacy | FR-MED-002..012, FR-GAL-013/017/018, FR-CON-004, FR-RES-002 | Validate actual file content; scan/quarantine; private assets outside public web root; authorized delivery; references and backups remain consistent |
| Gallery parent/child visibility | FR-GAL-001..018, FR-MED-004/005/012 | An unpublished/private child photo cannot leak through a published album, related content, share metadata, search, download or cache |
| Contact reliability | FR-PUB-007, FR-CON-001..005, NFR-REL-001, NFR-DATA-001 | Persist first; email delivery is independent/retry-safe; attachments are private; retention/deletion audited |
| Localization and SEO | FR-PUB-004, FR-SEO-001/002, FR-RES-001/002 | Correct language route, canonical/hreflang, published-only fallback and sitemap; never fall back to unpublished translation |
| Recovery integrity | FR-MED-012, FR-GAL-018, NFR-DR-001, NFR-DATA-001 | Database, media originals, variants, manifests and references restore consistently; measured RPO/RTO targets met |
| Accessibility and responsive design | FR-PUB-006, FR-GAL-007/010, NFR-ACC-001, NFR-COMP-001 | Keyboard, focus, screen reader, touch, reduced motion and dark/light contrast across supported viewports |

## 7. Release traceability and approval state

### 7.1 Confirmed decision

**Option A is confirmed:** R1 is the first public production release. Development and Staging are used for continuous testing before production, and production release remains subject to defined entry/exit gates.

### 7.2 Provisional requirement allocation

The release labels in Section 5 are planning recommendations derived from the current Scope v2 and the criticality of production protections. They are **not approved requirement-level commitments** until the owner approves `SCOPE_AND_RELEASES_v2.md`. In particular:

- Core public portfolio, secure single-admin foundation, contact persistence, published resume, essential Media Library and production safety controls are treated as proposed R1 scope. - Gallery is proposed as a secure foundation in R1, with advanced capabilities potentially completed in R2; this split requires explicit owner approval. - Advanced analytics and nonessential enhancements may be proposed for R2/R3 only if this does not defer essential security, privacy, accessibility, backup or recovery protections needed for R1 production. - RPO ≤4 hours and RTO ≤4 hours are acceptance targets in the PRD/catalog/technical documents; do not claim compliance until a measured restore drill demonstrates them.

### 7.3 Release allocation fields to complete after approval

For each requirement, add/confirm: approved release; full/partial delivery; dependency; deferral reason; approval/decision reference; release acceptance evidence. Never infer approval from a draft allocation table.

## 8. Verification and test traceability

The Testing Strategy defines test layers and critical scenarios but does not provide a complete stable test-case register. Create test IDs in a separate test-case register, then link them back here. Suggested test-case IDs should be allocated by the project test owner; this RTM deliberately does not fabricate them.

### 8.1 Minimum test-register schema

| Field | Required content |
|---|---|
| Test Case ID | Stable unique identifier, created in test register |
| Requirement IDs | One or more exact catalog IDs |
| Test level/type | Unit, integration, E2E, security, accessibility, performance, recovery |
| Preconditions / data | Environment and controlled test data |
| Steps | Reproducible execution steps |
| Expected result | Requirement acceptance criteria in observable form |
| Actual result | What happened during execution |
| Status | Not run / Pass / Fail / Blocked |
| Build and environment | Commit/build, configuration, environment |
| Evidence | CI run, report, screenshot, sanitized log or recovery record |
| Defect | Issue reference and severity when failed |
| Reviewer/date | Person and date confirming result |

### 8.2 Critical scenario-to-requirement links

| Testing Strategy scenario | Requirement links | Evidence required before Verified |
|---|---|---|
| Concurrent one-time admin setup; setup closes after success | FR-SEC-001, FR-SEC-002, FR-SEC-003, FR-SEC-006, NFR-SEC-002 | Repeatable concurrency test output and persisted admin/role state |
| MFA enrollment, lockout, reset expiry, session revocation | FR-SEC-004, FR-SEC-005, FR-SEC-007, NFR-SEC-001/002 | Integration/E2E and security test report |
| Draft, unpublished, private and unlisted exclusion from public discovery | FR-PUB-002, FR-ADM-003, FR-GAL-005/006/012, FR-RES-002, FR-SEO-002 | Route/search/sitemap/metadata/cache access tests |
| Private media and attachment authorization | FR-MED-003/004/011, FR-GAL-013, FR-CON-004, FR-RES-002, NFR-SEC-002 | Anonymous/unauthorized access-denial tests; storage-path inspection |
| Scanner unavailable or unsafe upload | FR-MED-002/003/011, NFR-SEC-001, NFR-REL-001 | Rejection/quarantine logs and integration tests |
| Gallery album/photo parent-child visibility | FR-GAL-005/006/009/010/011/012/013/018 | E2E matrix for each visibility and publication combination |
| Gallery empty before owner uploads; no placeholder imagery | FR-GAL-017, FR-GAL-001 | Empty-state E2E and content/storage inspection |
| Email outage after contact submission | FR-PUB-007, FR-CON-001/002/003, NFR-REL-001, NFR-DATA-001 | Database record plus independent delivery states and retry logs |
| Retention/deletion and attachment lifecycle | FR-CON-004/005, NFR-PRIV-001, NFR-DATA-001 | Audited retention/deletion test evidence |
| Backup/restore including media and manifest | FR-MED-012, FR-GAL-018, NFR-DR-001, NFR-DATA-001 | Backup verification report, restore drill, measured RPO/RTO and integrity report |
| WCAG 2.2 AA and browser/device coverage | FR-PUB-006, FR-GAL-010, NFR-ACC-001, NFR-COMP-001 | Automated scan plus documented manual review on target matrix |
| Performance budgets | NFR-PERF-001 | Numeric budgets approved and measured on representative Staging infrastructure |

## 9. Implementation traceability

Implementation links are intentionally **Not assigned** because the existing `implementation_plan_document.md` is known to cover only a subset of the product and contains decisions that conflict with the current baseline (including seeded admin credentials). Do not treat its current task list as complete coverage.

Before implementation begins in earnest, reconcile the plan against all 78 catalog requirements and the approved release scope. Each implementation item should record: task ID, requirement IDs, owner, dependencies, affected projects/layers, migration impact, security/privacy/accessibility impact, PR/commit, code location, and status.

A requirement must not be marked Implemented solely because an AI agent generated code or a task was closed. Confirm code exists, builds, conforms to architecture, and has appropriate tests.

## 10. Bidirectional coverage and orphan audit

The following audits are mandatory at each baseline change and before each release.

| Audit | Rule | Current result |
|---|---|---|
| Catalog → RTM | Every catalog ID appears exactly once in the master matrix | **Pass:** 78/78 IDs extracted and represented in this draft |
| RTM → Catalog | No invented or retired ID appears in the matrix | **Pass:** matrix uses only the 78 IDs extracted from current catalog |
| PRD → Catalog | Every testable product requirement in PRD has a catalog ID or an explicit documented exclusion | **Not fully audited**; perform detailed sentence-level review |
| Catalog → PRD | Every catalog requirement has a valid PRD source or is explicitly identified as technical/NFR-derived | **Partially mapped** by relevant PRD section; exact paragraph-level references require final source review |
| Catalog → Architecture | Every requirement maps to an owning module/boundary | **Mapped at module level**; detailed use cases/interfaces remain design-time work |
| Catalog → Technical Spec | Every requirement maps to a relevant TS section | **Mapped by section**; confirm section content after TS approval |
| Catalog → Release | Every requirement has an allocation or explicit cross-release status | **Proposed only**; final approval pending |
| Catalog → Implementation | Every requirement has a real task/PR/code link | **Gap:** task plan must be reconciled and IDs created |
| Catalog → Test | Every requirement has a verification approach and actual test ID | **Partial:** approach mapped; stable test IDs not yet created |
| Test → Requirement | Every test maps to one or more approved requirements | **Pending test-register creation** |
| Code → Requirement | No feature is implemented without an approved requirement or documented technical necessity | **Pending repository audit** |
| Release → Evidence | Every release gate has durable evidence | **Pending execution** |

## 11. Known gaps, decisions and dependencies

1. **Scope approval:** obtain owner approval of `SCOPE_AND_RELEASES_v2.md`, including the R1/R2 Gallery split and all per-requirement allocations. 2. **Technical baseline:** approve `TECHNICAL_SPEC_v2.md` or record requested changes; recommendations and deployment-dependent values must remain distinguishable from approved decisions. 3. **Catalog baseline:** confirm `REQUIREMENTS_CATALOG.md` is approved and freeze its 78 IDs; resolve any PRD/catalog omissions. 4. **Implementation plan:** replace or reconcile the current narrow plan; remove seeded default admin credentials and align it with one-time setup. 5. **Test register:** create stable test-case IDs and convert the critical scenarios into reproducible cases. 6. **Performance budgets:** approve numeric targets using representative hosting/Staging. 7. **Browser minimum versions:** define support policy. 8. **Hosting and operations:** decide production host/domain, persistent storage paths, scanner/email/backup provider configuration and secret/key management. 9. **Legal/policy review:** review privacy, terms, cookie, retention and attachment policies for deployment jurisdiction. 10. **Evidence:** no test, scan, backup, restore, deployment or accessibility result is currently asserted by this RTM.

## 12. Change impact analysis

For every change to a requirement, PRD section, architecture decision, technical decision, release allocation or acceptance criterion, record:

- Change ID and date; requester and rationale. - Source requirement IDs and old/new wording. - Impacted PRD, ADD, Technical Specification, implementation tasks, database schema/migrations, APIs/routes, UI, permissions, media, localization, operations and tests. - Security, privacy, accessibility, performance, recovery and deployment impact. - Alternatives considered and decision/approval authority. - Release impact, deferral/dependency and migration/rollback plan. - Updated RTM rows and test/evidence links.

A change is not complete until all affected documents and traceability links are updated. For architecture/technical deviations, create an ADR with context, decision, consequences, status and affected requirement IDs.

## 13. AI coding-agent execution contract

Any coding agent working on this product must follow these rules:

1. Read the PRD, Requirements Catalog, ADD, Technical Specification, Scope and Releases, RTM, Testing Strategy and current implementation plan before coding. 2. Use only exact catalog requirement IDs; never invent IDs. 3. Implement only approved scope and approved release work. If release allocation or a requirement is ambiguous, stop and request a decision rather than silently deciding. 4. Do not invent portfolio facts, achievements, project metrics, credentials, employment history, certificates or photographs. 5. Gallery images must be uploaded and selected by the owner; the initial Gallery must show a designed empty state. 6. Never create a second administrator, public registration, or seeded plaintext/default admin credentials. 7. Do not bypass MFA, authorization, anti-forgery, sanitization, file validation/scanning, private media delivery or audit controls to make a demo work. 8. Respect Clean Architecture dependency direction and approved interfaces; do not introduce microservices, SPA or multi-tenant scope without approval. 9. Add/maintain tests for each requirement slice; update the RTM with actual task/PR/test references. 10. Do not claim tests, security scans, deployment, backups, restore drills or external services succeeded unless actually executed and evidenced. 11. Do not mark a requirement Verified without passing test evidence reviewed against acceptance criteria. 12. Record deviations and blockers; never silently remove requirements.

## 14. Readiness assessment

**Current assessment: the RTM v2.0 is a comprehensive traceability baseline draft, not an implementation-ready sign-off.**

| Area | Assessment | Reason |
|---|---|---|
| Requirement inventory | Complete for current catalog | 78/78 IDs represented |
| Product trace | Broad mapping | PRD sections identified; detailed paragraph-level reconciliation remains |
| Architecture trace | Module-level mapped | Class/use-case mapping belongs to detailed design and must not be invented |
| Technical trace | Section-level mapped | Technical Specification v2 remains a review draft |
| Release trace | Provisional | Option A confirmed; individual release assignments pending scope approval |
| Implementation trace | Incomplete | Existing implementation plan is incomplete/inconsistent; task/PR/code refs absent |
| Test trace | Partially complete | Verification approaches and critical scenario links supplied; test IDs/results absent |
| Evidence | Not available | No execution evidence supplied or asserted |
| Production readiness | Not established | Requires approved baselines, implementation, tests, security/accessibility review and measured recovery evidence |

### 14.1 Recommended next sequence

1. Owner approves or revises `SCOPE_AND_RELEASES_v2.md` (especially Gallery allocation). 2. Owner approves the Requirements Catalog and Technical Specification baseline. 3. Perform sentence-level PRD ↔ Catalog audit and resolve omissions/duplicates. 4. Rebuild the Implementation Plan against all requirements and approved releases. 5. Create test-case register with stable IDs and map every acceptance criterion. 6. Implement in vertical slices; update RTM with real tasks/PRs/code. 7. Execute tests and attach evidence; perform bidirectional orphan audits. 8. Only then issue a release-readiness assessment.

## 15. Traceability metrics

Track these metrics at each review:

- Catalog coverage: requirement IDs represented in RTM / total catalog IDs. - PRD coverage: testable PRD statements mapped to catalog IDs / total identified testable statements. - Architecture mapping coverage: requirements with owner module / total requirements. - Technical mapping coverage: requirements with relevant TS section / total requirements. - Release allocation coverage: approved allocations / total requirements. - Implementation coverage: requirements linked to verified task/PR/code / total requirements. - Test design coverage: requirements with test IDs / total requirements. - Verification coverage: requirements with passing evidence / total requirements. - Orphan count: untraced requirements, tests, code features and release gates.

Do not present a high mapping percentage as delivery progress. Coverage of documentation is not implementation completion.

## 16. Approval and document history

| Version | Date | Change | Status |
|---|---|---|---|
| 1.0 | Previous baseline | Initial framework with sample rows and placeholder mappings | Superseded working draft |
| 2.0 | 8 November 2026 | Expanded to full 78-ID catalog inventory; added module/technical/release/test mappings, evidence controls, orphan audits and AI-agent rules | Review draft; not approved |

### Owner approval checklist

- [ ] Requirements Catalog is approved and frozen at 78 IDs (or updated inventory recorded). - [ ] Scope and release allocations are approved, including Gallery release split. - [ ] Technical Specification v2 is approved or superseding decisions are recorded. - [ ] PRD-to-catalog bidirectional audit is completed. - [ ] Implementation Plan is reconciled with all approved requirements. - [ ] Test-case register and stable IDs are created. - [ ] Release gates and evidence owners are assigned.

---

**End of document**

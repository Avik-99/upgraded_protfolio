# Requirements Alias Annex — legacy identifier mapping

**Document status:** Draft — created during the approved requirements reconciliation (decisions D1–D6, owner-conditioned, 8 November 2026). This annex is not a requirements source; it preserves historical identifiers and the exact legacy wordings that the reconciliation carried into current documents.

**Purpose.** The v2 planning documents replaced the legacy FR-*/NFR-* identifier scheme with a canonical 112-ID baseline defined in `REQUIREMENTS_CATALOG.md`. To keep the identifier chain auditable — and to honor the "stable IDs" principle in Catalog §3.1 and the history of the Implementation Plan — every previously published legacy identifier remains lookup-valid through this annex. No legacy identifier may be resurrected as an active allocation token in the Scope, Implementation Plan, RTM or Testing Strategy.

**Provenance.** All 78 defined legacy identifiers were extracted from the previous RTM v2.0 draft (§5, lines 66–143) and the Scope v2 allocation notes (§5, lines 205–578) before both documents were rebuilt. The three phantom FR-I18N identifiers were cataloged in Implementation_Plan.md §3.2 as referenced-but-never-defined; their intended meaning was recovered from the Scope v2 allocation note that referenced them and mapped per decision D4.

**Overlap rule.** Where a legacy requirement decomposed into several canonical IDs, the id column lists all destinations. Two special cases are marked explicitly: FR-SEC-002 and FR-SEC-003 merged into ID-002/ID-003 (identity family consolidation), and RE-010 (a duplicate catalog row, not a legacy Scope identifier) merged into AD-003 per decision D3.

## 1. Legacy → canonical mapping (78 defined + 3 phantom)

| Legacy ID | Legacy meaning (former RTM summary) | Canonical destination(s) | Reliability / notes |
|---|---|---|---|
| FR-PUB-001 | Distinct public portfolio pages | PR-001 | Exact |
| FR-PUB-002 | Published-content-only public output | CT-002, RE-002, GA-002 + Catalog §6.1 visibility matrix | Cross-cutting; §6.1 is the strongest guarantee of the legacy wording |
| FR-PUB-003 | Dark and light themes | PR-005 | Exact |
| FR-PUB-004 | English and Bangla public content | RE-003 (+ RE-004, RE-005, AD-003 for admin side) | Decomposed |
| FR-PUB-005 | Global search over published content | PR-003 | Exact |
| FR-PUB-006 | Responsive and accessible navigation/interactions | PR-004, PR-009 | Decomposed |
| FR-PUB-007 | Contact form with categories and optional attachments | CO-001, CO-005 | Decomposed |
| FR-PUB-008 | Published resume preview and download | RE-009, RE-007 | Decomposed |
| FR-ADM-001 | Single-admin protected management area | ID-006, AD-002 (with ID-001) | Partial: split across identity and admin-flows requirements |
| FR-ADM-002 | CRUD for portfolio content records | CT-001 (+ CT-004, CT-005) | Exact; content-status and long-form refinements are additions |
| FR-ADM-003 | Draft, preview, publish and unpublish workflow | CT-002, CT-003 | Decomposed |
| FR-ADM-004 | Scheduled publishing where appropriate | CT-006 | Exact; catalog criteria include audit of the scheduled action |
| FR-ADM-005 | Admin dashboard with real operational/content data | AD-001 | Exact ("no fabricated metrics" wording present) |
| FR-ADM-006 | Website settings management | AD-004 | Exact |
| FR-ADM-007 | Admin collection search/filter/sort/pagination | ML-001, CO-004, AD-002 + Catalog §6.8 | Concatenated clause carried to Catalog §6.8 — see section 2.1 |
| FR-ADM-008 | Unsaved-change warnings and destructive-action confirmation | AD-006 + Catalog §6.8 | Wording carried to AD-006 and §6.8 — see section 2.2 |
| FR-SEC-001 | Protected atomic one-time initial admin setup | ID-002 | Exact |
| FR-SEC-002 | Idempotent Admin role initialization | ID-002 | Merged: ID-002 criteria cover the concurrent/single-admin outcome |
| FR-SEC-003 | Create initial admin through ASP.NET Core Identity | ID-003 (+ ID-002) | Merged; implementation-detail wording, hasher criteria retained |
| FR-SEC-004 | Authenticator-app MFA and recovery codes | ID-004 | Exact |
| FR-SEC-005 | Secure password reset | ID-005 | Exact (single-use token, no account enumeration) |
| FR-SEC-006 | Prevent second-admin creation or assignment | ID-001 | Exact |
| FR-SEC-007 | Audit important security and admin actions | ID-007 | Exact |
| FR-MED-001 | Seven organized Media Library categories | ML-001 | Exact |
| FR-MED-002 | Single and bulk uploads with per-file progress/retry | ML-013 | Merged; R1 = safe single + basic bulk, R2 = progress/retry UX (Scope note preserved) |
| FR-MED-003 | Server-side file validation and quarantine | ML-003 | Exact |
| FR-MED-004 | Public and private storage separation | ML-002 | Exact; matches D-010 (Confirmed) |
| FR-MED-005 | Media reference tracking before replacement/deletion | ML-006, ML-007 | Decomposed |
| FR-MED-006 | Image variants/WebP while preserving originals | ML-005 | Exact ("originals must not be destroyed") |
| FR-MED-007 | Recycle bin, restore and safe permanent deletion | ML-008 | Exact |
| FR-MED-008 | SHA-256 duplicate detection | ML-009 | Exact |
| FR-MED-009 | Media metadata search and filters | ML-001, ML-014 | Partial; search/filter duties inside ML-001 collection controls |
| FR-MED-010 | Storage quotas and usage monitoring | ML-010 | Exact |
| FR-MED-011 | Antivirus scanning through scanner abstraction | ML-004 | Exact ("scanner outage never counts as clean") |
| FR-MED-012 | Media and metadata backup/restore integrity | OP-003, NFR-007, GA-010 | Partial (backup split across operations/DB/Gallery restore) |
| FR-GAL-001 | Dedicated public Personal/Travel Gallery | GA-001 | Exact |
| FR-GAL-002 | Album/collection and unified photo browsing | GA-006, GA-003 | Partial |
| FR-GAL-003 | Flexible album organization and destination metadata | GA-003, ML-014 | See section 2.3 (destination metadata, album-level only) |
| FR-GAL-004 | Photograph metadata with public-field controls | GA-003, ML-014 | Exact in combination |
| FR-GAL-005 | Independent album/photo publishing with parent safeguards | GA-005 | Exact; rule restated in Catalog §6.2 |
| FR-GAL-006 | Public, Unlisted and Private visibility | GA-004 | Exact |
| FR-GAL-007 | Masonry and uniform-grid layouts | GA-014 | Exact |
| FR-GAL-008 | Featured albums/photos and custom ordering | GA-003 | Partial (within album management) |
| FR-GAL-009 | Gallery search and filters | GA-006, GA-011 | Partial |
| FR-GAL-010 | Accessible full-screen photo viewer | GA-006 | Exact (keyboard/next-prev/swipe criteria) |
| FR-GAL-011 | Related albums/photos without visibility leakage | GA-012 | Exact |
| FR-GAL-012 | Shareable URLs and OpenGraph metadata | GA-013 | Exact |
| FR-GAL-013 | Permission-controlled downloads | GA-007 | Exact |
| FR-GAL-014 | Optional comments disabled by default | GA-008 | Merged into comments/moderation requirement |
| FR-GAL-015 | Admin comment moderation | GA-008 (approval-before-display criterion) | Merged |
| FR-GAL-016 | Privacy-friendly aggregate Gallery analytics | AN-006 | Exact |
| FR-GAL-017 | Owner-uploaded photographs only; designed empty state | GA-002 | Exact; D-012/D-035 Confirmed |
| FR-GAL-018 | Gallery integration with Media Library and backup | ML-002, OP-003, GA-010 (+ D-008 Confirmed) | See section 2.4 |
| FR-CON-001 | Persist contact messages before email attempts | CO-002 | Exact |
| FR-CON-002 | Track message and notification delivery lifecycle | CO-003 | Exact |
| FR-CON-003 | Contact conversation threads, replies and internal notes | CO-004 (+ CO-008 for retry idempotency) | Exact; R2 slice note preserved in Scope §5.6 |
| FR-CON-004 | Private attachments with strict limits and access rules | CO-005, CO-007 | Exact; numeric limits pending DEC-005 |
| FR-CON-005 | Contact retention and deletion controls | CO-006 | Exact |
| FR-RES-001 | Multiple language/professional resume versions | RE-001 (+ RE-007 default selection) | Exact; R1-default slice note preserved in Scope §5.6 |
| FR-RES-002 | Only published resume versions publicly accessible | RE-002 (+ RE-009 stable access) | Exact |
| FR-RES-003 | Aggregate resume download metrics | AN-005 | Exact |
| FR-SEO-001 | Language-prefixed /en/ and /bn/ routes and SEO metadata | PR-008, RE-003, RE-006 | Decomposed |
| FR-SEO-002 | Sitemap contains only eligible published/indexable content | PR-008, GA-009, RE-006 | Partial |
| FR-ANA-001 | Privacy-friendly aggregate analytics | AN-001, AN-004 (+ AN-010 cookieless posture) | Merged |
| FR-ANA-002 | Consent and tracking preference behavior | AN-003 | Exact |
| NFR-SEC-001 | OWASP-aligned secure defaults | SEC-001, SEC-002, SEC-003, SEC-005 | Merged (CSRF/headers/rate limits/dependency checks were inside this group per Scope §5.3 note) |
| NFR-SEC-002 | Server-side authorization for every admin operation | ID-006 | Exact |
| NFR-SEC-003 | Secrets held in environment/deployment secret management | SEC-004 | Exact |
| NFR-PRIV-001 | Data minimization, retention and privacy controls | AN-002, AN-010, SEC-007, SEC-009 | Merged |
| NFR-ACC-001 | WCAG 2.2 AA accessibility target | NFR-001 | Exact |
| NFR-PERF-001 | Performance optimization and measurable budgets | NFR-003 | Exact; numeric values pending D-037 |
| NFR-REL-001 | Reliability, centralized errors, health checks, bounded retries | NFR-005 | Exact |
| NFR-DR-001 | RPO ≤4 hours and RTO ≤4 hours demonstrated by recovery drills | OP-004 | Exact; D-015 Confirmed |
| NFR-COMP-001 | Current/recent desktop and mobile browser compatibility | NFR-002 (+ PR-009 responsive scope) | Exact |
| NFR-MAINT-001 | Modular maintainable architecture and documented interfaces | NFR-006 | Exact |
| NFR-DEP-001 | Docker compatibility and provider-portable deployment | OP-005, OP-006, OP-009, ML-011 | Partial; D-024 Confirmed |
| NFR-OBS-001 | Structured logs, health and background-job observability | OP-001, OP-010 | Merged |
| NFR-DATA-001 | Transactional data integrity and coordinated backup/restore | NFR-007, OP-003 | Exact |
| FR-I18N-001 | (phantom — never defined) English/Bangla public and admin language workflows | RE-003, AD-003 | Phantom; meaning recovered from Scope §5.7 allocation note (decision D4) |
| FR-I18N-002 | (phantom — never defined) Translation management | RE-005 | Phantom; same recovery trail |
| FR-I18N-003 | (phantom — never defined) Safe fallback behavior | RE-004, RE-011, RE-012 | Phantom; preference/fallback/switch clauses live in RE-011/RE-012 |

**Phantom retirement note (decision D4).** FR-I18N-001–003 were never defined anywhere in the documentation set; the only verifiable trace is the Scope v2 allocation note ("English/Bangla public and Admin interface workflows, translation management, and safe fallback. R1 remains explicitly English-first."). That meaning (not any speculative detail) is preserved above. Residual risk — that an undocumented detail could have existed inside a definition that was never written — is recorded as low and is isolated to R2 multilingual work items.

**Alias-only row (decision D3).** `RE-010` ("Support independent public and Admin language preferences") was a duplicate of `AD-003` and is retired as an alias; the sentence "Changing one preference does not unexpectedly change the other" is preserved inside AD-003's acceptance criteria.

## 2. Acceptance-criteria carry-over wordings (verbatim)

The legacy acceptance wordings below predates the catalog's current rows (or fall outside them). The approved reconciliation carried each wording into a current, located home; this section preserves the record that no criterion was silently dropped.

### 2.1 Admin collection ergonomics (from FR-ADM-007)

Legacy wording: "Search/filter/sort/pagination must be predictable wherever a collection is delivered."

Carried into: `REQUIREMENTS_CATALOG.md` §6.8 ("Admin collection ergonomics") and linked allocations ML-001, CO-004, AD-002. Scope v2 §5.2/§5.4 rows reference the carried clause.

### 2.2 Unsaved-change warnings and destructive-action confirmation (from FR-ADM-008)

Legacy wording: "Unsaved-change warnings and destructive-action confirmation for shipped admin workflows."

Carried into: AD-006 acceptance criteria (closing sentence) and Catalog §6.8. Consistent with the Admin unsaved-change workflow in PAGE_DESIGN_SPECIFICATION (Admin editor workflows).

### 2.3 Album destination metadata (from FR-GAL-003; owner condition 2)

Legacy wording: "Flexible album organization and destination metadata" (album fields include travel destination).

Evidence trail: PAGE_DESIGN_SPECIFICATION_v2.0.md §8.3 "Album editor" lists "Optional destination" and "Optional start and end dates" as album-editor fields (lines 914–934). PRD §8 provides only generic "optional metadata" support; no source document defines photo-level destination fields.

Carried into: GA-003 acceptance criteria — explicitly scoped as album-level only, with the unresolved-photo-level wording recorded here rather than invented. DO NOT extend to photo-level without a new verified source and owner approval.

### 2.4 Gallery reuse of Media Library (from FR-GAL-018)

Legacy wording: "Reuse Media Library storage, processing, usage tracking, backup, and restore behavior."

Carried into: Scope v2 §5.5 row (ML-002, OP-003, GA-010) and the architectural reuse rule anchored by decision D-008 (Confirmed) and GA-010/OP-003 restore-integrity criteria. Rebuilt Catalog rows reference the annex rather than restating a separate requirement.

## 3. Usage rules for agents and future editors

- Never reintroduce a legacy identifier as a live requirement, allocation, task or test-case reference.
- When reading older documents (PRD v1 references, historical plan revisions, this annex), resolve legacy identifiers through Section 1 above.
- When a canonical row's wording quotes "legacy" text, the authoritative preserved wording lives in this section 2, not in memory of the former RTM (whose v1 text has been superseded).
- Any future identifier change requires an ADR and a new row here; prefer retiring IDs as aliases over deleting their meaningful scope.

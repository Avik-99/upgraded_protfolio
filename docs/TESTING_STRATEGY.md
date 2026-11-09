# Testing Strategy

## 1. Test layers

-   Unit tests: domain invariants, validation, publishing and policy
    logic.
-   Integration tests: EF Core persistence, Identity, storage, email
    adapter, scanner adapter and background jobs.
-   End-to-end tests: critical visitor and admin journeys.
-   Security tests: authentication, authorization, upload, session,
    private resources and abuse controls.
-   Accessibility tests: automated scans plus manual keyboard and
    screen-reader checks.
-   Performance tests: representative page, query, upload and
    background-job workloads.
-   Recovery tests: backup integrity and isolated restore drills.

## 2. Critical scenarios

### Identity

-   Setup available only when no admin exists.
-   Two concurrent setup attempts cannot create multiple admins.
-   Setup becomes unavailable after success.
-   Public registration cannot assign Admin.
-   MFA enrollment and TOTP verification are required.
-   Lockout/rate limits work.
-   Reset token expires and cannot be reused.
-   Password reset does not bypass MFA and revokes sessions.

### Publishing and privacy

-   Draft never appears in public list, search, sitemap or direct public
    route.
-   Editing published content does not change current public version.
-   Unpublish invalidates relevant cache.
-   Unpublished translation is never used as fallback.
-   Private media is denied to anonymous and unauthorized users.
-   Unlisted content is direct-link only and excluded from
    indexing/discovery.

### Media and Gallery

-   Invalid extension, signature, size, corrupt image/PDF and scanner
    failure are rejected/quarantined.
-   Private uploads never enter public static paths.
-   Original remains intact after variant processing failure.
-   Duplicate detection does not leak private asset existence across
    authorization boundaries.
-   Referenced media cannot be permanently deleted.
-   Gallery is empty before admin upload.
-   Only admin-uploaded and selected photographs can be published.
-   Individual unpublished photo is inaccessible even inside published
    album.
-   Download permission is enforced server-side.
-   Comment is invisible until approved.
-   Restored album retains metadata and media links.

### Contact and email

-   Message is persisted before delivery attempt.
-   Mailtrap outage leaves message available in inbox.
-   Visitor confirmation and admin notification statuses are
    independent.
-   Retries do not create duplicate messages or duplicate replies.
-   Attachments obey count, size, allowlist and private-access rules.
-   Retention/deletion actions are confirmed and audited.

### Operations

-   Backup includes database and media manifest.
-   Integrity verification detects missing/corrupt backup objects.
-   Restore requires reauthentication, confirmation and pre-restore
    safety copy.
-   Restore validates database/media references.
-   RPO ≤4h and RTO ≤4h are demonstrated in documented test conditions.
-   Maintenance mode and health checks behave correctly.

## 3. Accessibility

Target WCAG 2.2 AA. Test keyboard-only operation, focus
visibility/order, semantic structure, labels, error associations,
contrast in dark/light themes, screen-reader announcements,
dialog/lightbox behavior and reduced motion.

## 4. Browser/device matrix

Test current/recent Chrome, Edge, Firefox and Safari; iOS Safari and
Android Chrome; mobile, tablet, laptop and desktop viewport sizes.
Define minimum versions before release.

## 5. Performance

Measure Core Web Vitals, page weight, image loading, database query
behavior, public page response, admin workflows and background
processing on representative staging infrastructure. Establish numeric
budgets before release sign-off.

## 6. Evidence and reporting

Each test references requirement IDs. Record environment, build, data
setup, steps, expected/actual result, logs/screenshots where
appropriate, defect ID and pass/fail. Never mark a requirement Verified
without evidence.

## 7. Release quality gates

-   All critical/high-severity defects resolved or formally accepted.
-   Security and authorization tests pass.
-   No private/draft content exposure.
-   Backup restore and recovery objectives verified.
-   Critical user journeys pass across supported browsers.
-   Accessibility review completed.
-   Performance budgets met or exceptions documented.
-   Documentation and traceability updated.

## 8. Requirement-to-scenario mapping (canonical identifiers)

**Identifier discipline (8 November 2026).** Test cases must reference
only canonical `REQUIREMENTS_CATALOG.md` IDs from the canonical 112-ID
baseline. Retired legacy identifiers (legacy `FR-*/NFR-*`, phantom
`FR-I18N-*`) must never appear in test names, case IDs, or evidence
records; resolve any historical reference through
`REQUIREMENTS_ALIAS_ANNEX.md`. The mappings below mirror the critical
scenario links in `REQUIREMENTS_TRACEABILITY_v2.md` §8.2 and remain
provisional until the owner approves the release baseline.

| Critical scenario (§2) | Canonical requirements covered |
|---|---|
| Setup availability and two concurrent setup attempts; setup closes after success | ID-001, ID-002, ID-003, ID-006 |
| MFA enrollment, lockout, reset expiry, session revocation | ID-004, ID-005, ID-006, ID-007, SEC-001–SEC-004 |
| Draft/private/unlisted exclusion from public list, search, sitemap and direct routes | CT-002, CT-003, RE-002, RE-004, RE-006, RE-009, GA-002, GA-004, GA-005, GA-013, PR-008 |
| Private media and attachment authorization | ML-002, ML-003, ML-004, GA-007, CO-005, CO-007, RE-002, RE-009, ID-006, SEC-007 |
| Scanner unavailable or unsafe upload quarantines fail-closed | ML-003, ML-004, ML-013, SEC-001–SEC-003, NFR-005 |
| Gallery parent/child visibility (unpublished photo inside published album) | GA-004, GA-005, GA-006, GA-007, GA-010, GA-011, GA-012, GA-013, ML-002, OP-003 |
| Gallery empty state before owner uploads; only owner-uploaded photographs | GA-001, GA-002 |
| Email/provider outage after contact submission must not lose the message | CO-001, CO-002, CO-003, CO-004, CO-008, NFR-005, NFR-007 |
| Retention/deletion and attachment lifecycle with confirmation and audit | CO-005, CO-006, CO-007, AN-002, AN-010, SEC-007, SEC-009, NFR-007, OP-003 |
| Backup including database and media manifest; restore integrity | ML-002, GA-010, OP-003, OP-004, OP-007, NFR-007 |
| WCAG 2.2 AA and browser/device coverage | PR-004, PR-006, PR-009, GA-011, NFR-001, NFR-002 |
| Performance budgets on representative staging | NFR-003 |

Cross-cutting non-functional coverage that is exercised across all
scenarios rather than owned by one scenario: SEC-001–SEC-009 (secure
defaults and hardening), AN-002 (admin actions excluded from visitor
metrics), OP-001 (health/observability), OP-002 (maintenance mode),
NFR-005 (reliability), NFR-006 (maintainability). Scenario coverage for
these is allocated during test-case authoring; do not claim a
requirement Verified until a test case with evidence references it
exactly once.

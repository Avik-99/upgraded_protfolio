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

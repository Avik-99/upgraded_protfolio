# Scope and Release Management

**Project:** Adib Hasan Avik --- Personal Portfolio & Travel Gallery\
**Document:** Scope and Release Management\
**Version:** 2.0-draft\
**Status:** Draft for product-owner review --- not yet approved\
**Release approach:** Option A --- R1 is the first public production
release\
**Supersedes:** `SCOPE_AND_RELEASES.md` only after explicit owner
approval

------------------------------------------------------------------------

## 1. Purpose

This document defines the approved product boundary, release allocation,
sequencing, dependencies, release gates, and scope-change process for
the Personal Portfolio & Travel Gallery.

It is intended to coordinate product decisions, engineering
implementation, testing, and AI-assisted development. It must be read
with the PRD, Requirements Catalog, Requirements Traceability, ADD,
Technical Specification, Testing Strategy, Assumptions and Dependencies,
and the implementation plan.

This document does not replace those documents:

-   **PRD:** defines what product should exist and how it should behave.
-   **Requirements Catalog:** provides stable requirement IDs and
    initial acceptance criteria.
-   **ADD:** defines architectural structure and technical boundaries.
-   **Technical Specification:** defines implementation choices,
    defaults, and deployment-dependent configuration.
-   **Testing Strategy:** defines test layers and critical scenarios.
-   **Requirements Traceability:** connects requirements to design,
    implementation, tests, and evidence.
-   **This document:** decides when approved capabilities are delivered
    and what must be true before each release is complete.

If a conflict is found, the coding agent must not silently choose a
convenient interpretation. It must identify the conflicting statements,
cite the affected documents/requirement IDs, and request a recorded
decision from the product owner.

## 2. Release approach and product boundary

### 2.1 Confirmed release approach

**Option A is selected:** Release 1 is intended to be the first public
production release on the canonical domain.

This does not mean testing starts at the end. Testing is continuous
throughout development:

1.  Development environment --- implementation, unit tests, and
    developer verification.
2.  Staging environment --- production-like integration, acceptance,
    security, accessibility, recovery, and deployment testing.
3.  Production environment --- the approved public release, with
    monitoring and controlled maintenance.

R1 must not be treated as a disposable prototype or an untested MVP. It
must meet the R1 production entry criteria in this document before
public launch.

### 2.2 Complete product scope

The complete approved product remains a dynamic, multi-page personal
portfolio and travel gallery with:

-   Public Viewer experience and a protected, single-administrator Admin
    Panel.
-   Public pages for Home, About, Education, Skills, Projects,
    Achievements, Certifications, Gallery, Resume, and Contact.
-   Structured content management, project case studies, and
    draft/preview/publish/unpublish workflows.
-   Single-admin initial setup, Identity authentication,
    authenticator-app MFA, recovery, and administrative audit.
-   Reusable Media Library with public and protected media handling.
-   Personal / Travel Gallery with albums, photographs, publication and
    visibility rules, browsing, and administration.
-   Contact inbox, message lifecycle, attachments, and independently
    tracked email delivery.
-   Resume language/professional variants and controlled publication.
-   English and Bangla content and Admin interface.
-   Search, SEO, privacy-conscious analytics, and consent/retention
    controls.
-   Security, accessibility, reliability, backup/restore, operational
    visibility, and portable deployment.

The complete product boundary is defined by the PRD and Requirements
Catalog. A later release assignment does not remove a requirement from
the product.

### 2.3 Explicit non-goals for the initial product

The following remain outside the initial approved scope unless
separately approved:

-   Multiple administrator accounts.
-   Public user accounts, visitor profiles, or general social-network
    functionality.
-   General-purpose multi-tenant SaaS CMS.
-   Public likes, ratings, or social engagement systems.
-   Full blog/newsletter.
-   Unrestricted page-builder functionality.
-   Automatic insertion of stock or AI-generated photographs as the
    owner's real portfolio or Gallery content.
-   Speculative integrations or architecture introduced without a
    demonstrated requirement.

Future possibilities listed in the PRD remain ideas, not delivery
commitments.

## 3. Prioritization and requirement status

Use MoSCoW together with business value, user impact, security/privacy
importance, technical dependencies, complexity, and release readiness.

-   **Must:** necessary for the assigned release to meet its purpose and
    acceptance gate.
-   **Should:** important and expected where feasible; any deferral
    requires a recorded reason and must not violate a Must requirement.
-   **Could:** beneficial but not required for the release.
-   **Won't in this release:** deliberately deferred; it remains in
    overall product scope unless explicitly removed by an approved scope
    change.

A requirement's release allocation is not permission to weaken its
acceptance criteria. If only a subset is delivered in a release,
identify that subset as a release slice and do not mark the complete
requirement as done unless its full catalog acceptance criteria are met.

### 3.1 Status vocabulary

Use these statuses consistently in planning and traceability:

-   **Planned:** allocated to a release but not started.
-   **In progress:** implementation or verification is underway.
-   **Implemented:** code/configuration exists; acceptance is not yet
    proven.
-   **Verified:** acceptance criteria passed with recorded evidence.
-   **Deferred:** deliberately assigned to a later release.
-   **Blocked:** cannot proceed because a dependency or decision is
    unresolved.
-   **Removed:** removed only through an approved scope change.

Do not equate "Implemented" with "Verified" or "Released."

## 4. Release overview

  ------------------------------------------------------------------------
  Release           Purpose           Public            Completion
                                      availability      standard
  ----------------- ----------------- ----------------- ------------------
  **R1 ---          Deliver the first First public      All R1 scope
  Professional      complete,         production        verified;
  Foundation**      credible, secure  release.          production
                    public portfolio                    security, privacy,
                    with essential                      accessibility,
                    owner-operated                      backup/recovery,
                    content                             deployment, and
                    management.                         operational gates
                                                        passed.

  **R2 --- Advanced Complete advanced Incremental       All R2 allocations
  Platform**        content           production        verified; no
                    operations,       release after     regression of R1
                    Gallery           staging           behavior; new
                    experience,       verification.     privacy/security
                    multilingual                        boundaries
                    workflows,                          verified.
                    search,                             
                    analytics, and                      
                    operational                         
                    management.                         

  **R3 ---          Improve and       Hardened          Full cross-product
  Production        independently     production        validation,
  Excellence**      validate          release.          documented
                    resilience,                         operational
                    security                            evidence, and all
                    maturity,                           remaining approved
                    performance,                        release
                    automation, and                     commitments
                    operational                         verified.
                    readiness across                    
                    the complete                        
                    product.                            
  ------------------------------------------------------------------------

**Important:** R3 is not the first time essential production security,
privacy, accessibility, or recovery protections are introduced. Those
protections are required for R1 wherever they apply to R1 features. R3
adds deeper validation, maturity, automation, and repeatable operational
evidence.

## 5. Requirement-to-release allocation

The following is the proposed allocation baseline derived from the PRD,
Requirements Catalog, Technical Specification, Testing Strategy, and the
current release outline. The allocation is a planning decision; it does
not rewrite the catalog's acceptance criteria. Where a full requirement
is split across releases, the release-specific slice must be recorded in
implementation tasks and traceability.

### 5.1 Public experience

  -----------------------------------------------------------------------
  Requirement IDs         Proposed allocation     Notes
  ----------------------- ----------------------- -----------------------
  `PR-001`, `PR-002`, `PR-007`            R1 foundation; R2       R1 delivers the
                          Gallery completion      portfolio pages and an
                                                  agreed Gallery
                                                  foundation. The Gallery
                                                  must not be silently
                                                  omitted from the
                                                  product.

  `CT-002` + Catalog §6.1            R1, continuous          Published-only
                                                  eligibility and no
                                                  draft/private leakage
                                                  are foundational.

  `PR-005`, `PR-006`            R1                      Dark/light themes and
                                                  persisted preference
                                                  are part of the first
                                                  public experience.

  `RE-003`            R2 complete; R1 English R1 is English-first and
                          baseline                must not claim full
                                                  bilingual support. R2
                                                  completes
                                                  English/Bangla public
                                                  workflows.

  `PR-003`            R2                      Global grouped search
                                                  across approved content
                                                  types.

  `PR-004`, `PR-009`            R1 baseline; R2/R3      Accessibility is built
                          regression and full     in from the start. R1
                          validation              must pass the
                                                  accessibility gate for
                                                  shipped journeys; later
                                                  releases expand and
                                                  repeat validation.

  `CO-001`, `CO-005`            R1 core; R2             R1 contact form and
                          conversation            durable inbox are
                          enhancements            production-safe. R2 may
                                                  add richer thread/reply
                                                  capabilities where not
                                                  included in R1.

  `RE-009`            R1 default published    Stable public access
                          resume; R2 variants     must never expose
                                                  drafts or unpublished
                                                  files.
  -----------------------------------------------------------------------

### 5.2 Admin and publishing

  -------------------------------------------------------------------------------
  Requirement IDs         Proposed allocation     Notes
  ----------------------- ----------------------- -------------------------------
  `ID-006`, `AD-002`            R1                      Single-admin protected
                                                  management area.

  `CT-001`, `CT-004`, `CT-005`            R1 core CRUD; R2        Every agreed module must be
                          completion of remaining allocated to a concrete task;
                          content types/workflows do not claim complete CRUD for
                                                  a module that is not
                                                  implemented.

  `CT-002`, `CT-003`            R1 core publishing; R2  Safe draft/published separation
                          advanced workflows as   is mandatory before public
                          needed                  release of managed content.

  `CT-006`            R2, if operationally    Scheduled publishing is
                          feasible and approved   required by the catalog where
                                                  appropriate. If deferred,
                                                  record the exact scope slice
                                                  and owner decision; do not
                                                  silently omit it.

  `AD-001`            R1 essential dashboard; R1 displays only real available
                          R2 expanded             counts and useful operational
                          operational/analytics   status; no fabricated metrics.
                          views                   

  `AD-004`            R1 essential settings;  Sensitive settings require
                          R2 remaining settings   validation, authorization, and
                                                  audit.

  `ML-001`, `CO-004` + Catalog §6.8            R1 for shipped          Search/filter/sort/pagination
                          collections; R2         must be predictable wherever a
                          remaining collections   collection is delivered (legacy FR-ADM-007 clause carried into Catalog §6.8; see REQUIREMENTS_ALIAS_ANNEX.md).

  `AD-006`            R1                      Unsaved-change warnings and
                                                  destructive-action confirmation
                                                  for shipped admin workflows (Catalog §6.8 carries the legacy wording; see REQUIREMENTS_ALIAS_ANNEX.md).
  -------------------------------------------------------------------------------

### 5.3 Identity and security workflows

  ------------------------------------------------------------------------------
  Requirement IDs                Proposed allocation     Notes
  ------------------------------ ----------------------- -----------------------
  `ID-001`--`ID-007`             R1                      One-time setup, role
                                                         seeding, secure admin
                                                         creation, MFA/recovery,
                                                         password reset, no
                                                         additional admin
                                                         creation, and audit are
                                                         production prerequisites.
                                                         Carries legacy
                                                         FR-SEC-001--FR-SEC-007
                                                         and NFR-SEC-002 (annex).

  `SEC-001`--`SEC-006`,
  plus `ID-006`                  R1 baseline; continuous Secure defaults,
                                                         server-side
                                                         authorization, secret
                                                         handling, CSRF, output
                                                         encoding, headers, rate
                                                         limits, and
                                                         dependency/container
                                                         checks apply from the
                                                         first public release.
                                                         R3 adds deeper hardening
                                                         and regression. Carries
                                                         legacy NFR-SEC-001--
                                                         NFR-SEC-003 (annex).

  `SEC-008`                      R1                      Reauthentication/MFA
                                                         for sensitive admin
                                                         actions.
  ------------------------------------------------------------------------------

### 5.4 Media Library

  ----------------------------------------------------------------------------
  Requirement IDs              Proposed allocation     Notes
  ---------------------------- ----------------------- -----------------------
  `ML-001`, `ML-012`,
  `ML-014`                     R1                      Seven approved media
                                                       categories are
                                                       established. Asset
                                                       metadata management
                                                       (`ML-014`) and media
                                                       audit history (`ML-012`)
                                                       cover the legacy
                                                       FR-MED-001/FR-MED-009
                                                       duties (annex).

  `ML-013`                     R1 basic upload; R2     R1 upload must be safe
                                robust bulk workflow    and reliable for its
                                                       supported use. R2
                                                       completes bulk
                                                       progress/retry
                                                       experience.

  `ML-003`, `ML-002`           R1                      Server-side content
                                                       validation and
                                                       public/private
                                                       separation are
                                                       mandatory before
                                                       uploads are used
                                                       publicly.

  `ML-006`, `ML-007`           R1 safe reference       No accidental deletion
                                protection; R2 richer   of referenced assets.
                                usage display

  `ML-005`                     R1 safe original        Processing failures
                                preservation; R2 full   must not destroy
                                responsive variant      originals in any
                                workflow                release.

  `ML-008`--`ML-010`,
  plus `ML-001` reuse          R2                      Recycle bin, duplicate
                                                       detection, advanced
                                                       search/filter, quotas,
                                                       and monitoring.

  `ML-004`                     R1                      A configured scanner or
                                                       equivalent approved
                                                       scanning service must
                                                       be operational for
                                                       uploaded content. Fail
                                                       closed/quarantine when
                                                       unavailable or
                                                       indeterminate.

  `ML-011`                     R1                      Persistent and portable
                                                       storage abstraction for
                                                       media.

  `OP-003`, `NFR-007`,
  `GA-010`                     R1 backup coverage; R2  Media and metadata must
                                management visibility;  be recoverable
                                R3 recovery drills      together. Carries legacy
                                                       FR-MED-012 (annex).
  ----------------------------------------------------------------------------

### 5.5 Personal / Travel Gallery

  ------------------------------------------------------------------------------
  Requirement IDs              Proposed allocation     Notes
  ---------------------------- ----------------------- -------------------------
  `GA-001`--`GA-006`           R1 secure foundation;   R1 includes a dedicated
                                R2 completion           route, core album/photo
                                                        management, media
                                                        integration, publication
                                                        rules, and safe
                                                        Public/Unlisted/Private
                                                        behavior for any exposed
                                                        Gallery functionality.
                                                        R2 completes the broader
                                                        experience. Album
                                                        destination fields per
                                                        Page Design Spec 8.3
                                                        (album-level only).

  `GA-007`--`GA-014`           R2                      Layout controls, featured
                                                        ordering, advanced
                                                        search/filter, full
                                                        viewer interactions,
                                                        related content, sharing
                                                        metadata, and controlled
                                                        downloads.

  `GA-008`                     R2, optional and        Comments remain disabled
                                disabled by default     unless moderation, rate
                                                        limits, privacy, and
                                                        retention are fully
                                                        implemented. Carries
                                                        legacy FR-GAL-014/
                                                        FR-GAL-015 (annex).

  `AN-006`                     R2                      Gallery-specific
                                                        aggregate analytics and
                                                        privacy controls.

  `GA-002`                     R1, continuous          Only
                                                        owner-uploaded/selected
                                                        photographs become real
                                                        Gallery content. Until
                                                        then, show an honest
                                                        empty state.

  `ML-002`, `OP-003`,
  `GA-010`                     R1 foundation; R2/R3    Reuse Media Library
                                validation              storage, processing,
                                                        usage tracking, backup,
                                                        and restore behavior.
                                                        Carries legacy
                                                        FR-GAL-018 (annex).

  `GA-015`                     R2 optional             Gallery content settings
                                                        management at album and
                                                        photograph level
                                                        (Catalog section 5.6).
  ------------------------------------------------------------------------------

**Gallery release rule:** R1 may deliver a deliberately limited Gallery
foundation, but it must not expose an incomplete access-control model.
If the product owner later chooses to defer the public Gallery entirely,
update the PRD, this allocation, traceability, and release acceptance
records together.

### 5.6 Contact, email, and resume

  ----------------------------------------------------------------------------
  Requirement IDs              Proposed allocation     Notes
  ---------------------------- ----------------------- -----------------------
  `CO-002`, `CO-003`           R1                      Persist before email;
                                                        track message and
                                                        notification delivery
                                                        independently; bounded
                                                        retry and idempotency.
                                                        Carries legacy
                                                        FR-CON-001/FR-CON-002
                                                        (annex).

  `CO-004`, `CO-008`           R2                      Conversation threads,
                                                        visitor-visible replies,
                                                        reliable replies (retry
                                                        must not create
                                                        duplicates). Carries
                                                        legacy FR-CON-003
                                                        (annex).

  `CO-005`, `CO-007`           R1                      Attachment policy
                                                        (numeric limits
                                                        configurable; DEC-005
                                                        pending), validation,
                                                        scanning, and private
                                                        authorized access are
                                                        required if attachments
                                                        are enabled in R1.
                                                        Carries legacy
                                                        FR-CON-004 (annex).

  `CO-006`                     R1 basic safe handling; Do not silently delete
                                R2 expanded retention   active messages. Audit
                                controls                retention/deletion
                                                        operations.

  `RE-001`, `RE-007`           R2 complete; R1 default R1 provides the initial
                                resume                  published resume. R2
                                                        adds independent
                                                        language/professional
                                                        variants. Carries legacy
                                                        FR-RES-001 (annex).

  `RE-002`, `RE-009`           R1                      Draft/unpublished
                                                        resume files must never
                                                        be public. Carries
                                                        legacy FR-RES-002
                                                        (annex).

  `AN-005`                     R2                      Aggregate download
                                                        analytics. Carries
                                                        legacy FR-RES-003
                                                        (annex).

  `RE-008`                     R1                      Limited resume version
                                                        distinguishability
                                                        (current/previous/
                                                        draft/unpublished);
                                                        not a version-control
                                                        system. Retention depth
                                                        is an unresolved owner
                                                        decision (Catalog DEC-013).
  ----------------------------------------------------------------------------

### 5.7 Multilingual, SEO, and analytics

  -------------------------------------------------------------------------------
  Requirement IDs                Proposed allocation     Notes
  ------------------------------ ----------------------- ------------------------
  `RE-003`, `RE-004`,
  `RE-005`                       R2                      English/Bangla public
                                                          workflows, translation
                                                          management, and safe
                                                          fallback. R1 remains
                                                          explicitly English-first.
                                                          Phantom FR-I18N-001--
                                                          FR-I18N-003 retired;
                                                          intended meaning mapped
                                                          to RE-003/RE-004/RE-005
                                                          and AD-003 (annex,
                                                          decision D4).

  `AD-003`                       R2                      Admin interface language
                                                          independent of the
                                                          public website
                                                          language; guaranteed
                                                          by the merged-from-
                                                          RE-010 clause in
                                                          Catalog AD-003 (annex).

  `PR-008`, `RE-003`, `RE-006`   R1 canonical/essential  R2 completes bilingual
                                  SEO; R2 complete        prefixes and localized
                                  localized routing       metadata behavior.
                                                          Carries legacy
                                                          FR-SEO-001 (annex).

  `PR-008`, `GA-009`, `RE-006`   R1 sitemap for          Draft/private/unlisted
                                  R1-eligible content; R2 exclusions apply from
                                  full multilingual       R1. Carries legacy
                                  eligibility             FR-SEO-002 (annex).

  `AN-001`--`AN-004`, `AN-010`   R2                      Privacy-conscious
                                                          aggregate analytics,
                                                          exports, consent, and
                                                          retention. R1 must not
                                                          introduce unapproved
                                                          invasive tracking.
                                                          Carries legacy
                                                          FR-ANA-001--FR-ANA-002
                                                          (annex).

  `AN-002`, `AN-007`, `AN-008`   R2                      Admin activity excluded
                                                          from visitor metrics;
                                                          authorized exports
                                                          without sensitive data;
                                                          retention per configured
                                                          policy (AN-008 value
                                                          pending D-038).

  `AN-009`                       R2 owner-gated          Should priority; date
                                                          comparisons require
                                                          explicit owner approval
                                                          before P20/P21 scope
                                                          lock (Catalog section
                                                          5.9).
  -------------------------------------------------------------------------------

### 5.8 Non-functional requirements

  ------------------------------------------------------------------------------
  Requirement IDs                Allocation              R1 production
                                                          requirement
  ------------------------------ ----------------------- -----------------------
  `SEC-001`--`SEC-006`,
  plus `ID-006`                  R1 baseline; R3         All essential security
                                  advanced review         controls for R1
                                                          features must pass
                                                          before launch. Carries
                                                          legacy NFR-SEC-001--
                                                          NFR-SEC-003 (annex).

  `AN-002`, `AN-010`,
  `SEC-007`, `SEC-009`           R1 baseline; R2         Data minimization,
                                  expanded workflows; R3  privacy disclosure,
                                  review                  safe access, and
                                                          retention decisions for
                                                          live features. Carries
                                                          legacy NFR-PRIV-001
                                                          (annex).

  `NFR-001`                      R1 for shipped          Shipped R1 journeys
                                  journeys; R2/R3         must meet the agreed
                                  expanded validation     accessibility target
                                                          before production
                                                          launch.

  `NFR-003`                      R1 baseline             Establish realistic
                                  measurement; R2         initial budgets before
                                  optimization; R3 load   R1 sign-off; do not
                                  testing                 invent numeric targets
                                                          (D-037 pending).

  `NFR-005`                      R1 baseline; continuous Central errors, health
                                                          checks, bounded
                                                          retries, idempotency,
                                                          and graceful handling
                                                          for production
                                                          dependencies.

  `OP-004`                       R1 production gate; R3  The approved RPO <=4h
                                  repeatable drills and   and RTO <=4h targets
                                  maturity                must be feasible and
                                                          demonstrated before the
                                                          first production launch
                                                          if they are retained as
                                                          hard production
                                                          commitments.

  `NFR-002`, `PR-009`            R1 supported-browser    Agree minimum supported
                                  baseline; R2/R3 full    versions before release
                                  regression              sign-off.

  `NFR-006`                      R1, continuous          Architecture
                                                          boundaries, tests, and
                                                          traceability maintained
                                                          from the start.

  `OP-005`, `OP-006`,
  `OP-009`, `ML-011`             R1                      Clean Docker-compatible
                                                          deployment to the
                                                          selected production
                                                          target. Carries legacy
                                                          NFR-DEP-001 (annex).

  `OP-001`, `OP-010`             R1 essential            R1 must provide enough
                                  monitoring; R2 expanded operational visibility
                                  dashboard; R3           to detect critical
                                  alert/runbook maturity  production failures.
                                                          Carries legacy
                                                          NFR-OBS-001 (annex).

  `NFR-007`, `OP-003`            R1, continuous          Transactions, reference
                                                          integrity, and
                                                          coordinated
                                                          database/media backup
                                                          behavior. Carries
                                                          legacy NFR-DATA-001
                                                          (annex).

  `OP-002`                       R1                      Controlled maintenance
                                                          mode (Catalog section
                                                          5.10).

  `OP-008`                       R1                      Canonical domain,
                                                          HTTPS, www policy and
                                                          certificate management;
                                                          final domain pending
                                                          D-036.
  ------------------------------------------------------------------------------

## 6. Release 1 --- Professional Foundation

### 6.1 Objective

Deliver the first public production version: a credible, polished
portfolio that the owner can manage without code edits, with secure
administration and dependable essential operations.

R1 is not required to contain every advanced feature in the complete
product, but every R1 feature must be complete enough to operate safely
in production.

### 6.2 Included scope

**Public experience** - Home, About, Education, Skills, Projects,
Achievements, Certifications, Resume, and Contact. - Professional
project case-study pages and project status presentation. - Executive
Dark design direction, deliberate light theme, responsive layouts, and
persistent theme preference. - English-first public content with a
clear, non-misleading language strategy; do not present incomplete
Bangla support as complete. - Essential metadata, canonical URLs,
sitemap, and published-only public content. - A secure, intentionally
limited Gallery foundation as allocated in Section 5.5.

**Admin and content** - Protected single-admin Admin Panel. - One-time
setup, Identity authentication, authenticator-app MFA, recovery codes,
password reset, and security audit events. - Core dashboard with
truthful counts/status. - Structured CRUD for the content types included
in R1. - Draft, preview, publish, and unpublish with published-version
isolation. - Safe form validation, unsaved-change warnings, and
destructive-action confirmation. - Core website settings needed for R1
operation.

**Media and files** - Seven Media Library categories. - Safe upload
validation and public/private storage separation. - Persistent storage
outside the disposable container layer. - Scanner integration with
fail-closed/quarantine behavior. - Original preservation and safe
failure handling for image processing. - Reference-aware
replacement/deletion safeguards. - Media and database included in a
coordinated backup approach.

**Contact and resume** - Contact form with approved inquiry
categories. - Optional attachments only if all R1 private-storage,
validation, scanning, authorization, and size/count rules are
implemented. - Persist contact messages before notification attempts. -
Admin inbox and independent visitor/admin notification delivery
status. - Mailtrap sandbox in development and configured production
sending after sender-domain verification. - Initial published resume
upload/preview/download with no public access to drafts.

**Engineering and operations** - Error handling, structured logs,
correlation where configured, health checks, and essential operational
visibility. - Rate limiting, anti-forgery, server-side validation,
output encoding, secure headers, secret management, and authorization. -
Automated unit, integration, architecture, web, and critical end-to-end
tests. - Docker-compatible production deployment, persistent volumes,
controlled migrations, TLS/HTTPS, backup, restore, and rollback
procedure. - Accessibility and performance verification for the actual
R1 pages and workflows.

### 6.3 R1 exclusions / deferrals

Unless a requirement is explicitly brought forward through an approved
decision, R1 does not include: - Complete Bangla content and Admin
interface translation workflows. - Global grouped search across all
approved content types. - Full advanced Gallery browsing, location/map
browsing, related content, advanced filters, optional comments, and
Gallery analytics. - Complete Media Library recycle bin, quotas,
duplicate-detection, and advanced management. - Advanced analytics and
exports. - Full contact conversation/reply workflows. - Multiple resume
variants. - Advanced operational dashboards and automated deployment
sophistication beyond what is needed for safe production.

### 6.4 R1 dependencies

-   Initial administrator setup depends on database migration, role
    creation, atomic setup guard, Identity, and MFA.
-   Publishing depends on authorization, versioning, eligibility policy,
    and cache invalidation.
-   Public media depends on validation, scanning, storage, and
    publication policy.
-   Contact attachments depend on private storage, scanning, retention,
    and authorized delivery.
-   Contact notifications depend on durable message persistence and
    retry-safe delivery.
-   Gallery foundation depends on Media Library, scan state, storage,
    image processing, publication, and parent/child visibility rules.
-   Production launch depends on domain, TLS, secrets, database,
    persistent media, external backup destination, and operational
    access.

### 6.5 R1 production entry and exit gates

R1 may be publicly launched only when all applicable conditions are
verified:

1.  All R1-assigned requirement slices have stable IDs, implementation
    tasks, acceptance tests, and recorded evidence.
2.  All public pages render correctly with real owner-approved content
    or honest empty states; no fabricated experience, metrics,
    credentials, or photographs.
3.  Admin setup is one-time and concurrency-safe; MFA and recovery work;
    no public registration or second-admin path exists.
4.  Every admin operation and private file endpoint is protected
    server-side.
5.  Draft, unpublished, private, and ineligible unlisted content cannot
    leak through pages, routes, search, sitemap, cache, thumbnails, or
    direct media delivery.
6.  Contact messages remain stored if email delivery fails; retries are
    bounded and do not duplicate messages.
7.  Upload validation and scanning work; scanner failure is not treated
    as clean; private files are not served by static-file middleware.
8.  Database and media backup/restore have been tested together. The
    four-hour RPO/RTO targets must be demonstrated before launch if
    retained as hard production commitments. If the selected
    hosting/database plan cannot meet them, production launch is blocked
    until the owner explicitly revises the target or chooses a capable
    deployment.
9.  R1 pages and workflows pass the agreed WCAG 2.2 AA acceptance
    checks; unresolved critical accessibility barriers block launch.
10. Critical user journeys pass on the agreed browser/device matrix.
11. Numeric performance budgets are set from a representative staging
    baseline and pass, or exceptions are explicitly accepted by the
    owner without compromising security or data integrity.
12. Production secrets are external to source control; HTTPS, secure
    cookies, headers, rate limits, logging, health checks, and error
    handling are verified.
13. Production deployment, migration, backup-before-change, rollback,
    and incident contact/runbook steps are documented and rehearsed.
14. No unresolved critical/high-severity defect remains unless the owner
    records an explicit risk acceptance with mitigation and
    expiry/review date.
15. Requirements Traceability and release documentation are updated;
    "Verified" is supported by evidence, not by the existence of code or
    screens.

## 7. Release 2 --- Advanced Platform

### 7.1 Objective

Complete the product's advanced content operations and visitor-discovery
experience while preserving R1 production behavior and security
boundaries.

### 7.2 Included scope

-   Complete English/Bangla public content and Admin interface
    workflows.
-   Translation editing, completion indicators, preview, independent
    publication, safe fallback, language switching, localized slugs,
    canonical/hreflang, and multilingual sitemap behavior.
-   Global grouped search across published projects, skills,
    achievements, certifications, and education.
-   Advanced Media Library workflows: bulk progress/retry, responsive
    variants, usage references, recycle bin, duplicate detection,
    metadata search/filter, quotas, and audit visibility.
-   Complete Gallery visitor experience: albums, unified browsing,
    masonry/uniform layouts, featured ordering, advanced search/filter,
    full-screen viewer, keyboard/mobile navigation, related content,
    shareable URLs, OpenGraph metadata, and controlled download
    behavior.
-   Gallery aggregate analytics and privacy controls.
-   Optional Gallery comments only if explicitly enabled, with
    moderation, rate limits, privacy protection, retention, and audit.
    They remain disabled by default.
-   Expanded analytics and exports with admin exclusion, consent, and
    retention behavior.
-   Resume language/professional variants and independent publication.
-   Richer contact conversations, replies, internal notes, and retention
    workflows.
-   Expanded backup management, operational dashboard,
    job/email/storage/scanner/backup visibility, and operational alerts.

### 7.3 R2 dependencies

-   Multilingual workflows depend on content translation model,
    localized slug strategy, route resolution, fallback policy,
    canonical/hreflang, and sitemap eligibility.
-   Global search depends on a shared published-content eligibility
    policy and indexing/update behavior.
-   Advanced Gallery depends on the R1 Media Library foundation,
    metadata, parent/child publication rules, image variants, cache
    invalidation, and authorized download delivery.
-   Comments depend on moderation, spam/abuse controls, rate limiting,
    retention, and admin audit.
-   Analytics depends on approved privacy/consent decisions, event
    definitions, retention, and admin exclusion.
-   Resume variants depend on secure private source storage and
    published-version delivery.
-   Operational dashboards depend on reliable job, email, storage,
    scanner, backup, and health telemetry.

### 7.4 R2 exit gates

-   All R2 requirement allocations are verified against catalog
    acceptance criteria.
-   R1 regression suite passes; R1 public behavior and data boundaries
    remain intact.
-   English/Bangla route switching and fallback never expose unpublished
    translations.
-   Search and analytics exclude drafts, private records, and
    unauthorized information.
-   Gallery album/photo eligibility is consistent across listing,
    detail, search, sitemap, cache, thumbnail, and download paths.
-   Comment moderation remains mandatory if comments are enabled.
-   Media deletion/replacement respects references and retention.
-   Backup/restore remains consistent after new data types and media
    workflows.
-   Accessibility, performance, security, and browser checks cover all
    newly added workflows.
-   Documentation, operational dashboards, and traceability reflect the
    shipped behavior.

## 8. Release 3 --- Production Excellence

### 8.1 Objective

Raise the maturity and repeatability of the complete platform through
deeper security review, resilience validation, performance work,
automation, and operational readiness.

R3 is an improvement and assurance release, not a place to postpone
protections required for R1 or R2 production features.

### 8.2 Included scope

-   Advanced security hardening, threat-model review,
    dependency/container scanning improvements, and security regression
    suite.
-   Repeatable disaster-recovery exercises, documented restore runbooks,
    recovery evidence, and operational review of RPO/RTO performance.
-   Comprehensive end-to-end, regression, cross-browser, accessibility,
    and failure-mode testing.
-   Performance profiling, load testing, image/query/cache optimization,
    and approved numeric budgets.
-   Deployment automation, controlled production migrations, rollback,
    release approvals, and environment consistency.
-   Operational alerting, incident procedures, maintenance workflow,
    backup verification, and monitoring maturity.
-   Final review of architecture boundaries, documentation completeness,
    traceability, and technical debt that materially affects reliability
    or maintainability.

### 8.3 R3 exit gates

-   All remaining approved product requirements are either verified,
    explicitly deferred with owner approval, or removed through formal
    scope change.
-   Security review findings are resolved or explicitly risk-accepted
    with mitigation and review date.
-   Recovery exercises demonstrate the agreed targets under documented
    conditions; failures result in a remediation plan and prevent claims
    of verified recovery.
-   Accessibility and browser/device validation evidence is current for
    the complete shipped product.
-   Performance budgets and load-test conditions are documented;
    material regressions are resolved or approved.
-   Deployment, migration, rollback, alerting, and incident runbooks are
    exercised.
-   Requirements Traceability has no unexplained missing links or
    unsupported "Verified" statuses.
-   The product owner approves the final release evidence and known
    residual risks.

## 9. Cross-release dependencies and sequencing

The following dependencies are architectural constraints, not optional
implementation preferences:

  -----------------------------------------------------------------------
  Capability                          Must precede / enable
  ----------------------------------- -----------------------------------
  Identity, one-time setup, MFA,      Admin Panel, settings, private
  authorization                       operations, protected media

  Published/draft version model and   Public pages, Gallery, search,
  eligibility policy                  sitemap, cache, resume publication

  Media Library, scanner, storage     Gallery, contact attachments,
  abstraction                         resume files, image processing,
                                      backup

  Parent/child visibility and         Gallery albums/photos, direct URLs,
  authorization policy                downloads, thumbnails

  Durable contact persistence and     Email notifications, replies,
  outbox/retry design                 delivery monitoring

  Translation model and localized URL English/Bangla editing, fallback,
  strategy                            hreflang, localized sitemap

  Telemetry/event definitions and     Analytics dashboards, exports,
  privacy decisions                   retention

  Database/media backup manifest and  RPO/RTO evidence, operational
  restore procedure                   backup dashboard

  Test environments and release       All release gates and production
  evidence conventions                approvals
  -----------------------------------------------------------------------

The implementation plan must respect these dependencies. Do not build a
public feature first and add its privacy or authorization rules later.

## 10. Continuous quality requirements

These practices apply to every release:

-   Use the stable requirement IDs in branch/task/PR/test naming where
    practical.
-   Implement and test domain invariants and application policies
    independently from MVC presentation.
-   Keep Domain/Application/Infrastructure/Presentation dependency
    direction consistent with the ADD.
-   Use server-side validation and authorization; hiding a control in
    the UI is not security.
-   Preserve public/private separation for media and content.
-   Keep secrets out of source code, logs, test artifacts, and
    documentation.
-   Use real owner-provided content only; use clearly identified
    placeholders in development and never publish them as facts.
-   Maintain automated tests for behavior that could expose private
    data, corrupt content, or break publishing.
-   Update technical documentation when implementation decisions
    materially differ from the Technical Specification.
-   Avoid speculative abstractions, microservices, or integrations
    without a documented requirement.
-   Do not mark a requirement Verified without test evidence.

## 11. Environments and release workflow

### 11.1 Environments

-   **Development:** local implementation, test data, sandbox email,
    local persistent media, and diagnostic logging.
-   **Staging:** production-like deployment configuration using
    non-production data and credentials; used for release acceptance,
    security, accessibility, performance, backup/restore, and rollback
    rehearsal.
-   **Production:** canonical public domain, HTTPS, production secrets,
    persistent storage, restricted access, monitoring, external backups,
    and controlled changes.

Production data must not be copied into development or staging without
an approved, privacy-safe sanitization process.

### 11.2 Release workflow

1.  Confirm release allocation and dependencies.
2.  Create implementation tasks referencing requirement IDs.
3.  Implement in small, reviewable increments.
4.  Run relevant unit, integration, architecture, and security tests
    continuously.
5.  Deploy candidate build to staging.
6.  Execute acceptance, accessibility, browser, performance,
    backup/restore, and operational checks applicable to the release.
7.  Record evidence and resolve defects.
8.  Obtain product-owner release approval.
9.  Deploy using controlled migration and backup procedures.
10. Verify production health and critical user journeys.
11. Monitor, record incidents, and update traceability.

## 12. Risks, assumptions, and release blockers

The following must remain visible in the release plan:

  -------------------------------------------------------------------------
  Risk / open item        Impact                  Required handling
  ----------------------- ----------------------- -------------------------
  Hosting cannot meet     Production recovery     Validate
  RPO/RTO ≤4h             commitment cannot be    provider/database/media
                          met                     backup capability before
                                                  R1; do not claim
                                                  compliance without a
                                                  timed restore.

  Production              Public launch and       Resolve before production
  domain/TLS/reverse      secure                  release.
  proxy unresolved        cookies/SEO/email       
                          configuration blocked   

  Scanner deployment      Unsafe files could be   Fail closed/quarantine;
  unavailable or          published               select a viable scanner
  unreliable                                      deployment before
                                                  enabling uploads.

  Media and database      Restored content may be Use coordinated backup
  backups diverge         broken                  manifest and integrity
                                                  checks.

  Gallery visibility      Private/unpublished     Shared policy across
  semantics inconsistent  content disclosure      album, photo, media,
                                                  cache, search, sitemap,
                                                  and download.

  Translation/slug        Broken language         Resolve before R2
  strategy unresolved     switching and duplicate multilingual
                          SEO URLs                implementation.

  Numeric performance     Cannot objectively sign Establish from
  budgets unresolved      off performance         representative staging
                                                  baseline before relevant
                                                  release gate.

  Legal/privacy wording   Inadequate disclosure   Obtain appropriate review
  unresolved              or retention handling   before production use of
                                                  affected
                                                  processing/analytics.

  Scope exceeds delivery  Delays and incomplete   Use explicit release
  capacity                releases                slicing and recorded
                                                  deferrals; never weaken
                                                  security gates to meet a
                                                  date.

  Owner content not yet   Empty or incomplete     Use honest empty states;
  supplied                public sections         do not fabricate facts,
                                                  photos, certificates, or
                                                  metrics.
  -------------------------------------------------------------------------

### 12.1 Open decisions are not silently resolved here

This document does not invent: - Canonical domain, DNS, hosting
provider, VPS/cloud plan, or deployment budget. - SQL Server hosting and
recovery mechanism. - Exact browser minimum versions. - Numeric
performance budgets. - Analytics provider and final consent/legal
wording. - Production malware-scanner hosting details. - Exact legal
policy language. - Any personal biography, project metric, certificate,
employment history, or Gallery photograph.

Track these in `ASSUMPTIONS_AND_DEPENDENCIES.md` and the Technical
Specification. Each open decision needs an owner, target milestone, and
impact assessment.

## 13. Scope-change control

No AI coding agent or contributor may silently add, remove, or
reclassify approved scope.

Every proposed scope change must record:

1.  Change ID and date.
2.  Requester and decision owner.
3.  Existing requirement ID(s), or proposed new requirement ID.
4.  Description and business justification.
5.  Whether the change is addition, removal, clarification, or release
    reassignment.
6.  Impact on user experience, architecture, data model,
    security/privacy, accessibility, performance, operations, and cost.
7.  Dependency and implementation impact.
8.  Test and documentation impact.
9.  Proposed release and any schedule/capacity impact.
10. Decision: approved, rejected, deferred, or needs clarification.
11. Approval evidence and affected document revisions.

A release reassignment does not delete a requirement. A requirement may
be removed only through explicit product-owner approval and updates to
the PRD, Requirements Catalog, Traceability, Testing Strategy, and
implementation plan.

## 14. Traceability and completion tracking

Maintain the traceability chain:

**Requirement → PRD section → ADD component → Technical Specification →
Release allocation → Implementation task → Test case/result → Release
evidence**

For each requirement, record at minimum:

-   Stable requirement ID.
-   Release and release slice.
-   Priority.
-   PRD and design/architecture references.
-   Technical decision or open dependency.
-   Implementation task/PR or commit reference.
-   Test case IDs and latest result.
-   Status: Planned, In progress, Implemented, Verified, Deferred,
    Blocked, or Removed.
-   Evidence location and owner approval where required.

The traceability file is `REQUIREMENTS_TRACEABILITY_v2.md`. Its matrix is
reconciled to the canonical 112-ID baseline (8 November 2026), and it
states that its readiness audit is pending. This document does not claim
that audit is complete. Update the traceability file after this release
allocation is approved.

## 15. AI coding-agent execution rules

The coding agent must:

1.  Treat the PRD and Requirements Catalog as the product-scope sources;
    use this document for release timing and scope allocation.
2.  Treat the ADD and Technical Specification as architecture/technical
    guidance, respecting their approved/recommended/deployment-dependent
    distinctions.
3.  Implement only the current approved release slice unless explicitly
    instructed otherwise.
4.  Preserve future-release requirements in the catalog and
    traceability; do not delete or ignore them.
5.  Never convert a recommendation, assumption, or TBD into an approved
    decision without authorization.
6.  Never claim a requirement is complete because a page, form, or
    database table exists.
7.  Produce tests and evidence for acceptance criteria, especially
    security, privacy, publication, file access, backup, and recovery.
8.  Identify conflicts between documents before implementation and
    request a decision rather than guessing.
9.  Keep the solution within the approved modular monolith/Clean
    Architecture direction unless an approved architecture change is
    recorded.
10. Avoid fabricating portfolio content, metrics, images, or
    credentials.
11. Update implementation tasks, tests, traceability, and relevant
    documentation when scope or behavior changes.
12. Stop and report when a dependency blocks safe implementation; do not
    bypass the dependency to make a demo appear functional.

## 16. Approval checklist and document status

### 16.1 Review checklist

-   [ ] Product owner confirms R1 is the first public production release
    (Option A).
-   [ ] Product owner confirms the proposed R1 Gallery foundation / R2
    completion allocation.
-   [ ] Product owner reviews requirement-to-release allocation and any
    release slices.
-   [ ] R1 production gates, including accessibility and recovery
    expectations, are accepted.
-   [ ] Open decisions and blockers have owners and target milestones.
-   [ ] Requirements Traceability is updated and audited.
-   [ ] Implementation Plan is reconciled with the approved release
    allocation.
-   [ ] Product owner approves this document as the release baseline.

### 16.2 Current status

**Version 2.0-draft --- proposed release baseline, pending owner
review.**

Option A is confirmed. The detailed allocations in this draft are
recommendations derived from the existing project documents; they are
not all individually approved merely because they appear here. In
particular, the R1 Gallery foundation, exact release slices, and R1
recovery/accessibility entry evidence require owner review and
confirmation.

The original `SCOPE_AND_RELEASES.md` should remain unchanged until this
draft is reviewed and explicitly approved. After approval, adopt this
document as the new canonical release baseline and update the
Requirements Traceability and Implementation Plan.

#### 2.0-r1 reconciliation note (8 November 2026)

Section 5 was rebuilt on the approved 112-ID canonical requirement baseline
(reconciliation decisions D1-D6, owner-conditioned): legacy FR-*/NFR-*
allocation tokens were re-pointed to `REQUIREMENTS_CATALOG.md` IDs, the
retired phantom FR-I18N-001--FR-I18N-003 were re-pointed per decision D4,
and every legacy identifier remains resolvable as an alias in
`REQUIREMENTS_ALIAS_ANNEX.md`. The four carried acceptance-criterion
wordings (admin search/filter/sort/pagination, admin unsaved-change
warnings, album destination metadata per Page Design Specification 8.3,
and Gallery reuse of Media Library storage) are preserved in the rebuilt
rows and the Catalog. Release slices (R1/R2/R3) are unchanged. Document
status remains draft --- pending owner review; this note does not declare
the baseline approved.

------------------------------------------------------------------------

**Document owner:** Product owner\
**Version:** 2.0-draft\
**Approval:** Pending

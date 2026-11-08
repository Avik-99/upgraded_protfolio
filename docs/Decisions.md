DECISIONS
=========

Product and Architecture Decision Register
------------------------------------------

**Project:** Adib Hasan Avik — Personal Portfolio & Travel Gallery**Document:** DECISIONS.md**Version:** 2.0**Status:** Comprehensive Review Draft — Owner Approval Required**Document Type:** Decision Register**Decision Authority:** Product Owner**Primary Platform:** .NET 10 / ASP.NET Core MVC**Related Documents:** PRD, Requirements Catalog, ADD, Technical Specification, Scope and Releases, Testing Strategy, Design System, Requirements Traceability Matrix, Implementation Plan, Agent Instructions

1\. Purpose
===========

This document is the authoritative register of approved, proposed, open, rejected and superseded product, architecture, technical, design and operational decisions for the Personal Portfolio & Travel Gallery.

Its purpose is to:

1.  Preserve decisions already approved by the Product Owner.
    
2.  Prevent contradictory decisions across project documentation.
    
3.  Distinguish approved commitments from technical recommendations.
    
4.  Record the reasoning and consequences of important decisions.
    
5.  Identify unresolved decisions and their dependencies.
    
6.  Provide reliable instructions to developers and AI coding agents.
    
7.  Establish a controlled process for changing decisions.
    
8.  Maintain traceability between decisions, requirements, architecture, implementation and testing.
    

This document records decisions. It does not replace the PRD, Architecture Design Document, Technical Specification or Requirements Catalog.

Those documents define their respective areas in greater detail.

2\. Authority and interpretation
================================

2.1 Decision authority
----------------------

The Product Owner has final authority over product scope, user-facing behavior, approved technology choices and changes to previously confirmed decisions.

Developers and AI coding agents may recommend alternatives, identify incompatibilities and propose improvements.

They must not silently replace confirmed decisions.

2.2 Relationship with other documents
-------------------------------------

DocumentResponsibilityPRDDefines product goals, scope, users and product requirementsRequirements CatalogDefines stable requirement IDs and acceptance criteriaADDDefines architectural structure and architectural boundariesTechnical SpecificationDefines technical implementation constraints and recommended defaultsDesign SystemDefines visual identity, design tokens, components and interaction rulesScope and ReleasesDefines delivery scope, release allocation and release gatesTesting StrategyDefines verification approach and quality gatesRequirements TraceabilityConnects requirements to design, implementation and testsImplementation PlanDefines implementation sequence, tasks and dependenciesDECISIONSRecords approved choices, proposed choices and unresolved decisions

2.3 Conflict resolution
-----------------------

When documentation conflicts:

1.  An explicitly confirmed Product Owner decision must not be silently overridden.
    
2.  The PRD remains the primary source for approved product scope and behavior.
    
3.  The Requirements Catalog is the primary source for stable requirement IDs and acceptance criteria.
    
4.  The ADD governs architectural structure and dependency boundaries.
    
5.  The Technical Specification governs detailed technical implementation within approved constraints.
    
6.  The Design System governs visual and interaction consistency.
    
7.  The Scope and Releases document governs release allocation.
    
8.  The Testing Strategy governs verification methodology.
    

A contradiction must be reported and resolved. Developers and AI agents must not independently invent a compromise.

3\. Decision status definitions
===============================

StatusMeaningConfirmedExplicitly approved by the Product OwnerProposedRecommended solution awaiting approvalOpenNo final decision has been madeRejectedConsidered and explicitly declinedSupersededReplaced by a newer decision

**Important:** A recommendation in a Technical Specification is not automatically a confirmed Product Owner decision.

A decision can be technically reasonable and still require approval.

4\. Decision record format
==========================

Each significant decision should contain:

*   **ID:** Permanent identifier.
    
*   **Title:** Short descriptive name.
    
*   **Status:** Current decision state.
    
*   **Decision:** The selected or proposed outcome.
    
*   **Rationale:** Why the decision exists.
    
*   **Consequences:** Important implications.
    
*   **Affected documents:** Documents that must remain consistent.
    
*   **Verification:** How compliance will be checked.
    

Dates and approval information must be recorded when known. Unknown approval dates must not be invented.

5\. Confirmed product decisions
===============================

D-001 — Portfolio product, not general-purpose CMS
--------------------------------------------------

**Status:** Confirmed

**Decision:** Build a professional, dynamic, multi-page personal portfolio and travel gallery with a protected single-administrator CMS.

The application is not a general-purpose CMS or multi-tenant SaaS product.

**Rationale:** The platform exists to present professional identity, credible engineering capabilities and authentic personal content.

**Consequences:**

*   No multi-tenant architecture.
    
*   No general-purpose page-builder platform.
    
*   No unrelated SaaS functionality.
    
*   Product complexity must remain proportional to the portfolio's actual needs.
    

**Affected documents:** PRD, ADD, Scope and Releases, Technical Specification.

D-002 — Single administrator
----------------------------

**Status:** Confirmed

**Decision:** Exactly one administrator is supported.

There is no public administrator registration, second-administrator creation workflow or multi-admin management system.

**Consequences:**

*   All protected management functionality belongs to the single administrator.
    
*   Authorization must be enforced server-side.
    
*   Public registration must never grant administrative privileges.
    

**Verification:** Automated tests must verify that additional administrator creation and assignment are prevented.

**Affected documents:** PRD, Requirements Catalog, ADD, Technical Specification, Testing Strategy.

D-003 — One-time initial administrator setup
--------------------------------------------

**Status:** Confirmed

**Decision:** A protected initial Setup Wizard creates the first administrator.

The administrator chooses their own credentials. The process assigns the Admin role, requires MFA enrollment and recovery-code generation, and permanently disables initial setup after successful completion.

The setup operation must be atomic with respect to administrator creation and setup completion.

**Additional constraints:**

*   Setup is available only when no administrator exists.
    
*   Concurrent setup attempts must not create multiple administrators.
    
*   Setup state must be verified on the server.
    
*   No seeded production administrator credentials.
    
*   No hard-coded default password.
    
*   No public route may reopen completed setup.
    

**Verification:** Test successful setup, interruption, concurrent requests, repeated initialization and attempted reopening.

**Affected documents:** PRD, Requirements Catalog, ADD, Technical Specification, Testing Strategy.

D-004 — Identity and multi-factor authentication
------------------------------------------------

**Status:** Confirmed

**Decision:** Use ASP.NET Core Identity for administrator authentication.

Authentication uses email and password, authenticator-app TOTP and recovery codes.

Password reset uses Identity token mechanisms and must not bypass the MFA security model.

**Additional constraints:**

*   Passwords must never be stored in plaintext.
    
*   Recovery codes must be handled securely.
    
*   MFA enrollment must be verified before normal administrative access.
    
*   Authentication and recovery operations must be rate-limited and audited where appropriate.
    
*   Administrative sessions and sensitive operations must follow the approved security policy.
    

**Affected documents:** PRD, Requirements Catalog, ADD, Technical Specification, Testing Strategy.

D-005 — Content publishing workflow
-----------------------------------

**Status:** Confirmed

**Decision:** Managed content supports Draft, Preview, Publish and Unpublish.

Where appropriate, scheduled publishing is supported according to the approved product requirements.

Changes to a published item must not become publicly visible until explicitly published.

**Consequences:**

*   Public pages display eligible published versions only.
    
*   Draft content cannot leak through search, direct routes, sitemap or language fallback.
    
*   Publishing and unpublishing must invalidate relevant cached content.
    
*   Preview must be protected from unauthorized access.
    

**Verification:** Test draft isolation, preview authorization, publication, unpublishing, caching and localization behavior.

**Affected documents:** PRD, Requirements Catalog, ADD, Technical Specification, Scope and Releases, Testing Strategy.

D-006 — Email provider
----------------------

**Status:** Confirmed

**Decision:** Use Mailtrap.

*   Development: Mailtrap Email Sandbox.
    
*   Production: Mailtrap Email Sending after sending-domain verification.
    

**Consequences:**

*   Credentials must be environment-specific.
    
*   Production sender identities and domain verification must be configured before launch.
    
*   Email delivery failure must not destroy a successfully persisted contact message.
    
*   Delivery status must be tracked independently from message persistence.
    

**Affected documents:** PRD, ADD, Technical Specification, Testing Strategy.

D-007 — Google reCAPTCHA v3
---------------------------

**Status:** Confirmed

**Decision:** Use Google reCAPTCHA v3 on protected public forms.

Server-side verification is mandatory.

**Approved constraints:**

*   Validate the expected action.
    
*   Validate the verification response.
    
*   Validate score according to a configurable threshold.
    
*   Proposed default threshold: 0.5.
    
*   Treat reCAPTCHA as an additional abuse-control mechanism, not a replacement for rate limiting, validation or other protections.
    

**Affected documents:** PRD, Requirements Catalog, ADD, Technical Specification, Testing Strategy.

D-008 — Media Library
---------------------

**Status:** Confirmed

**Decision:** Provide one reusable Media Library for the application.

It supports organized categories, searchable assets, metadata, usage references, public/private storage, replacement and deletion safety, processing status, scanning, quotas and audit history.

**Consequences:**

*   Media must be reusable across content modules.
    
*   Referenced assets must be protected against accidental permanent deletion.
    
*   Public and private assets must have different access policies.
    
*   Original files must be preserved according to the media lifecycle policy.
    
*   Processing and scanning status must be visible to the administrator.
    

**Affected documents:** PRD, Requirements Catalog, ADD, Technical Specification, Design System, Testing Strategy.

D-009 — Storage abstraction and portability
-------------------------------------------

**Status:** Confirmed

**Decision:** Use a storage abstraction so the initial local persistent storage implementation can later be replaced by object storage.

The initial implementation must not tightly couple application use cases to local filesystem paths.

**Consequences:**

*   Storage operations use application-owned abstractions.
    
*   Local storage is the initial implementation.
    
*   Future object-storage migration must not require rewriting core Media Library business rules.
    

**Affected documents:** ADD, Technical Specification, Implementation Plan.

D-010 — Private media protection
--------------------------------

**Status:** Confirmed

**Decision:** Private files must be stored outside wwwroot and delivered only through authorized application endpoints.

**Additional constraints:**

*   Private assets must not be exposed through static-file hosting.
    
*   Authorization must be checked on every protected request.
    
*   Predictable file paths must not grant access.
    
*   Unauthorized responses must not disclose private file existence or metadata.
    
*   Caching must not allow one user's authorized response to be reused for an unauthorized user.
    

**Affected documents:** PRD, Requirements Catalog, ADD, Technical Specification, Testing Strategy.

D-011 — Dedicated Personal / Travel Gallery
-------------------------------------------

**Status:** Confirmed

**Decision:** The application includes a dedicated Personal / Travel Gallery separate from Projects.

The Gallery supports albums, photographs, metadata, featured content, ordering, publication and visibility controls, public browsing, SEO and relevant analytics.

Optional moderated comments are included only according to their approved scope and moderation rules.

**Visibility rules:**

*   Public: eligible for public listings and indexing when published.
    
*   Unlisted: accessible through a direct link but excluded from public listings and indexing; not password-protected.
    
*   Private: administrator-only access through authorized endpoints.
    

**Affected documents:** PRD, Requirements Catalog, ADD, Technical Specification, Design System, Scope and Releases, Testing Strategy.

D-012 — Gallery image provenance
--------------------------------

**Status:** Confirmed

**Decision:** Real Gallery photographs must be uploaded and selected by the administrator.

All images previously used in planning, examples or design discussions are placeholders or visual references.

**Consequences:**

*   No placeholder, generated, stock or example image automatically becomes real Gallery content.
    
*   The initial Gallery must display a professionally designed empty state.
    
*   Only administrator-selected photographs can be published as actual Gallery content.
    

**Affected documents:** PRD, Design System, Technical Specification, Testing Strategy, Agent Instructions.

D-013 — English and Bangla localization
---------------------------------------

**Status:** Confirmed

**Decision:** English is the default language and Bangla is the additional supported language.

**Approved constraints:**

*   Language-prefixed URLs: /en/ and /bn/.
    
*   Independent content translations.
    
*   Independent Admin interface language.
    
*   Safe language fallback.
    
*   Manual language selection.
    
*   Equivalent-page preservation when available.
    
*   Canonical URLs and hreflang.
    
*   Published-content-only sitemap entries.
    
*   No unpublished translation may appear through fallback.
    

**Affected documents:** PRD, Requirements Catalog, ADD, Technical Specification, Design System, Testing Strategy.

D-014 — Accessibility
---------------------

**Status:** Confirmed

**Decision:** Target WCAG 2.2 Level AA.

Accessibility applies to both public and administrator experiences.

**Consequences:**

*   Keyboard accessibility.
    
*   Visible focus states.
    
*   Appropriate semantic structure.
    
*   Accessible forms and validation.
    
*   Screen-reader support.
    
*   Contrast validation in dark and light themes.
    
*   Accessible dialogs and lightboxes.
    
*   Reduced-motion support.
    
*   Responsive and usable touch interactions.
    

**Affected documents:** PRD, Requirements Catalog, Design System, Testing Strategy, Scope and Releases.

D-015 — Disaster recovery objectives
------------------------------------

**Status:** Confirmed

**Decision:** The approved recovery targets are:

*   Recovery Point Objective (RPO): 4 hours.
    
*   Recovery Time Objective (RTO): 4 hours.
    

These are product/operational commitments, not merely suggested targets.

**Consequences:**

*   Daily-only database backups are insufficient to guarantee the RPO.
    
*   Database and media recovery must be coordinated.
    
*   An external copy must exist in a separate failure domain.
    
*   Backup integrity must be verified.
    
*   Restoration must be demonstrated through documented tests.
    
*   Encryption and key recovery must be included in the recovery plan.
    

**Verification:** Recovery exercises must demonstrate both targets under documented test conditions.

**Affected documents:** PRD, Requirements Catalog, ADD, Technical Specification, Scope and Releases, Testing Strategy.

D-016 — Release strategy
------------------------

**Status:** Confirmed

**Decision:** The product follows three releases:

1.  R1 — Professional Foundation.
    
2.  R2 — Advanced Platform.
    
3.  R3 — Production Excellence.
    

All approved product requirements remain in the overall product scope. Release allocation determines delivery order, not whether an approved requirement has been removed.

**Confirmed release interpretation — Option A:**

R1 is the first public production release.

Development and staging verification must occur before production deployment. Testing is continuous throughout implementation.

Essential security, privacy, accessibility and recovery protections cannot be postponed merely because later releases include deeper hardening.

**Affected documents:** PRD, Scope and Releases, Requirements Catalog, Testing Strategy, Implementation Plan.

D-017 — Hybrid documentation structure
--------------------------------------

**Status:** Confirmed

**Decision:** Use a hybrid documentation structure.

The PRD remains the central product document, supported by separate requirements, scope, assumptions, traceability, architecture, technical, design, testing, implementation and agent documents.

**Consequences:**

*   Each document has a clearly defined responsibility.
    
*   Requirements and decisions must have stable IDs.
    
*   Cross-document contradictions must be resolved.
    
*   Changes must be propagated to affected documents.
    

**Affected documents:** Entire documentation set.

6\. Architecture and technology decisions
=========================================

D-018 — Frontend CSS framework
------------------------------

**Status:** Confirmed

**Decision:** Use Bootstrap 5 with a custom CSS design system.

Bootstrap is a responsive implementation foundation. It does not define the final visual identity.

**Additional constraints:**

*   Custom design tokens and CSS remain the visual source of truth.
    
*   Avoid generic Bootstrap template appearance.
    
*   Use custom layouts and page-specific compositions.
    
*   Preserve responsive behavior and accessibility.
    
*   Self-host core frontend assets where specified by the Technical Specification.
    

**Affected documents:** ADD, Technical Specification, Design System, Implementation Plan.

D-019 — .NET platform and web framework
---------------------------------------

**Status:** Confirmed

**Decision:** Use .NET 10 and ASP.NET Core MVC.

The application is a multi-page MVC website with separate public and protected Admin experiences in one deployable application.

**Consequences:**

*   Razor is the primary server-rendered UI technology.
    
*   Public and Admin layouts are logically separated.
    
*   A separate SPA frontend is not required by the current product scope.
    
*   The solution must use compatible framework and package versions.
    

**Affected documents:** PRD, ADD, Technical Specification, Implementation Plan.

D-020 — Database and ORM
------------------------

**Status:** Confirmed

**Decision:** Use Microsoft SQL Server with Entity Framework Core 10 Code First.

**Consequences:**

*   Database schema is managed through EF Core migrations.
    
*   Persistence must respect the architecture's dependency boundaries.
    
*   Database constraints and application validation must protect important invariants.
    
*   Database migrations must be reviewed and deployed through a controlled process.
    

**Affected documents:** ADD, Technical Specification, Implementation Plan, Testing Strategy.

D-021 — Clean Architecture and modular monolith
-----------------------------------------------

**Status:** Confirmed

**Decision:** Use Clean Architecture with a modular monolith.

The principal layers are:

1.  Domain.
    
2.  Application.
    
3.  Infrastructure.
    
4.  Presentation.
    

The application uses one ASP.NET Core MVC host.

**Consequences:**

*   Domain contains business rules and invariants.
    
*   Application contains use cases and application policies.
    
*   Infrastructure implements persistence and external integrations.
    
*   Presentation handles HTTP and user-interface concerns.
    
*   Infrastructure dependencies must not leak into Domain.
    
*   Microservices are not part of the initial architecture.
    

**Affected documents:** ADD, Technical Specification, Implementation Plan, Agent Instructions.

D-022 — Application patterns
----------------------------

**Status:** Confirmed

**Decision:** The architecture uses:

*   CQRS with MediatR.
    
*   Repository abstractions.
    
*   Unit of Work abstraction.
    
*   Mapster.
    
*   FluentValidation.
    
*   Asynchronous I/O.
    

These patterns must support clear separation of responsibilities and testability rather than become unnecessary ceremony.

**Additional constraints:**

*   CQRS does not require separate read/write databases.
    
*   Avoid unrestricted generic repositories that simply duplicate DbSet.
    
*   Domain invariants belong in the Domain layer.
    
*   Use-case orchestration belongs in Application.
    
*   External implementations belong in Infrastructure.
    

**Affected documents:** ADD, Technical Specification, Implementation Plan, Agent Instructions.

D-023 — Dependency injection
----------------------------

**Status:** Confirmed

**Decision:** Use built-in .NET dependency injection as the initial container.

Autofac is not required.

It may be reconsidered only if a demonstrated technical requirement justifies introducing it.

**Affected documents:** ADD, Technical Specification, Implementation Plan.

D-024 — Docker-compatible deployment
------------------------------------

**Status:** Confirmed

**Decision:** The application must be designed for Docker-compatible deployment.

**Consequences:**

*   Application runtime must support container deployment.
    
*   SQL Server must be separately managed from the application's ephemeral container filesystem.
    
*   Database and media data must persist outside disposable container layers.
    
*   Media storage must use persistent volumes or equivalent mounts.
    
*   Secrets must be supplied through environment-specific secure configuration.
    
*   Logs and operational state must remain accessible outside ephemeral container storage.
    
*   Backup copies must be independent of the running application container.
    
*   Health checks and graceful shutdown must be supported.
    

Docker compatibility does not require microservices.

**Affected documents:** ADD, Technical Specification, Scope and Releases, Implementation Plan.

7\. Integrations and implementation defaults
============================================

D-025 — Background job provider
-------------------------------

**Status:** Proposed

**Decision:** Use Hangfire with SQL Server-backed persistent storage as the recommended initial background-processing provider.

**Rationale:** The application requires reliable scheduled publishing, retries and background processing.

**Proposed constraints:**

*   Jobs must be observable.
    
*   Retry behavior must be bounded.
    
*   Repeated execution must be safe.
    
*   Failed jobs must be visible to the administrator where relevant.
    
*   Job persistence must survive application restarts.
    
*   Background work must not silently lose business-critical notifications.
    

**Approval required:** Product Owner confirmation of Hangfire as the selected provider.

**Affected documents:** ADD, Technical Specification, Implementation Plan, Testing Strategy.

D-026 — Transactional outbox
----------------------------

**Status:** Proposed

**Decision:** Use a transactional outbox for reliable asynchronous business notifications, especially contact-related email delivery.

The business record and corresponding outbox event should be committed consistently before external delivery is attempted.

**Proposed constraints:**

*   Idempotent dispatch.
    
*   Bounded retry.
    
*   Observable delivery state.
    
*   Duplicate notification prevention.
    
*   Recovery after temporary provider failure.
    

**Approval required:** Confirm the detailed implementation approach during technical review.

**Affected documents:** ADD, Technical Specification, Testing Strategy.

D-027 — Rich-text editor
------------------------

**Status:** Open

**Decision:** A rich-text editor is required for long-form content management, but the final editor has not been selected.

**Recommended default:** Quill, subject to security, maintenance, licensing and deployment review.

**Mandatory constraints:**

*   Server-side HTML sanitization.
    
*   Strict allowed-element and attribute policy.
    
*   Safe link handling.
    
*   No trust in browser-generated HTML.
    
*   Accessible editing experience.
    
*   Secure preview and publishing.
    

**Approval required:** Select the editor after reviewing its suitability and security implications.

**Affected documents:** PRD, ADD, Technical Specification, Design System, Testing Strategy.

D-028 — File scanning provider
------------------------------

**Status:** Proposed

**Decision:** Use an application-owned scanner abstraction.

ClamAV is the proposed initial scanner implementation.

**Proposed security behavior:**

*   Scanner unavailable or indeterminate means quarantine.
    
*   A file must not be treated as clean without a successful scan result.
    
*   Scanning must not be bypassed by client-side metadata.
    
*   Scanner timeout and failure must be observable.
    
*   Private and public assets must follow the same required security checks.
    

**Approval required:** Confirm the initial scanner provider and deployment model.

**Affected documents:** ADD, Technical Specification, Testing Strategy.

D-029 — Image processing provider
---------------------------------

**Status:** Open

**Decision:** Image processing must be implemented behind an abstraction.

The final image-processing library has not been approved.

**Mandatory constraints:**

*   Preserve originals according to retention policy.
    
*   Generate optimized variants.
    
*   Support responsive image delivery.
    
*   Validate actual file content.
    
*   Handle corrupt or unsupported files safely.
    
*   Review dependency maintenance, licensing and deployment compatibility.
    

**Affected documents:** ADD, Technical Specification, Testing Strategy.

D-030 — Logging and observability
---------------------------------

**Status:** Confirmed

**Decision:** Use Serilog for structured application logging, including console and rolling-file sinks as specified in the Technical Specification.

**Constraints:**

*   Never log passwords, tokens, secrets or recovery codes.
    
*   Avoid logging private message contents and private file contents.
    
*   Include appropriate correlation information.
    
*   Support health checks and operational diagnostics.
    
*   Keep log retention and access controlled.
    

**Affected documents:** ADD, Technical Specification, Testing Strategy.

D-031 — Initial cache strategy
------------------------------

**Status:** Proposed

**Decision:** Begin with ASP.NET Core in-process caching/output caching for eligible public content.

Keep cache behavior and invalidation explicit so a distributed cache can be introduced if actual deployment requirements justify it.

**Proposed constraints:**

*   Never expose drafts through cached public responses.
    
*   Invalidate affected content after publication changes.
    
*   Do not share private responses across unauthorized users.
    
*   Cache behavior must respect localization and visibility.
    

**Approval required:** Confirm the initial caching strategy during technical review.

**Affected documents:** ADD, Technical Specification, Testing Strategy.

8\. Design and user experience decisions
========================================

D-032 — Executive Dark visual direction
---------------------------------------

**Status:** Confirmed

**Decision:** Use an Executive Dark visual direction with a professionally designed light theme.

The design must communicate credibility, engineering capability and a premium professional identity.

**Constraints:**

*   Avoid generic template aesthetics.
    
*   Use purposeful page-specific compositions.
    
*   Maintain visual consistency without making every page look identical.
    
*   Keep interactions restrained and professional.
    
*   Prioritize readability and accessibility.
    

**Affected documents:** PRD, Design System, Technical Specification.

D-033 — Theme behavior
----------------------

**Status:** Confirmed

**Decision:** Support dark and light themes.

On first visit, the application follows the visitor's system preference. An explicit user selection persists.

Both themes require independent visual and contrast validation.

**Affected documents:** PRD, Design System, Technical Specification, Testing Strategy.

D-034 — Responsive design
-------------------------

**Status:** Confirmed

**Decision:** Support mobile, tablet, laptop and desktop experiences.

Responsive behavior must be designed deliberately for both public pages and the Admin Panel.

**Constraints:**

*   No unintended horizontal overflow.
    
*   Tables and complex admin tools must remain usable on smaller screens.
    
*   Navigation must adapt to available space.
    
*   Touch interactions must remain accessible.
    
*   Responsive behavior must not compromise content hierarchy.
    

**Affected documents:** PRD, Design System, Testing Strategy.

D-035 — Authentic portfolio imagery
-----------------------------------

**Status:** Confirmed

**Decision:** Actual personal, project and travel imagery is selected and managed by the administrator.

Planning mockups, placeholders and design references must never be represented as verified real portfolio content.

**Affected documents:** PRD, Design System, Technical Specification, Testing Strategy.

9\. Deployment and operational decisions
========================================

D-036 — Production hosting and canonical domain
-----------------------------------------------

**Status:** Open

**Decision:** The production hosting provider and canonical domain have not been selected.

**Required considerations:**

*   .NET 10 hosting compatibility.
    
*   SQL Server availability and operational model.
    
*   Persistent media storage.
    
*   Backup and restore capabilities.
    
*   TLS and domain configuration.
    
*   Monitoring and logs.
    
*   Deployment and rollback support.
    
*   Data protection and secret management.
    
*   Recovery objectives.
    

**Resolution stage:** Before production infrastructure is finalized.

**Affected documents:** Technical Specification, Scope and Releases, Implementation Plan, Testing Strategy.

D-037 — Performance budgets
---------------------------

**Status:** Open

**Decision:** Numeric performance budgets will be finalized after the staging environment and representative workloads are known.

**Required measurements:**

*   Core Web Vitals.
    
*   Public page response times.
    
*   Database query performance.
    
*   Search behavior.
    
*   Media loading.
    
*   Upload processing.
    
*   Background job execution.
    

**Resolution stage:** Before release performance sign-off.

**Affected documents:** PRD, Technical Specification, Testing Strategy, Scope and Releases.

D-038 — Analytics implementation and retention
----------------------------------------------

**Status:** Open

**Decision:** Analytics functionality is in product scope, but the implementation provider/approach and final retention periods remain unresolved.

**Approved product constraints:**

*   Privacy-conscious aggregated analytics.
    
*   Administrator activity excluded from visitor analytics.
    
*   Avoid invasive visitor profiling.
    
*   Prefer cookieless analytics.
    
*   Consent for non-essential tracking where required.
    
*   Retention and export controls.
    

**Resolution stage:** Before analytics implementation is finalized and before production deployment.

**Affected documents:** PRD, Requirements Catalog, Technical Specification, Testing Strategy.

D-039 — Backup cadence and retention
------------------------------------

**Status:** Proposed / Requires Validation

**Decision:** The backup design must meet D-015's confirmed RPO and RTO.

The proposed approach is:

*   Database recovery points frequent enough to meet RPO 4 hours.
    
*   Coordinated database and media backup.
    
*   External backup copy in a separate failure domain.
    
*   Backup integrity verification.
    
*   Documented retention and deletion policy.
    
*   Recovery of required encryption and application keys.
    
*   Regular restoration exercises.
    

**Important:** The exact backup schedule and retention periods are not yet confirmed.

A backup schedule must be validated against the actual database, media volume, storage cost, recovery process and operational capability.

**Affected documents:** PRD, ADD, Technical Specification, Testing Strategy, Scope and Releases.

D-040 — Production security and secret management
-------------------------------------------------

**Status:** Confirmed

**Decision:** Production secrets must not be committed to source control or baked into container images.

Environment-specific secrets and sensitive configuration must be supplied through an appropriate secure deployment mechanism.

**Constraints:**

*   Separate development, staging and production configuration.
    
*   Protect Data Protection keys and other encryption-related material.
    
*   Restrict access to operational credentials.
    
*   Rotate compromised secrets.
    
*   Avoid sensitive values in logs and error responses.
    

**Affected documents:** ADD, Technical Specification, Testing Strategy, Implementation Plan.

D-041 — Operational visibility
------------------------------

**Status:** Confirmed

**Decision:** The Admin Panel must provide relevant operational visibility for the administrator.

This includes applicable status information for:

*   Background jobs.
    
*   Email delivery.
    
*   Media processing and scanning.
    
*   Storage.
    
*   Cache.
    
*   Backup and restore.
    
*   Application health.
    
*   Maintenance mode.
    
*   Important security and administrative activity.
    

Sensitive operations require appropriate authorization, confirmation and reauthentication/MFA where necessary.

**Affected documents:** PRD, Requirements Catalog, Design System, ADD, Technical Specification, Testing Strategy.

10\. Open decisions register
============================

The following decisions remain unresolved and must not be treated as approved implementation choices.

IDDecisionCurrent statusRequired resolutionD-027Rich-text editorOpenSelect and security-review editorD-029Image processing providerOpenSelect maintained, compatible libraryD-036Hosting and domainOpenSelect production environmentD-037Performance budgetsOpenEstablish measurable targetsD-038Analytics implementation and retentionOpenConfirm approach and policyD-025Background job providerProposedApprove or replace HangfireD-026Transactional outbox implementationProposedConfirm implementation approachD-028File scanner providerProposedConfirm ClamAV or alternativeD-031Initial cache strategyProposedConfirm initial implementationD-039Backup cadence and retentionProposedValidate schedule and retention

An open decision does not automatically block every development activity. Its impact and resolution deadline must be considered when planning dependent work.

11\. Decision change management
===============================

11.1 Changing a confirmed decision
----------------------------------

A confirmed decision may only be changed through an explicit review and approval.

The change record must include:

1.  Existing decision ID.
    
2.  Previous decision.
    
3.  Proposed replacement.
    
4.  Reason for change.
    
5.  Product impact.
    
6.  Architecture and technical impact.
    
7.  Security, privacy and accessibility impact where applicable.
    
8.  Requirements and acceptance-criteria impact.
    
9.  Testing and release impact.
    
10.  Affected documents.
    
11.  Approval and date.
    

11.2 Superseding decisions
--------------------------

Do not delete or silently rewrite a previously confirmed decision.

When a decision is replaced:

*   Mark the previous decision Superseded.
    
*   Record the replacement decision ID.
    
*   Preserve the historical reason.
    
*   Update affected documentation.
    
*   Update implementation and test references.
    

11.3 AI coding agent restrictions
---------------------------------

AI coding agents must:

*   Treat Confirmed decisions as binding.
    
*   Treat Proposed decisions as recommendations, not authorization.
    
*   Never invent approval for an Open decision.
    
*   Never silently replace a selected technology.
    
*   Identify contradictions before implementing conflicting behavior.
    
*   Ask for approval when a material product or architectural decision is required.
    
*   Report any unavoidable technical incompatibility with evidence.
    
*   Update relevant documentation when an approved decision changes.
    
*   Preserve stable decision IDs.
    
*   Never claim that a proposed or implemented choice has been approved or verified without evidence.
    

12\. Cross-document traceability matrix
=======================================

Decision groupPrimary affected documentsD-001–D-002PRD, Requirements Catalog, ADD, Scope and ReleasesD-003–D-004PRD, Requirements Catalog, ADD, Technical Specification, Testing StrategyD-005PRD, Requirements Catalog, ADD, Technical Specification, Testing StrategyD-006–D-007PRD, ADD, Technical Specification, Testing StrategyD-008–D-010PRD, Requirements Catalog, ADD, Technical Specification, Testing StrategyD-011–D-012PRD, Requirements Catalog, Design System, Testing StrategyD-013–D-014PRD, Requirements Catalog, Design System, Testing StrategyD-015PRD, Scope and Releases, Technical Specification, Testing StrategyD-016PRD, Scope and Releases, Implementation Plan, Testing StrategyD-017Entire documentation setD-018–D-024ADD, Technical Specification, Implementation Plan, Agent InstructionsD-025–D-031ADD, Technical Specification, Implementation Plan, Testing StrategyD-032–D-035PRD, Design System, Technical Specification, Testing StrategyD-036–D-040Technical Specification, Scope and Releases, Implementation Plan, Testing StrategyD-041PRD, Requirements Catalog, Design System, Technical Specification, Testing Strategy

This matrix identifies the principal documents affected by each decision group. Detailed requirement-level mapping belongs in the Requirements Traceability Matrix.

13\. Revision history
=====================

VersionDescriptionStatus1.0Initial decision log containing 22 decisionsPrevious baseline2.0Expanded decision register; corrected Bootstrap status; added architecture, technology, integration, design, deployment and governance decisionsReview draft

14\. Final document status
==========================

**DECISIONS v2.0 is a comprehensive review draft.**

It is not automatically an approval of every proposed technical default.

The confirmed decisions represent the established product and architecture direction. Proposed and open decisions remain subject to explicit review and approval.

Before this document becomes the authoritative approved decision register:

1.  Review the proposed technical defaults.
    
2.  Confirm or revise the open decisions.
    
3.  Verify consistency with the current Requirements Catalog and Technical Specification.
    
4.  Update the Requirements Traceability Matrix.
    
5.  Update the Scope and Releases and Implementation Plan where decisions affect delivery.
    
6.  Record the approval date and final document status.
    

**Final governance principle:** No implementation agent or developer may silently turn an open or proposed decision into a binding Product Owner commitment.
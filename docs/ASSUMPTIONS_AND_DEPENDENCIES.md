ASSUMPTIONS\_AND\_DEPENDENCIES
==============================

Assumptions, Open Decisions, Dependencies, Constraints and Risk Management
--------------------------------------------------------------------------

**Project:** Adib Hasan Avik — Personal Portfolio & Travel Gallery**Document:** Assumptions and Dependencies**Version:** 2.0**Status:** Comprehensive Review Draft — Pending Product Owner Approval**Document Owner:** Product Owner**Review Authority:** Product Owner**Supersedes:** ASSUMPTIONS\_AND\_DEPENDENCIES v1.0, after approval**Related Documents:** PRD, DECISIONS, REQUIREMENTS\_CATALOG, ADD, TECHNICAL\_SPEC, DESIGN\_SYSTEM, SCOPE\_AND\_RELEASES, TESTING\_STRATEGY, REQUIREMENTS\_TRACEABILITY, IMPLEMENTATION\_PLAN

1\. Purpose
===========

This document identifies the assumptions, unresolved decisions, dependencies, environmental constraints, and delivery risks that may affect the successful design, implementation, testing, deployment, operation, and maintenance of the Personal Portfolio & Travel Gallery.

Its purpose is to prevent the development team and AI coding agents from:

*   Treating unverified assumptions as established facts.
    
*   Implementing proposed technical choices without approval.
    
*   Depending on unavailable infrastructure or external services.
    
*   Introducing undocumented scope or architectural changes.
    
*   Overlooking operational, security, privacy, content, and recovery risks.
    
*   Declaring a feature complete when a necessary dependency remains unresolved.
    

This document is a project-control document. It does not replace the PRD, architecture, technical specification, requirements catalog, or testing strategy.

2\. Document Authority and Relationships
========================================

The following documents define the project's documentation responsibilities.

DocumentPrimary responsibilityPRDProduct vision, scope, user journeys and product requirementsDECISIONSApproved decisions, proposed defaults and unresolved decisionsREQUIREMENTS\_CATALOGStable requirement identifiers and acceptance criteriaADDArchitecture, modules, boundaries and technical principlesTECHNICAL\_SPECImplementation technologies, providers and configurationDESIGN\_SYSTEMVisual identity, components, accessibility and interaction rulesSCOPE\_AND\_RELEASESRelease allocation, sequencing and production gatesTESTING\_STRATEGYVerification methods and quality gatesREQUIREMENTS\_TRACEABILITYRequirement-to-design, implementation and test traceabilityIMPLEMENTATION\_PLANEngineering tasks, sequencing and delivery progressASSUMPTIONS\_AND\_DEPENDENCIESPlanning assumptions, uncertainties, dependencies and risks

2.1 Conflict resolution
-----------------------

When documents disagree:

1.  Identify the conflicting statements and affected document sections.
    
2.  Identify any related decision IDs and requirement IDs.
    
3.  Determine whether the conflict concerns product scope, architecture, implementation, or deployment.
    
4.  Do not silently select whichever interpretation is easiest to implement.
    
5.  Record the resolution in DECISIONS and update affected documents.
    
6.  Obtain Product Owner approval where the resolution changes an approved commitment.
    

A coding agent must stop and report a material unresolved conflict rather than inventing a product decision.

3\. Status Definitions
======================

The following status definitions apply throughout this document.

StatusMeaningConfirmedExplicitly approved by the Product Owner or established as a binding project constraintProposedRecommended approach awaiting explicit approvalOpenRequires a decision, clarification or validationAssumedAccepted temporarily for planning, but not yet verifiedValidatedEvidence demonstrates that the assumption or dependency is satisfiedBlockedWork cannot safely or correctly proceed until the issue is resolvedDeferredIntentionally postponed; not automatically removed from overall product scopeRejectedEvaluated and explicitly declined

**Important distinctions:**

*   A confirmed decision is not the same as a validated deployment condition.
    
*   A proposed technical default is not an approved implementation commitment.
    
*   An assumption must not be represented as a verified fact.
    
*   A dependency being available in development does not prove it is available in production.
    
*   An implemented feature is not necessarily verified or released.
    

4\. Confirmed Project Assumptions and Constraints
=================================================

The following items form the current planning baseline. Their approval status must remain consistent with the DECISIONS document.

IDAssumption or constraintStatusASM-001The product is a professional, dynamic, multi-page personal portfolio and travel gallery, not a general-purpose CMS or multi-tenant SaaS platform.ConfirmedASM-002The application provides a public Viewer Panel and a protected Admin Panel within one application.ConfirmedASM-003Exactly one administrator is supported in the initial product. Public registration and additional administrator creation are excluded.ConfirmedASM-004Initial administrator creation uses a one-time setup process. No seeded default administrator credentials are permitted.ConfirmedASM-005Administrator authentication uses ASP.NET Core Identity with authenticator-app MFA and recovery codes.ConfirmedASM-006Password reset must not bypass MFA or weaken administrator authentication.ConfirmedASM-007The backend uses ASP.NET Core MVC and C#.ConfirmedASM-008SQL Server is the relational database platform and EF Core Code First is the persistence approach.ConfirmedASM-009The architecture follows Clean Architecture principles and a modular-monolith deployment model.ConfirmedASM-010Bootstrap 5 is the responsive UI foundation; custom CSS, design tokens and page-specific layouts remain the visual authority.ConfirmedASM-011English is the default language and Bangla is an additional supported language.ConfirmedASM-012The product includes a dedicated Personal / Travel Gallery.ConfirmedASM-013Gallery photographs must be genuine photographs uploaded or selected by the administrator.ConfirmedASM-014The Gallery begins empty until the administrator publishes actual photographs.ConfirmedASM-015Media storage must support public and private assets through a storage abstraction.ConfirmedASM-016Initial local media storage must use persistent storage rather than an ephemeral application-container filesystem.ConfirmedASM-017Private media must not be directly exposed through public static-file paths.ConfirmedASM-018Mailtrap Email Sandbox is used for development email testing, with production email sending configured separately.ConfirmedASM-019Google reCAPTCHA v3 is used for applicable protected public forms, with server-side verification.ConfirmedASM-020The application combines appropriate abuse protection with Identity, authorization and rate limiting.ConfirmedASM-021WCAG 2.2 AA is the accessibility target for shipped experiences.ConfirmedASM-022Executive Dark is the primary visual direction, with a deliberate light theme.ConfirmedASM-023Projects must distinguish completed, in-progress and planned work clearly.ConfirmedASM-024The initial deployment must be Docker-compatible. Docker must not dictate domain or application business logic.ConfirmedASM-025The database and media recovery strategy must support an RPO of four hours and an RTO of four hours.ConfirmedASM-026Development and staging verification precede the first public production release, R1. Testing continues throughout development.Confirmed

4.1 Constraints on interpretation
---------------------------------

These commitments must not be weakened through implementation convenience.

Examples:

*   A developer cannot introduce public registration because Identity supports it.
    
*   A developer cannot publish placeholder photographs to make the Gallery appear populated.
    
*   A developer cannot expose private media through a predictable URL.
    
*   A developer cannot remove MFA because password recovery is inconvenient.
    
*   A developer cannot postpone essential security or accessibility protections until R3.
    
*   A developer cannot replace the approved Bootstrap foundation without a documented change.
    

5\. Assumption Validation Register
==================================

This section distinguishes established project commitments from environmental and operational assumptions that must be verified.

IDPlanning assumptionValidation methodValidation stageStatusAV-001Production hosting supports the selected .NET runtime.Deploy and run a representative build.Before productionOpenAV-002The production host supports persistent mounted media storage.Write, read, restart and container-recreation tests.StagingAssumedAV-003Database and media backups can be stored independently from the application runtime.Configure backup destinations and verify access.StagingAssumedAV-004The production database supports the selected SQL Server and EF Core configuration.Migration and integration tests.StagingAssumedAV-005The administrator can provide verified portfolio content.Owner content review and publication approval.Before content publicationAssumedAV-006English and Bangla content can be professionally reviewed.Translation review and language-route verification.Before bilingual releaseAssumedAV-007Mailtrap production sending can be enabled using a verified sending domain.Domain verification and controlled delivery test.Before production email activationOpenAV-008Google reCAPTCHA keys and authorized hostnames can be configured securely.Server-side verification in staging.StagingAssumedAV-009ClamAV can be deployed and maintained in the selected hosting environment.Resource, connectivity, update and failure tests.StagingOpenAV-010Hosting resources are sufficient for image processing and background jobs.Representative workload and resource monitoring.StagingOpenAV-011Required DNS and TLS capabilities are available.Domain resolution and certificate validation.Before productionOpenAV-012Backup restoration can be completed within the four-hour recovery target.Timed database and media restoration drill.Before production and periodically thereafterOpen

An assumption must be changed to **Validated** only when the validation method has produced recorded evidence.

6\. Open Decisions Register
===========================

Open decisions must have an owner and a resolution point. They must not be silently converted into implementation choices.

IDOpen decisionWhy it mattersRecommended resolutionStatusOD-001Production hosting provider and deployment topologyDetermines runtime support, storage, database connectivity, networking and operational capabilities.Evaluate hosting against the production architecture and recovery requirements before committing.OpenOD-002Production domain and DNS configurationRequired for public deployment, canonical URLs, email verification and TLS.Select the canonical domain and configure DNS before production launch.OpenOD-003Numeric performance budgetsRequired for measurable performance acceptance.Define page response, Core Web Vitals, image, query and background-processing budgets using representative staging infrastructure.OpenOD-004Analytics implementation and retentionAffects privacy, consent, storage and reporting.Select a privacy-conscious approach and approve metrics, retention and consent requirements.OpenOD-005Backup cadence and retentionRequired to demonstrate RPO/RTO and data recoverability.Design coordinated database and media recovery points, external copies, retention and restore testing.Proposed pending approvalOD-006Final English and Bangla contentRequired for accurate bilingual publication.Obtain and review owner-approved translations before publishing each language.OpenOD-007Final factual portfolio contentPrevents unsupported claims and misleading portfolio information.Require administrator verification of profile facts, project status, descriptions, achievements and metrics.OpenOD-008Rich-text editor selectionAffects content authoring, sanitization, accessibility and security.Evaluate Quill as the recommended candidate, including maintenance, licensing, accessibility and sanitization.OpenOD-009Mailtrap delivery integration methodAffects implementation and diagnostics.Compare supported API and SMTP approaches against current Mailtrap capabilities and the selected hosting environment.OpenOD-010Production ClamAV deploymentScanner availability, update process, resource sizing and network behavior depend on hosting.Validate ClamAV deployment and failure behavior on staging before production approval.OpenOD-011Minimum supported browser versionsRequired for reliable compatibility acceptance.Establish the browser support baseline before release sign-off.OpenOD-012Legal and privacy reviewAffects contact data, privacy disclosures, retention and consent.Review applicable legal obligations and publish appropriate privacy information before production.OpenOD-013Exact production resource sizingAffects availability, image processing and recovery performance.Establish CPU, memory, storage and database requirements through representative staging tests.OpenOD-014Final analytics implementation detailsDetermines the actual data collected and administrative reports.Confirm the metrics, aggregation, retention and access rules before implementation.Open

**Resolution rule:** OD-004 and OD-014 concern overlapping analytics topics. They must be consolidated into one approved analytics decision before implementation rather than maintained as competing decisions.

6.1 Previously resolved decision
--------------------------------

**Bootstrap versus Tailwind is not an open decision.**

Bootstrap 5 with custom CSS and design tokens is the approved direction. The original open-decision entry must be retired and its resolution referenced from the DECISIONS document.

6.2 Proposed technical defaults
-------------------------------

The following are recommendations, not automatically approved commitments.

IDProposed defaultReasonApproval neededPD-001Hangfire with SQL Server-backed persistenceDurable background job scheduling and monitoring.YesPD-002Transactional outbox for reliable external side effectsReduces the risk of losing work between database transactions and background processing.YesPD-003Quill as rich-text editor candidateProvides a structured editing experience, subject to security and maintenance review.YesPD-004ClamAV as the initial malware scanner behind IFileSecurityScannerProvides a replaceable scanner integration while retaining a fail-closed security policy.YesPD-005ASP.NET Core in-process caching initiallyAvoids unnecessary distributed infrastructure for the initial deployment.YesPD-006Image-processing provider behind an application-owned abstractionPrevents the application from depending on one image library.YesPD-007Built-in .NET dependency injectionSufficient for the proposed modular monolith.Yes, if not already approved in DECISIONS

7\. External Dependencies Register
==================================

External dependencies are services or systems outside the application's direct ownership.

IDDependencyPurposeRequired environmentFailure consequenceValidationDEP-EXT-001Mailtrap SandboxDevelopment email testing.DevelopmentEmail tests cannot be completed.Controlled sandbox delivery.DEP-EXT-002Mailtrap production sendingVisitor confirmation and administrator notifications.ProductionNotifications may be delayed or unavailable.Verified domain and delivery test.DEP-EXT-003Google reCAPTCHA v3Abuse protection for applicable public forms.Staging and productionVerification failures may block protected submissions.Valid and invalid token tests.DEP-EXT-004ClamAV serviceMalware scanning of uploaded files.Staging and production if approvedUpload processing must fail safely or quarantine files.Clean, malicious-test and unavailable-service scenarios.DEP-EXT-005DNS providerDomain resolution.ProductionWebsite or email domain may become unreachable.DNS resolution checks.DEP-EXT-006TLS certificate providerEncrypted public access.ProductionBrowser security warnings or unavailable HTTPS.Certificate and renewal checks.DEP-EXT-007Hosting providerApplication runtime and network infrastructure.Staging and productionApplication availability and operational capability are affected.Deployment and recovery tests.DEP-EXT-008Backup destinationIndependent recovery copies.ProductionRecovery objectives may not be achievable.Backup integrity and restore tests.

7.1 External service management requirements
--------------------------------------------

For each production external service:

*   Maintain configuration outside source code.
    
*   Store credentials in protected runtime configuration.
    
*   Record service health and relevant failure information.
    
*   Define timeouts and retry behavior where appropriate.
    
*   Prevent unlimited retries and duplicate processing.
    
*   Document the responsible operator and recovery procedure.
    
*   Avoid logging credentials, tokens or private personal data.
    

External service failure must not silently corrupt application data.

8\. Internal and Platform Dependencies
======================================

These dependencies are controlled by the application architecture and deployment configuration.

IDDependencyPurposeValidationDEP-INT-001.NET 10 runtime and SDKApplication development and execution.Build and deployment verification.DEP-INT-002ASP.NET Core MVCPublic and administrator web experiences.HTTP and end-to-end tests.DEP-INT-003SQL ServerPersistent relational data.Connection, migration, transaction and recovery tests.DEP-INT-004EF Core 10ORM and database access.Integration and migration tests.DEP-INT-005ASP.NET Core IdentityAdministrator identity and authentication.Authentication and authorization tests.DEP-INT-006Persistent Data Protection keysProtects authentication-related and other protected application data across restarts.Container restart and recovery tests.DEP-INT-007Persistent media storageStores uploaded files and generated variants.File lifecycle and container recreation tests.DEP-INT-008Background job infrastructureProcesses scheduled or asynchronous work if approved.Retry, persistence and failure tests.DEP-INT-009Transactional outbox infrastructureSupports reliable dispatch of committed application events if approved.Transaction and duplicate-dispatch tests.DEP-INT-010Image-processing library/providerCreates validated media variants.Corrupt input and processing-failure tests.DEP-INT-011Cache infrastructureImproves response performance where enabled.Invalidation and privacy tests.DEP-INT-012Logging and observabilitySupports diagnostics and operational monitoring.Log integrity and sensitive-data review.DEP-INT-013Docker and container configurationProvides reproducible runtime packaging.Build, deployment and persistence tests.DEP-INT-014Database migration processEvolves the schema safely.Staging migration and rollback/recovery tests.

9\. Infrastructure and Environment Dependencies
===============================================

9.1 Development
---------------

Development must provide:

*   Compatible .NET SDK and runtime.
    
*   Local SQL Server or an approved development database instance.
    
*   Mailtrap Sandbox configuration.
    
*   Development reCAPTCHA configuration where required.
    
*   Local persistent media directory.
    
*   Docker and Compose configuration for containerized development.
    
*   Test configuration that does not depend on production credentials.
    
*   Automated build and test execution.
    

Development data must not contain real production secrets.

9.2 Staging
-----------

Staging must approximate production sufficiently to validate:

*   Runtime compatibility.
    
*   Database connectivity and migrations.
    
*   Media persistence.
    
*   Scanner integration.
    
*   Image processing.
    
*   Background job processing if enabled.
    
*   Email integration using controlled sending.
    
*   reCAPTCHA server-side verification.
    
*   HTTPS, proxy and domain behavior.
    
*   Backup and restoration.
    
*   Performance and accessibility.
    
*   Security and privacy boundaries.
    

Staging must not be treated as a substitute for production monitoring.

9.3 Production
--------------

Production requires:

*   Approved domain and DNS.
    
*   Valid HTTPS/TLS configuration.
    
*   Secure runtime secrets.
    
*   Persistent database storage or an approved managed database.
    
*   Persistent media storage.
    
*   Independent database and media backups.
    
*   Protected Data Protection keys.
    
*   Application health checks.
    
*   Operational logging.
    
*   Controlled migrations and deployment rollback.
    
*   Verified external service configuration.
    
*   Documented incident and recovery procedures.
    

Production must not depend on files stored only inside an ephemeral container layer.

10\. Content and Owner Dependencies
===================================

The application provides the publishing platform, but it cannot independently guarantee the truth or completeness of personal portfolio information.

The administrator is responsible for supplying and verifying:

IDRequired contentDependencyDEP-CNT-001Name and professional profileVerified personal information.DEP-CNT-002About and biography contentOwner-reviewed factual statements.DEP-CNT-003Education informationAccurate institution, qualification and dates.DEP-CNT-004Skills and technologiesGenuine skills and appropriate proficiency descriptions.DEP-CNT-005Project informationVerified project details, responsibilities, technologies and status.DEP-CNT-006AchievementsVerifiable achievement information.DEP-CNT-007CertificationsAccurate certification information.DEP-CNT-008Resume files and contentOwner-approved versions and language variants.DEP-CNT-009Gallery photographsGenuine administrator-selected photographs.DEP-CNT-010English and Bangla translationsReviewed language content.DEP-CNT-011Contact information and social linksVerified destination and visibility settings.DEP-CNT-012Privacy and legal contentOwner-reviewed and legally appropriate content.

10.1 Content publication rules
------------------------------

*   The system must not fabricate personal qualifications, work experience, achievements or project metrics.
    
*   Planned projects must not be represented as completed projects.
    
*   In-progress projects must be visibly distinguished from completed work.
    
*   Placeholder and reference images must not be presented as the administrator's real photographs.
    
*   Unreviewed translations must not be silently published as verified translations.
    
*   Unpublished content must not leak through public routes, search, sitemap, metadata or fallback behavior.
    

11\. Dependency Sequencing and Critical Path
============================================

The following sequence describes important prerequisites. It is a planning dependency model, not a replacement for the release allocation in SCOPE\_AND\_RELEASES.

WorkstreamRequired prerequisiteConsequence if unresolvedInitial administrator setupIdentity configuration, secure setup rules, database persistenceAdministrator access cannot be safely established.PublishingContent model, authorization, version isolationPublic draft leakage risk.Media LibraryStorage abstraction, validation, scanner policyUnsafe or unavailable uploads.GalleryMedia Library, publication rules, visibility controlsGallery cannot safely publish photos.Private mediaPersistent private storage, authorized delivery endpointPrivacy exposure.Contact workflowDatabase persistence, validation, email adapterLost or undelivered visitor messages.Background processingApproved job provider and failure/retry policyUnreliable asynchronous operations.AnalyticsApproved privacy and retention decisionsUnapproved collection or retention of visitor data.Bilingual publicationReviewed translations and language routingIncomplete or inaccurate language experience.Production deploymentHosting, domain, TLS, secrets, database and media storagePublic launch blocked.Production recoveryCoordinated backup, restore procedure and tested recoveryRPO/RTO cannot be demonstrated.

11.1 Critical-path controls
---------------------------

A downstream feature must not be declared production-ready when a critical prerequisite is missing.

Examples:

*   Gallery publication requires validated media and visibility controls.
    
*   Private media publication requires authorization and non-public storage.
    
*   Production email activation requires a verified sending configuration.
    
*   Production launch requires recovery evidence, not merely a successful backup command.
    
*   Bilingual release requires reviewed translations, not just language routing.
    

12\. Risk Management Method
===========================

Risks are assessed using qualitative likelihood and impact.

### Likelihood

RatingMeaningLowUnlikely under the current planMediumPlausible and requires monitoringHighLikely or already indicated by known conditions

### Impact

RatingMeaningLowLimited inconvenience or recoverable issueMediumMaterial feature, delivery or operational disruptionHighSecurity, privacy, data loss, major outage or release-blocking impact

### Severity

SeverityInterpretationLowManage through normal development and monitoringMediumRequires an assigned mitigation and reviewHighRequires explicit mitigation and contingency before affected releaseCriticalMust be resolved or formally accepted by the Product Owner before the affected production release

Likelihood and impact ratings are initial planning assessments, not measured statistical probabilities.

13\. Risk Register
==================

13.1 Security and identity risks
--------------------------------

IDRiskLikelihoodImpactSeverityMitigation and contingencyRSK-001Concurrent setup requests create multiple administrator accounts.MediumHighHighAtomic setup transaction or locking, unique constraints and concurrency tests. Disable setup after success.RSK-002Private media becomes publicly accessible.MediumCriticalCriticalStore outside public web root, enforce authorization on every request, control cache behavior and test direct access.RSK-003Upload validation is bypassed.MediumHighHighValidate extension, content signature, size, processing result and scanner outcome. Reject unsupported content.RSK-004Malware scanner becomes unavailable or outdated.MediumHighHighFail closed, quarantine pending files, monitor scanner health and define recovery procedure.RSK-005Administrator loses authenticator access.MediumHighHighProvide secure recovery codes, controlled recovery procedures and audited account recovery.RSK-006Session or Data Protection keys are lost during container replacement.MediumHighHighPersist and protect keys, test restart and recovery, document key backup.RSK-007Rate limiting or reCAPTCHA is incorrectly configured.MediumMediumMediumTest valid and invalid submissions, monitor abuse and validate environment-specific keys.RSK-008Sensitive information is exposed through logs or error messages.MediumHighHighStructured logging with redaction, safe error handling and log review.

13.2 Data and publishing risks
------------------------------

IDRiskLikelihoodImpactSeverityMitigation and contingencyRSK-009Draft content appears publicly.MediumCriticalCriticalSeparate published and draft visibility, enforce server-side queries and test direct routes, search and sitemap.RSK-010Unpublished translation leaks through fallback behavior.MediumHighHighUse published-only fallback rules and test every language route.RSK-011Database records and media files become inconsistent.MediumHighHighUse coordinated backup manifests, safe media lifecycle operations and integrity checks.RSK-012Media deletion breaks content references.MediumHighHighTrack references, prevent unsafe deletion, use recycle-bin workflows and verify restoration.RSK-013Database migration fails during deployment.MediumHighHighTest migrations in staging, back up before risky changes and define a recovery/rollback procedure.RSK-014Duplicate background processing sends repeated notifications or performs actions more than once.MediumMediumMediumUse idempotency, deduplication and controlled retries.RSK-015Cache serves stale or private content after publication changes.MediumHighHighDefine cache boundaries, invalidate affected entries and test draft/private isolation.

13.3 Email and external-service risks
-------------------------------------

IDRiskLikelihoodImpactSeverityMitigation and contingencyRSK-016Mail provider outage prevents notification delivery.MediumMediumMediumPersist messages first, track delivery independently, retry safely and expose failures to the administrator.RSK-017Invalid production sending-domain configuration prevents delivery.MediumMediumMediumVerify domain and controlled delivery before enabling production notifications.RSK-018reCAPTCHA service outage blocks legitimate form submissions.MediumMediumMediumDefine a secure failure policy and monitored operational response. Do not silently disable abuse protection.RSK-019External provider credentials expire or are rotated incorrectly.MediumHighHighDocument rotation, validate configuration and monitor service failures.

13.4 Infrastructure and recovery risks
--------------------------------------

IDRiskLikelihoodImpactSeverityMitigation and contingencyRSK-020Application container is recreated and local media disappears.MediumCriticalCriticalUse persistent mounted storage and test container recreation.RSK-021Backup completes but contains unusable or incomplete data.MediumCriticalCriticalVerify integrity, test restoration and compare database/media references.RSK-022Daily-only database backups fail to meet four-hour RPO.HighHighCriticalUse sufficiently frequent recovery points and verify actual recovery-point age.RSK-023Recovery takes longer than four hours.MediumHighHighDocument restore steps, test timed recovery and improve automation where necessary.RSK-024Storage capacity becomes exhausted.MediumHighHighMonitor capacity, establish warning thresholds and define safe cleanup/expansion procedures.RSK-025Hosting resources are insufficient for image processing and background workloads.MediumMediumMediumBenchmark representative workloads, monitor resource usage and adjust capacity.RSK-026TLS certificate expires or DNS is misconfigured.LowHighMediumMonitor certificate validity, document renewal and validate DNS before deployment.RSK-027Production secrets or Data Protection keys are lost or exposed.MediumCriticalCriticalUse protected runtime configuration, restricted access, secure key persistence and documented recovery.

13.5 Product, content and delivery risks
----------------------------------------

IDRiskLikelihoodImpactSeverityMitigation and contingencyRSK-028Unsupported profile or project claims damage credibility.MediumHighHighRequire administrator verification before publication.RSK-029Placeholder images are mistaken for genuine portfolio photographs.MediumHighHighKeep the Gallery empty until real administrator-selected photographs are published.RSK-030Translation is inaccurate or incomplete.MediumMediumMediumRequire reviewed language content and language-specific publication validation.RSK-031Performance targets are not measurable before release.HighMediumHighDefine numeric budgets and verify them against representative staging infrastructure.RSK-032Accessibility regressions occur during visual implementation.MediumHighHighInclude automated and manual WCAG 2.2 AA checks in continuous verification.RSK-033Browser compatibility is incomplete.MediumMediumMediumEstablish minimum supported versions and test the agreed browser/device matrix.RSK-034Legal or privacy obligations are overlooked.MediumHighHighReview contact-data handling, retention, consent and privacy disclosures before production.RSK-035Scope expands through undocumented AI-agent implementation choices.HighHighHighRequire requirement IDs, approved decisions and documented change control for new scope.

13.6 Risk ownership
-------------------

The Product Owner is accountable for accepting residual product and release risk.

Technical owners must be assigned during implementation for:

*   Application security and identity.
    
*   Database and media persistence.
    
*   External integrations.
    
*   Deployment and infrastructure.
    
*   Backup and recovery.
    
*   Accessibility and performance verification.
    

No critical risk may be marked resolved solely because a mitigation has been documented. Evidence must demonstrate that the mitigation works.

14\. Failure Handling and Contingency Requirements
==================================================

The following behaviors are required planning constraints.

Failure conditionRequired application or operational behaviorClamAV unavailableDo not publish or release unscanned uploads. Quarantine or reject them until scanning succeeds.Image processing failsPreserve the original safely; do not expose incomplete or invalid variants. Record the processing failure.Email provider unavailablePreserve the visitor's message and record delivery failure independently.SQL Server unavailableFail safely, provide a controlled error response and avoid reporting failed writes as successful.Media storage unavailablePrevent unsafe upload/publication operations and expose an operational warning.Backup integrity failsMark the backup unusable, alert the responsible operator and preserve the last known valid recovery point.Background job fails repeatedlyRecord the failure, apply bounded retries and expose the failed job for investigation.Cache invalidation failsAvoid exposing unpublished or private content; provide a safe invalidation/recovery path.DNS or TLS failureBlock or correct production release readiness until public HTTPS access is valid.Insufficient storagePrevent partial or corrupt uploads and notify the administrator.

Failure behavior must be tested, not merely described.

15\. Release Dependencies and Readiness
=======================================

Release allocation remains governed by SCOPE\_AND\_RELEASES.

15.1 R1 — Professional Foundation
---------------------------------

Before the first public production release:

*   Single-administrator setup and recovery must be secure.
    
*   Identity and MFA controls must be verified.
    
*   Draft/published separation must work.
    
*   Private media must be protected.
    
*   Gallery publication must use genuine administrator-selected photographs.
    
*   Contact messages must persist independently of email delivery.
    
*   Essential production security and accessibility protections must pass.
    
*   Production database and media storage must be persistent.
    
*   Backup and restoration must demonstrate the four-hour recovery objectives.
    
*   Domain, DNS, TLS and production configuration must be verified.
    
*   Critical release tests must pass with recorded evidence.
    

15.2 R2 — Advanced Platform
---------------------------

Dependencies include:

*   Reviewed English/Bangla content for bilingual workflows.
    
*   Validated translation publication and fallback behavior.
    
*   Approved analytics and privacy implementation.
    
*   Approved advanced content and operational workflows.
    
*   Validated search, media and Gallery enhancements.
    
*   No regression of R1 security or privacy guarantees.
    

15.3 R3 — Production Excellence
-------------------------------

Dependencies include:

*   Full operational and recovery evidence.
    
*   Performance budgets and repeatable performance tests.
    
*   Security and accessibility regression evidence.
    
*   Improved monitoring and operational procedures.
    
*   Verification of remaining approved product requirements.
    
*   Documented maintenance and recovery readiness.
    

Essential security, privacy, accessibility and recovery protections for shipped features must not be deferred until R3.

16\. Validation and Evidence Management
=======================================

Each assumption, dependency and material risk must be validated using appropriate evidence.

Evidence may include:

*   Build and deployment logs.
    
*   Automated test results.
    
*   Integration and end-to-end test reports.
    
*   Security and authorization test results.
    
*   Accessibility audit results.
    
*   Performance measurements.
    
*   Database migration reports.
    
*   Backup integrity reports.
    
*   Timed restoration reports.
    
*   Storage persistence tests.
    
*   External service delivery tests.
    
*   Owner-approved content records.
    
*   Production configuration checklists.
    

16.1 Validation record
----------------------

For each validated item, record:

FieldDescriptionItem IDASM, OD, DEP or RSK identifierValidation resultPass, Fail, Partial or BlockedEnvironmentDevelopment, staging or productionBuild/versionApplication version testedMethodTest or inspection performedEvidence referenceReport, log, ticket or test IDVerified byResponsible personVerification dateDate of validationFollow-upRemaining action, if any

A dependency must not be marked validated without appropriate evidence.

17\. Change Management
======================

Changes to assumptions, dependencies, decisions or risks must be controlled.

17.1 Change triggers
--------------------

A review is required when:

*   Hosting or deployment architecture changes.
    
*   A third-party service changes its capabilities or availability.
    
*   A technical provider is replaced.
    
*   A security vulnerability affects an approved component.
    
*   A recovery objective cannot be achieved.
    
*   New product requirements introduce dependencies.
    
*   A dependency becomes unavailable or materially more expensive.
    
*   An assumption is disproved by testing.
    
*   A new risk materially affects an approved release.
    
*   An AI coding agent proposes a change to an approved architectural or product constraint.
    

17.2 Change procedure
---------------------

1.  Identify the affected item and its stable ID.
    
2.  Describe the reason and impact.
    
3.  Identify affected requirements and documents.
    
4.  Evaluate security, privacy, architecture, schedule, cost and release consequences.
    
5.  Propose a resolution.
    
6.  Obtain approval from the authorized owner.
    
7.  Update the relevant decision and documentation.
    
8.  Update implementation and testing plans.
    
9.  Preserve the previous decision in revision history.
    

Confirmed decisions must not be silently overwritten.

18\. Cross-Document Traceability
================================

The following mapping identifies where assumptions, dependencies and risks must be reflected elsewhere.

Item groupRelated documentsExpected consistencyASM-001–ASM-003PRD, DECISIONS, REQUIREMENTS\_CATALOGProduct boundary and single-admin modelASM-004–ASM-006DECISIONS, ADD, TECHNICAL\_SPEC, TESTING\_STRATEGYSetup, Identity and MFAASM-007–ASM-010ADD, TECHNICAL\_SPEC, DESIGN\_SYSTEMPlatform, architecture and UI foundationASM-011–ASM-014PRD, REQUIREMENTS\_CATALOG, DESIGN\_SYSTEMLocalization, Gallery and content authenticityASM-015–ASM-017ADD, TECHNICAL\_SPEC, TESTING\_STRATEGYMedia storage and privacyASM-018–ASM-020DECISIONS, TECHNICAL\_SPEC, TESTING\_STRATEGYEmail and abuse protectionASM-021–ASM-022DESIGN\_SYSTEM, TESTING\_STRATEGYAccessibility and visual experienceASM-024–ASM-025ADD, TECHNICAL\_SPEC, TESTING\_STRATEGYDocker and recoveryOD-001–OD-014DECISIONS, TECHNICAL\_SPEC, SCOPE\_AND\_RELEASESOpen decisions and technical validationDEP-EXT-001–DEP-EXT-008TECHNICAL\_SPEC, IMPLEMENTATION\_PLANExternal integrations and operationsDEP-INT-001–DEP-INT-014ADD, TECHNICAL\_SPEC, IMPLEMENTATION\_PLANPlatform and internal architectureDEP-CNT-001–DEP-CNT-012PRD, DESIGN\_SYSTEM, SCOPE\_AND\_RELEASESOwner-supplied contentRSK-001–RSK-035TESTING\_STRATEGY, REQUIREMENTS\_TRACEABILITY, SCOPE\_AND\_RELEASESRisk mitigation and verificationRelease dependenciesSCOPE\_AND\_RELEASES, IMPLEMENTATION\_PLANRelease readiness and sequencing

18.1 Requirement traceability rule
----------------------------------

Where a risk or dependency affects an approved requirement:

*   Record the relevant requirement ID.
    
*   Identify the affected acceptance criterion.
    
*   Identify the implementation task.
    
*   Identify the test or verification evidence.
    
*   Record any residual risk or approved exception.
    

Do not create duplicate requirement IDs merely to represent an operational risk.

19\. AI Coding Agent Instructions
=================================

Any AI coding agent working on this project must follow these rules.

1.  Read the current approved PRD, DECISIONS, Requirements Catalog, ADD, Technical Specification, Design System, Scope and Releases, and Testing Strategy before implementing affected work.
    
2.  Treat Confirmed decisions as binding.
    
3.  Treat Proposed decisions as recommendations requiring approval.
    
4.  Do not implement Open decisions as though they were approved.
    
5.  Do not invent production credentials, provider accounts, domains, personal information or portfolio claims.
    
6.  Do not introduce new dependencies or packages without explaining their purpose and compatibility.
    
7.  Do not weaken security, privacy, MFA, media protection or recovery requirements for convenience.
    
8.  Do not expose private media or unpublished content.
    
9.  Do not replace the approved UI foundation or architecture without an approved change.
    
10.  Do not claim that a backup, restore, deployment, scanner or external integration has been validated without evidence.
    
11.  Report newly discovered assumptions, dependencies and risks.
    
12.  Update affected documentation when an approved implementation change alters the technical baseline.
    
13.  Preserve stable document and requirement IDs.
    
14.  Stop and request clarification when a material conflict cannot be resolved from approved documentation.
    
15.  Clearly report implemented, tested, verified, blocked and deferred work separately.
    

20\. Review and Approval Checklist
==================================

Before this document is approved, the Product Owner should review:

*   Confirmed assumptions match the latest DECISIONS document.
    
*   No resolved decision remains incorrectly listed as open.
    
*   Proposed technical defaults have not been represented as confirmed.
    
*   Open decisions have clear owners and resolution points.
    
*   External dependencies have failure consequences and validation methods.
    
*   Internal dependencies match the ADD and Technical Specification.
    
*   Content dependencies reflect actual owner responsibilities.
    
*   Critical risks have mitigation and contingency plans.
    
*   RPO and RTO objectives have corresponding validation requirements.
    
*   R1 production prerequisites match SCOPE\_AND\_RELEASES.
    
*   Risk and dependency traceability is consistent with the Testing Strategy.
    
*   AI coding agent instructions do not conflict with approved project decisions.
    
*   Cross-document inconsistencies have been resolved or explicitly recorded.
    

21\. Document Maintenance
=========================

This document must be reviewed:

*   When a material project decision changes.
    
*   Before a release-readiness review.
    
*   When a major dependency changes.
    
*   When a critical or high risk is discovered.
    
*   After a significant production incident.
    
*   When recovery testing reveals a failure.
    
*   When an assumption is validated or disproved.
    

The document owner is responsible for ensuring that its status and contents remain aligned with the approved project baseline.

22\. Revision History
=====================

VersionDescriptionStatus1.0Initial assumptions, open decisions, dependencies and risks register.Previous baseline2.0Comprehensive restructuring; clarified decision status, added assumption validation, external/internal dependency registers, critical path, expanded risk management, failure handling, release dependencies, evidence requirements, traceability and AI-agent instructions.Review Draft

23\. Final Document Status
==========================

**Version:** 2.0**Status:** Comprehensive Review Draft — Pending Product Owner Approval

This document establishes a structured planning and risk-management baseline for the Personal Portfolio & Travel Gallery.

It does not imply that every proposed technical default has been approved, every environment dependency is available, or every risk has been eliminated.

The document becomes the authoritative Assumptions and Dependencies baseline only after Product Owner approval and consistency review against the related project documents.

**Approval authority:** Product Owner

**Approval date:** Pending

**Next review:** Before implementation readiness approval and before the first production release.
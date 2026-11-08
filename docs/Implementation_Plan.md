IMPLEMENTATION PLAN
===================

**Project:** Adib Hasan Avik — Personal Portfolio & Travel Gallery**Document:** Implementation Plan**Version:** 3.0**Status:** Comprehensive Execution Blueprint — Owner Review Required**Document Owner:** Adib Hasan Avik**Implementation Model:** Human Developer + AI Coding Agents**Primary Platform:** .NET 10 / ASP.NET Core MVC**Architecture:** Clean Architecture / Modular Monolith**Database:** SQL Server / Entity Framework Core 10**Frontend:** Razor / Bootstrap 5 / Custom CSS Design System**Release Strategy:** R1 is the first public production release (Option A)

1\. Purpose
===========

This document defines the dependency-aware implementation sequence for the Personal Portfolio & Travel Gallery.

It is the primary execution blueprint for human developers and AI coding agents. It converts the approved product and architecture baselines into bounded implementation phases with measurable completion conditions.

The plan is designed to ensure that:

*   Every implementation phase has one coherent objective.
    
*   Work follows actual architectural and technical dependencies.
    
*   Every applicable task references existing requirement IDs.
    
*   Security, privacy, accessibility and data integrity are built into the relevant features.
    
*   AI agents can execute work in bounded sessions without loading or modifying the entire application unnecessarily.
    
*   A phase is completed only after its verification and acceptance conditions pass.
    
*   Release readiness is based on evidence, not generated code or completed screens.
    

This plan does not replace the PRD, Requirements Catalog, ADD, Technical Specification, Testing Strategy, or Scope and Releases document.

2\. Execution Principles
========================

2.1 Phase execution
-------------------

Implementation is divided into 25 phases: P00 through P24.

Each phase must:

1.  Have its prerequisites satisfied.
    
2.  Implement only its stated scope and necessary dependencies.
    
3.  Produce identifiable code, configuration, tests or documentation.
    
4.  Pass the specified verification.
    
5.  Meet its acceptance criteria.
    
6.  Report blockers and unresolved decisions.
    
7.  Update implementation progress only after completion is evidenced.
    

A phase may contain several small implementation tasks. An AI agent may execute those tasks in multiple working sessions when necessary.

**A phase is a coherent delivery boundary, not a requirement to finish every task in one AI conversation.**

2.2 Vertical-slice implementation
---------------------------------

Where practical, implement features as complete vertical slices:

User interaction → MVC Controller → Application use case → Domain rules → Infrastructure → Database/external service → Response

Do not create large amounts of unused infrastructure before implementing a real use case.

2.3 Security and integrity first
--------------------------------

Do not postpone essential protections until final production hardening.

Examples:

*   Authorization must exist when protected functionality is introduced.
    
*   Private storage must be private from its first implementation.
    
*   Upload validation must exist before uploaded files can be used.
    
*   Publishing rules must be enforced in application logic, not only in the UI.
    
*   Database constraints and concurrency behavior must be considered when the relevant data is introduced.
    
*   Secrets must never be committed.
    
*   Contact messages must be persisted before notification delivery.
    

2.4 No silent scope changes
---------------------------

Do not introduce new product features, alternative frameworks, additional administrators, public accounts, microservices or a separate SPA without an approved decision.

If implementation reveals a missing requirement or architectural conflict:

1.  Stop the affected work.
    
2.  Identify the conflicting documents and requirement IDs.
    
3.  Explain the technical and delivery impact.
    
4.  Propose the smallest reasonable resolution.
    
5.  Obtain the required approval.
    
6.  Update the relevant documentation and traceability before continuing.
    

2.5 Implementation status vocabulary
------------------------------------

StatusMeaningNot StartedNo implementation work has begun.In ProgressWork is actively being implemented.BlockedWork cannot safely continue because of an unresolved dependency or decision.ImplementedCode or configuration exists, but acceptance has not yet been demonstrated.VerifiedAll applicable acceptance criteria passed and evidence was recorded.ReleasedThe verified work has been deployed to its intended environment.DeferredWork is assigned to a later approved release.

Never treat Implemented, Verified and Released as interchangeable.

3\. Authoritative Documentation
===============================

Before implementation, inspect the actual repository and identify the current approved versions of the project documents.

DocumentAuthorityPRD.mdProduct goals, scope, user journeys and user-visible behavior.REQUIREMENTS\_CATALOG.mdStable requirement IDs and acceptance criteria.ADD\_Comprehensive.mdArchitecture, module responsibilities and dependency boundaries.TECHNICAL\_SPEC\_v2.mdApproved technical baseline, proposed defaults and deployment-dependent configuration.DECISIONS.mdRecorded product, architecture and technical decisions.ASSUMPTIONS\_AND\_DEPENDENCIES.mdAssumptions, open decisions, dependencies and risks.SCOPE\_AND\_RELEASES\_v2.mdRelease goals, proposed allocations and release gates.TESTING\_STRATEGY.mdTest layers, critical scenarios and quality gates.REQUIREMENTS\_TRACEABILITY\_v2.mdRequirement-to-design, implementation and test traceability.DESIGN\_SYSTEM.mdVisual language, components, interaction and accessibility rules, if present in the repository.PAGE\_DESIGN\_SPECIFICATION.mdPage composition, Admin workflows and visitor journeys, if present in the repository.AGENTS.mdRepository-specific instructions for coding agents, if present.

### 3.1 Conflict resolution

Use this precedence model:

1.  Approved product scope and behavior: PRD and Requirements Catalog.
    
2.  Architecture boundaries: approved ADD.
    
3.  Technical implementation: approved Technical Specification and recorded decisions.
    
4.  Release allocation: approved Scope and Releases.
    
5.  Visual and interaction rules: approved Design System and Page Design Specification.
    
6.  Verification: Testing Strategy and registered test cases.
    
7.  Implementation sequencing: this document.
    

A draft recommendation is not automatically an approved decision.

If two authoritative documents conflict, do not choose whichever is easiest to implement. Record the conflict and request a decision.

### 3.2 Baseline issues that must be reconciled

The available documentation identifies the following issues:

*   SCOPE\_AND\_RELEASES\_v2.md is a review draft; detailed requirement-level release allocations remain provisional.
    
*   TECHNICAL\_SPEC\_v2.md distinguishes approved technology choices from proposed defaults and unresolved deployment decisions.
    
*   The Requirements Catalog contains 78 requirement IDs.
    
*   The current RTM identifies implementation-task mapping as incomplete.
    
*   The current Scope v2 references FR-I18N-001 through FR-I18N-003, but those IDs are absent from the current Requirements Catalog. Do not use these IDs as if they were valid.
    
*   The PRD describes an independently switchable Bangla Admin interface, but the current catalog does not provide a distinct requirement ID for that workflow.
    
*   The current implementation plan contains seeded default administrator credentials, an unresolved Bootstrap/Tailwind choice, an environment-specific database connection string and a much narrower feature scope than the current PRD.
    

Resolve or explicitly record these issues before treating the plan as a fully approved execution baseline.

4\. Implementation Baseline
===========================

4.1 Approved technology baseline
--------------------------------

AreaBaselineRuntime.NET 10Web frameworkASP.NET Core MVCArchitectureClean ArchitectureApplication shapeModular MonolithDatabaseSQL ServerORMEntity Framework Core 10FrontendRazor ViewsCSS foundationBootstrap 5Visual stylingCustom CSS and approved design tokensIdentityASP.NET Core IdentityApplication patternsCQRS, MediatR, Repository and Unit of Work abstractionsMappingMapsterValidationFluentValidationLoggingSerilogDeploymentDocker-compatibleEmail providerMailtrap Sandbox in Development; Mailtrap Email Sending in Production after domain verificationAnti-bot protectionGoogle reCAPTCHA v3 with server-side verificationAccessibility targetWCAG 2.2 AARecovery objectivesRPO no greater than 4 hours; RTO no greater than 4 hours

Do not replace these baseline choices without an approved decision.

4.2 Recommended defaults requiring status preservation
------------------------------------------------------

The following choices are recorded as recommendations or proposed defaults, not as automatically approved infrastructure:

AreaCurrent treatmentBackground jobsHangfire with SQL Server persistence is proposed.Reliable event deliveryTransactional outbox is proposed as the reliability approach.Rich-text editorQuill is recommended but remains open pending review.File scanning providerClamAV is proposed behind an IFileSecurityScanner abstraction.Cache providerStart with the simplest suitable ASP.NET Core cache; confirm the exact strategy.Image processing libraryUse an abstraction; confirm the provider after compatibility and licensing review.Dependency injectionBuilt-in .NET DI is the recommended default.Production hostingProvider remains deployment-dependent.Backup destination and retentionMust be confirmed against the recovery objectives and hosting capabilities.

Do not install or integrate a proposed provider merely because it appears in an example.

4.3 Architecture boundaries
---------------------------

Maintain the dependency direction defined by the ADD:

*   **Domain:** business entities, value objects, domain rules and invariants.
    
*   **Application:** commands, queries, use cases, validation, authorization decisions and application-owned interfaces.
    
*   **Infrastructure:** EF Core, SQL Server, Identity persistence, media storage, email, scanner, background jobs and external integrations.
    
*   **Web/Presentation:** MVC controllers, Razor Views, filters, middleware, authentication configuration and HTTP behavior.
    

Rules:

*   Domain must not reference Application, Infrastructure or Web.
    
*   Application must not reference Infrastructure or Web.
    
*   Infrastructure must not reference Web.
    
*   Controllers must not contain business logic or directly implement persistence workflows.
    
*   Do not expose EF Core entities directly as public presentation contracts.
    
*   Keep external provider implementations behind appropriate application-owned abstractions.
    
*   Do not introduce microservices or a separate frontend application.
    

The exact solution and project names must be discovered from the repository. Do not rename existing projects simply to match examples in this document.

5\. Phase Dependency Overview
=============================

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   P00  Baseline Reconciliation   |  P01  Repository and Development Environment   |  P02  Solution and Architecture Skeleton   |  P03  Web Host and Cross-Cutting Foundation   |  P04  Database and Persistence Foundation   |  P05  Domain Model and Business Invariants   |  P06  Application Layer and Use-Case Foundation   |  P07  Single-Administrator Identity and Security   |  P08  Admin Shell and Dashboard Foundation   |  P09  Publishing and Content Lifecycle   |  P10  Core Portfolio Content Management   |  P11  Projects, Achievements and Certifications Management   |  P12  Public Site Foundation and Core Pages   |  P13  Public Projects and Supporting Content Pages   |  P14  Resume Management and Delivery   |  P15  Media Storage and Secure Upload Foundation   |  P16  Media Library Workflows   |  P17  Contact, Email and Inbox   |  P18  Gallery Foundation   |  P19  Advanced Gallery Experience   |  P20  Localization and SEO   |  P21  Search and Analytics   |  P22  Operations, Backup and Recovery   |  P23  Cross-Cutting Quality and Production Hardening   |  P24  Production Deployment and Release   `

This is the default dependency order. A phase may be partially prepared earlier only when its prerequisites are already satisfied and doing so does not bypass a security, data-integrity or architectural dependency.

6\. Implementation Phases
=========================

P00 — Baseline Reconciliation and Implementation Readiness
----------------------------------------------------------

**Objective**

Establish a trustworthy implementation baseline before code changes begin. Prevent agents from implementing outdated scope, invalid requirement references or unapproved technical choices.

**Prerequisites**

*   Access to the repository.
    
*   Access to the current project documentation.
    

**Implementation tasks**

1.  Inspect the repository root, solution files, project files, existing code, tests, configuration and Git status.
    
2.  Locate and read AGENTS.md and any nested agent instructions.
    
3.  Identify the actual filenames and versions of the project documents.
    
4.  Compare the current repository against the approved architecture and technical baseline.
    
5.  Extract the exact 78 requirement IDs from the current Requirements Catalog; do not invent or rename IDs.
    
6.  Identify missing, duplicate, contradictory or orphan requirement references.
    
7.  Record the unresolved FR-I18N-\* references and the missing catalog trace for the independently switchable Admin language workflow.
    
8.  Identify decisions that block immediate implementation, including any provider or deployment choice required by the first planned work.
    
9.  Confirm whether the repository is empty, partially scaffolded or already contains implementation.
    
10.  Prepare a concise baseline and blocker report.
    

**Requirements traceability**

Cross-cutting: all 78 catalog requirements. No feature is marked implemented by this phase.

**Expected deliverables**

*   Repository inventory.
    
*   Documentation/version inventory.
    
*   Requirement-ID validation report.
    
*   Architecture and technical conflict report.
    
*   Open-decision and blocker list.
    
*   Initial phase status register.
    

**Verification**

*   Compare every requirement ID against the catalog.
    
*   Confirm no invented requirement IDs appear in the plan.
    
*   Confirm actual solution/project names and target frameworks.
    
*   Confirm all discovered agent instructions are accounted for.
    
*   Confirm no existing work is overwritten or discarded.
    

**Acceptance criteria**

*   The repository structure is understood.
    
*   The current requirements baseline is identified.
    
*   Invalid traceability references are explicitly recorded.
    
*   Unresolved decisions have owners or a clear approval requirement.
    
*   No implementation begins against a known contradictory baseline.
    

**Definition of Done**

The baseline report is complete, and all issues that would materially change the first implementation phases are either resolved or recorded as blockers.

**Next phase**

P01 — Repository and Development Environment.

**Execution command**

Execute P00: Reconcile the Repository, Documentation and Implementation Baseline

P01 — Repository and Development Environment
--------------------------------------------

**Objective**

Establish a reproducible local development environment and safe repository workflow.

**Prerequisites**

*   P00 complete.
    
*   Actual solution/repository state identified.
    

**Implementation tasks**

1.  Verify the installed .NET 10 SDK and runtime compatibility.
    
2.  Verify SQL Server development connectivity or the approved local database approach.
    
3.  Confirm the repository's existing Git branch and working-tree state.
    
4.  Establish or document the branch and commit conventions.
    
5.  Add or validate .gitignore for .NET, IDE, build and local environment files.
    
6.  Add .editorconfig and the agreed formatting conventions.
    
7.  Configure nullable reference types and compiler settings consistently with the project baseline.
    
8.  Establish safe local configuration and secret-loading conventions.
    
9.  Add an example configuration file containing placeholders only.
    
10.  Confirm that local secrets, connection strings and credentials are excluded from source control.
    
11.  Configure the selected CI workflow only after the repository's CI platform is identified and approved.
    

**Requirements traceability**

NFR-SEC-003, NFR-MAINT-001, NFR-DEP-001.

**Expected deliverables**

*   Reproducible local development setup.
    
*   Repository conventions.
    
*   Safe configuration template.
    
*   Validated .gitignore and .editorconfig.
    
*   Documented environment prerequisites.
    

**Verification**

Run from the repository root:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   dotnet --info  dotnet --list-sdks  git status --short   `

Inspect tracked files for secrets and environment-specific configuration.

**Acceptance criteria**

*   The required SDK is available.
    
*   Local development prerequisites are documented.
    
*   No real secrets or production credentials are committed.
    
*   Git and formatting conventions are usable.
    

**Definition of Done**

Another developer can prepare the local environment using the documented instructions without needing undocumented machine-specific values.

**Next phase**

P02 — Solution and Architecture Skeleton.

**Execution command**

Execute P01: Establish the Repository and Local Development Environment

P02 — Solution and Architecture Skeleton
----------------------------------------

**Objective**

Create or validate the solution structure and enforce Clean Architecture dependency boundaries.

**Prerequisites**

*   P01 complete.
    
*   Approved architecture baseline available.
    

**Implementation tasks**

1.  Reuse the existing solution structure if it already follows the approved architecture.
    
2.  If the repository is empty, create the solution and the agreed Domain, Application, Infrastructure and Web projects.
    
3.  Create the required test projects using the testing approach selected for the repository.
    
4.  Configure project references according to the ADD.
    
5.  Keep Domain independent from infrastructure and presentation packages.
    
6.  Establish consistent folder and namespace conventions.
    
7.  Add modular service-registration entry points where appropriate.
    
8.  Add architecture tests or equivalent automated checks for dependency direction.
    
9.  Document the purpose of each project and its allowed dependencies.
    
10.  Do not add speculative modules, microservices or a separate SPA.
    

**Requirements traceability**

NFR-MAINT-001, NFR-DEP-001.

**Expected deliverables**

*   Valid solution structure.
    
*   Correct project references.
    
*   Architecture boundary checks.
    
*   Project responsibility documentation.
    

**Verification**

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`dotnet restore   dotnet build  --no-restore  dotnet test` 

Use the actual solution path discovered in P00.

**Acceptance criteria**

*   All projects restore and build.
    
*   Dependency direction matches the ADD.
    
*   Domain has no prohibited outer-layer dependency.
    
*   Architecture tests detect a deliberately introduced prohibited reference in a controlled test or equivalent validation.
    

**Definition of Done**

The solution builds and its architectural boundaries are automatically testable.

**Next phase**

P03 — Web Host and Cross-Cutting Foundation.

**Execution command**

Execute P02: Establish the Clean Architecture Solution and Project Boundaries

P03 — Web Host and Cross-Cutting Foundation
-------------------------------------------

**Objective**

Create a reliable ASP.NET Core MVC host with consistent configuration, diagnostics and request handling.

**Prerequisites**

*   P02 complete.
    

**Implementation tasks**

1.  Configure the Web project's startup and composition root.
    
2.  Register Application and Infrastructure services through their designated registration methods.
    
3.  Configure Serilog structured logging using the approved initial sinks.
    
4.  Implement centralized exception handling and safe error responses.
    
5.  Configure strongly typed options and startup validation for required settings.
    
6.  Configure request correlation or trace identifiers.
    
7.  Configure health-check endpoints with appropriate liveness and readiness behavior.
    
8.  Configure anti-forgery services and global security defaults.
    
9.  Add appropriate security headers without enabling production-only settings prematurely.
    
10.  Configure environment-specific behavior for Development, Staging and Production.
    
11.  Ensure logs redact secrets and sensitive personal data.
    
12.  Do not expose detailed exceptions or configuration values to public visitors.
    

**Requirements traceability**

NFR-SEC-001, NFR-SEC-003, NFR-REL-001, NFR-DEP-001, NFR-OBS-001.

**Expected deliverables**

*   Running MVC host.
    
*   Centralized logging and exception handling.
    
*   Configuration and options validation.
    
*   Health checks.
    
*   Initial security defaults.
    

**Verification**

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`dotnet restore   dotnet build  --no-restore  dotnet test` 

Start the Web application using the repository's actual startup project and verify its health endpoints.

**Acceptance criteria**

*   Application starts in Development.
    
*   Invalid required configuration fails clearly.
    
*   Exceptions return safe responses and are logged appropriately.
    
*   Health endpoints distinguish application health from dependency readiness.
    
*   No secret appears in logs or public responses.
    

**Definition of Done**

The Web host provides a stable, observable foundation for feature development.

**Next phase**

P04 — Database and Persistence Foundation.

**Execution command**

Execute P03: Configure the ASP.NET Core Host and Cross-Cutting Services

P04 — Database and Persistence Foundation
-----------------------------------------

**Objective**

Establish SQL Server persistence, EF Core mappings, migration discipline and data-integrity foundations.

**Prerequisites**

*   P02 and P03 complete.
    
*   SQL Server development/test connectivity available.
    

**Implementation tasks**

1.  Configure SQL Server through environment-specific connection settings.
    
2.  Configure Entity Framework Core 10 and the application's DbContext.
    
3.  Define entity configurations using the ADD and domain model.
    
4.  Configure primary keys, foreign keys, indexes, unique constraints and delete behavior.
    
5.  Establish transaction boundaries and concurrency handling.
    
6.  Implement the approved Repository and Unit of Work abstractions where required by the architecture.
    
7.  Avoid unnecessary generic repository complexity.
    
8.  Configure Identity persistence integration without creating the initial administrator.
    
9.  Implement idempotent Admin role creation only, if required by the Identity design.
    
10.  Create the initial migration after reviewing the model.
    
11.  Document the controlled migration procedure for Development, Staging and Production.
    
12.  Do not automatically apply unreviewed migrations during production startup.
    

**Requirements traceability**

FR-SEC-002, NFR-DATA-001, NFR-MAINT-001, NFR-REL-001.

**Expected deliverables**

*   SQL Server connection configuration.
    
*   DbContext and entity mappings.
    
*   Persistence abstractions and implementations.
    
*   Initial migration.
    
*   Migration and database setup instructions.
    

**Verification**

Use the actual Infrastructure and Web project paths:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`dotnet build   dotnet test` 

Where EF tooling is installed and configured:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`dotnet ef migrations list --project --startup-project` 

Apply migrations only to an explicitly selected Development or test database.

**Acceptance criteria**

*   The application can connect to the intended development database.
    
*   Migrations apply successfully.
    
*   Constraints and relationships behave as designed.
    
*   Repeated initialization does not duplicate or corrupt the Admin role.
    
*   Production migration behavior is controlled and documented.
    

**Definition of Done**

Database persistence and migration behavior are repeatable and covered by integration tests.

**Next phase**

P05 — Domain Model and Business Invariants.

**Execution command**

Execute P04: Establish SQL Server, EF Core and Persistence Infrastructure

P05 — Domain Model and Business Invariants
------------------------------------------

**Objective**

Implement the domain model required by the approved product scope without embedding infrastructure or MVC concerns.

**Prerequisites**

*   P02 complete.
    
*   P04 persistence conventions established.
    
*   Relevant PRD and ADD sections reviewed.
    

**Implementation tasks**

1.  Identify the domain aggregates and ownership boundaries from the ADD and Requirements Catalog.
    
2.  Model the approved portfolio content: profile, experience, education, skills, projects, achievements and certifications.
    
3.  Model content lifecycle and publication-related domain rules where they belong in the Domain layer.
    
4.  Model resume, contact, media and Gallery concepts according to their actual aggregate boundaries.
    
5.  Define value objects and enumerations only where they express meaningful domain concepts.
    
6.  Define validation and state-transition invariants.
    
7.  Define safe parent/child visibility rules for Gallery albums and photographs.
    
8.  Define media-reference and deletion invariants.
    
9.  Define audit-related domain information without storing secrets or unnecessary personal data.
    
10.  Avoid speculative entity fields, aggregate boundaries and abstractions.
    
11.  Keep EF Core configuration outside the Domain layer.
    

**Requirements traceability**

FR-ADM-002, FR-ADM-003, FR-MED-005, FR-GAL-003–FR-GAL-006, FR-CON-001–FR-CON-005, FR-RES-001–FR-RES-003, NFR-DATA-001, NFR-MAINT-001.

**Expected deliverables**

*   Domain entities and value objects.
    
*   Aggregate and relationship definitions.
    
*   Domain invariants.
    
*   Domain unit tests.
    

**Verification**

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`dotnet build   dotnet test` 

Use actual project paths and test project names.

**Acceptance criteria**

*   Domain rules are testable without SQL Server or MVC.
    
*   Invalid state transitions are rejected.
    
*   No prohibited Infrastructure, EF Core or MVC dependencies enter Domain.
    
*   Relationships and invariants match the documented product behavior.
    

**Definition of Done**

The domain model is sufficiently stable for application use cases and persistence integration.

**Next phase**

P06 — Application Layer and Use-Case Foundation.

**Execution command**

Execute P05: Implement the Domain Model and Business Invariants

P06 — Application Layer and Use-Case Foundation
-----------------------------------------------

**Objective**

Establish consistent application use cases, validation, mapping and cross-cutting application behavior.

**Prerequisites**

*   P02 and P05 complete.
    

**Implementation tasks**

1.  Configure MediatR and the approved CQRS conventions.
    
2.  Establish feature-oriented command, query, handler and validator organization.
    
3.  Configure Mapster mappings for application contracts.
    
4.  Implement FluentValidation integration.
    
5.  Add validation pipeline behavior where appropriate.
    
6.  Define application-owned interfaces for persistence and external services.
    
7.  Define consistent application result and error handling conventions.
    
8.  Establish transaction behavior for use cases that require multiple writes.
    
9.  Define cancellation-token propagation and asynchronous execution conventions.
    
10.  Add authorization checks at the application/use-case boundary where required.
    
11.  Avoid creating handlers, DTOs or abstractions without an actual use case.
    
12.  Add unit tests for representative command, query and validation flows.
    

**Requirements traceability**

Cross-cutting application support for FR-ADM-002–FR-ADM-008, FR-SEC-001–FR-SEC-007, FR-MED-001–FR-MED-012, FR-GAL-001–FR-GAL-018, FR-CON-001–FR-CON-005, FR-RES-001–FR-RES-003, NFR-MAINT-001, NFR-DATA-001.

**Expected deliverables**

*   Application service registration.
    
*   CQRS conventions.
    
*   Validation and mapping configuration.
    
*   Application-owned interfaces.
    
*   Representative unit tests.
    

**Verification**

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`dotnet build   dotnet test` 

**Acceptance criteria**

*   Application use cases compile independently of Web and Infrastructure.
    
*   Validators execute through the agreed pipeline.
    
*   Mapping behavior is tested.
    
*   Application handlers do not directly depend on Infrastructure implementations.
    
*   Transactions are applied at the correct use-case boundary.
    

**Definition of Done**

A new feature can be implemented using a predictable application pattern without duplicating cross-cutting logic.

**Next phase**

P07 — Single-Administrator Identity and Security.

**Execution command**

Execute P06: Establish CQRS, Validation, Mapping and Application Use Cases

P07 — Single-Administrator Identity and Security
------------------------------------------------

**Objective**

Implement the complete one-administrator authentication and protection model.

**Prerequisites**

*   P03, P04 and P06 complete.
    
*   Identity security decisions confirmed.
    

**Implementation tasks**

1.  Configure ASP.NET Core Identity with the approved user and role model.
    
2.  Implement the one-time initial administrator Setup Wizard.
    
3.  Make administrator creation atomic under concurrent requests.
    
4.  Ensure setup is available only while no administrator exists.
    
5.  Disable setup permanently after successful administrator creation.
    
6.  Create the Admin role idempotently; do not seed a default administrator account or password.
    
7.  Require authenticator-app TOTP enrollment and verification.
    
8.  Generate and safely handle recovery codes.
    
9.  Implement login, logout, lockout and session controls.
    
10.  Implement secure password reset with expiry, rate limiting and generic responses.
    
11.  Ensure password reset does not bypass MFA and revokes sessions according to the approved policy.
    
12.  Prevent public registration and additional Admin role assignment.
    
13.  Apply server-side authorization to every Admin route, action and protected resource.
    
14.  Integrate Google reCAPTCHA v3 with server-side action and score verification for the approved protected forms.
    
15.  Configure rate limiting and anti-forgery protection.
    
16.  Audit security-sensitive actions without recording passwords, tokens, MFA codes or recovery codes.
    

**Requirements traceability**

FR-ADM-001, FR-SEC-001–FR-SEC-007, NFR-SEC-001, NFR-SEC-002, NFR-SEC-003.

**Expected deliverables**

*   Identity configuration.
    
*   One-time Setup Wizard.
    
*   MFA and recovery workflow.
    
*   Authentication and authorization policies.
    
*   Security audit behavior.
    
*   Identity integration and security tests.
    

**Verification**

Run the relevant unit, integration and Web tests.

Verify these scenarios explicitly:

*   Setup unavailable when an administrator already exists.
    
*   Two simultaneous setup attempts cannot create two administrators.
    
*   Setup becomes unavailable after success.
    
*   Public registration cannot create an Admin.
    
*   MFA is required.
    
*   Recovery does not bypass the security policy.
    
*   Unauthorized users cannot access Admin routes or private operations.
    
*   Password reset tokens expire and cannot be reused.
    

**Acceptance criteria**

All critical Identity scenarios in TESTING\_STRATEGY.md pass with recorded evidence.

**Definition of Done**

The application has exactly one secure administrator setup and access workflow, with no seeded default administrator credentials.

**Next phase**

P08 — Admin Shell and Dashboard Foundation.

**Execution command**

Execute P07: Implement Secure Single-Administrator Identity and MFA

P08 — Admin Shell and Dashboard Foundation
------------------------------------------

**Objective**

Create the protected Admin Panel structure and its core navigation, dashboard and shared management interactions.

**Prerequisites**

*   P07 complete.
    
*   Design System and Page Design Specification reviewed.
    

**Implementation tasks**

1.  Create or validate the ASP.NET Core MVC Admin Area.
    
2.  Implement the Admin layout, sidebar, topbar and responsive navigation.
    
3.  Apply server-side authorization to the entire protected area.
    
4.  Implement the dashboard using real persisted data only.
    
5.  Add the approved overview of content, recent activity and contact inbox status.
    
6.  Provide operational status placeholders only where the underlying monitoring capability is not yet implemented; do not fabricate healthy states.
    
7.  Implement shared list patterns for search, filters, sorting and pagination.
    
8.  Implement empty, loading, validation, error and permission-denied states.
    
9.  Implement unsaved-change warnings and contextual destructive-action confirmations.
    
10.  Implement the authorized website settings foundation.
    
11.  Ensure sensitive Admin actions are auditable.
    
12.  Keep the dashboard modular so later modules can contribute their own status and summary data.
    

**Requirements traceability**

FR-ADM-001, FR-ADM-005, FR-ADM-006, FR-ADM-007, FR-ADM-008, NFR-OBS-001, NFR-ACC-001.

**Expected deliverables**

*   Admin layout and navigation.
    
*   Protected dashboard.
    
*   Shared Admin list and form patterns.
    
*   Settings foundation.
    
*   UI state components and tests.
    

**Verification**

*   Verify anonymous and unauthorized access is denied.
    
*   Verify Admin navigation and pages work at supported viewport sizes.
    
*   Verify dashboard values come from real application data.
    
*   Verify filters, pagination, empty states and confirmation behavior.
    

**Acceptance criteria**

The Admin Panel has a consistent, protected and responsive foundation. No dashboard metric or operational status is fabricated.

**Definition of Done**

The Admin shell is ready for individual content and operational modules.

**Next phase**

P09 — Publishing and Content Lifecycle.

**Execution command**

Execute P08: Build the Protected Admin Shell and Dashboard Foundation

P09 — Publishing and Content Lifecycle
--------------------------------------

**Objective**

Implement safe draft, preview, publish, unpublish and publication-state handling before broad content management is exposed.

**Prerequisites**

*   P04, P05, P06 and P07 complete.
    

**Implementation tasks**

1.  Implement the content publication lifecycle according to the PRD.
    
2.  Separate editable draft state from the currently published public state.
    
3.  Ensure edits to a published item do not change the live version until publication.
    
4.  Implement authorized preview routes that never expose draft content to anonymous visitors.
    
5.  Implement publish and unpublish use cases.
    
6.  Enforce publication eligibility in application queries and public routes.
    
7.  Implement cache invalidation for publication, unpublication and relevant content changes.
    
8.  Ensure drafts and unpublished content are excluded from public search and sitemap queries.
    
9.  Define the behavior for scheduled publishing only if the requirement and provider decision are confirmed.
    
10.  Make scheduled execution idempotent and observable if implemented.
    
11.  Add audit records for publication changes.
    
12.  Test parent/child publication rules where relevant.
    

**Requirements traceability**

FR-ADM-003, FR-ADM-004, FR-PUB-002, FR-GAL-005, FR-GAL-006, FR-RES-002, FR-SEO-002.

**Expected deliverables**

*   Publication lifecycle.
    
*   Preview authorization.
    
*   Public eligibility rules.
    
*   Cache invalidation behavior.
    
*   Publication tests.
    

**Verification**

Test that:

*   Draft content is not publicly accessible.
    
*   Editing a published item does not alter its live version.
    
*   Preview requires authorized access.
    
*   Unpublishing removes content from public routes and discovery.
    
*   Cache invalidation prevents stale public content.
    
*   Scheduled publication, if approved, is retry-safe and observable.
    

**Acceptance criteria**

Public visitors can only access content eligible for publication, and Admin edits cannot leak before publication.

**Definition of Done**

Publication behavior is implemented and tested independently of individual content modules.

**Next phase**

P10 — Core Portfolio Content Management.

**Execution command**

Execute P09: Implement Draft, Preview, Publish and Unpublish Workflows

P10 — Core Portfolio Content Management
---------------------------------------

**Objective**

Implement Admin management for the foundational personal and professional portfolio content.

**Prerequisites**

*   P05, P06, P08 and P09 complete.
    

**Implementation tasks**

1.  Implement profile content management.
    
2.  Implement experience management.
    
3.  Implement education management.
    
4.  Implement skills and skill-category management.
    
5.  Add the required create, view, update and safe delete/archive use cases.
    
6.  Add server-side validation for all management forms.
    
7.  Integrate the publishing lifecycle.
    
8.  Implement sorting and display-order management where required.
    
9.  Prevent invalid or incomplete content from being published.
    
10.  Add audit history for important content changes.
    
11.  Ensure the public query model returns only eligible published data.
    
12.  Do not invent personal facts, employment history, educational details or skills; use owner-provided verified content.
    

**Requirements traceability**

FR-ADM-002, FR-ADM-006, FR-ADM-007, FR-ADM-008, FR-PUB-001, FR-PUB-002, NFR-DATA-001.

**Expected deliverables**

*   Profile, experience, education and skills Admin modules.
    
*   Application handlers and validators.
    
*   Persistence mappings and migrations where required.
    
*   Admin views and public read queries.
    
*   Unit and integration tests.
    

**Verification**

Test CRUD, validation, ordering, publication and unauthorized access for each content type.

**Acceptance criteria**

The administrator can manage the foundational content without source-code changes. Public pages receive only eligible published content.

**Definition of Done**

All four content modules pass their relevant CRUD, validation, authorization and publication tests.

**Next phase**

P11 — Projects, Achievements and Certifications Management.

**Execution command**

Execute P10: Implement Profile, Experience, Education and Skills CMS

P11 — Projects, Achievements and Certifications Management
----------------------------------------------------------

**Objective**

Implement structured management of engineering projects, achievements and certifications.

**Prerequisites**

*   P05, P06, P08 and P09 complete.
    

**Implementation tasks**

1.  Implement project management with completed, in-progress and planned statuses.
    
2.  Implement project featured-state and display-order controls.
    
3.  Implement structured project case-study sections supported by the PRD.
    
4.  Support project technologies, links, images and relevant resources through approved media references.
    
5.  Implement achievement management.
    
6.  Implement certification management.
    
7.  Add validation for dates, URLs, ordering and required content.
    
8.  Integrate draft, preview, publish and unpublish.
    
9.  Ensure planned work is never represented as completed.
    
10.  Ensure project details display only verified facts supplied or approved by the owner.
    
11.  Implement safe media-reference handling.
    
12.  Add tests for project status, publication and content integrity.
    

**Requirements traceability**

FR-ADM-002, FR-ADM-003, FR-ADM-007, FR-ADM-008, FR-PUB-001, FR-PUB-002.

**Expected deliverables**

*   Projects CMS.
    
*   Achievements CMS.
    
*   Certifications CMS.
    
*   Project case-study data model and management views.
    
*   Tests for status and publication behavior.
    

**Verification**

*   Test all project statuses.
    
*   Test featured and ordering behavior.
    
*   Test draft and published project details.
    
*   Test that unpublished content cannot be retrieved publicly.
    
*   Test media reference integrity.
    

**Acceptance criteria**

The administrator can manage all three content types. Public case studies accurately reflect approved content and project status.

**Definition of Done**

All management workflows and publication rules for projects, achievements and certifications pass their tests.

**Next phase**

P12 — Public Site Foundation and Core Pages.

**Execution command**

Execute P11: Implement Projects, Achievements and Certifications CMS

P12 — Public Site Foundation and Core Pages
-------------------------------------------

**Objective**

Build the public-facing design foundation and the first group of portfolio pages.

**Prerequisites**

*   P08, P09 and P10 complete.
    
*   Approved Design System and Page Design Specification available.
    

**Implementation tasks**

1.  Implement the public layout and shared navigation.
    
2.  Implement the public footer and shared page composition patterns.
    
3.  Apply the Executive Dark visual direction.
    
4.  Implement the deliberate light theme.
    
5.  Use system preference on the first visit and persist an explicit visitor selection.
    
6.  Implement responsive navigation and theme controls.
    
7.  Build Home, About, Education and Skills pages.
    
8.  Connect pages to published application queries.
    
9.  Implement page-specific empty states where owner content is not yet available.
    
10.  Apply semantic HTML, accessible labels, keyboard focus and reduced-motion behavior.
    
11.  Use Bootstrap 5 only as the responsive foundation; apply the custom design system for visual identity.
    
12.  Do not populate the site with fabricated profile information or placeholder portfolio claims.
    

**Requirements traceability**

FR-PUB-001, FR-PUB-002, FR-PUB-003, FR-PUB-006, FR-ADM-006, NFR-ACC-001, NFR-COMP-001.

**Expected deliverables**

*   Public layout.
    
*   Navigation and footer.
    
*   Dark/light theme behavior.
    
*   Home, About, Education and Skills pages.
    
*   Responsive and accessibility tests.
    

**Verification**

*   Test routes and published-only output.
    
*   Test theme persistence and system preference behavior.
    
*   Test keyboard navigation and visible focus.
    
*   Test narrow and wide viewport layouts.
    
*   Run automated accessibility checks on the implemented pages.
    

**Acceptance criteria**

The initial public experience is coherent, responsive and accessible. It uses real approved content and does not expose drafts.

**Definition of Done**

The public shell and four core pages meet their page-level acceptance criteria.

**Next phase**

P13 — Public Projects and Supporting Content Pages.

**Execution command**

Execute P12: Build the Public Layout, Themes and Core Portfolio Pages

P13 — Public Projects and Supporting Content Pages
--------------------------------------------------

**Objective**

Complete the main public portfolio content experience beyond the foundational pages.

**Prerequisites**

*   P11 and P12 complete.
    

**Implementation tasks**

1.  Implement the Projects listing page.
    
2.  Implement project featured sections and status filters.
    
3.  Implement project case-study detail pages with stable routes.
    
4.  Display only the case-study sections supported by verified owner content.
    
5.  Implement Achievements and Certifications pages.
    
6.  Implement the relevant public navigation and cross-links.
    
7.  Add appropriate empty, not-found and unavailable-content states.
    
8.  Ensure project status is represented accurately.
    
9.  Apply responsive image presentation and meaningful alternative text.
    
10.  Verify that unpublished and planned content is presented according to its approved status and visibility rules.
    

**Requirements traceability**

FR-PUB-001, FR-PUB-002, FR-PUB-006.

**Expected deliverables**

*   Projects listing.
    
*   Project detail/case-study pages.
    
*   Achievements page.
    
*   Certifications page.
    
*   Route and publication tests.
    

**Verification**

*   Verify listing and detail routes.
    
*   Verify status filtering.
    
*   Verify unpublished content is inaccessible.
    
*   Verify invalid slugs return the appropriate not-found behavior.
    
*   Verify responsive presentation and keyboard navigation.
    

**Acceptance criteria**

Visitors can understand the owner's engineering work through accurate, structured and published project evidence.

**Definition of Done**

All assigned public project and supporting-content journeys pass their route, content and accessibility checks.

**Next phase**

P14 — Resume Management and Delivery.

**Execution command**

Execute P13: Implement Public Projects, Case Studies and Supporting Pages

P14 — Resume Management and Delivery
------------------------------------

**Objective**

Implement secure resume version management, publication, preview and download.

**Prerequisites**

*   P06, P09 and the initial Media Library storage foundation from P15 must be available before final file integration. Resume metadata and application contracts may be prepared earlier, but file delivery must wait for secure storage.
    

**Implementation tasks**

1.  Define the resume version model according to the PRD.
    
2.  Support language and professional variants.
    
3.  Implement Admin upload and metadata management.
    
4.  Validate PDF content and file constraints server-side.
    
5.  Implement independent draft and publication states.
    
6.  Implement selection of the default published resume version.
    
7.  Provide public preview and download for eligible versions only.
    
8.  Ensure draft and previous unpublished versions cannot be retrieved publicly.
    
9.  Implement stable public access according to the approved URL policy.
    
10.  Record aggregate download events for later analytics integration.
    
11.  Use protected source storage and controlled public delivery.
    
12.  Do not create or publish an invented resume.
    

**Requirements traceability**

FR-PUB-008, FR-RES-001, FR-RES-002, FR-RES-003, FR-MED-003, FR-MED-004, NFR-SEC-002, NFR-PRIV-001.

**Expected deliverables**

*   Resume management module.
    
*   Resume versioning and publication.
    
*   Secure PDF validation and delivery.
    
*   Download event integration.
    
*   Resume tests.
    

**Verification**

*   Test invalid PDF rejection.
    
*   Test draft and unpublished version denial.
    
*   Test default-version selection.
    
*   Test public preview and download.
    
*   Test authorization and stable URL behavior.
    

**Acceptance criteria**

Only the intended published resume version is available publicly. Private source files and unpublished versions remain protected.

**Definition of Done**

Resume management and delivery pass their functional, publication and access-control tests.

**Next phase**

P15 — Media Storage and Secure Upload Foundation.

**Execution command**

Execute P14: Implement Resume Versioning, Publication and Secure Delivery

P15 — Media Storage and Secure Upload Foundation
------------------------------------------------

**Objective**

Establish durable media storage and a secure upload pipeline that can be reused by the Resume, Contact and Gallery modules.

**Prerequisites**

*   P04 and P06 complete.
    
*   Storage and scanner interfaces defined.
    
*   Scanner deployment choice confirmed before enabling production uploads.
    

**Implementation tasks**

1.  Implement the approved storage abstraction.
    
2.  Implement local persistent storage using deployment-mounted locations.
    
3.  Separate public and private storage.
    
4.  Ensure private files are stored outside wwwroot.
    
5.  Implement authorized private-file delivery endpoints.
    
6.  Validate file extension, detected content type, file signature and actual structure.
    
7.  Enforce configured file-size limits server-side.
    
8.  Implement safe temporary upload staging.
    
9.  Integrate the IFileSecurityScanner abstraction.
    
10.  Treat scanner errors, timeouts and unavailable states as untrusted; quarantine or reject according to the approved policy.
    
11.  Keep ClamAV as a proposed provider until its deployment and resource requirements are approved.
    
12.  Prevent unscanned or quarantined files from being published or downloaded.
    
13.  Record processing and scanning states.
    
14.  Ensure storage paths are not directly exposed for private assets.
    
15.  Preserve originals when later processing fails.
    

**Requirements traceability**

FR-MED-001, FR-MED-002, FR-MED-003, FR-MED-004, FR-MED-011, FR-CON-004, FR-GAL-018, NFR-SEC-001, NFR-SEC-002, NFR-PRIV-001, NFR-REL-001.

**Expected deliverables**

*   Storage abstraction and local provider.
    
*   Public/private storage separation.
    
*   Secure upload pipeline.
    
*   Scanner abstraction and provider integration when approved.
    
*   Private-file authorization.
    
*   Upload and access tests.
    

**Verification**

Test:

*   Extension/signature mismatch.
    
*   Unsupported and oversized files.
    
*   Corrupt images and PDFs.
    
*   Scanner clean, infected, timeout and unavailable outcomes.
    
*   Anonymous and unauthorized private-file access.
    
*   Container restart with persistent media.
    
*   No private file under public static paths.
    

**Acceptance criteria**

No unsafe or unscanned file can become available as trusted content. Private assets cannot be accessed without authorization. Media survives container replacement when the configured persistent volume is retained.

**Definition of Done**

The reusable media storage and secure upload foundation passes its negative and positive security tests.

**Next phase**

P16 — Media Library Workflows.

**Execution command**

Execute P15: Implement Persistent Media Storage and Secure Upload Protection

P16 — Media Library Workflows
-----------------------------

**Objective**

Complete the reusable Media Library management capabilities.

**Prerequisites**

*   P08, P09 and P15 complete.
    

**Implementation tasks**

1.  Implement the seven approved Media Library categories.
    
2.  Implement single and bulk upload with per-file status and retry behavior.
    
3.  Implement metadata management and search.
    
4.  Implement category, visibility, file-type, date and processing filters.
    
5.  Implement image optimization, thumbnails and responsive variants through the approved processing abstraction.
    
6.  Preserve originals when processing succeeds or fails.
    
7.  Implement media usage/reference tracking.
    
8.  Show known references before replacement or deletion.
    
9.  Implement safe replacement without breaking existing content links.
    
10.  Implement recycle-bin behavior and retention.
    
11.  Implement permanent deletion with reference and concurrency rechecks.
    
12.  Implement SHA-256 duplicate detection without leaking private asset existence.
    
13.  Implement storage quota calculation and safe upload blocking.
    
14.  Integrate media metadata and stored objects with backup/restore.
    
15.  Record important media operations in audit history.
    

**Requirements traceability**

FR-MED-001–FR-MED-012, FR-ADM-007, FR-ADM-008, NFR-DATA-001, NFR-PERF-001, NFR-PRIV-001.

**Expected deliverables**

*   Complete Media Library workflows.
    
*   Metadata and reference management.
    
*   Image variants and original preservation.
    
*   Recycle bin and duplicate detection.
    
*   Quota and audit behavior.
    
*   Media lifecycle tests.
    

**Verification**

*   Test each media category.
    
*   Test independent bulk-upload success/failure.
    
*   Test metadata search and filters.
    
*   Test processing failure and retry.
    
*   Test replacement and reference protection.
    
*   Test recycle and restore.
    
*   Test duplicate detection privacy boundaries.
    
*   Test quota enforcement.
    
*   Test media backup and restoration.
    

**Acceptance criteria**

The administrator can manage media safely throughout its lifecycle without breaking content references or exposing private assets.

**Definition of Done**

All assigned Media Library acceptance criteria pass with integration and security evidence.

**Next phase**

P17 — Contact, Email and Inbox.

**Execution command**

Execute P16: Complete Media Library Management and Asset Lifecycle

P17 — Contact, Email and Inbox
------------------------------

**Objective**

Implement the complete visitor contact submission and Admin inbox workflow with reliable notification behavior.

**Prerequisites**

*   P07, P08 and P15 complete.
    
*   Mailtrap configuration available for Development.
    
*   Production sending domain remains deployment-dependent.
    

**Implementation tasks**

1.  Implement the public Contact page and form.
    
2.  Implement the approved inquiry categories.
    
3.  Validate visitor input server-side.
    
4.  Apply anti-forgery, reCAPTCHA v3 and rate limiting.
    
5.  Validate optional attachments using the approved allowlist and limits.
    
6.  Store attachments privately and require scanning before use.
    
7.  Persist the contact message and attachment references before attempting email delivery.
    
8.  Implement independent visitor-confirmation and administrator-notification delivery states.
    
9.  Integrate the Mailtrap Sandbox adapter for Development.
    
10.  Configure production Mailtrap sending through protected environment configuration after domain verification.
    
11.  Implement the Admin inbox with search, filters and message status.
    
12.  Implement conversation threads, visitor-visible replies and separate Admin-only internal notes.
    
13.  Implement archive, deletion and retention controls.
    
14.  Ensure retries do not create duplicate messages or replies.
    
15.  Preserve submitted messages during email-provider outages.
    
16.  Add operational visibility for failed or delayed delivery.
    

**Requirements traceability**

FR-PUB-007, FR-CON-001–FR-CON-005, FR-ADM-005, FR-ADM-007, FR-MED-003, FR-MED-004, NFR-SEC-001, NFR-SEC-002, NFR-PRIV-001, NFR-REL-001, NFR-DATA-001.

**Expected deliverables**

*   Public contact form.
    
*   Contact application workflows.
    
*   Mailtrap development integration.
    
*   Production email configuration adapter.
    
*   Admin inbox and conversation management.
    
*   Attachment protection.
    
*   Email outage and retry tests.
    

**Verification**

Simulate:

*   Invalid form data.
    
*   reCAPTCHA rejection.
    
*   Rate-limit rejection.
    
*   Invalid and oversized attachments.
    
*   Scanner failure.
    
*   Database failure.
    
*   Email-provider outage.
    
*   Duplicate delivery attempts.
    
*   Unauthorized attachment access.
    
*   Retention and deletion actions.
    

**Acceptance criteria**

A valid message is persisted before delivery is attempted. Email failure does not lose the message. Visitor and administrator notification states remain independent. Private attachments remain protected.

**Definition of Done**

The Contact workflow passes its functional, security, privacy and failure-recovery tests.

**Next phase**

P18 — Gallery Foundation.

**Execution command**

Execute P17: Implement Contact Submission, Mailtrap and Admin Inbox

P18 — Gallery Foundation
------------------------

**Objective**

Implement the secure Gallery foundation and its core album/photo publishing behavior.

**Prerequisites**

*   P09, P15 and P16 complete.
    
*   Gallery release allocation confirmed by the product owner before release commitment.
    

**Implementation tasks**

1.  Implement Gallery album and photograph management.
    
2.  Integrate photographs with existing Media Library assets.
    
3.  Implement required album fields and optional destination/travel metadata.
    
4.  Implement photograph metadata and administrator-controlled public fields.
    
5.  Implement album and photograph publication states.
    
6.  Implement Public, Unlisted and Private visibility.
    
7.  Enforce the strictest applicable parent/child visibility rule.
    
8.  Ensure a published album cannot expose an unpublished or private photograph.
    
9.  Implement featured album/photo and ordering foundations.
    
10.  Implement the Gallery public landing page and album route.
    
11.  Implement the designed empty state when no real photographs have been uploaded and published.
    
12.  Use only administrator-uploaded and selected real photographs.
    
13.  Do not populate Gallery with stock, generated, placeholder or sample content.
    
14.  Integrate Gallery media references with the Media Library and backup model.
    

**Requirements traceability**

FR-GAL-001–FR-GAL-006, FR-GAL-008, FR-GAL-017, FR-GAL-018, FR-PUB-001, FR-PUB-002, NFR-SEC-002, NFR-PRIV-001, NFR-DATA-001.

**Expected deliverables**

*   Gallery album/photo models.
    
*   Admin album and photo management foundation.
    
*   Public Gallery landing and album pages.
    
*   Visibility and publication policies.
    
*   Empty-state implementation.
    
*   Gallery access tests.
    

**Verification**

Test every relevant combination of:

*   Album publication state.
    
*   Album visibility.
    
*   Photograph publication state.
    
*   Photograph visibility.
    
*   Anonymous and authenticated Admin access.
    

Also verify:

*   Empty Gallery before owner upload.
    
*   Unlisted content is excluded from discovery.
    
*   Private content requires Admin authorization.
    
*   Media references remain valid.
    

**Acceptance criteria**

No photograph can become publicly accessible unless its own state and all parent rules permit it. The initial Gallery remains empty until real owner-selected content is published.

**Definition of Done**

Gallery foundation and negative-access tests pass.

**Next phase**

P19 — Advanced Gallery Experience.

**Execution command**

Execute P18: Implement Gallery Albums, Photos and Visibility Foundation

P19 — Advanced Gallery Experience
---------------------------------

**Objective**

Complete the visitor-facing Gallery experience and its advanced management controls.

**Prerequisites**

*   P18 complete.
    
*   Approved Gallery design and interaction specifications available.
    

**Implementation tasks**

1.  Implement the approved masonry and uniform-grid presentation options.
    
2.  Implement the accessible full-screen lightbox/photo viewer.
    
3.  Implement previous/next navigation and keyboard controls.
    
4.  Implement mobile-appropriate viewer interactions.
    
5.  Implement Gallery search and filters.
    
6.  Implement related album/photo behavior.
    
7.  Implement shareable public and unlisted URLs with appropriate OpenGraph metadata.
    
8.  Enforce download permissions server-side.
    
9.  Implement original-resolution download restrictions.
    
10.  Implement optional comments only if enabled by the administrator.
    
11.  Keep comments disabled by default.
    
12.  Require moderation approval before comments become public.
    
13.  Keep commenter email private.
    
14.  Audit moderation and reporting actions.
    
15.  Implement Gallery empty, loading, error and unavailable states.
    
16.  Verify responsive behavior and accessibility.
    

**Requirements traceability**

FR-GAL-007–FR-GAL-015, FR-PUB-001, FR-PUB-006, FR-ADM-007, NFR-ACC-001, NFR-PRIV-001.

**Expected deliverables**

*   Advanced Gallery layouts.
    
*   Accessible lightbox.
    
*   Search/filter experience.
    
*   Sharing metadata and URL behavior.
    
*   Download controls.
    
*   Optional moderated comments.
    
*   Gallery UI and security tests.
    

**Verification**

*   Keyboard-only viewer operation.
    
*   Previous/next and close behavior.
    
*   Mobile viewer behavior.
    
*   Search/filter exclusion of private and unpublished items.
    
*   Download permission enforcement.
    
*   Comment moderation and public visibility.
    
*   OpenGraph behavior for public/unlisted/private content.
    
*   Automated accessibility scans and manual keyboard checks.
    

**Acceptance criteria**

The Gallery provides the approved visitor experience without violating publication, privacy, download or moderation rules.

**Definition of Done**

All advanced Gallery acceptance criteria pass with access-control and accessibility evidence.

**Next phase**

P20 — Localization and SEO.

**Execution command**

Execute P19: Complete Gallery Browsing, Viewer, Sharing and Moderation

P20 — Localization and SEO
--------------------------

**Objective**

Implement the approved multilingual public experience and search-engine metadata behavior.

**Prerequisites**

*   P09, P12 and relevant content modules complete.
    
*   Translation workflow and Admin language requirements reconciled with the Requirements Catalog.
    
*   Owner-provided English and Bangla content available before content publication.
    

**Implementation tasks**

1.  Implement language-prefixed public routes using /en/ and /bn/.
    
2.  Implement English as the default language and Bangla as the additional language.
    
3.  Implement language-specific content and metadata.
    
4.  Implement language selection and persistence.
    
5.  Preserve equivalent-page navigation when a translated destination exists.
    
6.  Use the approved fallback behavior when a translation is unavailable.
    
7.  Never fall back to an unpublished translation.
    
8.  Implement the translation management workflow after its requirement and acceptance criteria are confirmed.
    
9.  Implement the independently switchable Admin interface language only after its missing catalog traceability is resolved.
    
10.  Implement canonical URLs and hreflang.
    
11.  Implement published-only sitemap generation.
    
12.  Exclude Admin, draft, private and unlisted content from public indexing.
    
13.  Implement appropriate metadata and robots behavior.
    
14.  Ensure language-specific slugs and redirects follow the approved URL policy.
    
15.  Do not invent translations or publish unreviewed language content.
    

**Requirements traceability**

FR-PUB-001, FR-PUB-002, FR-PUB-004, FR-SEO-001, FR-SEO-002, FR-RES-001, NFR-PRIV-001.

**Traceability blocker**

The current Requirements Catalog does not contain FR-I18N-001–FR-I18N-003, although Scope v2 references them. Do not use those identifiers until the Catalog is formally updated. The independently switchable Admin interface language also requires explicit requirement traceability.

**Expected deliverables**

*   Language-prefixed routing.
    
*   Language selection and fallback behavior.
    
*   Translation management workflow, once approved.
    
*   Canonical/hreflang metadata.
    
*   Published-only sitemap.
    
*   Localization and SEO tests.
    

**Verification**

*   Test English and Bangla routes.
    
*   Test equivalent-page switching.
    
*   Test unavailable translation fallback.
    
*   Test unpublished translation exclusion.
    
*   Test canonical and hreflang values.
    
*   Test sitemap exclusion of private, unlisted and unpublished content.
    
*   Test Admin language independence after its requirement is approved.
    

**Acceptance criteria**

Language routing and SEO behavior follow the approved rules. No unpublished or private content leaks through language fallback, metadata or sitemap generation.

**Definition of Done**

All catalog-backed localization and SEO criteria pass. Any additional Admin translation workflow has approved requirement coverage.

**Next phase**

P21 — Search and Analytics.

**Execution command**

Execute P20: Implement Localization, Language Routing and SEO

P21 — Search and Analytics
--------------------------

**Objective**

Implement global public search and privacy-conscious analytics using only eligible published content.

**Prerequisites**

*   P09, P12 and the relevant content modules complete.
    
*   Analytics privacy, consent and retention decisions confirmed before nonessential tracking is enabled.
    

**Implementation tasks**

1.  Implement global search across the approved content types.
    
2.  Group search results into meaningful categories.
    
3.  Ensure results link to the correct public routes.
    
4.  Exclude drafts, private content, unpublished translations and non-discoverable unlisted content.
    
5.  Implement Gallery search/filter integration.
    
6.  Implement aggregate visitor metrics according to the approved privacy model.
    
7.  Implement Gallery analytics where approved.
    
8.  Implement aggregate resume-download metrics.
    
9.  Exclude administrator activity from visitor analytics.
    
10.  Implement consent behavior for nonessential tracking.
    
11.  Implement date comparisons and exports where required by the catalog.
    
12.  Apply retention controls and data minimization.
    
13.  Ensure analytics does not become invasive visitor profiling.
    
14.  Display truthful analytics and operational values in the Admin dashboard.
    
15.  Avoid selecting an external analytics provider before the decision is approved.
    

**Requirements traceability**

FR-PUB-005, FR-GAL-009, FR-GAL-016, FR-RES-003, FR-ANA-001, FR-ANA-002, FR-ADM-005, NFR-PRIV-001, NFR-PERF-001.

**Expected deliverables**

*   Global search.
    
*   Search result grouping and filtering.
    
*   Analytics event/aggregation model.
    
*   Consent and retention behavior.
    
*   Admin analytics presentation.
    
*   Search and privacy tests.
    

**Verification**

*   Test search across every approved content type.
    
*   Test that private and unpublished content never appears.
    
*   Test administrator exclusion.
    
*   Test consent behavior.
    
*   Test aggregation and date comparisons.
    
*   Test retention behavior.
    
*   Test analytics failure without breaking public pages.
    

**Acceptance criteria**

Search returns only eligible public content. Analytics is aggregated, privacy-conscious and consistent with approved consent and retention rules.

**Definition of Done**

Search and analytics meet their functional and privacy acceptance criteria, with evidence.

**Next phase**

P22 — Operations, Backup and Recovery.

**Execution command**

Execute P21: Implement Global Search and Privacy-Conscious Analytics

P22 — Operations, Background Processing, Backup and Recovery
------------------------------------------------------------

**Objective**

Provide dependable operational visibility and demonstrate the application's recovery objectives.

**Prerequisites**

*   P03 and P04 complete.
    
*   Relevant feature modules and persistent storage available.
    
*   Background-job provider and backup destination decisions approved before provider-specific implementation.
    

**Implementation tasks**

1.  Define the background-processing requirements for scheduled publishing, email/outbox delivery, image processing, cleanup and backup workflows.
    
2.  Confirm the background-job provider before integrating provider-specific code.
    
3.  If Hangfire is approved, configure persistent SQL Server-backed job storage.
    
4.  Implement durable, idempotent and bounded-retry job behavior.
    
5.  Implement the transactional outbox if approved by the technical decision process.
    
6.  Prevent duplicate job execution from causing duplicate notifications or destructive operations.
    
7.  Implement job status and failure visibility.
    
8.  Implement email/outbox delivery monitoring.
    
9.  Implement storage availability and capacity monitoring.
    
10.  Implement scanner and image-processing status visibility.
    
11.  Implement backup scheduling and external backup copies.
    
12.  Coordinate database, media originals, variants and media manifests.
    
13.  Protect backup encryption keys and recovery credentials.
    
14.  Implement backup integrity verification.
    
15.  Implement a controlled restore workflow with reauthentication, confirmation and a pre-restore safety copy.
    
16.  Validate restored database/media references.
    
17.  Implement maintenance mode and operational audit.
    
18.  Write operational runbooks for backup, restore, failed jobs, email outages and storage problems.
    
19.  Conduct isolated restore drills and record measured recovery results.
    

**Requirements traceability**

FR-ADM-005, FR-ADM-006, FR-ADM-004, FR-CON-002, FR-CON-005, FR-MED-012, FR-GAL-018, NFR-REL-001, NFR-DR-001, NFR-OBS-001, NFR-DATA-001.

**Expected deliverables**

*   Background-processing integration.
    
*   Job and delivery monitoring.
    
*   Backup and restore workflows.
    
*   External backup configuration.
    
*   Operational dashboard capabilities.
    
*   Runbooks and recovery evidence.
    

**Verification**

*   Simulate transient and permanent job failures.
    
*   Verify bounded retries and idempotency.
    
*   Verify email/outbox recovery.
    
*   Verify backup completeness and checksums.
    
*   Restore database and media into an isolated environment.
    
*   Verify restored references and media integrity.
    
*   Measure RPO and RTO.
    
*   Verify maintenance mode and operational status reporting.
    

**Acceptance criteria**

The system can detect and report critical operational failures. Database and media restore consistently. RPO is no greater than four hours and RTO is no greater than four hours under the documented recovery test conditions.

**Definition of Done**

The required recovery objectives are demonstrated through recorded restore evidence. A configured backup schedule alone is not sufficient.

**Next phase**

P23 — Cross-Cutting Quality and Production Hardening.

**Execution command**

Execute P22: Implement Operations, Background Jobs and Verified Recovery

P23 — Cross-Cutting Quality and Production Hardening
----------------------------------------------------

**Objective**

Validate the complete application against its security, accessibility, performance, compatibility and maintainability requirements.

**Prerequisites**

*   All release-required feature phases complete.
    
*   P22 recovery evidence available for production readiness.
    
*   Supported browser policy and numeric performance budgets approved.
    

**Implementation tasks**

1.  Review all Admin and private-resource authorization boundaries.
    
2.  Run security tests for authentication, authorization, CSRF, XSS, account enumeration, rate limits and file uploads.
    
3.  Review rich-text sanitization and output encoding.
    
4.  Verify private media and attachments cannot be accessed through static paths or unauthorized endpoints.
    
5.  Scan dependencies and container images using the selected tools.
    
6.  Review secret handling and Data Protection key persistence.
    
7.  Run automated accessibility scans.
    
8.  Perform manual WCAG 2.2 AA checks for keyboard navigation, focus, labels, errors, contrast, screen-reader announcements, dialogs, lightbox and reduced motion.
    
9.  Test dark and light themes.
    
10.  Test current/recent Chrome, Edge, Firefox and Safari, plus iOS Safari and Android Chrome.
    
11.  Test the approved mobile, tablet, laptop and desktop viewport matrix.
    
12.  Measure Core Web Vitals, page weight, image delivery, database query behavior and background processing.
    
13.  Compare measurements against approved performance budgets.
    
14.  Review slow queries, N+1 behavior, pagination and resource limits.
    
15.  Verify logs and operational status do not expose sensitive data.
    
16.  Run the full regression suite.
    
17.  Review architecture boundaries and remove only demonstrably unnecessary implementation artifacts.
    
18.  Update the RTM with actual implementation and test references.
    
19.  Record unresolved defects and formally accepted exceptions.
    

**Requirements traceability**

FR-PUB-003, FR-PUB-006, FR-ADM-001, FR-SEC-001–FR-SEC-007, FR-MED-003, FR-MED-004, FR-MED-011, FR-GAL-005, FR-GAL-006, FR-GAL-010, FR-GAL-013, FR-CON-004, NFR-SEC-001–NFR-SEC-003, NFR-PRIV-001, NFR-ACC-001, NFR-PERF-001, NFR-COMP-001, NFR-MAINT-001, NFR-REL-001, NFR-DATA-001.

**Expected deliverables**

*   Security test report.
    
*   Accessibility report and manual checklist.
    
*   Browser/device regression report.
    
*   Performance measurements.
    
*   Dependency/container scan results.
    
*   Full regression test results.
    
*   Updated RTM and defect register.
    

**Verification**

Run the full solution build and test suite. Execute the security, accessibility, browser, performance and recovery checks defined in TESTING\_STRATEGY.md.

**Acceptance criteria**

*   No unresolved critical security defect.
    
*   No known private/draft content exposure.
    
*   WCAG 2.2 AA target is validated for the release scope.
    
*   Supported browser/device journeys pass.
    
*   Approved performance budgets are met or formally accepted exceptions are recorded.
    
*   Critical/high-severity defects are resolved or formally accepted by the owner.
    
*   Test and traceability evidence is complete.
    

**Definition of Done**

All applicable quality gates pass, and every exception has a documented owner decision and impact.

**Next phase**

P24 — Production Deployment and Release.

**Execution command**

Execute P23: Complete Security, Accessibility, Performance and Regression Validation

P24 — Production Deployment and Release
---------------------------------------

**Objective**

Deploy the verified application to the selected production environment and complete the approved release process.

**Prerequisites**

*   P23 complete.
    
*   Hosting provider and canonical domain selected.
    
*   Production secrets and sending domain configured securely.
    
*   Production database and persistent media strategy verified.
    
*   Release scope approved.
    
*   Required RPO/RTO evidence available.
    

**Implementation tasks**

1.  Confirm the production hosting target and deployment architecture.
    
2.  Prepare the production Docker image using a supported .NET 10 runtime.
    
3.  Use a multi-stage build and run as a non-root user where supported.
    
4.  Configure persistent database, media and Data Protection key storage.
    
5.  Configure HTTPS, canonical domain, trusted proxy behavior and required security headers.
    
6.  Configure production Mailtrap sending after domain verification.
    
7.  Configure reCAPTCHA production keys through protected configuration.
    
8.  Configure scanner, background jobs, storage and backup integrations according to approved decisions.
    
9.  Verify environment configuration and secret availability.
    
10.  Create and verify a pre-deployment backup.
    
11.  Review and approve database migrations before applying them.
    
12.  Deploy the application image.
    
13.  Verify liveness, readiness and critical dependencies.
    
14.  Run production smoke tests for public pages, Admin authentication/MFA, content publication, media delivery, contact persistence and background jobs.
    
15.  Verify logs, operational monitoring and backup status.
    
16.  Verify the canonical domain, HTTPS, redirects, sitemap and robots behavior.
    
17.  Record the deployed build/image version and release result.
    
18.  Execute the documented rollback or forward-fix procedure if deployment fails.
    
19.  Update release documentation and the RTM with deployment evidence.
    

**Requirements traceability**

NFR-SEC-003, NFR-REL-001, NFR-DR-001, NFR-DEP-001, NFR-OBS-001, NFR-DATA-001, plus all requirements allocated to the release being deployed.

**Expected deliverables**

*   Production Docker image.
    
*   Production configuration.
    
*   Database migration record.
    
*   Deployment and smoke-test report.
    
*   Backup verification record.
    
*   Release record and rollback instructions.
    
*   Updated RTM.
    

**Verification**

Where Docker Compose is the selected deployment mechanism:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   docker compose config  docker compose build  docker compose up -d  docker compose ps  docker compose logs --tail=200   `

Use the actual Compose file and deployment configuration. Do not assume production SQL Server must run in the same Compose stack; the production database may be externally managed.

Run the approved production smoke-test checklist.

**Acceptance criteria**

*   Application is deployed to the approved production environment.
    
*   HTTPS and canonical domain behavior are correct.
    
*   Database and media persistence are verified.
    
*   Admin authentication and MFA work.
    
*   Public content is published-only.
    
*   Contact messages persist independently of email delivery.
    
*   Private media remains protected.
    
*   Monitoring and backup verification are operational.
    
*   Required recovery objectives have supporting evidence.
    
*   Release record and rollback procedure are available.
    

**Definition of Done**

The release is deployed, smoke-tested, monitored and documented. Only then may the release be marked Released.

**Next phase**

No next implementation phase is implied. Begin the next approved release cycle or maintenance work through the same change-control process.

**Execution command**

Execute P24: Deploy, Verify and Record the Approved Production Release

7\. Requirements-to-Phase Traceability
======================================

This section provides the master implementation destination for the 78 requirement IDs in the current REQUIREMENTS\_CATALOG.md.

The mapping identifies where a requirement is implemented or verified. It does not mean that the requirement is already implemented or that every release contains its full acceptance scope.

Requirement IDImplementation phase(s)FR-PUB-001P12, P13, P18, P19, P20FR-PUB-002P09, P12, P13, P14, P18, P19, P20, P21FR-PUB-003P12, P23FR-PUB-004P20FR-PUB-005P21FR-PUB-006P12, P19, P23FR-PUB-007P17FR-PUB-008P14FR-ADM-001P07, P08FR-ADM-002P10, P11FR-ADM-003P09, P10, P11FR-ADM-004P09, P22FR-ADM-005P08, P22FR-ADM-006P08, P10, P11, P22FR-ADM-007P08, P10, P11, P16, P17, P19, P21FR-ADM-008P08, P10, P11FR-SEC-001P07FR-SEC-002P04, P07FR-SEC-003P07FR-SEC-004P07FR-SEC-005P07FR-SEC-006P07FR-SEC-007P07, P08, P16, P17, P18, P19, P22FR-MED-001P15, P16FR-MED-002P15, P16FR-MED-003P15FR-MED-004P15FR-MED-005P16FR-MED-006P16FR-MED-007P16FR-MED-008P16FR-MED-009P16FR-MED-010P16FR-MED-011P15FR-MED-012P16, P22FR-GAL-001P18, P19FR-GAL-002P18, P19FR-GAL-003P18FR-GAL-004P18FR-GAL-005P18FR-GAL-006P18FR-GAL-007P19FR-GAL-008P19FR-GAL-009P19, P21FR-GAL-010P19, P23FR-GAL-011P19FR-GAL-012P19, P20FR-GAL-013P19FR-GAL-014P19FR-GAL-015P19FR-GAL-016P21FR-GAL-017P18FR-GAL-018P18, P22FR-CON-001P17FR-CON-002P17, P22FR-CON-003P17FR-CON-004P15, P17FR-CON-005P17, P22FR-RES-001P14, P20FR-RES-002P14FR-RES-003P14, P21FR-SEO-001P20FR-SEO-002P20, P21FR-ANA-001P21FR-ANA-002P21NFR-SEC-001P03, P07, P15, P17, P23NFR-SEC-002P07, P15, P17, P18, P19, P23NFR-SEC-003P01, P03, P24NFR-PRIV-001P17, P20, P21, P22, P23NFR-ACC-001P08, P12, P19, P23NFR-PERF-001P03, P16, P21, P23NFR-REL-001P03, P17, P22, P24NFR-DR-001P22, P24NFR-COMP-001P12, P19, P23NFR-MAINT-001P01, P02, P03, P05, P06, P23NFR-DEP-001P01, P02, P03, P24NFR-OBS-001P03, P08, P22, P24NFR-DATA-001P04, P05, P15, P16, P17, P22

7.1 Traceability rules
----------------------

1.  Preserve all existing requirement IDs exactly.
    
2.  Do not invent test IDs or claim test cases exist before they are registered.
    
3.  A phase may reference a requirement without completing its full acceptance criteria.
    
4.  If a requirement is delivered incrementally, record the exact release slice.
    
5.  Do not mark a requirement Verified until all applicable acceptance criteria pass.
    
6.  Do not mark a requirement Released until its verified implementation is deployed.
    
7.  Update the RTM with actual task, pull request/commit, code location, test case and evidence references.
    
8.  Run both Catalog-to-Plan and Plan-to-Catalog orphan checks after any baseline change.
    

7.2 Catalog gaps
----------------

The following must be resolved through the requirements change process:

*   FR-I18N-001–FR-I18N-003 are referenced by the current Scope v2 but do not exist in the current Requirements Catalog.
    
*   The PRD's independently switchable Admin interface language requires an explicit requirement and acceptance criteria if it remains committed scope.
    
*   Do not silently add these IDs to the implementation plan as though they were already approved.
    

8\. Release Alignment
=====================

The release assignments below follow the current Scope v2 proposal and must remain provisional until the product owner approves the release allocation.

**The confirmed release approach is Option A: R1 is the first public production release.** Development and Staging testing occur continuously before that launch.

PhaseProposed release alignmentNotesP00–P09Foundation for R1Architecture, environment, persistence, Identity, Admin and publishing foundations.P10–P17R1Core CMS, public portfolio, resume, essential media and contact functionality.P18R1 secure Gallery foundation, subject to approvalSecure foundation and empty state; confirm exact public Gallery scope.P19R2 proposedAdvanced Gallery experience, layouts, viewer, sharing and moderation.P20R2 proposedFull English/Bangla and localization workflow. R1 must not misrepresent incomplete translation support.P21R2 proposedGlobal search and expanded privacy-conscious analytics.P22R1 production gate plus R2/R3 maturityEssential monitoring, backup and demonstrated recovery objectives must exist before R1 production if the four-hour RPO/RTO commitment remains binding.P23R1 production gate plus R2/R3 regression maturityEssential security, privacy, accessibility and compatibility checks cannot be deferred if doing so would make R1 unsafe or violate an approved requirement.P24R1 first production release; repeated for R2/R3Deployment, smoke tests, release evidence and rollback.

8.1 Release 1 — Professional Foundation
---------------------------------------

Proposed scope:

*   Public Home, About, Education, Skills, Projects, Achievements, Certifications, Resume and Contact.
    
*   Project case studies and status presentation.
    
*   Single-admin setup, Identity, MFA and recovery.
    
*   Admin dashboard and core content CRUD/publishing.
    
*   Essential Media Library and persistent storage.
    
*   Contact persistence, Mailtrap integration and inbox.
    
*   Initial published resume.
    
*   Executive Dark/light themes and responsive experience.
    
*   Essential security, logging, health checks and deployment configuration.
    
*   Secure Gallery foundation if the proposed allocation is approved.
    
*   Required production backup/restore and operational protections.
    

R1 must be a real production release, not an untested prototype.

8.2 Release 2 — Advanced Platform
---------------------------------

Proposed scope:

*   Advanced Gallery experience.
    
*   Full Media Library workflows.
    
*   English/Bangla content and Admin interface localization.
    
*   Global search and expanded SEO.
    
*   Privacy-conscious analytics and consent.
    
*   Optional moderated comments, disabled by default.
    
*   Expanded operational dashboard.
    
*   Resume variants and richer contact workflows.
    

8.3 Release 3 — Production Excellence
-------------------------------------

Proposed scope:

*   Further security hardening and regression maturity.
    
*   Repeated backup/restore and disaster-recovery exercises.
    
*   Performance optimization and load testing.
    
*   Full browser/device regression.
    
*   Deployment automation and operational runbook maturity.
    
*   Release governance and monitoring improvements.
    

**Release rule:** Essential security, privacy, accessibility, backup and recovery protections must not be postponed merely because an enhancement is listed in R2 or R3.

9\. AI Coding-Agent Execution Protocol
======================================

This protocol applies to Claude Code, Codex and other coding agents working in the repository.

9.1 Before starting a phase
---------------------------

1.  Read this implementation plan.
    
2.  Read the root AGENTS.md and any relevant nested agent instructions, if present.
    
3.  Inspect the current Git status and existing implementation.
    
4.  Read only the project documents relevant to the current phase, in addition to the mandatory baseline documents.
    
5.  Confirm that the phase prerequisites are satisfied.
    
6.  Confirm the exact requirement IDs and release allocation.
    
7.  Identify unresolved decisions that materially affect the work.
    
8.  If a blocker exists, report it before changing code.
    

Do not repeatedly load every document when a phase only requires a small, known subset. Use the document authority table to select the relevant source.

9.2 During implementation
-------------------------

1.  Execute only the current phase and its necessary dependencies.
    
2.  Follow existing repository conventions.
    
3.  Reuse approved architectural patterns and existing abstractions.
    
4.  Make the smallest coherent set of changes that satisfies the phase.
    
5.  Avoid unrelated refactoring.
    
6.  Avoid speculative features and unnecessary packages.
    
7.  Preserve security, authorization, privacy and data-integrity controls.
    
8.  Add or update tests with the implementation.
    
9.  Update migrations when the data model changes.
    
10.  Do not fabricate personal content, credentials, photos, achievements or project metrics.
    
11.  Do not change an approved decision without authorization.
    
12.  Do not mark work complete based only on code generation.
    

9.3 After implementation
------------------------

1.  Run the phase's specified verification commands.
    
2.  Run relevant existing regression tests.
    
3.  Fix failures introduced by the current changes.
    
4.  Review the Git diff for unrelated changes, secrets and accidental deletions.
    
5.  Update the RTM with actual implementation and test references.
    
6.  Update phase status only when the Definition of Done is satisfied.
    
7.  Report any unresolved issue or deferred item.
    

9.4 Required phase completion report
------------------------------------

At the end of every phase, the agent must provide:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   PHASE: Pxx — Phase Name  STATUS: Verified / Implemented / Blocked  1. Objective     - What the phase was intended to accomplish.  2. Completed tasks     - Exact tasks completed.  3. Modified areas     - Files, projects and modules changed.  4. Requirements     - Exact requirement IDs addressed.  5. Database changes     - Migrations, schema changes and data impact, if any.  6. Verification     - Commands executed.     - Build result.     - Test result.     - Manual/security/accessibility checks performed.  7. Evidence     - Test report, CI run, logs or other reproducible evidence.  8. Outstanding issues     - Defects, unresolved decisions and blocked work.  9. Architecture or scope deviations     - Deviation, reason, impact and approval reference.  10. Next phase      - Whether the next phase prerequisites are satisfied.   `

The agent must not claim a command or test passed unless it actually executed successfully.

9.5 Stop conditions
-------------------

Stop and request clarification when:

*   A required product decision is unresolved.
    
*   A requirement conflicts with the PRD or approved architecture.
    
*   The current repository differs materially from the plan.
    
*   A proposed provider is not approved.
    
*   A security control cannot be implemented safely.
    
*   A migration may destroy or corrupt existing data.
    
*   A release allocation is ambiguous.
    
*   A requirement appears to be missing from the catalog.
    
*   The agent would need to invent personal or professional content.
    

10\. Global Verification and Quality Gates
==========================================

10.1 Build and test gates
-------------------------

Use the actual solution and project paths discovered in P00.

Standard solution-level commands:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`dotnet restore   dotnet build  --no-restore  dotnet test` 

Run targeted project tests when a phase affects a limited module. Run the complete regression suite at the required integration and release gates.

Do not assume test project names or test frameworks that do not exist in the repository.

10.2 Database gates
-------------------

For database-related phases:

*   Review migration contents before applying them.
    
*   Verify migration ordering.
    
*   Verify unique constraints and foreign keys.
    
*   Test transaction boundaries.
    
*   Test concurrency behavior.
    
*   Test rollback or recovery strategy where applicable.
    
*   Use a real SQL Server test environment for relational behavior where practical.
    
*   Do not treat EF Core InMemory tests as proof of SQL Server transaction or constraint behavior.
    
*   Never run destructive database commands against Production as a development verification shortcut.
    

10.3 Security gates
-------------------

Before a release:

*   Verify every Admin route and operation has server-side authorization.
    
*   Verify private media and attachments are protected.
    
*   Verify setup cannot create multiple administrators.
    
*   Verify MFA and recovery behavior.
    
*   Verify anti-forgery and rate limits.
    
*   Verify reCAPTCHA server-side validation.
    
*   Verify file signature and content validation.
    
*   Verify scanner failure is not treated as a clean result.
    
*   Verify rich-text sanitization and output encoding.
    
*   Verify secrets are not present in source control, logs or images.
    
*   Verify security-sensitive actions are audited safely.
    

10.4 Privacy and publishing gates
---------------------------------

*   Drafts must not appear in public pages, search, sitemap or direct public routes.
    
*   Unpublished edits must not replace the live published version.
    
*   Unpublished translations must never be used as public fallback.
    
*   Private content must require authorization.
    
*   Unlisted content must not be indexed or listed publicly.
    
*   Contact attachments must remain private.
    
*   Analytics must follow approved consent, minimization and retention rules.
    
*   Administrator activity must be excluded from visitor analytics.
    

10.5 Accessibility and UI gates
-------------------------------

*   Validate semantic structure and heading hierarchy.
    
*   Verify keyboard-only operation.
    
*   Verify visible and logical focus behavior.
    
*   Verify form labels and associated errors.
    
*   Verify contrast in dark and light themes.
    
*   Verify dialogs and lightbox focus management.
    
*   Verify screen-reader announcements for dynamic updates.
    
*   Verify reduced-motion preferences.
    
*   Verify mobile navigation and touch interactions.
    
*   Verify no unintended horizontal overflow.
    

10.6 Reliability and recovery gates
-----------------------------------

*   Verify bounded retries and idempotency.
    
*   Verify graceful behavior when email, scanner, storage or other noncritical dependencies fail.
    
*   Verify health checks report meaningful states.
    
*   Verify database and media backups are coordinated.
    
*   Verify backup integrity.
    
*   Restore into an isolated environment.
    
*   Validate media references after restoration.
    
*   Record measured RPO and RTO.
    
*   Do not claim recovery objectives are met without a documented restore drill.
    

11\. Progress Tracking and Completion Rules
===========================================

Maintain a phase progress register in the repository or approved project-tracking location.

PhaseNameStatusRequirementsVerification evidenceBlockerP00Baseline ReconciliationNot StartedCross-cutting——P01Development EnvironmentNot StartedNFR-SEC-003, NFR-MAINT-001, NFR-DEP-001——P02Architecture SkeletonNot StartedNFR-MAINT-001, NFR-DEP-001——P03Web Host FoundationNot StartedNFR-SEC-001, NFR-REL-001, NFR-OBS-001——P04Persistence FoundationNot StartedFR-SEC-002, NFR-DATA-001——P05Domain ModelNot StartedDomain-related requirements——P06Application FoundationNot StartedCross-cutting use cases——P07Identity and SecurityNot StartedFR-ADM-001, FR-SEC-001–007——P08Admin ShellNot StartedFR-ADM-005–008——P09PublishingNot StartedFR-ADM-003–004, FR-PUB-002——P10Core Content CMSNot StartedFR-ADM-002, FR-PUB-001——P11Projects and Supporting CMSNot StartedFR-ADM-002, FR-PUB-001——P12Public Core PagesNot StartedFR-PUB-001, 003, 006——P13Public Projects and Supporting PagesNot StartedFR-PUB-001, 002——P14ResumeNot StartedFR-PUB-008, FR-RES-001–003——P15Secure Media FoundationNot StartedFR-MED-001–004, FR-MED-011——P16Media Library WorkflowsNot StartedFR-MED-001–012——P17Contact and InboxNot StartedFR-PUB-007, FR-CON-001–005——P18Gallery FoundationNot StartedFR-GAL-001–006, 008, 017–018——P19Advanced GalleryNot StartedFR-GAL-007–015——P20Localization and SEONot StartedFR-PUB-004, FR-SEO-001–002—Catalog gapP21Search and AnalyticsNot StartedFR-PUB-005, FR-GAL-016, FR-ANA-001–002——P22Operations and RecoveryNot StartedNFR-REL-001, NFR-DR-001, NFR-OBS-001, NFR-DATA-001—Provider decisionsP23Quality and HardeningNot StartedCross-cutting NFRs—Budgets/browser policyP24Production ReleaseNot StartedRelease requirements—Hosting/domain

The progress register is a starting template. Update it with actual task references and evidence as implementation proceeds.

11.1 Phase completion rule
--------------------------

A phase can be marked Verified only when:

*   All in-scope tasks are complete.
    
*   Required build succeeds.
    
*   Required tests pass.
    
*   Acceptance criteria pass.
    
*   Security/privacy implications are verified.
    
*   Documentation and RTM are updated.
    
*   No unresolved blocker prevents safe progression.
    
*   Evidence is recorded.
    

A phase with failing tests remains In Progress or Blocked, not Verified.

12\. Risks, Blockers and Unresolved Decisions
=============================================

The following items must be tracked and resolved at the appropriate stage.

IDItemImpactRequired actionBL-001SCOPE\_AND\_RELEASES\_v2.md remains a review draft.Release assignments may change.Obtain owner approval before treating allocations as final.BL-002TECHNICAL\_SPEC\_v2.md remains a review draft.Some technical defaults are not final.Approve or revise technical choices before provider-specific work.BL-003FR-I18N-001–FR-I18N-003 are referenced by Scope v2 but absent from the Catalog.Invalid requirement traceability.Correct Scope or formally add approved requirements to the Catalog.BL-004Admin interface language requirement lacks a distinct catalog trace.Admin localization acceptance cannot be proven.Add or explicitly map the requirement through the approved change process.BL-005Hosting provider and canonical domain are unresolved.Production architecture and deployment configuration.Select before P24.BL-006Minimum browser versions are unresolved.Compatibility testing scope.Approve the support policy before release sign-off.BL-007Numeric performance budgets are unresolved.Performance acceptance cannot be measured against a target.Establish and approve budgets using representative Staging infrastructure.BL-008Rich-text editor remains open.Admin content editor implementation.Review editor security, maintenance and licensing before selection.BL-009Background-job provider is proposed, not automatically approved.Scheduled jobs, retries and operational visibility.Approve provider before provider-specific integration.BL-010Transactional outbox is proposed.Reliable email and event delivery.Confirm design and implementation scope before integrating.BL-011ClamAV deployment is proposed.Secure upload pipeline and hosting resources.Confirm hosting compatibility and deployment model.BL-012Image-processing provider is unresolved.Media variants and processing operations.Select a supported provider after compatibility and licensing review.BL-013Analytics provider, consent and retention details remain open.Privacy and analytics implementation.Approve privacy model before enabling nonessential tracking.BL-014Backup destination and retention are not final.Recovery objectives and operating cost.Select a separate failure-domain destination and validate recovery.BL-015Production Mailtrap sending requires domain verification.Production contact notifications.Verify the sending domain and configure protected credentials.BL-016Owner content and translations are required.Credibility and publication readiness.Supply and review accurate profile, project, resume, Gallery and translation content.BL-017Legal and privacy policy wording requires review.Production privacy and policy readiness.Review wording for the actual deployment jurisdiction.BL-018Test-case register is not complete.Acceptance evidence cannot be consistently referenced.Create stable test IDs and map them to the 78 catalog requirements.

12.1 Risk handling rules
------------------------

*   Do not convert an assumption into an approved decision without authorization.
    
*   Do not invent performance, recovery or security evidence.
    
*   Do not silently defer a production-critical control.
    
*   Do not mark a release ready while a critical blocker remains unresolved.
    
*   Record the owner, impact, due phase and resolution evidence for each blocker.
    

13\. Change Management
======================

Any change to this plan must preserve requirement traceability and architecture consistency.

For every proposed change:

1.  Identify the affected phase.
    
2.  Identify the affected requirement IDs.
    
3.  Identify the source-document decision or conflict.
    
4.  Explain the reason for the change.
    
5.  Assess architecture, database, security, privacy, accessibility and release impact.
    
6.  Identify new dependencies and tests.
    
7.  Obtain approval where the change affects approved scope or decisions.
    
8.  Update this plan and the RTM.
    
9.  Record the change in the appropriate decision or ADR document.
    

Do not delete a requirement from the plan merely because implementation is difficult.

Do not renumber existing requirement IDs.

Do not mark a proposed release allocation as approved without owner confirmation.

14\. Final Execution Rules
==========================

The following rules are mandatory for every human developer and AI coding agent:

1.  Inspect before modifying.
    
2.  Follow the approved architecture.
    
3.  Execute phases in dependency order.
    
4.  Work within the current phase.
    
5.  Keep changes small and coherent.
    
6.  Preserve existing functionality.
    
7.  Use exact requirement IDs.
    
8.  Test the behavior, not merely the existence of code.
    
9.  Enforce security on the server.
    
10.  Protect private data and files.
    
11.  Never commit secrets.
    
12.  Never fabricate personal or portfolio content.
    
13.  Never treat an unavailable scanner as a clean result.
    
14.  Never claim a backup or restore succeeded without evidence.
    
15.  Never mark a phase complete while required verification fails.
    
16.  Update the RTM and progress register with actual evidence.
    
17.  Stop and ask for approval when a material decision is unresolved.
    

**A successful implementation is not measured by how much code an agent generates. It is measured by whether the approved requirements are correctly implemented, verified and safely released.**

15\. Document Review and Revision History
=========================================

15.1 Revision history
---------------------

VersionDescriptionStatus1.0Initial implementation outline.Historical2.0Five-phase modular implementation plan.Superseded; contained outdated and conflicting implementation assumptions.3.0Dependency-aware, requirement-traceable, verification-driven implementation blueprint with bounded execution phases and AI-agent protocol.Owner review required

15.2 Document status
--------------------

**Version 3.0 is a comprehensive implementation-plan review draft.**

It is designed to become the primary execution blueprint after the owner:

*   Reviews and approves the phase structure.
    
*   Approves the final Scope and Releases baseline.
    
*   Approves or revises the Technical Specification baseline.
    
*   Resolves the requirement traceability gaps.
    
*   Confirms the remaining technical and deployment decisions.
    

The plan does not claim that any phase has been implemented, verified or released.

**End of IMPLEMENTATION\_PLAN.md**
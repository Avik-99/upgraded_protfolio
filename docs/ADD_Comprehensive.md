# Architecture Design Document (ADD)

**Project:** Personal Portfolio & Travel Gallery\
**Platform:** .NET 10 / ASP.NET Core MVC\
**Database:** SQL Server\
**ORM:** Entity Framework Core 10\
**Document status:** Architecture proposal for review\
**Version:** 1.0-draft\
**Related documents:** PRD.md, REQUIREMENTS_CATALOG.md,
TECHNICAL_SPEC_v2.md, AGENTS.md, TESTING_STRATEGY.md

------------------------------------------------------------------------

## 1. Purpose and status of this document

This Architecture Design Document defines the proposed software
architecture for the Personal Portfolio & Travel Gallery application. It
translates the approved product requirements into a technical structure:
layers, responsibilities, dependency rules, persistence boundaries,
application flows, integrations, security controls, and deployment
concerns.

The architecture is intentionally a **modular monolith**. The
application has one deployable ASP.NET Core MVC host, with clearly
separated modules and layers. Microservices are not justified by the
current product scope and would add deployment, networking,
observability, and data-consistency costs without a demonstrated
benefit.

This document follows the requested Clean Architecture / Onion /
Hexagonal principles and explicitly includes CQRS with MediatR,
Repository and Unit of Work abstractions, Mapster, FluentValidation, SQL
Server, EF Core 10, ASP.NET Core Identity, Serilog, and asynchronous
programming.

### 1.1 Decision status

This document is an architecture proposal. The patterns and technologies
explicitly requested by the product owner are treated as required design
constraints for this draft. Choices that still need a separate
operational or implementation decision are marked **Proposed** or **To
confirm**.

  -----------------------------------------------------------------------
  Decision                            Status
  ----------------------------------- -----------------------------------
  .NET 10 and ASP.NET Core MVC        Required by request

  Clean Architecture with strict      Required by request
  dependency direction                

  CQRS and MediatR                    Required by request

  Repository and Unit of Work         Required by request
  abstractions                        

  Mapster                             Required by request

  FluentValidation                    Required by request

  SQL Server and EF Core 10 Code      Required by request
  First                               

  ASP.NET Core Identity               Required by request

  Serilog Console and File sinks      Required by request

  Native .NET DI                      Recommended default

  Autofac                             Optional; use only if a concrete
                                      need justifies it

  One initial application DbContext   Recommended initial design

  Background job provider             To confirm in Technical
                                      Specification

  Image processing and malware        To confirm in Technical
  scanning providers                  Specification

  Cache provider                      To confirm in Technical
                                      Specification

  Production hosting and backup       To confirm
  destination                         
  -----------------------------------------------------------------------

This document does not claim that every package version, hosting
provider, job scheduler, scanner, or image-processing library has
already been selected. Those choices belong in the Technical
Specification and deployment decision records.

------------------------------------------------------------------------

## 2. Architectural goals

The architecture must:

1.  Keep business rules independent of ASP.NET Core, EF Core, SQL
    Server, Identity, Mailtrap, file systems, and other external
    technologies.
2.  Make use cases explicit and independently testable.
3.  Keep MVC controllers thin and focused on HTTP concerns.
4.  Enforce authorization and business invariants on the server, not
    merely in the UI.
5.  Support public and administrator experiences within one application
    while maintaining strict access boundaries.
6.  Support draft, preview, publish, unpublish, language-specific
    content, and published-version isolation.
7.  Support public and private media, image variants, scanning, and
    replace/delete safety.
8.  Preserve consistency between database records and asynchronous
    operations such as email delivery and image processing.
9.  Make data access, transactions, and external integrations
    replaceable behind application-owned abstractions.
10. Support automated testing, observability, container deployment,
    backup, and recovery.
11. Avoid unnecessary complexity: patterns must solve a real requirement
    and must not become ceremony without value.

### 2.1 Non-goals

The initial architecture does not require:

-   Microservices or distributed databases.
-   Event sourcing as the primary persistence model.
-   A public multi-tenant CMS.
-   A general-purpose page-builder framework.
-   A separate API backend solely to serve the MVC website.
-   CQRS read/write databases.
-   Distributed transactions across independent services.

These may be reconsidered only if future requirements justify them.

------------------------------------------------------------------------

## 3. Architectural style and system shape

### 3.1 Clean Architecture

The solution uses four principal layers:

1.  **Domain** --- enterprise business concepts and invariants.
2.  **Application** --- use cases, orchestration, contracts, validation,
    and application policies.
3.  **Infrastructure** --- technical implementations such as EF Core,
    Identity persistence, file storage, email, scanning, and external
    services.
4.  **Presentation** --- ASP.NET Core MVC areas, controllers, views,
    view models, middleware, filters, and HTTP-specific behaviour.

The dependency rule is inward:

-   Domain depends on no outer project.
-   Application depends on Domain.
-   Infrastructure depends on Application and Domain.
-   Presentation depends on Application. The web host references
    Infrastructure only at the composition root to register
    implementations.

Infrastructure implements interfaces defined by the inner layers. The
inner layers do not reference Infrastructure.

### 3.2 Dependency diagram

``` mermaid
flowchart TB
    Browser[Browser]
    Web[Presentation<br/>ASP.NET Core MVC]
    App[Application<br/>Use cases / CQRS / validators]
    Domain[Domain<br/>Entities / value objects / rules]
    Infra[Infrastructure<br/>EF Core / Identity / storage / email]
    SQL[(SQL Server)]
    External[External systems<br/>Mailtrap / reCAPTCHA / scanner]
    Files[(Persistent media storage)]

    Browser --> Web
    Web --> App
    App --> Domain
    Infra --> App
    Infra --> Domain
    Infra --> SQL
    Infra --> External
    Infra --> Files
    Web -. composition root registers .-> Infra
```

The diagram represents compile-time dependencies and runtime calls
separately. The Presentation project can reference Infrastructure for
dependency-registration extensions in the startup composition root, but
controllers and view models must not use Infrastructure classes
directly.

### 3.3 Hexagonal interpretation

Application use cases are the core. Interfaces such as
`IApplicationDbContext`, `IUnitOfWork`, `IStorageProvider`,
`IEmailSender`, `IFileSecurityScanner`, and `IClock` are ports. EF Core,
local disk/object storage, Mailtrap, scanner clients, and system time
are adapters.

------------------------------------------------------------------------

## 4. Solution and project structure

### 4.1 Proposed solution layout

``` text
Portfolio.sln
│
├── src/
│   ├── Portfolio.Domain/
│   │   ├── Common/
│   │   │   ├── Entity.cs
│   │   │   ├── AuditableEntity.cs
│   │   │   ├── IDomainEvent.cs
│   │   │   └── Result.cs
│   │   ├── Content/
│   │   │   ├── Profile/
│   │   │   ├── Experience/
│   │   │   ├── Education/
│   │   │   ├── Skill/
│   │   │   ├── Project/
│   │   │   ├── Achievement/
│   │   │   └── Certification/
│   │   ├── Publishing/
│   │   │   ├── PublicationStatus.cs
│   │   │   └── PublishedRevision.cs
│   │   ├── Localization/
│   │   ├── Media/
│   │   ├── Gallery/
│   │   ├── Contact/
│   │   ├── Resume/
│   │   ├── Analytics/
│   │   └── Security/
│   │
│   ├── Portfolio.Application/
│   │   ├── Abstractions/
│   │   │   ├── Persistence/
│   │   │   ├── Storage/
│   │   │   ├── Email/
│   │   │   ├── Security/
│   │   │   ├── BackgroundJobs/
│   │   │   ├── Caching/
│   │   │   ├── Time/
│   │   │   └── CurrentUser/
│   │   ├── Behaviors/
│   │   │   ├── ValidationBehavior.cs
│   │   │   ├── LoggingBehavior.cs
│   │   │   └── PerformanceBehavior.cs
│   │   ├── Common/
│   │   │   ├── Models/
│   │   │   ├── Exceptions/
│   │   │   └── Constants/
│   │   ├── Features/
│   │   │   ├── Profile/
│   │   │   │   ├── Commands/
│   │   │   │   ├── Queries/
│   │   │   │   ├── DTOs/
│   │   │   │   └── Validators/
│   │   │   ├── Projects/
│   │   │   ├── Gallery/
│   │   │   ├── Media/
│   │   │   ├── Contact/
│   │   │   ├── Resume/
│   │   │   ├── Localization/
│   │   │   ├── Publishing/
│   │   │   ├── Analytics/
│   │   │   ├── AdminSetup/
│   │   │   └── Operations/
│   │   ├── Mapping/
│   │   └── DependencyInjection.cs
│   │
│   ├── Portfolio.Infrastructure/
│   │   ├── Persistence/
│   │   │   ├── PortfolioDbContext.cs
│   │   │   ├── Configurations/
│   │   │   ├── Repositories/
│   │   │   ├── UnitOfWork.cs
│   │   │   ├── Interceptors/
│   │   │   └── Migrations/
│   │   ├── Identity/
│   │   │   ├── ApplicationUser.cs
│   │   │   ├── IdentityServices/
│   │   │   └── Authorization/
│   │   ├── Storage/
│   │   │   ├── LocalStorageProvider.cs
│   │   │   └── StorageOptions.cs
│   │   ├── Email/
│   │   │   └── MailtrapEmailSender.cs
│   │   ├── Recaptcha/
│   │   ├── FileSecurity/
│   │   ├── ImageProcessing/
│   │   ├── BackgroundJobs/
│   │   ├── Caching/
│   │   ├── Analytics/
│   │   ├── Backups/
│   │   ├── Observability/
│   │   └── DependencyInjection.cs
│   │
│   └── Portfolio.Web/
│       ├── Areas/
│       │   └── Admin/
│       │       ├── Controllers/
│       │       ├── ViewModels/
│       │       ├── Views/
│       │       └── Policies/
│       ├── Controllers/
│       ├── ViewModels/
│       ├── Views/
│       ├── ViewComponents/
│       ├── Filters/
│       ├── Middleware/
│       ├── Authorization/
│       ├── Mapping/
│       ├── wwwroot/
│       ├── Extensions/
│       └── Program.cs
│
└── tests/
    ├── Portfolio.Domain.UnitTests/
    ├── Portfolio.Application.UnitTests/
    ├── Portfolio.Infrastructure.IntegrationTests/
    ├── Portfolio.Web.IntegrationTests/
    └── Portfolio.ArchitectureTests/
```

The structure is a starting convention, not a requirement to create
every folder on day one. Add folders when a real feature or class needs
them. Feature folders should keep commands, queries, validators,
handlers, and DTOs close to the use case they serve.

### 4.2 Project reference rules

  ----------------------------------------------------------------------------
  Project                 May reference                Must not reference
  ----------------------- ---------------------------- -----------------------
  Domain                  BCL and carefully selected   Application,
                          domain-only packages         Infrastructure, Web, EF
                                                       Core, Identity, MVC

  Application             Domain, MediatR,             Infrastructure, Web, EF
                          FluentValidation, Mapster    Core provider types,
                          abstractions/configuration   MVC
                          as needed                    

  Infrastructure          Application, Domain, EF      Web controllers/views
                          Core, SQL Server provider,   
                          Identity EF, external SDKs   

  Web                     Application, ASP.NET Core    Direct EF
                          MVC; Infrastructure only for queries/repositories
                          composition root             from controllers
  ----------------------------------------------------------------------------

Enforce these rules with architecture tests and code review.

------------------------------------------------------------------------

## 5. Layer responsibilities and rules

### 5.1 Domain layer

The Domain layer owns business meaning and invariants. It must not know
about HTTP, MVC, SQL Server, EF Core, Identity, file paths, Mailtrap, or
UI view models.

It contains:

-   Entities and aggregate roots.
-   Value objects.
-   Domain enums.
-   Domain events.
-   Domain exceptions or result types for business-rule failures.
-   Invariant enforcement methods.

Examples of domain concepts:

-   `Project`, `ProjectRevision`, `ProjectTranslation`.
-   `MediaAsset`, `MediaReference`.
-   `GalleryAlbum`, `GalleryPhoto`.
-   `ContactConversation`, `ContactMessage`.
-   `ResumeVersion`.
-   `PublicationState`, `MediaVisibility`, `GalleryVisibility`.

Domain methods should express meaningful actions such as `Publish`,
`Unpublish`, `AddPhoto`, `ChangeVisibility`, and `Archive`, rather than
exposing unrestricted setters for every property.

**Aggregate guidance:** Choose aggregate boundaries around consistency
rules, not merely around database tables. For example, a GalleryAlbum
aggregate may control album-level publication and ordering, while media
binary processing belongs to the Media module. Avoid loading an entire
media library merely to update one photo.

Domain events represent facts that have happened inside the domain, such
as `ProjectPublishedDomainEvent`. They are not a replacement for
application commands. Dispatch events only after the database
transaction commits when handlers perform external side effects. For
reliable external work, persist an outbox message in the same
transaction and process it asynchronously.

### 5.2 Application layer

The Application layer implements use cases. It coordinates domain
objects and ports but does not implement SQL, filesystem, SMTP/API
clients, or MVC behaviour.

It contains:

-   MediatR commands, queries, handlers.
-   Request/response DTOs.
-   Application interfaces (ports).
-   FluentValidation validators.
-   MediatR pipeline behaviours.
-   Authorization checks that are use-case-specific.
-   Mapping configuration for application DTOs.
-   Transaction orchestration where a use case requires it.
-   Result types and application exceptions.

Each use case should have a clear responsibility. Do not place business
rules in controllers or EF repositories. The handler coordinates the use
case; the Domain model enforces domain invariants.

Application code should be asynchronous for I/O. Use `CancellationToken`
and pass it through MediatR, repository, EF Core, and external service
calls. Do not wrap synchronous code in `Task.Run` to pretend it is
asynchronous.

### 5.3 Infrastructure layer

Infrastructure implements application-owned interfaces and contains:

-   EF Core DbContext, entity configurations, migrations.
-   Repository implementations and Unit of Work implementation.
-   ASP.NET Core Identity persistence and adapters.
-   Local or object storage adapters.
-   Mailtrap email adapter.
-   reCAPTCHA verification adapter.
-   File scanner and image/PDF processing adapters.
-   Cache implementation.
-   Background job provider integration.
-   Backup/restore adapters.
-   Infrastructure-specific logging and health checks.

Infrastructure must not decide product policy. For example, it may store
an asset and report its scan result; the Application/Domain workflow
decides whether that asset may be published.

### 5.4 Presentation layer

Presentation is the ASP.NET Core MVC host. It contains:

-   Public MVC controllers and views.
-   Protected Admin Area controllers and views.
-   HTTP-specific ViewModels.
-   Model binding and HTTP validation response handling.
-   Authentication/authorization configuration.
-   Anti-forgery, filters, middleware, routing.
-   Static public assets.
-   Error pages and ProblemDetails handling for AJAX/API-style requests.

Controllers should: 1. Bind and validate HTTP input shape. 2. Map the
input ViewModel to an Application request. 3. Send it through
`ISender`/MediatR. 4. Translate the result into a view, redirect, or
appropriate HTTP response.

Controllers must not inject `PortfolioDbContext`, `DbSet`, repository
implementations, `UserManager` for general business use cases, or
storage implementation classes. Identity-specific sign-in endpoints may
use a dedicated Application identity abstraction rather than leaking
Identity types into the controller.

------------------------------------------------------------------------

## 6. CQRS and MediatR

### 6.1 CQRS approach

Use CQRS at the application request level:

-   **Commands** express intent to change state.
-   **Queries** retrieve data and do not change state.

For this application, CQRS does not require separate databases or event
sourcing. Both command and query handlers may use the same SQL Server
database and DbContext.

Examples:

  Command                         Query
  ------------------------------- -----------------------------
  `CreateProjectCommand`          `GetProjectForEditQuery`
  `PublishProjectCommand`         `GetPublishedProjectsQuery`
  `UploadMediaCommand`            `SearchMediaLibraryQuery`
  `CreateGalleryAlbumCommand`     `GetPublicGalleryQuery`
  `SubmitContactMessageCommand`   `GetContactInboxQuery`
  `SetDefaultResumeCommand`       `GetPublicResumeQuery`

### 6.2 MediatR responsibilities

MediatR dispatches requests to handlers and supports pipeline
behaviours. It does not replace domain modelling, validation,
authorization, persistence, or transaction design.

Use `ISender` in controllers and handlers. Avoid making every service
call a MediatR request if a simple internal method is clearer. Avoid
handlers that merely forward to another handler without adding use-case
value.

### 6.3 Pipeline order

A recommended pipeline is:

1.  Request logging / correlation enrichment.
2.  Validation.
3.  Use-case authorization (where implemented as a behaviour).
4.  Transaction behaviour for commands that require a transaction.
5.  Handler.
6.  Commit and outbox persistence.
7.  Post-commit dispatch/queue processing.

The exact order must be implemented deliberately. Validation must happen
before database changes. Do not start a transaction for read-only
queries. Avoid a generic transaction behaviour if it obscures which use
cases need explicit transaction boundaries; document transaction policy
for each command category.

### 6.4 FluentValidation

Register validators from the Application assembly. A MediatR validation
behaviour should run all validators for the request and return a
structured validation failure or throw a defined validation exception
that the Presentation layer translates consistently.

Validation has two levels:

-   **Input validation:** required fields, lengths, formats, ranges,
    collection sizes.
-   **Domain validation:** rules that must always hold regardless of
    caller, such as publication prerequisites or album invariants.

Never rely on browser-side validation alone.

------------------------------------------------------------------------

## 7. Repository and Unit of Work patterns

### 7.1 Repository policy

Repository interfaces belong in Application (or Domain only when they
are genuinely domain abstractions); implementations belong in
Infrastructure.

Use repositories to express meaningful aggregate persistence operations.
Prefer focused interfaces such as `IProjectRepository`,
`IGalleryRepository`, and `IMediaAssetRepository` over one huge generic
repository that exposes every EF operation.

A repository should not: - Return `IQueryable` to the Web layer. -
Expose `DbContext` or `DbSet`. - Contain business rules. - Save after
every individual method automatically. - Hide query performance
characteristics behind opaque magic.

For read-heavy pages, a query-specific read service may use EF Core
projections directly inside Infrastructure and return Application DTOs.
This is still behind an Application-owned interface and avoids forcing
complex reporting/search queries through aggregate repositories.

### 7.2 Unit of Work policy

EF Core `DbContext` already provides change tracking and unit-of-work
behaviour. The requested `IUnitOfWork` abstraction should therefore be a
thin application-facing boundary, not a second transaction engine or a
duplicate change tracker.

A practical contract:

``` csharp
public interface IUnitOfWork
{
    Task<int> SaveChangesAsync(CancellationToken cancellationToken = default);
    Task ExecuteInTransactionAsync(
        Func<CancellationToken, Task> operation,
        CancellationToken cancellationToken = default);
}
```

In many handlers, a transaction wrapper is unnecessary because one
`SaveChangesAsync` call is atomic for the changes in that DbContext. Use
an explicit database transaction when a use case requires multiple saves
or coordinated database operations. Do not open nested transactions
casually.

If the `ExecuteInTransactionAsync` delegate is used, ensure retries and
transaction execution strategy are compatible. Do not retry a
non-idempotent operation blindly.

### 7.3 Repository and Unit of Work example contracts

``` csharp
public interface IProjectRepository
{
    Task<Project?> GetByIdAsync(Guid id, CancellationToken cancellationToken);
    Task AddAsync(Project project, CancellationToken cancellationToken);
    void Remove(Project project);
}

public interface IProjectReadService
{
    Task<ProjectDetailsDto?> GetDetailsAsync(
        Guid id,
        string languageCode,
        CancellationToken cancellationToken);
}
```

The read service is separate because public listing/detail projections
may need optimized joins and projection that do not map naturally to
aggregate loading.

------------------------------------------------------------------------

## 8. Mapster mapping strategy

Mapster is used for mapping between application DTOs and appropriate
models, but mapping must not bypass domain invariants.

Recommended rules:

1.  Map incoming MVC ViewModels to command objects in Presentation.
2.  Map domain entities to response DTOs in Application.
3.  Use explicit mapping configuration for non-trivial mappings.
4.  Use EF Core projection (`ProjectToType`) for supported query
    projections where it generates efficient SQL.
5.  Do not map untrusted input directly onto tracked entities with
    unrestricted property copying.
6.  Do not map a DTO onto an aggregate to perform an update; load the
    aggregate and call its domain methods.
7.  Keep Web ViewModels out of Domain and Infrastructure.
8.  Avoid circular references and over-fetching in DTOs.

Example mapping configuration:

``` csharp
public sealed class ProjectMappingConfig : IRegister
{
    public void Register(TypeAdapterConfig config)
    {
        config.NewConfig<Project, ProjectSummaryDto>()
            .Map(dest => dest.Id, src => src.Id)
            .Map(dest => dest.Title, src => src.Title)
            .Map(dest => dest.Slug, src => src.Slug)
            .Map(dest => dest.Status, src => src.PublicationStatus.ToString());
    }
}
```

The exact Mapster registration and source-generator approach should be
selected in the Technical Specification. Mapping configuration should be
validated in tests.

------------------------------------------------------------------------

## 9. Database and EF Core architecture

### 9.1 Database approach

Use SQL Server with EF Core 10 Code First. Entity configurations use
`IEntityTypeConfiguration<T>` and are applied from the Infrastructure
assembly. Migrations are committed to source control and reviewed before
deployment.

### 9.2 DbContext boundary

**Recommended initial boundary: one `PortfolioDbContext` for the
portfolio application data and Identity tables in the same SQL Server
database.**

This is the simplest way to preserve transactions across related
operations such as admin setup, content metadata, media references,
contact records, and outbox records.

The DbContext may derive from
`IdentityDbContext<ApplicationUser, ApplicationRole, Guid>` so Identity
and application tables share one EF Core unit of work. Domain entities
must not inherit from Identity classes and must not reference Identity
types.

Logical modules remain separated through entity configurations,
repositories, feature folders, and table naming. A separate DbContext
should be introduced only when a genuine isolation requirement exists
(different database, independent lifecycle, separate scaling/security
boundary, or incompatible ownership). Splitting contexts merely to make
folders look modular can make transactions and migrations harder.

### 9.3 Context rules

-   Only Infrastructure may reference the concrete DbContext.
-   Application may reference a narrow persistence abstraction if a use
    case needs it; prefer repositories/read services for most use cases.
-   Controllers and Views never access EF Core.
-   Do not expose tracked entities outside the Application boundary.
-   Keep one scoped DbContext per web request / DI scope.
-   Do not use one DbContext concurrently across parallel tasks.
-   Use `AsNoTracking` for read-only entity queries when appropriate.
-   Project directly to DTOs for list/detail reads to avoid loading
    unnecessary graphs.
-   Avoid lazy loading as a default because it can hide N+1 queries.
-   Use explicit loading or projection where required.
-   Use optimistic concurrency (for example, a row-version/concurrency
    token) for important admin-editable records.
-   Apply unique constraints for slugs, language-specific identifiers,
    and other business uniqueness rules.
-   Use database constraints as a final integrity boundary, not only
    application validation.

### 9.4 Proposed logical data areas

The following are logical areas, not a final physical schema. Exact
entities, columns, relationships, indexes, and delete behaviours belong
in the Technical Specification and data model review.

  -----------------------------------------------------------------------
  Module                              Example data
  ----------------------------------- -----------------------------------
  Identity                            Users, roles, claims, logins,
                                      tokens, MFA-related Identity data

  Profile                             Profile content and localized
                                      versions

  Career/Education                    Experience, education, skills

  Projects                            Projects, revisions, technologies,
                                      links, localized content

  Achievements                        Achievements and localized content

  Certifications                      Certification records and media
                                      references

  Publishing                          Draft/published revisions,
                                      publication metadata

  Localization                        Supported languages and translation
                                      records

  Media                               Asset metadata, variants, hashes,
                                      scan/processing state

  Gallery                             Albums, photos, photo metadata,
                                      ordering, visibility

  Contact                             Conversations, messages,
                                      attachments, delivery attempts

  Resume                              Resume documents, versions,
                                      language, default selection

  Analytics                           Aggregated events/statistics,
                                      consent/preferences

  Operations                          Audit events, backup manifests,
                                      job/outbox records, operational
                                      history
  -----------------------------------------------------------------------

### 9.5 Indexing and query performance

Add indexes based on actual query patterns, including:

-   Unique slug indexes with language scope where appropriate.
-   Publication status + publish date for public listings.
-   Foreign keys used in joins and filters.
-   Album/photo ordering and visibility.
-   Media hash for duplicate detection.
-   Contact inbox status + received date.
-   Outbox status + next-attempt time.
-   Audit timestamp and category where needed.

Do not create indexes speculatively on every column. Review generated
SQL and execution plans for expensive queries. Use pagination for admin
lists and public collections. Use bounded page sizes and avoid unbounded
exports.

### 9.6 Migrations

-   Development: automatic migration may be allowed for local
    convenience, but it must be configurable.
-   Staging/production: migrations are controlled deployment steps, not
    an uncontrolled startup side effect.
-   Back up before production schema changes.
-   Review generated migration scripts.
-   Test upgrade from the currently deployed schema and
    rollback/recovery procedure.
-   Do not run multiple application instances that race to apply
    migrations.
-   Use a deployment identity with only the required database
    permissions.

------------------------------------------------------------------------

## 10. Transaction management and consistency

### 10.1 General rule

A transaction should cover one consistent database use case. Keep
external network calls and long-running file operations outside database
transactions.

### 10.2 Transaction examples

  -----------------------------------------------------------------------
  Use case                            Transaction policy
  ----------------------------------- -----------------------------------
  Update one profile record           One SaveChanges transaction is
                                      usually sufficient

  Create project plus translations    One database transaction
  and relationships                   

  Publish a revision and update       One database transaction
  publication pointers                

  Contact submission plus attachment  One database transaction after
  metadata and outbox notifications   files are safely staged/scanned

  Upload a large file                 Do not hold a SQL transaction while
                                      streaming; stage file,
                                      scan/process, then persist
                                      metadata/status

  Send email                          Never send inside an open database
                                      transaction; enqueue outbox item
                                      and send after commit

  Backup/restore                      Dedicated operational workflow with
                                      checkpoints and safety backup; not
                                      an ordinary request transaction
  -----------------------------------------------------------------------

### 10.3 External side effects and the outbox pattern

A database transaction cannot atomically commit SQL Server changes and
guarantee delivery through Mailtrap or a background-job provider. Use an
Outbox pattern for reliable work:

1.  Save the business record and an outbox message in the same SQL
    transaction.
2.  Commit.
3.  A background worker claims pending outbox messages.
4.  It performs the external action.
5.  It marks success or schedules bounded retry.
6.  Failed messages become visible in operations monitoring.

Use idempotency keys or stable message identifiers to prevent duplicate
processing. The outbox is especially important for contact email
notifications, publishing notifications, and post-commit processing
events.

### 10.4 Concurrency

-   Use optimistic concurrency tokens for simultaneous admin edits.
-   Use database uniqueness constraints for one-time admin setup and
    unique slugs.
-   Make setup creation atomic: the server must verify no administrator
    exists and create the first administrator under a
    transaction/constraint strategy that prevents races.
-   Use idempotent job handlers.
-   Use row-level claiming or a provider-supported distributed lock for
    background work; do not rely on an in-process boolean when multiple
    app instances may run.
-   Detect duplicate form submissions using an idempotency token or
    persisted request key where the user experience requires it.

------------------------------------------------------------------------

## 11. Identity, authentication and authorization

### 11.1 Identity implementation

Use ASP.NET Core Identity with a custom `ApplicationUser` and
`ApplicationRole`, using `Guid` keys unless the final technical
specification establishes another reason.

Identity persistence and managers belong in Infrastructure. Application
use cases should expose purpose-specific abstractions such as
`IAdminAccountService`, `IAuthenticationService`, or
`IAccountRecoveryService`; avoid leaking `UserManager`, `SignInManager`,
or Identity EF entities into Domain.

Possible user extensions should be limited to fields with a real product
need (for example, display name and account status). Do not duplicate
fields already managed by Identity without a reason.

### 11.2 Authorization model

-   One administrator is supported by the initial product.
-   Admin MVC Area is protected by a server-side Admin policy/role.
-   Sensitive operations may require recent authentication and MFA
    confirmation.
-   Public routes must never expose admin drafts, private media, private
    contact attachments, or operational endpoints.
-   UI hiding is not authorization.
-   Every command that changes protected data must enforce authorization
    at the use-case or endpoint boundary.
-   Prevent normal user-management workflows from granting another Admin
    role.
-   The one-time setup route is available only while no administrator
    exists and becomes permanently unavailable after successful setup.
-   Use resource-based authorization for private assets and sensitive
    operations when a simple role check is insufficient.

### 11.3 Authentication security

Configure secure cookies, HTTPS, appropriate SameSite policy,
anti-forgery validation for state-changing MVC forms, lockout/rate
limiting, password-reset tokens, security-stamp validation, MFA
enrollment and recovery codes. Do not log passwords, MFA codes, recovery
codes, reset tokens, or session cookies.

The PRD's one-time setup, MFA, recovery, and single-admin requirements
remain authoritative. Exact Identity options and session lifetime belong
in the Technical Specification.

------------------------------------------------------------------------

## 12. Public and Admin presentation architecture

### 12.1 One host, separate MVC areas

The public Viewer Panel and Admin Panel are logical areas in one MVC
application:

-   Public controllers render only published and public content.
-   Admin controllers are placed under `Areas/Admin`.
-   Admin endpoints use explicit authorization policies.
-   Admin and public layouts, navigation, view models, and error
    handling are separated.
-   Shared components may be reused only where their behaviour and
    security context are genuinely shared.

### 12.2 ViewModel rules

-   MVC ViewModels belong in the Web project.
-   Application DTOs belong in Application.
-   Do not pass EF entities directly to Razor views.
-   Do not bind database entities directly from HTTP requests.
-   Use dedicated input models for create/update forms to prevent
    over-posting.
-   Map ViewModels to commands with Mapster or explicit mapping.
-   Map response DTOs to display ViewModels where the view needs
    presentation-specific formatting.

### 12.3 Controller example

``` csharp
[Area("Admin")]
[Authorize(Policy = "AdminOnly")]
public sealed class ProjectsController(ISender sender) : Controller
{
    [HttpPost]
    [ValidateAntiForgeryToken]
    public async Task<IActionResult> Create(
        CreateProjectViewModel model,
        CancellationToken cancellationToken)
    {
        if (!ModelState.IsValid)
            return View(model);

        var command = model.Adapt<CreateProjectCommand>();
        var result = await sender.Send(command, cancellationToken);

        if (result.IsFailure)
        {
            ModelState.AddModelError(string.Empty, result.Error);
            return View(model);
        }

        return RedirectToAction(nameof(Index));
    }
}
```

The example assumes an application result type and a Mapster
configuration. The exact result type should be standardized in the
Application project.

------------------------------------------------------------------------

## 13. End-to-end CQRS examples

The following examples are illustrative and show the intended dependency
flow. Names and DTO properties must be reconciled with the final Domain
model and Technical Specification before implementation.

### 13.1 Create Project command

**Flow:** MVC ViewModel → Mapster → MediatR command → FluentValidation
pipeline → handler → repository → Unit of Work → SQL Server.

Command:

``` csharp
public sealed record CreateProjectCommand(
    string Title,
    string Slug,
    string Summary,
    string LanguageCode) : IRequest<Result<Guid>>;
```

Validator:

``` csharp
public sealed class CreateProjectCommandValidator
    : AbstractValidator<CreateProjectCommand>
{
    public CreateProjectCommandValidator()
    {
        RuleFor(x => x.Title)
            .NotEmpty()
            .MaximumLength(160);

        RuleFor(x => x.Slug)
            .NotEmpty()
            .MaximumLength(180)
            .Matches("^[a-z0-9]+(?:-[a-z0-9]+)*$");

        RuleFor(x => x.Summary)
            .NotEmpty()
            .MaximumLength(600);

        RuleFor(x => x.LanguageCode)
            .NotEmpty()
            .Length(2, 10);
    }
}
```

Handler:

``` csharp
public sealed class CreateProjectCommandHandler(
    IProjectRepository projects,
    IUnitOfWork unitOfWork,
    ICurrentUser currentUser,
    IClock clock)
    : IRequestHandler<CreateProjectCommand, Result<Guid>>
{
    public async Task<Result<Guid>> Handle(
        CreateProjectCommand request,
        CancellationToken cancellationToken)
    {
        var slugExists = await projects.SlugExistsAsync(
            request.Slug,
            request.LanguageCode,
            cancellationToken);

        if (slugExists)
            return Result<Guid>.Failure("A project with this slug already exists.");

        var project = Project.CreateDraft(
            request.Title,
            request.Slug,
            request.Summary,
            request.LanguageCode,
            currentUser.UserId,
            clock.UtcNow);

        await projects.AddAsync(project, cancellationToken);
        await unitOfWork.SaveChangesAsync(cancellationToken);

        return Result<Guid>.Success(project.Id);
    }
}
```

Repository contract:

``` csharp
public interface IProjectRepository
{
    Task<bool> SlugExistsAsync(
        string slug,
        string languageCode,
        CancellationToken cancellationToken);

    Task AddAsync(Project project, CancellationToken cancellationToken);
}
```

Infrastructure implementation:

``` csharp
internal sealed class ProjectRepository(PortfolioDbContext db)
    : IProjectRepository
{
    public Task<bool> SlugExistsAsync(
        string slug,
        string languageCode,
        CancellationToken cancellationToken)
    {
        return db.Projects.AnyAsync(
            x => x.Slug == slug && x.LanguageCode == languageCode,
            cancellationToken);
    }

    public async Task AddAsync(
        Project project,
        CancellationToken cancellationToken)
    {
        await db.Projects.AddAsync(project, cancellationToken);
    }
}
```

The database must also enforce the corresponding unique constraint. The
pre-check improves the user experience but cannot prevent races by
itself. Handle a unique-constraint violation and return a safe conflict
result.

### 13.2 Query published projects

**Flow:** MVC controller → MediatR query → query handler → read
service/repository projection → DTO → Mapster/ViewModel → Razor view.

Query:

``` csharp
public sealed record GetPublishedProjectsQuery(
    string LanguageCode,
    int Page,
    int PageSize) : IRequest<PagedResult<ProjectCardDto>>;
```

DTO:

``` csharp
public sealed record ProjectCardDto(
    Guid Id,
    string Title,
    string Slug,
    string Summary,
    string? CoverImageUrl,
    DateTimeOffset PublishedAt);
```

Handler:

``` csharp
public sealed class GetPublishedProjectsQueryHandler(
    IProjectReadService readService)
    : IRequestHandler<GetPublishedProjectsQuery, PagedResult<ProjectCardDto>>
{
    public Task<PagedResult<ProjectCardDto>> Handle(
        GetPublishedProjectsQuery request,
        CancellationToken cancellationToken)
    {
        return readService.GetPublishedPageAsync(
            request.LanguageCode,
            request.Page,
            request.PageSize,
            cancellationToken);
    }
}
```

Infrastructure read service should filter to published, publicly visible
content and project only the required columns. It should apply the
approved language fallback rules and deterministic ordering. The query
must never return drafts or private content.

### 13.3 Mapster query projection

A read service may use Mapster's EF projection support when the
configured mapping is translatable:

``` csharp
public async Task<IReadOnlyList<ProjectCardDto>> GetCardsAsync(
    string languageCode,
    CancellationToken cancellationToken)
{
    return await db.Projects
        .AsNoTracking()
        .Where(x => x.PublicationStatus == PublicationStatus.Published
                    && x.LanguageCode == languageCode)
        .OrderByDescending(x => x.PublishedAt)
        .ProjectToType<ProjectCardDto>(config)
        .ToListAsync(cancellationToken);
}
```

Confirm the actual projection is translated to SQL and does not trigger
client-side evaluation or load full entity graphs. Language fallback may
require a more explicit query than this simplified example.

### 13.4 FluentValidation pipeline behaviour

``` csharp
public sealed class ValidationBehavior<TRequest, TResponse>(
    IEnumerable<IValidator<TRequest>> validators)
    : IPipelineBehavior<TRequest, TResponse>
    where TRequest : notnull
{
    public async Task<TResponse> Handle(
        TRequest request,
        RequestHandlerDelegate<TResponse> next,
        CancellationToken cancellationToken)
    {
        var context = new ValidationContext<TRequest>(request);

        var results = await Task.WhenAll(
            validators.Select(v => v.ValidateAsync(context, cancellationToken)));

        var failures = results
            .SelectMany(x => x.Errors)
            .Where(x => x is not null)
            .ToArray();

        if (failures.Length > 0)
            throw new ValidationException(failures);

        return await next();
    }
}
```

This is a conceptual example. Check the installed MediatR version's
exact delegate signature when implementing.

------------------------------------------------------------------------

## 14. Media Library and storage architecture

### 14.1 Separation of responsibilities

-   Media domain/application modules own asset metadata, lifecycle,
    references, visibility, and processing state.
-   Storage adapters own physical file operations.
-   Scanner adapters determine whether a file is safe.
-   Image/PDF processors create derivatives or previews.
-   Gallery owns album/photo organization and presentation metadata; it
    references approved media assets.

### 14.2 Storage abstraction

Application-owned interface:

``` csharp
public interface IStorageProvider
{
    Task<StoredObject> SaveAsync(
        Stream content,
        string safeFileName,
        string contentType,
        CancellationToken cancellationToken);

    Task<Stream?> OpenReadAsync(
        string storageKey,
        CancellationToken cancellationToken);

    Task DeleteAsync(
        string storageKey,
        CancellationToken cancellationToken);

    Task<bool> ExistsAsync(
        string storageKey,
        CancellationToken cancellationToken);
}
```

Persist opaque storage keys, not absolute paths. The local provider maps
keys to a configured root directory and must prevent path traversal. A
future object-storage provider can implement the same contract.

### 14.3 Public and private media

-   Public assets may be served from a controlled public media location
    after successful scanning and publication.
-   Private assets must be stored outside `wwwroot` and served through
    an authorized endpoint.
-   Never expose private filesystem paths or storage keys as public
    URLs.
-   Public/private visibility is enforced by server-side authorization
    and publication rules.
-   A media record is not publishable while scanning or processing is
    pending or failed under the approved policy.

### 14.4 Upload lifecycle

Recommended lifecycle:

``` mermaid
flowchart TD
    A[Receive upload] --> B[Validate size, extension, signature]
    B -->|Invalid| X[Reject and record safe error]
    B -->|Valid| C[Stage in quarantine]
    C --> D[Malware/security scan]
    D -->|Infected or error| Q[Keep quarantined / reject]
    D -->|Clean| E[Create media metadata]
    E --> F[Process image or PDF derivatives]
    F --> G[Mark available]
    G --> H[Allow authorized reference/publication]
```

Never trust client-provided MIME type, filename, or extension. Enforce
allowlists, actual file signatures, size limits, safe generated storage
names, image dimensions, PDF handling rules, scanner timeouts, and
quarantine. Scanner unavailable or timeout must not be interpreted as
clean.

### 14.5 File replacement and deletion

-   Preserve originals as immutable source files.
-   Replacements create a new asset or controlled new version; do not
    overwrite an original silently.
-   Track all content references to an asset.
-   Block deletion while referenced; show the administrator where it is
    used.
-   A recycle bin/retention process must re-check references before
    permanent deletion.
-   Update public caches when visibility or asset references change.

------------------------------------------------------------------------

## 15. Gallery architecture

Gallery is a content module, not a physical folder in the Media Library.

-   `GalleryAlbum` owns album title, description, destination, dates,
    category, cover, ordering, visibility, and publication.
-   `GalleryPhoto` owns album relationship, order, optional
    caption/story/location/date/tags, and publication state.
-   `MediaAsset` owns binary file metadata, storage, scan state, and
    generated variants.
-   A GalleryPhoto references an approved MediaAsset.

Visibility semantics:

-   **Public:** eligible for public listing and indexing only when
    published.
-   **Unlisted:** direct-link access where allowed, excluded from public
    discovery and sitemap.
-   **Private:** administrator-only.
-   **Unpublished:** inaccessible publicly regardless of parent album
    status.

A public album must not accidentally reveal an unpublished or private
photo. Every public query must apply album and photo
visibility/publication rules.

------------------------------------------------------------------------

## 16. Contact, email, and background processing

### 16.1 Contact submission

1.  Validate anti-forgery, input, reCAPTCHA, and rate limits.
2.  Validate attachments and stage them securely.
3.  Scan attachments; private files remain protected.
4.  Persist the contact message, attachment references, and notification
    outbox records in one database transaction.
5.  Commit.
6.  Process visitor confirmation and administrator notification
    independently.
7.  Record delivery status and retry transient failures with bounded
    backoff.
8.  Preserve the submitted message if email is unavailable.

### 16.2 Email abstraction

Application owns an `IEmailSender` or purpose-specific notification
interface. Infrastructure implements the Mailtrap adapter. Development
uses the configured Mailtrap sandbox; production uses the configured
sending service after domain verification. Secrets are supplied through
environment-specific secret configuration, never committed.

### 16.3 Background jobs

Use a background-job abstraction for work that must survive beyond the
HTTP request:

-   Image/PDF processing.
-   Email/outbox delivery retries.
-   Scheduled publication if included.
-   Analytics aggregation.
-   Retention and recycle-bin cleanup.
-   Backup orchestration and verification.

Jobs must be durable, idempotent, bounded in retry, observable, and safe
under multiple application instances. Do not use untracked `Task.Run`,
`async void`, or fire-and-forget work inside controllers.

The actual scheduler/provider is a Technical Specification decision.

------------------------------------------------------------------------

## 17. Caching architecture

Cache only data that is safe for the relevant audience.

-   Public published content may be cached.
-   Admin drafts, private content, private media, and contact records
    must not enter shared public caches.
-   Cache keys include content identity, language, and relevant
    variation.
-   Publish, unpublish, edit, delete, translation update, and visibility
    changes invalidate affected detail, listing, search, sitemap, and
    metadata entries.
-   Admin preview bypasses public caches.
-   Cache failure should degrade to database reads where safe.
-   Do not cache authorization decisions longer than the security model
    allows.

Start with the simplest cache that meets measured needs. A distributed
cache is not required until multi-instance hosting or measured
performance needs justify it.

------------------------------------------------------------------------

## 18. Cross-cutting concerns

### 18.1 Dependency injection

Use modular registration extensions:

``` csharp
// Program.cs - composition root
builder.Services
    .AddApplication()
    .AddInfrastructure(builder.Configuration)
    .AddWebServices();

builder.Host.UseSerilog();
```

Each project owns its registration extension. Application registers
handlers, validators, and pipeline behaviours. Infrastructure registers
DbContext and external adapters. Web registers MVC, filters, middleware,
authentication, and authorization.

**Recommendation:** use native .NET DI initially. It supports
constructor injection, scopes, open generics, and the application's
likely needs. Use Autofac only if a concrete requirement appears (for
example, advanced module scanning or specialised lifetime/interception
features). Do not register the same service twice with conflicting
lifetimes.

### 18.2 Structured logging with Serilog

Use Serilog with Console and rolling File sinks. Enrich logs with
application name, environment, correlation/trace ID, and relevant safe
identifiers.

Log: - Application startup/shutdown. - Request and dependency
failures. - Background job lifecycle and retries. - Security-relevant
events without secrets. - Backup and restore operations. - Important
administrative actions.

Never log passwords, MFA codes, recovery codes, reset tokens, cookies,
reCAPTCHA secrets, private file contents, or full private
contact-message bodies. Apply retention and access controls to log
files. Logs are operational evidence, not a substitute for a dedicated
immutable audit trail.

### 18.3 Exception handling

Use ASP.NET Core exception-handling middleware and a central
exception-to-response mapping.

-   Unexpected exceptions: log with correlation ID; return a generic
    error.
-   Validation errors: return field-level validation information.
-   Not found: return 404.
-   Unauthorized/forbidden: return 401/403 or appropriate MVC redirect
    behaviour.
-   Concurrency conflicts: return a safe conflict message and preserve
    user input where possible.
-   Browser requests: render friendly error pages.
-   AJAX/API-style requests: return standard ProblemDetails.
-   Never expose stack traces, SQL, filesystem paths, secrets, or
    internal exception messages in production.

The middleware must not swallow cancellation exceptions as ordinary
server faults. Use environment-specific developer exception pages only
in Development.

### 18.4 Async programming

Use `async`/`await` for I/O in controllers, handlers, repositories,
storage, email, and external service adapters. Pass `CancellationToken`
through the call chain. Avoid `.Result`, `.Wait()`, sync-over-async, and
`async void` except framework-required event handlers. CPU-heavy image
work belongs in a controlled background worker with resource limits.

### 18.5 Time and identifiers

-   Store timestamps in UTC (`DateTimeOffset` recommended).
-   Convert to display timezone in Presentation.
-   Use an injectable `IClock` for testable time-dependent rules.
-   Use opaque identifiers in public URLs where appropriate; slugs
    remain user-friendly and must not expose private sequential data.
-   Normalize language codes consistently.

------------------------------------------------------------------------

## 19. Security architecture

Security is applied in depth:

1.  HTTPS and secure cookie configuration.
2.  ASP.NET Core Identity password hashing, lockout, MFA, reset-token
    protections.
3.  Role/policy/resource authorization on every protected request.
4.  Anti-forgery protection for state-changing MVC requests.
5.  Input validation and output encoding.
6.  Parameterized EF Core queries; no unsafe SQL concatenation.
7.  Upload allowlists, file-signature validation, quarantine and
    scanning.
8.  Private media outside public static directories.
9.  Rate limiting on login, setup, password reset, contact and other
    abuse-prone endpoints.
10. Secure secret management by environment.
11. Security headers and an appropriately tested Content Security
    Policy.
12. Dependency and container image scanning in CI.
13. Audit logging for sensitive administrator actions.
14. Least-privilege database, filesystem and deployment identities.

reCAPTCHA is an additional abuse signal; it does not replace
authentication, authorization, MFA, anti-forgery, or rate limiting.
Validate server-side token success, expected action, hostname where
applicable, and configured score policy.

------------------------------------------------------------------------

## 20. Observability, health, and operations

Provide:

-   Structured application logs.
-   Correlation IDs and distributed trace context where available.
-   Liveness and readiness health checks.
-   SQL Server connectivity checks.
-   Storage read/write availability checks that do not expose secrets.
-   Mail delivery and outbox backlog monitoring.
-   Scanner availability and quarantine backlog monitoring.
-   Background job failure/retry visibility.
-   Backup destination, checksum, and restore-readiness status.
-   Operational audit history.

Health endpoints must not expose internal configuration, secrets,
connection strings, or sensitive infrastructure details publicly.
Separate public liveness from restricted detailed readiness/operations
views.

------------------------------------------------------------------------

## 21. Backup, restore, and disaster recovery architecture

The PRD defines RPO and RTO targets of four hours. Architecture must
support those targets; a daily-only backup schedule would not satisfy a
four-hour RPO unless another recovery mechanism is in place.

-   Back up SQL data and media originals/variants with a consistent
    manifest.
-   Keep at least one backup copy in a separate failure domain.
-   Verify backup integrity and checksums.
-   Track backup job status, duration, size, and failures.
-   Document restore order and dependency relationships.
-   Restore requires privileged authorization, recent
    authentication/MFA, explicit target selection, pre-restore safety
    backup, audit, and post-restore integrity validation.
-   Test restore regularly; a successful backup job alone does not prove
    recoverability.
-   Keep backup encryption keys separately protected and document
    recovery procedures.

Exact SQL backup strategy, media synchronization strategy, retention,
encryption key management, and external destination are
deployment/operations decisions for the Technical Specification.

------------------------------------------------------------------------

## 22. Deployment architecture

### 22.1 Initial topology

``` mermaid
flowchart TB
    User[Visitor / Administrator]
    Proxy[HTTPS reverse proxy]
    App[Portfolio.Web<br/>ASP.NET Core MVC container]
    DB[(SQL Server)]
    Media[(Persistent media volume)]
    Backup[(Separate backup destination)]
    Mail[Mailtrap]
    Scanner[File scanner]
    Jobs[Background worker / job host]

    User --> Proxy --> App
    App --> DB
    App --> Media
    App --> Mail
    App --> Scanner
    App --> Jobs
    DB --> Backup
    Media --> Backup
```

The application and background worker may initially run in the same
deployment unit if the job provider and hosting model support it safely.
The diagram shows logical responsibilities, not a mandatory separate
microservice.

### 22.2 Environments

-   Development: local SQL Server/compatible SQL Server instance,
    sandbox email, local persistent media, verbose diagnostics.
-   Staging: production-like configuration with non-production data and
    verified deployment/migration procedure.
-   Production: HTTPS, managed secrets, restricted database access,
    persistent media, external backups, monitoring, controlled
    migrations.

Use Docker-compatible configuration and persistent volumes. Container
filesystem storage must not be treated as durable media storage.

### 22.3 Configuration and secrets

Use strongly typed options with startup validation. Keep non-secret
defaults in configuration files and secret values in environment
variables or a secret manager. Never commit production connection
strings, Mailtrap credentials, reCAPTCHA secrets, encryption keys, or
backup credentials.

------------------------------------------------------------------------

## 23. Testing architecture

### 23.1 Domain tests

Test invariants without a database: - Publishing prerequisites. -
Visibility rules. - Translation fallback eligibility. - Album/photo
publication constraints. - Media reference and deletion rules. - Contact
lifecycle rules.

### 23.2 Application tests

Test handlers with mocked/fake application interfaces: - Command
validation. - Authorization decisions. - Correct repository calls. -
Transaction boundaries. - Outbox creation. - Failure and retry
decisions. - Cancellation propagation.

### 23.3 Infrastructure integration tests

Use a real SQL Server test instance/container where practical for: - EF
mappings and migrations. - Unique constraints and concurrency. -
Transaction behaviour. - Query projections and indexes. - Identity
persistence. - Repository implementations.

Avoid relying exclusively on EF Core's in-memory provider for relational
behaviour.

### 23.4 Web integration tests

Test: - Public/admin route separation. - Authentication and policy
enforcement. - Anti-forgery. - Draft/private content exclusion. -
Contact submission. - Setup wizard concurrency and lockout after
completion. - Private media authorization. - Error response behaviour.

### 23.5 Architecture tests

Automate dependency rules: - Domain must not reference outer layers. -
Application must not reference Infrastructure or Web. - Infrastructure
must not reference Web. - Controllers must not depend on
DbContext/repository implementations. - Domain must not reference EF
Core, Identity, or MVC.

------------------------------------------------------------------------

## 24. Performance and scalability principles

-   Use server-side pagination and bounded result sizes.
-   Project only fields required by the page.
-   Use `AsNoTracking` for read-only entity queries.
-   Avoid N+1 queries and unbounded eager loading.
-   Index measured query patterns.
-   Generate responsive image variants and serve modern formats where
    supported.
-   Lazy-load below-the-fold images.
-   Cache public published content with reliable invalidation.
-   Process large files and expensive image work outside request
    threads.
-   Set upload, request, job concurrency, and memory limits.
-   Measure Core Web Vitals and database query performance before
    introducing more infrastructure.

The initial modular monolith can scale vertically and to multiple web
instances if shared storage, distributed job coordination, cache
strategy, and session/authentication configuration are designed
accordingly.

------------------------------------------------------------------------

## 25. Key architectural decisions and trade-offs

  ------------------------------------------------------------------------------
  Topic                   Decision                Reason / trade-off
  ----------------------- ----------------------- ------------------------------
  System style            Modular monolith        Lower operational complexity;
                                                  modules remain separable

  Layering                Clean Architecture      Protects domain/use cases from
                                                  infrastructure details

  CQRS                    MediatR commands and    Explicit use cases; adds
                          queries                 handler/DTO structure

  Persistence             EF Core 10 + SQL Server Required relational stack and
                                                  Code First workflow

  Repository              Focused aggregate       Encapsulates persistence
                          repositories            without generic-repository
                                                  leakage

  Unit of Work            Thin wrapper over       Avoids duplicating EF change
                          DbContext               tracking/transactions

  Mapping                 Mapster                 Efficient mapping; must not
                                                  bypass domain methods

  Validation              FluentValidation        Consistent request validation
                          pipeline                before handlers

  Identity                ASP.NET Core Identity   Mature
                                                  authentication/token/lockout
                                                  support

  DI                      Native .NET DI          Adequate and simpler; Autofac
                          initially               remains optional

  Logging                 Serilog Console + File  Structured diagnostics

  DbContext               One initial context     Simpler transaction boundary;
                          including Identity      split only for a real need

  Background work         Durable job/outbox      Avoids losing work after HTTP
                          design                  request ends

  External side effects   Outbox pattern          SQL commit and email/job
                                                  dispatch cannot be one atomic
                                                  transaction
  ------------------------------------------------------------------------------

------------------------------------------------------------------------

## 26. Risks and mitigations

  -----------------------------------------------------------------------
  Risk                    Impact                  Mitigation
  ----------------------- ----------------------- -----------------------
  Overusing CQRS/MediatR  Excessive boilerplate   Use request handlers
                                                  for meaningful use
                                                  cases; keep simple code
                                                  simple

  Generic repository      Poor query performance  Focused repositories
  hides EF Core           and leaky abstractions  and query-specific read
                                                  services

  Unit of Work duplicates Confusing transaction   Keep abstraction thin
  DbContext               ownership               and document
                                                  transaction boundaries

  Mapster bypasses domain Invalid domain state    Map inputs to commands;
  invariants                                      update aggregates
                                                  through methods

  Background task lost on Missing                 Durable outbox/job
  process restart         email/processing        storage and retry
                                                  monitoring

  Public/private media    Privacy/security        Separate storage and
  leak                    incident                server-side
                                                  authorization

  Concurrent admin setup  Multiple administrators Atomic setup workflow
                                                  and database
                                                  constraints

  Migration failure       Deployment outage/data  Reviewed scripts,
                          loss                    pre-deployment backup,
                                                  staging rehearsal

  Backup exists but       Extended outage         Regular restore drills
  cannot restore                                  and integrity
                                                  verification

  Cache contains          Incorrect or sensitive  Targeted invalidation
  stale/private data      output                  and strict cache
                                                  separation
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## 27. Implementation sequence

Architecture should be implemented incrementally:

1.  Create solution and project references; add architecture tests.
2.  Configure Domain primitives and core entities.
3.  Configure Application abstractions, MediatR, FluentValidation, and
    pipeline behaviours.
4.  Configure Infrastructure, EF Core 10, SQL Server, Identity,
    migrations, repositories, and Unit of Work.
5.  Configure Web host, MVC areas, authorization, middleware, and error
    handling.
6.  Implement first vertical slice: profile or project draft creation
    and public query.
7.  Implement publishing and language rules.
8.  Implement media storage, quarantine, scanning, and image processing.
9.  Implement gallery and private-media access.
10. Implement contact/outbox/email workflows.
11. Implement resume, analytics, backup/restore, and operations modules.
12. Complete integration, security, accessibility, performance,
    deployment, and recovery testing.

Do not build all abstractions up front without a working vertical slice.
Validate the architecture early with one write flow, one read flow, one
protected admin route, and one public page.

------------------------------------------------------------------------

## 28. Open decisions for the Technical Specification

The following must be confirmed before implementation:

1.  Exact MediatR package/version and licensing implications for the
    intended use.
2.  Exact Mapster package and configuration/registration approach.
3.  Exact FluentValidation integration and pipeline registration.
4.  Native .NET DI versus Autofac (native DI is recommended).
5.  Background job provider and hosting model.
6.  Image processing library and supported formats/limits.
7.  Malware scanner deployment and failure policy.
8.  Cache provider and whether production will run multiple instances.
9.  SQL Server hosting/version and production connection strategy.
10. Public/private media storage root and backup destination.
11. Outbox/job persistence and retry/retention policies.
12. Exact Identity user fields, role/policy matrix, MFA/session
    configuration.
13. Migration execution process in production.
14. Analytics storage and consent implementation.
15. Exact database entities, relationships, constraints, indexes, and
    concurrency tokens.

No production secrets or credentials should be placed in this document.

------------------------------------------------------------------------

## 29. Architecture acceptance checklist

The ADD is ready to guide implementation when:

-   [ ] Project references enforce the inward dependency rule.
-   [ ] Domain has no dependency on MVC, EF Core, Identity, or
    Infrastructure.
-   [ ] Application use cases are expressed as commands/queries with
    clear handlers.
-   [ ] FluentValidation runs before handlers.
-   [ ] Repository interfaces are separated from Infrastructure
    implementations.
-   [ ] Unit of Work has one clear transaction owner and does not
    duplicate DbContext behaviour.
-   [ ] Mapster mappings are explicit and tested; domain invariants are
    not bypassed.
-   [ ] EF Core configurations, migrations, indexes, and concurrency
    rules are documented.
-   [ ] Controllers use Application requests and do not access EF Core
    directly.
-   [ ] Identity and one-time setup enforce a single administrator.
-   [ ] Public/private media access is enforced server-side.
-   [ ] External side effects use durable post-commit processing.
-   [ ] Serilog and exception handling do not expose sensitive
    information.
-   [ ] Architecture tests enforce project dependency rules.
-   [ ] Production migration, backup, restore, and deployment procedures
    are defined.
-   [ ] Open decisions in Section 28 are resolved or explicitly accepted
    before the affected feature is implemented.

------------------------------------------------------------------------

## 30. Relationship to other project documents

-   **PRD.md** remains the source of truth for product vision, scope,
    and user-facing requirements.
-   **REQUIREMENTS_CATALOG.md** defines detailed functional requirements
    and acceptance criteria.
-   **ADD_Comprehensive.md** (this document) defines architectural
    boundaries, responsibilities, and system design.
-   **TECHNICAL_SPEC_v2.md** defines exact package versions, configuration,
    schema, endpoints, implementation contracts, and operational
    settings.
-   **DESIGN_SYSTEM.md** and **PAGE_DESIGN_SPECIFICATION_v2.0.md** define
    the UI system and page behaviour.
-   **TESTING_STRATEGY.md** defines how requirements and architecture
    are verified.
-   **AGENTS.md** defines the rules AI coding agents must follow.

If documents conflict, do not silently choose one. Record the conflict,
identify the owning decision, and obtain approval before implementation.

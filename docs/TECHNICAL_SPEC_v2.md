# Technical Specification

**Project:** Adib Hasan Avik — Personal Portfolio & Travel Gallery  
**Platform:** .NET 10 / ASP.NET Core MVC  
**Architecture:** Clean Architecture modular monolith  
**Database:** SQL Server  
**ORM:** Entity Framework Core 10  
**Document status:** Revised implementation-ready proposal — owner review required  
**Version:** 2.0-draft  
**Purpose:** Provide the technical decisions and implementation constraints for the coding agent. This document does not claim that the application has already been implemented, deployed, or tested.

---

## 1. Decision status and interpretation

This specification distinguishes three kinds of decisions. The coding agent must preserve this distinction in implementation notes, pull requests, and deployment documentation.

### 1.1 Approved decisions

These are product-owner-approved requirements or technology choices. Do not replace them without explicit approval.

| Area | Approved decision |
|---|---|
| Framework | .NET 10 and ASP.NET Core MVC |
| Architecture | Clean Architecture, modular monolith, strict inward dependency direction |
| Application patterns | CQRS with MediatR, Repository and Unit of Work abstractions |
| Mapping and validation | Mapster and FluentValidation |
| Data | SQL Server, EF Core 10, Code First migrations |
| Identity | ASP.NET Core Identity; exactly one administrator |
| Frontend foundation | Bootstrap 5 plus a custom CSS design system |
| Visual direction | Executive Dark, with a professionally designed light theme |
| Frontend principle | Bootstrap is a responsive foundation only; it must not dictate the visual identity or produce default Bootstrap-looking pages |
| Public application | Multi-page portfolio and travel gallery with distinct URLs |
| Admin application | Dedicated, protected, multi-page Admin CMS for one administrator |
| Email | Mailtrap Email Sandbox in development; Mailtrap Email Sending in production after domain verification |
| Anti-bot | Google reCAPTCHA v3, server-side verification |
| Media storage | Public and private storage, behind a storage abstraction; local persistent volume initially and cloud/object-storage portability later |
| File scanning | Scanner abstraction; ClamAV is the initial proposed scanner, with fail-closed quarantine behavior |
| Gallery provenance | Only photographs uploaded and selected by the administrator become real gallery content; no stock, generated, or placeholder images may be populated automatically |
| Localization | English default and Bangla additional language; `/en/` and `/bn/` route prefixes |
| Accessibility | WCAG 2.2 AA target |
| Recovery | RPO 4 hours and RTO 4 hours, demonstrated through restore testing |
| Scope | Preserve the approved PRD and requirements catalogue; do not add multi-admin, public accounts, or unrelated CMS/SaaS scope |

### 1.2 Recommended technical defaults

These are the recommended implementation choices for making the system concrete. They are not claims that a provider has already been purchased or deployed. Use them unless a technical incompatibility, licensing issue, or documented deployment constraint is discovered. If a change is necessary, record the reason and proposed replacement before implementation.

| Area | Recommended default |
|---|---|
| Solution shape | One ASP.NET Core MVC host and the four existing Clean Architecture projects: Domain, Application, Infrastructure, Web |
| Dependency injection | Built-in .NET dependency injection; do not add Autofac without a demonstrated requirement |
| Database access | One application DbContext initially; EF Core repositories and Unit of Work implement application-owned abstractions |
| Background processing | Hangfire with SQL Server-backed persistent storage for retryable and scheduled jobs; use an outbox table for reliable business notifications |
| Email reliability | Transactional outbox persisted with the business record; background dispatcher with bounded retries and idempotency |
| Rich-text editing | Quill editor hosted locally, with a strict server-side HTML allowlist sanitizer; editor output is untrusted input |
| Image processing | Isolated image-processing adapter; select a maintained library only after confirming its current license and deployment compatibility |
| File scanning | ClamAV behind `IFileSecurityScanner`; unavailable or indeterminate scanner means quarantine, not clean |
| Cache | ASP.NET Core output/data caching for eligible public content, initially using the in-process provider; keep cache interfaces and invalidation explicit |
| Logging | Serilog structured logging to console and rolling file; do not log secrets, tokens, message bodies, or private file contents |
| Health | ASP.NET Core health checks for liveness/readiness and dependencies |
| Testing | Unit, integration, architecture, security, accessibility, and end-to-end tests; NUnit/Moq/Shouldly may be used where consistent with the existing test strategy |
| UI composition | Razor layouts, partials, and ViewComponents; separate public and Admin layouts |
| Theme preference | Detect system preference on first visit; persist explicit visitor selection in localStorage |
| Static assets | Self-host Bootstrap and project-owned frontend assets; avoid runtime dependence on public CDNs for core layout or admin operation |
| Deployment | Docker-compatible deployment; persistent mounts for media and a separately managed SQL Server service/database |
| Configuration | Strongly typed options with environment-specific configuration and deployment secrets |

### 1.3 Deployment-dependent configuration

The following values must be configured for each environment. The coding agent must not hard-code developer paths, production credentials, hostnames, or provider-specific assumptions.

- SQL Server host, database name, credentials, encryption and connection options.
- Canonical domain, DNS, TLS certificate, reverse proxy and forwarded-header configuration.
- Public and private storage roots, volume/bind-mount locations, capacity limits and backup destination.
- Mailtrap credentials, verified sending domain and sender identities.
- reCAPTCHA site key, secret key, allowed hostnames and score threshold.
- ClamAV endpoint, timeout, resource limits and update policy.
- Background worker count, queue names, retry limits and job retention.
- Cache duration and distributed cache choice if multiple application instances are introduced.
- Backup schedule, retention, encryption-key recovery and external failure-domain destination.
- Performance budgets, request limits, rate limits and operational alert thresholds.
- Analytics retention, consent configuration and privacy/legal policy settings.
- Application secrets, Data Protection key persistence and encryption-key management.

---

## 2. Platform, framework and dependency policy

### 2.1 Framework target

- Target `net10.0` for all application projects unless a documented tool or provider compatibility issue requires otherwise.
- Use EF Core 10 packages and a SQL Server provider compatible with the selected .NET/EF Core 10 patch level.
- Use the latest supported patch releases within the chosen major versions at project creation, then pin package versions centrally.
- Keep Microsoft.Extensions and ASP.NET Core package versions aligned with the .NET 10 target.
- Do not mix incompatible major versions of EF Core, Identity persistence, MediatR, or provider packages.
- Record package versions in the solution's central package management file (`Directory.Packages.props`) where practical.
- Commit `packages.lock.json` for deterministic restore if the team enables NuGet lock-file mode.
- Review dependency licenses, maintenance activity, security advisories and transitive dependencies before adding a package.
- Upgrade packages through a reviewed change with build and test evidence; do not perform unreviewed major-version upgrades.

The coding agent must not invent exact package patch versions in this document. The actual pinned versions must be selected and verified when the solution is created.

### 2.2 Required core technologies

- ASP.NET Core MVC and Razor.
- SQL Server and EF Core 10.
- ASP.NET Core Identity.
- MediatR for application request dispatch.
- FluentValidation for application input validation.
- Mapster for object mapping where it improves clarity.
- Serilog for structured logging.
- Bootstrap 5 and custom CSS.
- Docker-compatible build and runtime configuration.

### 2.3 Optional dependencies

Do not add optional dependencies merely because they are common in tutorials.

- Autofac: not required; use built-in DI unless a concrete registration/lifetime capability cannot be handled cleanly.
- Redis or another distributed cache: defer until multiple instances or measured cache requirements justify it.
- A separate search engine: out of initial scope; use SQL Server capabilities and measured query patterns.
- Microservices, event sourcing, CQRS read databases and distributed transactions: out of scope unless future requirements justify them.

---

## 3. Solution structure and dependency direction

Use the approved Clean Architecture structure:

```text
Portfolio.sln
├── src/
│   ├── Portfolio.Domain/
│   ├── Portfolio.Application/
│   ├── Portfolio.Infrastructure/
│   └── Portfolio.Web/
└── tests/
    ├── Portfolio.Domain.UnitTests/
    ├── Portfolio.Application.UnitTests/
    ├── Portfolio.Infrastructure.IntegrationTests/
    ├── Portfolio.Web.IntegrationTests/
    └── Portfolio.ArchitectureTests/
```

Project names may be adjusted consistently, but layer responsibilities and dependency rules must remain unchanged.

### 3.1 Dependency rules

- Domain depends on no outer project and contains no EF Core, MVC, Identity, SQL Server, filesystem, or Mailtrap implementation details.
- Application depends on Domain and owns use-case interfaces/ports.
- Infrastructure implements Application-owned ports and references Application and Domain.
- Web references Application and uses Infrastructure only at the composition root for dependency registration.
- Controllers must not directly use DbContext, DbSet, concrete repositories, storage implementations, or infrastructure SDKs.
- Razor views receive presentation ViewModels, not EF entities or Identity persistence entities.
- Enforce dependency rules with architecture tests.

### 3.2 Application patterns

- Use commands for state changes and queries for reads.
- CQRS is at the application request level; it does not require separate databases.
- Use Repository and Unit of Work abstractions for aggregate persistence and transaction coordination. Avoid generic repository methods that expose unrestricted IQueryable or simply duplicate DbSet.
- Keep business invariants in Domain entities/aggregates.
- Keep use-case orchestration in Application handlers.
- Keep external technology implementations in Infrastructure.
- Use asynchronous I/O and propagate `CancellationToken`.
- Do not wrap synchronous work in `Task.Run` to simulate asynchronous behavior.
- Use Mapster for mapping only where mappings remain explicit and maintainable; use manual mapping for complex or security-sensitive transformations.

---

## 4. Frontend architecture and design system

### 4.1 Approved design principle

Bootstrap 5 is the responsive and interaction foundation, not the design system. The Executive Dark visual direction and the custom design system are the source of visual truth.

The final interface must look like a deliberately art-directed professional portfolio—not a Bootstrap starter theme, dashboard template, or generic CMS theme.

### 4.2 Bootstrap usage

Use Bootstrap 5 for appropriate foundations such as:

- Responsive grid and breakpoint utilities.
- Form controls and validation layout where suitable.
- Accessible navigation patterns and responsive collapse behavior.
- Modal, offcanvas, dropdown and other interaction primitives when they meet accessibility and design requirements.
- Utility classes selectively, without allowing utility-class accumulation to replace a coherent design system.

Do not rely on unmodified Bootstrap defaults for the site's color palette, typography, card design, buttons, shadows, borders, spacing rhythm, navigation appearance, or page composition. Avoid importing a full prebuilt Bootstrap theme.

Self-host the required Bootstrap CSS/JS assets. Customize through project-owned CSS variables and component styles. Keep overrides organized rather than scattering one-off overrides across page stylesheets.

### 4.3 Design tokens

Create a central token layer using CSS custom properties. The following palette is the approved visual direction's starting proposal and may be refined during visual implementation without changing the product scope:

| Token purpose | Initial value |
|---|---|
| Deep background | `#080D19` |
| Elevated surface | `#101A2C` |
| Raised/interactive surface | `#1D2D48` |
| Primary accent | `#3978F6` |
| Secondary accent | `#7657E8` |
| Light-theme text reference | `#F4F6FA` |
| Muted text reference | `#A8B3C7` |

Define semantic tokens rather than using raw colors throughout components. Include tokens for page background, surface levels, text primary/secondary, borders, focus ring, links, primary/secondary actions, success, warning, danger, shadows, radii, spacing, typography, and motion.

Check text and interactive-state contrast in both themes against WCAG 2.2 AA. Do not assume the sample palette automatically passes every contrast combination.

### 4.4 Theme behavior

- Dark theme is the default visual direction.
- On a first visit with no saved choice, respect the operating system's `prefers-color-scheme`.
- Provide an accessible, visible theme control.
- Persist an explicit visitor choice in localStorage.
- Apply the theme early enough to avoid a visible flash of the wrong theme.
- Both themes must be fully designed; light mode must not be a simple inversion of dark mode.
- Theme choice must not affect server authorization, content visibility, or security decisions.
- Respect `prefers-reduced-motion`.

### 4.5 Typography, layout and page composition

- Use a deliberate type scale, readable line lengths, consistent spacing and clear hierarchy.
- Use a small, purposeful font family set; self-host licensed font files where appropriate.
- Build reusable components for shared elements, but give each page its own composition and content hierarchy.
- Home: cinematic, confident executive introduction with clear evidence of engineering work.
- Education: academic/editorial timeline or structured progression.
- Achievements: engineering milestone journal with evidence and context.
- Contact: refined, trustworthy communication experience.
- Projects: case-study-led presentation with technical depth and clear project status.
- Gallery: photography-led layout that remains empty until real administrator-selected photographs are published.
- Ensure responsive behavior from mobile through wide desktop; do not merely shrink desktop layouts.

### 4.6 Frontend structure

Use separate public and Admin layouts. Organize CSS by tokens, base styles, shared components, public page compositions and Admin-specific components. Organize JavaScript by feature and keep it minimal.

Prefer Razor partials and ViewComponents for repeated server-rendered elements. Do not introduce a SPA framework or a separate frontend application; that would change the approved architecture.

### 4.7 Accessibility and interaction states

- Target WCAG 2.2 AA.
- Use semantic landmarks, correct heading order, visible keyboard focus, keyboard-operable controls and accessible names.
- Support screen readers, zoom, high contrast where supported, reduced motion and touch interaction.
- Dialogs, menus, filters, lightboxes and validation messages must have accessible focus behavior.
- Provide loading, success, error, empty, partial-success and disabled states.
- Avoid motion that distracts from content or causes discomfort.
- Do not communicate status by color alone.

---

## 5. Identity, administrator setup and authorization

### 5.1 Single administrator

- There is exactly one administrator in the initial product.
- No public registration and no second-admin creation workflow.
- Email is the login identifier.
- Use ASP.NET Core Identity password hashing; never store plaintext passwords.
- Admin role assignment is permitted only through the protected initial setup use case.
- Admin authorization must be enforced server-side on every protected endpoint and use case.

### 5.2 One-time setup wizard

The `/admin/setup` wizard is available only while no administrator exists.

Required sequence:

1. Check administrator existence server-side.
2. Collect the administrator's email and password.
3. Validate the password using the configured Identity policy.
4. Create the Identity user using Identity APIs.
5. Assign the Admin role.
6. Require authenticator-app TOTP enrollment and successful verification.
7. Generate and securely present one-time recovery codes.
8. Persist setup completion.
9. Permanently disable setup after success.

The operation must be atomic/concurrency-safe. Re-check administrator existence immediately before final commit. Enforce uniqueness in the database where feasible. Two simultaneous setup attempts must not create two administrators. Recovery codes must never be logged and must be displayed only through the intended secure flow.

### 5.3 MFA and account recovery

- Use authenticator-app TOTP.
- Require MFA for administrator sign-in and sensitive operations as specified by the security design.
- Provide one-time recovery codes; protect stored representations and invalidate each code after use.
- MFA recovery must not become an unauthenticated bypass.
- Password reset must not disable MFA.
- Password reset tokens must be time-limited, single-use in the effective workflow and delivered through Mailtrap.
- Return generic responses that do not disclose whether an email address exists.
- Revoke existing sessions/security stamps after password reset and sensitive credential changes.
- Provide session/device visibility and revocation as required by the PRD.
- Apply lockout and rate limits to login, setup, MFA, recovery and reset flows.

### 5.4 Cookie and session defaults

Use secure authentication cookies with HttpOnly and an appropriate SameSite policy. Set Secure in HTTPS environments and require HTTPS in production. Define explicit idle and absolute session lifetimes during implementation and document them in configuration. Use security-stamp validation and revoke sessions after sensitive changes. Never log cookies, password-reset tokens, MFA codes or recovery codes.

---

## 6. Database, EF Core and migrations

### 6.1 Database approach

- SQL Server is the relational database.
- EF Core 10 Code First migrations define schema evolution.
- Start with one application DbContext unless a clear bounded-context or operational reason requires separation.
- Configure entities using explicit `IEntityTypeConfiguration<T>` classes.
- Use UTC for persisted timestamps; convert to visitor-local display time at presentation boundaries.
- Use decimal types with explicit precision for any future monetary values.
- Use database constraints for uniqueness, required relationships and valid state where possible.
- Use optimistic concurrency tokens for records that may be edited concurrently.
- Avoid cascade-delete behavior that could silently remove referenced media or audit history.

### 6.2 Indexing

Create indexes based on known query paths and verify them with query plans. Expected candidates include:

- Unique normalized administrator email (Identity-managed).
- Unique content slug within the appropriate content type and language.
- Publication status and publish date for public listings.
- Language and content relationship keys.
- Foreign keys and frequently filtered category/status fields.
- Contact message status and received date.
- Media category, scan/processing status and hash lookup, subject to privacy boundaries.
- Analytics event date/type dimensions where used.

Do not add indexes blindly; document important indexes and review query plans as data grows.

### 6.3 Migration policy

- Development may apply migrations automatically when explicitly configured for local development.
- Staging and production migrations are controlled deployment steps.
- Do not automatically run production schema migrations on every web application startup.
- Back up the database before production migrations that may be destructive or difficult to reverse.
- Review generated migration SQL before applying it to production.
- Prefer forward-fix migrations over assuming every production migration can be safely rolled back.
- Record migration identity and deployment result.
- Role seeding must be idempotent. Seeding must not create or promote additional administrators.

### 6.4 Data integrity and lifecycle

Use transactions for database changes that must succeed together. Keep long-running file streams and external network calls outside database transactions. Use explicit state transitions for publishing, scanning, processing, deletion and restore workflows. Preserve media reference integrity; block deletion while an asset is in use unless the approved replacement/removal workflow has updated references.

---

## 7. Background jobs, outbox and retries

### 7.1 Background processing

Recommended default: Hangfire with SQL Server-backed persistent storage.

Use background jobs for work that must survive application restarts, such as:

- Image variant generation after a successful scan.
- Contact email delivery and retry.
- Outbox dispatch.
- Scheduled publishing where enabled.
- Cleanup and retention tasks.
- Backup verification or other approved maintenance tasks.

Do not use fire-and-forget `Task.Run`, in-memory timers, or `Thread.Sleep` loops for durable production work.

### 7.2 Job requirements

- Jobs must be idempotent or use a durable deduplication key.
- Use bounded retries with exponential backoff and a maximum attempt count.
- Distinguish transient failures from permanent failures.
- Move exhausted jobs to a visible failed/dead-letter state for administrator review.
- Record correlation IDs and safe operational metadata.
- Never log private content, credentials or file contents.
- Configure concurrency limits and resource usage for image processing.
- Prevent two workers from processing the same logical operation concurrently.
- Expose queue health and failed-job status in the Admin Operations area.
- Protect job dashboard/management endpoints with Admin authorization.

### 7.3 Transactional outbox

When a database change requires a later external side effect, write an outbox record in the same SQL transaction as the business change. A background dispatcher processes the outbox after commit.

Use this for contact notifications and other important email or integration work. Store stable message IDs, attempt counts, next-attempt time, status and safe failure information. The dispatcher must tolerate duplicate execution without duplicate business effects.

---

## 8. Email and Mailtrap

- Development uses Mailtrap Email Sandbox.
- Production uses Mailtrap Email Sending after sending-domain verification.
- Do not use personal Gmail SMTP as the production mail transport.
- Define an application-owned email abstraction; Mailtrap implementation belongs in Infrastructure.
- Persist contact messages before attempting email delivery.
- Track visitor confirmation and administrator notification independently.
- Retry transient delivery failures through the outbox/job workflow.
- Do not delete a contact message because email delivery failed.
- Store provider message identifiers and delivery outcomes where available.
- Do not log message body, attachment contents, credentials or private contact data unnecessarily.
- Configure sender address, sender name, API credentials and environment through deployment configuration.

---

## 9. reCAPTCHA v3 and abuse protection

Use Google reCAPTCHA v3 on the approved flows: Admin Setup, Login, Forgot Password, risk-based Reset Password and Contact.

Configuration names:

```text
RECAPTCHA__SITEKEY=
RECAPTCHA__SECRETKEY=
RECAPTCHA__SCORETHRESHOLD=0.5
```

- Site key may be delivered to the browser.
- Secret key is server-only.
- Verify tokens server-side.
- Validate expected action, hostname/environment and score.
- Reject invalid verification; do not treat verification outages as successful checks.
- Threshold `0.5` is the initial recommended setting and must be configurable.
- Review false positives and abuse signals before changing threshold.
- reCAPTCHA supplements, but does not replace, Identity, MFA, authorization, lockout and rate limiting.
- Never commit real keys or include them in logs, documentation or screenshots.

Apply endpoint-specific rate limits and request-size limits. Use generic public responses where account enumeration is a risk.

---

## 10. Media library, storage and file security

### 10.1 Storage abstraction

Use an application-owned abstraction such as `IStorageProvider` or `IMediaStorageService`. The interface must support save, open/read, delete, existence checks and metadata as required by the media use cases.

The first implementation uses local persistent storage. The abstraction must permit a future S3/Azure Blob adapter without rewriting Media Library business logic.

### 10.2 Public and private storage

- Public media may be served from a configured public storage root mapped to the web server's public asset path.
- Private media must be stored outside `wwwroot`.
- Private media must be delivered through an authorized endpoint that checks access on every request.
- Do not expose physical paths or internal storage keys in public responses.
- Do not rely on obscurity of a URL as authorization.
- Configure persistent Docker volume/bind mounts; container filesystem alone is not durable.
- Production host paths are deployment configuration, not source-code constants.

Illustrative local mapping only:

```yaml
volumes:
  - ./data/public-media:/app/wwwroot/uploads
  - ./data/private-media:/app/private-media
```

The actual host paths, ownership, permissions, backup coverage and mount strategy must be configured for the target host.

### 10.3 Allowed formats and limits

Initial allowlist:

- Media Library images: JPG/JPEG, PNG, WebP.
- Media Library documents: PDF.
- Contact attachments: PDF, JPG/JPEG, PNG.
- SVG disabled initially.
- HTML, JavaScript, executables and unapproved formats prohibited.

Initial server-enforced limits:

- Image: 10 MB per file.
- PDF in Media Library: 15 MB per file.
- Contact: maximum 3 attachments, 5 MB each, 15 MB total.

Limits must be configurable but may not be relaxed without reviewing security, storage and performance impact.

### 10.4 Validation and quarantine

Do not trust filename extensions or client-provided MIME types. Validate:

- Extension against allowlist.
- Declared MIME type as a secondary signal.
- File signature/magic bytes.
- Structural parsing and file validity.
- Image dimensions and decompression/resource limits.
- PDF validity and safe delivery behavior.

Generate server-side storage names. Prevent path traversal and unsafe filename handling. Stage uploads outside public access. Quarantine files until scanning has positively succeeded. A scanner timeout, unavailable scanner, malformed response or indeterminate result is not a clean result; keep the file quarantined and surface operational status.

### 10.5 Malware scanning

Use `IFileSecurityScanner`; ClamAV is the initial recommended adapter. Configure scanner endpoint, timeout, resource limits and update monitoring per environment. Do not expose quarantined content. Provide safe retry after scanner recovery. Record scan result and timestamp without logging file content.

### 10.6 Image processing

- Preserve original bytes.
- Scan before optimization or public publication.
- Generate WebP display variants and thumbnails where supported.
- Do not upscale.
- Preserve aspect ratio by default.
- Support focal point/crop settings without modifying original bytes.
- Proposed variant widths:

| Content use | Widths |
|---|---|
| Profile | 150, 400, 800 |
| Projects | 320, 640, 960, 1280, 1920 |
| Certificates | 320, 640, 1200 |
| Achievements | 320, 640, 960, 1280 |

- Process large variants in background jobs.
- Show processing state and allow safe retry.
- Optimization failure must not destroy the original.
- Keep the image-processing library behind an adapter and verify licensing, maintenance and native deployment requirements before pinning it.

### 10.7 Duplicate detection, replacement and deletion

Use SHA-256 to identify byte-identical files, while respecting public/private access boundaries. Do not reveal the existence or metadata of a private asset to an unauthorized user through duplicate detection.

On replacement, update references only after confirmation and successful processing, or create a new asset and retain the old asset until references are safely migrated. Block deletion of referenced assets. Use a recycle/retention workflow and audit important actions.

### 10.8 Private documents and downloads

Enforce access on every request. Set safe content-disposition and content-type headers. Prevent private responses from being cached by shared caches. Disable original downloads where configured, but do not claim that screenshots or capture of displayed content can be prevented.

---

## 11. Gallery visibility and publication

Resolve publication state and visibility on the server for every gallery request.

- Public: eligible for public listing and indexing only when published.
- Unlisted: accessible by direct link under the approved unlisted behavior; excluded from public listings, search and sitemap. Unlisted is not password protection.
- Private: administrator-only, delivered through authorized endpoints.
- Draft and unpublished content must not leak through page source, metadata, search, cache, structured data, language fallback or sitemap.
- Public gallery starts with a designed empty state.
- Only real photographs uploaded and selected by the administrator may be published.
- Optional photo metadata must not render empty labels or fabricated values.
- Downloads are enforced server-side according to the configured asset policy.
- Comments remain disabled by default; if enabled, require moderation/approval, abuse controls, rate limiting and audit history.

---

## 12. Publishing, versioning and localization

### 12.1 Publishing lifecycle

Support Draft → Preview → Publish → Unpublish. Editing a published item must not change the public version until the administrator explicitly republishes the changes. Use a revision/version model or equivalent persistence strategy that makes the public revision unambiguous.

Scheduled publishing may be supported where already included in the PRD. It must use persistent background processing and explicit timezone handling.

### 12.2 Public cache behavior

Cache only eligible published public content. Never put admin previews, drafts, private files, contact messages or authenticated responses in shared public caches.

On publish, unpublish, delete or relevant media replacement, invalidate all affected cache entries, including:

- Individual content page.
- Listing/category pages.
- Search results.
- Home page/featured content.
- Sitemap and language variants.
- Relevant metadata/structured data.

### 12.3 Localization

- English is the default public language; Bangla is additional.
- Use `/en/` and `/bn/` prefixes.
- Keep translated content separate and independently publishable.
- Returning visitor preference takes priority.
- For a new visitor, browser language may be used to suggest English or Bangla; unsupported languages fall back to English.
- Manual selection is always available and persists.
- Switching language should preserve the equivalent page when a published equivalent exists.
- If no equivalent exists, send the visitor to the selected-language home page.
- Selected-language content is preferred; English fallback is permitted only under the approved rules.
- Never fall back to an unpublished translation.
- Admin interface language is separate from public content language; English default and Bangla additional.
- Use localized metadata/slugs where appropriate, canonical URLs and correct `hreflang`.
- Sitemap contains only published, public, indexable language versions.

---

## 13. Rich text and content safety

The Admin CMS requires structured fields and a rich editor for long-form content, including headings, paragraphs, lists, links, images and code snippets.

Recommended default: locally hosted Quill editor. The browser editor is not a security boundary.

- Treat editor HTML as untrusted input.
- Sanitize on the server using a strict allowlist of tags, attributes and URL schemes.
- Disallow scripts, event-handler attributes, unsafe embeds, arbitrary iframes and unsafe URL schemes.
- Restrict image insertion to approved Media Library assets rather than arbitrary external image URLs, unless a specific approved use case requires otherwise.
- Render sanitized output only through a clearly named safe-rendering path.
- Keep plain-text or structured content available where search, accessibility or future migrations require it.
- Test sanitizer behavior against XSS payloads and malformed HTML.
- Keep editor configuration and sanitizer allowlist aligned; client-side toolbar restrictions alone are insufficient.

---

## 14. Contact messages and attachments

- Persist the contact message and attachment metadata before email delivery.
- Store attachments privately, scan them and enforce the contact limits in Section 10.
- Support conversation threads, replies, internal notes, statuses, delivery tracking, search, filtering and archive behavior.
- Visitor confirmation and admin notification are independent outbox deliveries.
- A Mailtrap outage must not lose the original message.
- Prevent duplicate submissions with a persisted request/idempotency key where appropriate.
- Apply reCAPTCHA, server-side validation, rate limits and privacy controls.
- Apply the approved retention/deletion policy and audit relevant administrative actions.
- Do not expose internal notes or private attachments through public routes.

---

## 15. Resume management

- Support English and Bangla resume versions and multiple professional variants.
- Administrator selects the default public version.
- Each version has independent draft/publish state and version history.
- Only published versions are public.
- Validate uploaded PDF files and store unpublished/private versions securely.
- Provide browser preview and download for published versions.
- Keep a stable public URL where the approved product behavior requires it.
- Track aggregated downloads without invasive visitor profiling.
- Provide a graceful empty state if no resume is published.

---

## 16. Analytics and privacy

Use privacy-conscious aggregate analytics.

Required reporting includes approved aggregate measures such as visitor/page-view trends, popular pages/projects/albums, traffic-source categories, device/browser categories, contact conversions and relevant resume/download events.

- Exclude administrator activity.
- Avoid invasive profiling, unnecessary identifiers and sensitive visitor profiles.
- Prefer cookieless measurement.
- Obtain consent for non-essential tracking where required.
- Allow consent preference changes/withdrawal.
- Define event schema, retention, export and deletion behavior before enabling production analytics.
- Analytics must not expose private content or contact-message data.
- Legal/privacy requirements must be reviewed for the actual deployment and audience.

---

## 17. Caching and performance

### 17.1 Caching

Start with ASP.NET Core caching for eligible public content. Keep cache policy and invalidation behind explicit application/web abstractions so a distributed cache can be introduced if deployment topology requires it.

Do not cache:

- Admin pages and previews.
- Authenticated or private responses in shared caches.
- Private media or contact attachments.
- Draft or unpublished content.

### 17.2 Performance practices

- Use responsive image variants and lazy loading where appropriate.
- Set image dimensions/aspect ratios to reduce layout shift.
- Minimize render-blocking resources.
- Self-host essential frontend assets.
- Use asynchronous database and file I/O.
- Avoid N+1 queries; project to read DTOs and inspect generated SQL.
- Add indexes based on actual query patterns.
- Paginate Admin lists and large public listings.
- Apply request/body limits and resource limits to image/PDF processing.
- Monitor slow queries, job duration, memory, storage and request latency.

### 17.3 Performance budgets

Do not invent hosting-independent response-time guarantees. Before release, define measurable targets for Core Web Vitals, public page response, Admin operations, page weight, image transfer, query duration and background processing throughput. Measure on representative staging infrastructure and record thresholds in release acceptance evidence.

---

## 18. Security baseline

Apply defense in depth and test the controls.

- OWASP Top 10-aligned secure coding and review.
- Server-side authorization on every protected endpoint and resource.
- Anti-forgery tokens for state-changing browser requests.
- Output encoding and strict rich-text sanitization.
- Parameterized EF Core queries; review any raw SQL.
- Secure authentication cookies, HTTPS and session revocation.
- MFA, lockout, rate limiting and generic account-recovery responses.
- Content Security Policy appropriate to the self-hosted frontend.
- HSTS only after production HTTPS is correctly configured.
- `X-Content-Type-Options`, suitable Referrer-Policy and other appropriate security headers.
- Safe file upload, quarantine, scanning and private-file delivery.
- Secret management and Data Protection key persistence.
- Dependency/container vulnerability review.
- Safe error responses; detailed exceptions only in protected logs.
- Audit security-sensitive actions without recording secrets.
- No credentials, reset tokens, MFA codes, recovery codes, session cookies or encryption keys in source control, logs, screenshots or ordinary audit payloads.

Use explicit authorization policies for Admin, sensitive operations and private media. Sensitive operations such as restore, key changes and destructive maintenance require recent authentication/MFA confirmation where appropriate, clear confirmation and audit history.

---

## 19. Logging, monitoring and health

Use Serilog structured logging with console and rolling file sinks as the initial default.

- Include timestamp, level, environment, application, correlation/trace ID and safe contextual identifiers.
- Use structured properties rather than string interpolation for operational events.
- Redact secrets and sensitive personal data.
- Define log retention and rotation.
- Ensure container logs can be collected by the deployment platform.
- Add liveness and readiness health checks.
- Readiness may check critical dependencies such as SQL Server; liveness should not fail merely because a noncritical external integration is temporarily unavailable.
- Monitor SQL connectivity, email/outbox delivery, background jobs, storage availability/capacity, scanner availability, cache and backup status.
- Provide actionable Admin Operations status without exposing credentials or internal infrastructure details publicly.
- Alert on failed backup verification, exhausted outbox retries, prolonged scanner outage, storage capacity thresholds and repeated application failures.

---

## 20. Backup, restore and disaster recovery

Approved recovery objectives:

- **RPO: 4 hours maximum data loss.**
- **RTO: 4 hours maximum restoration time.**

A daily database backup alone does not satisfy a four-hour RPO.

Requirements:

- Back up SQL Server data using a schedule/recovery model capable of meeting the RPO.
- Back up public and private media originals and generated variants.
- Keep an application-level manifest that maps media records to stored objects and checksums.
- Keep at least one backup copy in a separate failure domain from the primary host.
- Encrypt backups and protect encryption keys separately.
- Document how keys are recovered during disaster recovery.
- Verify checksums and backup completeness.
- Perform periodic restore drills in an isolated environment.
- Validate database/media references after restore.
- Before an administrator-initiated restore, require reauthentication/MFA as appropriate, explicit confirmation and a safety backup of the current state.
- Keep restore operations out of ordinary request transactions.
- Record restore start, completion, result and operator in audit history.
- Define retention only after confirming storage capacity, legal requirements and operational cost.

RPO/RTO are acceptance targets, not claims. The project is not production-ready until measured recovery drills demonstrate them.

---

## 21. Configuration and secrets

Use strongly typed options with startup validation for required configuration. Keep environment-specific values outside source code.

Examples of configuration names (values intentionally blank):

```text
ConnectionStrings__Portfolio=
RECAPTCHA__SITEKEY=
RECAPTCHA__SECRETKEY=
RECAPTCHA__SCORETHRESHOLD=0.5
Mail__Provider=
Mail__ApiKey=
Mail__FromAddress=
Storage__PublicRoot=
Storage__PrivateRoot=
Scanner__Endpoint=
Scanner__TimeoutSeconds=
DataProtection__KeyRingPath=
```

- `.env.example` contains variable names and safe placeholders only.
- Never commit real credentials, connection strings with passwords, API keys, private keys or encryption keys.
- Use deployment secret management for production.
- Persist ASP.NET Core Data Protection keys securely across container restarts and application instances.
- Restrict filesystem permissions for private media, key rings, logs and backup files.
- Validate required options at startup and fail clearly if a required production secret is missing.
- Do not expose configuration values through health endpoints or Admin pages.

---

## 22. Docker and deployment

### 22.1 Environments

Maintain separate Development, Staging and Production configuration. Never use production secrets or real private visitor data in local development fixtures.

### 22.2 Container requirements

- Use a supported .NET 10 SDK image for build and a supported ASP.NET Core runtime image for execution.
- Use a multi-stage Docker build.
- Run as a non-root user where supported.
- Keep the container filesystem immutable except for explicitly mounted persistent data.
- Mount public media, private media, Data Protection keys and any required persistent operational data.
- Do not bake secrets or production uploads into the image.
- Configure health checks and graceful shutdown.
- Set CPU/memory limits appropriate to the host, especially for image processing.
- Keep SQL Server and the web application separately managed; do not treat a container's ephemeral filesystem as database or media persistence.

### 22.3 Production deployment sequence

1. Build the application and run automated tests.
2. Scan dependencies and container image.
3. Create/verify a pre-deployment database and media backup.
4. Apply reviewed database migrations as a controlled step.
5. Deploy the application image.
6. Verify health/readiness and critical integrations.
7. Run smoke tests for public pages, Admin login/MFA, media delivery, contact persistence and background jobs.
8. Confirm logs, backups and monitoring.
9. Record deployment version and result.
10. If deployment fails, follow the documented rollback/forward-fix procedure; do not assume database rollback is always safe.

---

## 23. SEO, domain and HTTP behavior

- Configure one canonical production domain.
- Enforce HTTPS in production.
- Enable HSTS only after TLS and subdomain policy are verified.
- Configure trusted forwarded headers correctly when behind a reverse proxy.
- Prevent mixed content.
- Provide canonical URLs, localized metadata, `hreflang`, robots behavior and XML sitemap.
- Include only published, public, indexable content in the sitemap.
- Exclude Admin, drafts, private and unlisted content from public discovery.
- Use stable, readable slugs and safe redirects when a published slug changes.
- Provide meaningful 404/500 pages without leaking stack traces.
- Monitor domain/certificate expiry through the chosen hosting/operations process.

---

## 24. Testing and release evidence

The separate `TESTING_STRATEGY.md` remains authoritative for the full test inventory. This section defines the minimum technical implementation expectations.

- Domain unit tests for business invariants and lifecycle transitions.
- Application unit tests for command/query handlers, validators, authorization decisions and failure handling.
- Infrastructure integration tests against a real supported SQL Server test instance/container for migrations, constraints, transactions, concurrency and outbox behavior.
- Web integration tests for routing, authentication, authorization, anti-forgery, model binding, headers and public/private boundaries.
- Architecture tests for project dependency direction.
- End-to-end tests for setup, MFA, publishing, localization, media upload, scanning, gallery visibility, contact flow and Admin operations.
- Security tests for XSS, CSRF, authorization bypass, account enumeration, rate limits, upload validation, private-file access and session revocation.
- Accessibility checks against WCAG 2.2 AA, including keyboard and screen-reader-oriented manual checks.
- Performance tests on representative staging infrastructure.
- Backup/restore drills that measure RPO/RTO and verify media references.

A test is not passed merely because code was generated. Record test command, environment, result and any known limitation. Never claim a deployment, scan, restore drill or external integration has succeeded without evidence.

---

## 25. Operational Admin capabilities

The Admin Operations area must provide safe visibility and control for the agreed product scope:

- Application/dependency health.
- Background job queues and failed jobs.
- Email/outbox delivery status.
- Storage usage, quota and availability.
- Cache status/maintenance controls where applicable.
- Backup verification and restore workflow.
- Logs/diagnostic summaries appropriate for the administrator.
- Maintenance mode and visitor notifications.
- Migration/deployment status where safely available.
- Security and activity history.

Operational controls must not expose secrets. Destructive actions require explicit confirmation and appropriate reauthentication/MFA. Long-running operations must report progress and final status; do not present a button click as proof of success.

---

## 26. Legal, retention and policy pages

Provide administrator-manageable, versioned policy content for Privacy, Terms, Cookie, attachment handling, analytics and relevant retention/deletion practices. Initial policy content requires appropriate legal review for the actual deployment and jurisdiction. Do not invent legal compliance claims or represent template text as legal advice.

---

## 27. Explicit non-goals and scope protection

The implementation must not silently expand into:

- Multi-administrator management.
- Public visitor accounts or social networking.
- A general-purpose multi-tenant CMS/SaaS product.
- A separate SPA frontend or microservices architecture.
- A public blog/newsletter platform in the initial release.
- AI-generated portfolio content or automatic gallery population.
- A search engine or distributed data platform without demonstrated need.

Future possibilities listed in the PRD remain future possibilities and must not delay the approved portfolio.

---

## 28. Implementation rules for the coding agent

1. Read the PRD, ADD, requirements catalogue, traceability matrix, scope/releases, assumptions/dependencies and testing strategy before implementation.
2. Treat approved decisions in Section 1.1 and the PRD as authoritative.
3. Use Section 1.2 recommendations as defaults, but verify compatibility and licensing before pinning packages.
4. Keep Section 1.3 values configurable per environment.
5. Do not invent personal profile facts, project metrics, employment history, certificates, photographs or achievements.
6. Do not publish sample, generated, stock or placeholder gallery imagery as real content.
7. Do not create additional administrator accounts or public registration.
8. Do not bypass scanning, authorization, MFA, anti-forgery, sanitization or private-media checks to make a demo work.
9. Do not silently remove requirements because they are difficult. Record blockers and propose a decision.
10. Implement in small vertical slices, with tests and documentation updated alongside each slice.
11. Do not claim tests, security scans, deployment, backup or restore verification succeeded unless actually run and evidenced.
12. For any deviation from this specification, record the affected requirement, reason, impact, alternatives and approval status in an Architecture Decision Record (ADR).

---

## 29. Related documents and precedence

Use these documents together:

- `PRD.md` / approved PRD: product goals, audience, user-visible behavior and scope.
- `ADD_Comprehensive.md`: architecture layers, responsibilities, patterns and dependency rules.
- `REQUIREMENTS_CATALOG.md`: detailed requirement definitions (canonical 112-ID baseline; retired legacy identifiers aliased in `REQUIREMENTS_ALIAS_ANNEX.md`).
- `REQUIREMENTS_TRACEABILITY_v2.md`: mapping from requirements to design, implementation and tests.
- `SCOPE_AND_RELEASES_v2.md`: release boundaries and priorities.
- `ASSUMPTIONS_AND_DEPENDENCIES.md`: assumptions and external dependencies.
- `TESTING_STRATEGY.md`: test coverage and release quality strategy.
- `Implementation_Plan.md`: delivery sequencing.
- `TECHNICAL_SPEC_v2.md` (this document): technical defaults, implementation constraints and deployment configuration.

If documents appear to conflict:
1. Product scope and user-visible behavior are governed by the approved PRD and requirements catalogue.
2. Architectural dependency rules are governed by the approved ADD.
3. This Technical Specification defines technical choices within those constraints.
4. Resolve any genuine conflict explicitly through an ADR and update affected documents; do not silently choose whichever statement is easiest to implement.

---

## 30. Implementation-readiness checklist

Before coding a feature, confirm:

- [ ] The feature maps to an approved requirement and release.
- [ ] Domain invariants and aggregate ownership are clear.
- [ ] Application commands/queries and authorization requirements are defined.
- [ ] Persistence constraints, indexes and concurrency behavior are considered.
- [ ] External side effects use the outbox/background-job strategy where required.
- [ ] Public/private visibility and cache invalidation are defined.
- [ ] Validation, failure states and operational visibility are defined.
- [ ] Accessibility and responsive behavior are considered.
- [ ] Unit/integration/end-to-end tests are identified.
- [ ] Deployment configuration and secrets are not hard-coded.
- [ ] Documentation and traceability are updated.

**Review status:** This revised specification is submitted for owner review. It becomes the implementation baseline only after the owner approves it and any requested changes are incorporated.

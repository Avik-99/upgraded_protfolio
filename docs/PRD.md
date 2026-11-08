# Product Requirements Document (PRD)

## 1. Product summary

Build a polished, credible, dynamic personal portfolio for **Adib Hasan
Avik**. The site must communicate practical software-engineering
capability, professional identity and the ability to design and build
real-world software products. Practical engineering capability is the
strongest intended impression.

The product is a multi-page ASP.NET Core MVC application backed by SQL
Server. It has two distinct experiences: - **Viewer Panel:** public
portfolio pages and visitor interactions. - **Admin Panel:** a
protected, single-administrator workspace for managing published
content, media, messages, settings and operations.

These are logically separated areas in one application, not separate
independently deployed applications.

## 2. Problem and opportunity

A static portfolio is difficult to keep accurate and current. This
product provides structured content management and publishing controls
so that project case studies, skills, education, achievements,
certifications, resume versions and gallery content can be maintained
without changing application source code.

## 3. Product goals

1.  Establish a premium, professional first impression.
2.  Present engineering work with evidence and technically meaningful
    case studies.
3.  Allow the administrator to manage all agreed dynamic portfolio
    content.
4.  Provide safe draft, preview, publish and unpublish workflows.
5.  Protect administrator access, private files, visitor messages and
    operational controls.
6.  Deliver accessible, responsive, performant public pages.
7.  Keep architecture portable and maintainable, with future
    integrations possible without building speculative features now.

## 4. Audiences

The following audiences have equal importance: - Recruiters and hiring
managers. - Senior developers and technical reviewers. - Companies, CTOs
and business decision-makers. - Developers and potential collaborators.

## 5. Product principles

-   Credibility over exaggeration.
-   Evidence-backed content over unsupported claims.
-   Clear separation between public and private information.
-   Security and privacy by default.
-   Consistent design with purposeful visual hierarchy.
-   Administrator control over all real portfolio imagery.
-   Build the agreed product fully before adding speculative features.

## 6. Public experience

The public site is a multi-page experience with distinct URLs: - Home -
About - Education - Skills - Projects and project details -
Achievements - Certifications - Resume - Personal / Travel Gallery,
albums and photo views - Contact

A global navigation and search experience should help visitors discover
relevant content. Public pages must only render content eligible for
public publication.

## 7. Projects

The Projects experience supports completed, in-progress and planned
project records. It uses featured projects, a unified listing and status
filters. A project detail page is an engineering case study, with
applicable sections such as overview, problem, objectives, requirements,
user journeys, features, technology, architecture, database design,
implementation, engineering challenges, testing, deployment, lessons
learned and resources.

Only sections supported by verified project facts should be shown.
Planned work must not be represented as completed.

## 8. Gallery

The Gallery is a dedicated public feature, separate from Projects. It
supports albums/collections, featured photographs, filters, search,
album pages and an accessible lightbox.

**Image provenance requirement:** all previously discussed or shown
Gallery images are placeholders/design references. Actual Gallery
photographs must be uploaded and selected by the administrator through
the Admin Panel. No placeholder, generated, stock or example image may
automatically become real portfolio content. The initial Gallery must
show a designed empty state until real photographs are uploaded and
published.

The administrator can create albums, upload photographs, choose covers
and featured images, add optional metadata, reorder content, control
visibility, preview and publish.

Visibility modes: - Public: eligible for public listings and indexing
when published. - Unlisted: direct-link access, excluded from public
listings and indexing; not password protection. - Private:
administrator-only access through authorized endpoints.

## 9. Admin Panel

The Admin Panel is a complete, multi-page management area for one
administrator. It includes dashboard, profile, experience, education,
skills, projects, achievements, certifications, Media Library, Gallery
Management, resume, contact inbox, comment moderation, website settings,
analytics, security/activity and operational tools.

Content management supports structured fields and a rich editor for
long-form material. Editing a published item must not expose unfinished
changes. Public visitors see the last published version until the new
version is explicitly published.

## 10. Publishing and content lifecycle

Support drafts, preview, publish and unpublish. Where appropriate,
support scheduled publishing. Publishing changes must invalidate
relevant cached content. Drafts and unpublished translations must never
leak through public pages, search, sitemap or fallback behavior.

## 11. Identity and administrator setup

There is exactly one administrator. There is no public admin
registration and no supported workflow to create a second administrator.

Initial setup is a one-time protected Setup Wizard available only while
no administrator exists. The user chooses the administrator email and
password. The password is stored using ASP.NET Core Identity password
hashing. The wizard assigns the Admin role, requires MFA enrollment and
recovery-code generation, and is permanently disabled atomically after
successful setup. Normal access uses email/password and
authenticator-app TOTP. Recovery codes are stored safely; recovery must
not bypass the intended security checks.

## 12. Contact

Visitors can submit a contact message with name, email, subject,
category and message. Categories include Job Opportunity, Project
Collaboration, Technical Discussion and General Inquiry. Optional
attachments use a strict allowlist and private storage. Messages are
persisted before email delivery is attempted. Visitor confirmation and
administrator notification are independent delivery outcomes.

The Admin Panel provides inbox, conversation threads, replies, internal
notes, statuses, search, filters, archive and deletion/retention
controls. Mailtrap is the selected email provider: Sandbox for
development testing and Email Sending for production after domain
verification.

## 13. Resume

Support multiple language and professional versions, such as
English/Bangla and Software Engineer/Backend Developer. The
administrator selects a default version and controls publication
independently. Only published versions are public. Provide browser
preview and download, secure PDF validation, stable public access and
aggregated download analytics.

## 14. Multilingual experience

English is the default public language and Bangla is an additional
language. Use language-prefixed URLs (`/en/`, `/bn/`), language-specific
content and SEO metadata, `hreflang`, canonical URLs and
published-content-only sitemap entries.

Returning visitor preference takes priority. For new visitors, browser
language detection may suggest English or Bangla; unsupported languages
fall back to English. Manual selection always remains available and
persists. Switching language should preserve the equivalent page when
available. If no equivalent destination exists, use the selected
language home page. Prefer the selected language; fall back to English
only under the approved fallback rules, never to unpublished content.

Admin interface language is independently switchable; English is the
default and Bangla is additional. Interface translations are separate
from portfolio content translations.

## 15. Media Library

Provide one reusable library with categories: 1. Profile & Personal
Images 2. Project Images & Screenshots 3. Education & Certificates 4.
Achievement Images 5. Resume & Documents 6. Personal / Travel Gallery 7.
Other Assets

Support public and private assets, search, filters, metadata, usage
tracking, replacement, recycle bin, safe deletion, duplicate detection,
quotas, processing status and audit history. Preserve originals and
generate optimized WebP/responsive variants. Use an
`IStorageProvider`-style abstraction so local persistent storage can
later move to object storage without changing core Media Library logic.

Public images may be served from public storage. Private documents and
photographs must live outside `wwwroot` and be delivered only through
authorized endpoints.

## 16. Analytics and privacy

Provide aggregated analytics for visitors, page views, popular
pages/projects/albums, trends, traffic sources, device/browser
categories, contact conversions and relevant downloads/shares. Exclude
administrator activity. Avoid invasive visitor profiling and unnecessary
personal or sensitive data. Prefer cookieless analytics; obtain consent
for non-essential tracking where required. Provide retention and export
controls.

## 17. Security, reliability and operations

Apply secure authentication, MFA, authorization, validation, output
encoding, CSRF protection, rate limiting, security headers,
dependency/container checks, secret management, audit logging and
security testing. Use centralized exception handling, health checks,
controlled retries, idempotency and graceful degradation.

Provide admin operational visibility for background jobs, email
delivery, storage, cache, backups/restores, logs, maintenance mode,
migrations/deployments and service health. Sensitive operations require
authorization, reauthentication/MFA where appropriate and explicit
confirmation.

## 18. Backup and disaster recovery

Back up SQL metadata and public/private media, including originals and
generated variants. Keep an external copy in a separate failure domain.
Verify backup integrity and restoration. The approved recovery targets
are **RPO 4 hours** and **RTO 4 hours**; the implementation must
demonstrate these targets through testing. A once-daily database backup
alone is insufficient to guarantee a four-hour RPO.

## 19. Quality attributes

-   Accessibility target: WCAG 2.2 AA.
-   Responsive support: mobile, tablet, laptop and desktop.
-   Browser support: current/recent Chrome, Edge, Firefox and Safari,
    including iOS Safari and Android Chrome.
-   Performance: measurable Core Web Vitals and page/API targets to be
    finalized in the technical specification against the actual hosting
    environment.
-   Reliability: health checks, monitoring, retry policies,
    backup/restore tests and documented recovery procedures.
-   Maintainability: modular architecture, automated tests, clear
    documentation and traceability.

## 20. Scope exclusions and future possibilities

Not in initial scope: multi-admin management, public user accounts,
general-purpose SaaS CMS, public likes/ratings, a full blog/newsletter
platform and speculative AI content generation. Future possibilities may
include a blog, newsletter, AI-assisted CMS features and additional
languages. These must not delay the agreed portfolio.

## 21. Success criteria

-   The administrator can manage all agreed dynamic content without
    source-code edits.
-   Visitors can navigate all public pages and project case studies.
-   Draft and private content remain inaccessible publicly.
-   Gallery remains empty until the administrator uploads and publishes
    real photographs.
-   Admin setup can succeed only once and cannot be reopened through
    public routes.
-   Contact messages are retained even if email delivery temporarily
    fails.
-   Private media access is authorized on every request.
-   Backup restoration preserves database/media relationships.
-   Accessibility, security, performance and recovery criteria are
    verified with documented tests.

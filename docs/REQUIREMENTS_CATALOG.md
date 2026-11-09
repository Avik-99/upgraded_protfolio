\# REQUIREMENTS\_CATALOG\_v2.0.md

\## Draft for product-owner review

\### Option A selected

\---

\*\*Project:\*\* Adib Hasan Avik — Personal Portfolio & Travel Gallery

\*\*Document:\*\* Requirements Catalog

\*\*Version:\*\* 2.0

\*\*Status:\*\* Draft — pending cross-document reconciliation and owner approval

\*\*Supersedes:\*\* Requirements Catalog v1.x, after approval

\*\*Authority:\*\* Product requirements baseline, subordinate to recorded product-owner decisions

\*\*Release strategy:\*\* R1 is the first public production release (Option A)

\---

\## 1. Purpose

This document defines the functional and non-functional requirements for the Personal Portfolio & Travel Gallery.

It establishes:

\- What the product must provide.

\- How required behavior will be evaluated.

\- Which product constraints must be preserved.

\- How requirements are identified and traced.

\- Which decisions must be resolved before implementation or release.

The catalog is intended for product planning, architecture, implementation, testing, acceptance, release management and AI-assisted software development.

It is not an implementation guide. Unless a requirement explicitly specifies a technology or constraint, the Technical Specification determines the implementation approach.

\## 2. Product overview

The product is a premium, dynamic, multi-page personal portfolio and travel gallery with two distinct experiences:

1\. \*\*Public Viewer Panel:\*\* presents professional identity, engineering capabilities, projects, achievements, education, certifications, resume, personal/travel photographs and contact information.

2\. \*\*Admin Panel:\*\* provides the portfolio owner with secure control over content, media, publishing, gallery, messages, analytics, website settings, security and operations.

The primary product objective is to communicate practical software engineering capability credibly, while also presenting a professional identity and the ability to independently design and build real-world software products.

The application supports one administrator. It is not a multi-tenant CMS or a public-user platform.

\## 3. Requirement principles

\### 3.1 Stable identifiers

Every requirement has a unique, stable ID.

\- Existing IDs from the previous catalog are preserved.

\- New requirements receive new IDs.

\- Retired requirements must not have their IDs silently reused.

\- Changes to requirement meaning must be recorded in the change history.

\- The Requirements Traceability Matrix (RTM) must use the exact IDs in this document.

\### 3.2 Acceptance criteria

Acceptance criteria describe observable outcomes.

They should be:

\- Testable.

\- Unambiguous.

\- Verifiable through inspection, demonstration, analysis or testing.

\- Independent of implementation details unless a technical constraint is explicitly required.

\### 3.3 Requirement versus implementation

For example:

\- \*\*Requirement:\*\* private media must not be accessible to unauthorized visitors.

\- \*\*Implementation:\*\* private files are stored outside wwwroot and delivered through an authorized endpoint.

The first belongs in this catalog. The second belongs in the Technical Specification because the current PRD explicitly establishes that storage constraint.

\### 3.4 Requirement status

The following statuses are used in document review and traceability:

| Status | Meaning |

|---|---|

| Proposed | Added to the v2.0 draft; awaiting owner approval. |

| Approved | Explicitly accepted by the product owner. |

| Clarification required | The intended outcome is known, but a decision or measurable value is missing. |

| Deferred | Accepted product scope, assigned to a later release. |

| Rejected | Explicitly excluded by the product owner. |

| Verified | Acceptance criteria passed with recorded evidence. |

A requirement must not be marked Verified merely because its code exists.

\### 3.5 Requirement categories

The catalog is organized into:

1\. Product and public experience

2\. Content and publishing

3\. Identity and administration

4\. Admin experience and website management

5\. Media Library

6\. Gallery

7\. Contact and email

8\. Resume and multilingual

9\. Analytics and privacy

10\. Operations and deployment

11\. Security

12\. Non-functional requirements

\## 4. Product boundaries and constraints

The following are confirmed product boundaries from the PRD:

\- One administrator: the portfolio owner.

\- No public administrator registration.

\- No multi-administrator functionality.

\- No public visitor accounts or profiles.

\- No general-purpose multi-tenant CMS/SaaS functionality.

\- No public likes, ratings or social-network features.

\- No unrestricted visual page builder.

\- No full blog/newsletter unless separately approved.

\- No automatic publication of stock, generated, placeholder or reference photographs as real personal/travel content.

\- The administrator supplies and selects the actual photographs.

\- The Gallery must display an empty state until real photographs are uploaded and published.

\- Public content and Admin Panel functionality must remain separated by server-enforced authorization.

These boundaries are not invitations to add adjacent features without approval.

\## 5. Functional requirements

\### 5.1 Product and public experience

| ID | Requirement | Acceptance criteria |

|---|---|---|

| PR-001 | Provide a premium, multi-page portfolio. | Every agreed public page has a distinct route, responsive layout and navigation entry. The agreed page inventory is Home, About, Education, Skills, Projects, Achievements, Certifications, Personal/Travel Gallery, Resume and Contact. |

| PR-002 | Communicate practical engineering capability credibly. | Project and skill claims are evidence-backed; unsupported claims and fabricated metrics are absent. Completed, in-progress and planned projects are clearly distinguished. |

| PR-003 | Provide global public search. | Search covers published, eligible public Projects, Skills, Achievements, Certifications and Education. Results are grouped by relevant content type and link to appropriate public pages. Draft, private, unpublished and ineligible unlisted content is excluded. |

| PR-004 | Provide accessible public navigation. | Keyboard users can reach all navigation items; current page and focus state are perceivable. |

| PR-005 | Support dark and light themes. | Theme preference can be changed and persisted. On first visit, the theme follows the system preference unless an approved product default is explicitly selected. |

| PR-006 | Support reduced motion. | Motion-sensitive preference disables or reduces non-essential animation. |

| PR-007 | Provide project browsing controls. | Visitors can browse projects in a unified listing, distinguish completed, in-progress and planned projects, and use the agreed project status filters and sorting. Featured projects receive the agreed prominent placement. |

| PR-008 | Provide search-engine metadata for public pages. | Eligible published public pages provide appropriate page titles, descriptions, canonical URLs and indexability directives. Draft, private and unpublished content is not exposed through search metadata or indexing. |

| PR-009 | Provide responsive public content presentation. | Public content remains readable and usable across the agreed desktop, tablet and mobile viewport matrix without unintended horizontal overflow or loss of essential functionality. |

\### 5.2 Content and publishing

| ID | Requirement | Acceptance criteria |

|---|---|---|

| CT-001 | Manage profile, experience, education, skills, projects, achievements and certifications. | Admin can create, view, edit, publish and unpublish each supported content type. Ordinary content management does not require source-code edits. |

| CT-002 | Separate draft edits from published content. | Editing a published item does not change public output until the publish action succeeds. |

| CT-003 | Preview content before publication. | Preview is authenticated and does not expose drafts through public routes. |

| CT-004 | Support project status and case-study sections. | Completed, in-progress and planned statuses are distinct; unsupported case-study sections can be omitted. |

| CT-005 | Support rich long-form content. | Editor supports headings, paragraphs, lists, links, images and code snippets with safe rendering. |

| CT-006 | Support scheduled publishing where appropriate. | Scheduled job publishes only eligible content at the configured time and records the outcome. Failed or missed publication attempts are observable and safely retryable. |

\### 5.3 Identity and administration

| ID | Requirement | Acceptance criteria |

|---|---|---|

| ID-001 | Enforce a single administrator. | System cannot create or assign a second Admin account through public or ordinary admin workflows. |

| ID-002 | Provide a one-time Setup Wizard. | Setup is available only when no admin exists and is disabled atomically after success. Concurrent setup attempts cannot create multiple administrators. |

| ID-003 | Use Identity for credential handling. | Passwords are hashed by the configured Identity password hasher; plaintext passwords are never persisted or logged. |

| ID-004 | Require MFA for admin access. | Authenticator TOTP is enrolled and verified; recovery codes are generated and stored safely. Admin access cannot bypass required MFA. |

| ID-005 | Provide secure password reset. | Reset uses time-limited, single-use Identity tokens and generic responses that do not reveal account existence. Abuse controls are applied. |

| ID-006 | Protect all admin operations. | Every admin route/action and private resource applies server-side authorization. Hiding a UI element is not considered authorization. |

| ID-007 | Record security and administrative activity. | Important actions and security events are searchable in protected audit history. Sensitive credentials, tokens and authentication secrets are never recorded. |

\### 5.4 Admin experience and website management

The PRD explicitly defines an Admin dashboard and management modules beyond authentication. These requirements make that scope independently verifiable.

| ID | Requirement | Acceptance criteria |

|---|---|---|

| AD-001 | Provide an administrative dashboard. | Authorized administrator can access a dashboard that summarizes relevant content activity, messages, publishing activity and operational status through appropriate links to management modules. |

| AD-002 | Provide complete content-management navigation. | Admin can access the agreed management areas for Profile, Experience, Education, Skills, Projects, Achievements, Certifications, Media Library, Resume, Gallery, Contact Messages, Comment Moderation, Website Settings, Analytics, Security & Activity, and Operations & Backups. |

| AD-003 | Support English and Bangla Admin interface language. | Administrator can use the Admin Panel in English or Bangla independently of the selected public website language. Interface language preference is persisted. Changing one preference does not unexpectedly change the other (merged from RE-010; see `REQUIREMENTS_ALIAS_ANNEX.md`). |

| AD-004 | Provide website settings management. | Authorized administrator can manage the agreed configurable website settings without source-code edits. Settings changes are validated, protected and auditable. |

| AD-005 | Provide management of legal and privacy information. | Public Privacy Policy, Terms and Cookie Policy are available with content that accurately describes the product's applicable data, attachment, analytics and retention practices. Publication and updates are controlled. |

| AD-006 | Provide safe administrative content operations. | Admin create, update, publish, unpublish, archive and delete actions provide appropriate validation, confirmation and feedback. Destructive operations cannot silently bypass dependent records or media references. Unsaved-change warnings and destructive-action confirmation apply to shipped admin workflows (carried from legacy FR-ADM-008; see `REQUIREMENTS_ALIAS_ANNEX.md`). |

\### 5.5 Media Library

| ID | Requirement | Acceptance criteria |

|---|---|---|

| ML-001 | Provide a categorized reusable Media Library. | Assets can be searched, filtered, previewed and reused across supported content modules. Categories include Profile & Personal Images, Project Images & Screenshots, Education & Certificates, Achievement Images, Resume & Documents, Personal/Travel Gallery and Other Assets. |

| ML-002 | Support public and private storage. | Public assets are served publicly; private assets are outside wwwroot and require authorization. |

| ML-003 | Validate uploaded files server-side. | Extension, signature/content, size and structural checks reject invalid files. Validation does not rely solely on browser-supplied MIME types or filenames. |

| ML-004 | Scan uploads before use. | Files remain quarantined until the scanner reports clean; scanner outage never counts as clean. |

| ML-005 | Preserve originals and create optimized variants. | Original remains retrievable; generated variants are linked and processing status is visible. |

| ML-006 | Track asset usage. | Admin can see all content references before replacing or deleting an asset. |

| ML-007 | Prevent broken references. | Referenced assets cannot be permanently deleted until references are safely removed or replaced. |

| ML-008 | Support recycle bin and restoration. | Deleted assets can be restored during retention; purge rechecks references. |

| ML-009 | Detect duplicate content. | Server-side SHA-256 detects identical bytes and offers safe reuse without crossing privacy boundaries. |

| ML-010 | Enforce quotas. | Global, public/private and per-file limits are enforced server-side under concurrent uploads. |

| ML-011 | Support persistent, portable storage. | Local storage survives container replacement through mounted persistent storage; storage is abstracted. |

| ML-012 | Record Media Library activity. | Upload, replacement, metadata change, visibility change, restoration, deletion and permanent purge actions are recorded in protected audit history with actor, timestamp, action and affected asset. |

| ML-013 | Support safe bulk media upload. | Authorized administrator can upload multiple files through a controlled workflow. Each file independently passes validation, quarantine/scanning and processing; partial failures are reported without treating failed files as successful. |

| ML-014 | Support media metadata management. | Admin can manage applicable asset metadata, including title, alternative text, description, category and other supported fields. Metadata changes do not bypass publication or privacy controls. |

\### 5.6 Gallery

| ID | Requirement | Acceptance criteria |

|---|---|---|

| GA-001 | Provide a dedicated Gallery separate from Projects. | Gallery landing, album and photo views have stable public routes. |

| GA-002 | Use administrator-uploaded photographs only. | No placeholder, generated, stock or reference image is published automatically; empty state appears before upload. |

| GA-003 | Manage albums and photos. | Admin can create albums, upload photos, choose cover/featured images, add metadata and reorder. Album editing supports the defined album fields including optional destination and travel-range metadata (Page Design Specification §8.3); destination metadata is album-level only — no photo-level destination fields are currently defined. |

| GA-004 | Support public, unlisted and private visibility. | Public content is listed; unlisted content is direct-link only and excluded from public listings, search and indexing; private content is admin-only. |

| GA-005 | Support individual photo publication controls. | Unpublished photos are inaccessible publicly even when the album is published. |

| GA-006 | Provide gallery browsing and lightbox. | Search/filter, previous/next, keyboard navigation and mobile swipe work accessibly. |

| GA-007 | Control original downloads. | Global, album and photo settings are enforced server-side for eligible published content. |

| GA-008 | Moderate comments. | Comments are disabled by default; when enabled, they require admin approval before public display. |

| GA-009 | Provide Gallery SEO. | Only eligible published public content appears in sitemap and indexable metadata. |

| GA-010 | Include Gallery in backup and restore. | Restored albums retain photo relationships, metadata and required file variants. |

| GA-011 | Support Gallery metadata-based discovery. | Visitors can search and filter eligible published Gallery content using configured metadata such as destination, date, category, collection and tags. |

| GA-012 | Support related photographs and albums. | Eligible public photo and album pages can present relevant related content without exposing unpublished, private or otherwise ineligible items. |

| GA-013 | Provide shareable Gallery URLs. | Published eligible albums and photographs have stable shareable URLs. Unlisted URLs are not included in public discovery or indexing. Private and unpublished content cannot be made public through sharing controls. |

| GA-014 | Support Gallery presentation options. | Gallery can present photographs using the configured masonry or uniform-grid display options. Admin-configured presentation settings are applied consistently to eligible public content. |

| GA-015 | Support independent album and photograph settings. | Admin can manage album and individual-photo publication, visibility, metadata, download and applicable sharing/comment settings. Parent album access rules remain enforced. |

\### 5.7 Contact and email

| ID | Requirement | Acceptance criteria |

|---|---|---|

| CO-001 | Provide a validated contact form. | Required fields, category and server validation are enforced; spam protection is active. Categories include Job Opportunity, Project Collaboration, Technical Discussion and General Inquiry. |

| CO-002 | Persist messages before sending email. | A Mailtrap or other configured email-provider outage does not lose the submitted message. |

| CO-003 | Track email delivery independently. | Visitor confirmation and admin notification have separate delivery states and retry behavior. |

| CO-004 | Provide conversation management. | Admin can view threads, reply, add internal notes, search, filter and archive. |

| CO-005 | Support secure optional attachments. | Only approved formats are accepted; files are private and served through authorized endpoints. Actual file content is validated and uploads are scanned before use. |

| CO-006 | Apply configurable retention and deletion. | Active conversations are not silently auto-deleted; permanent deletion is confirmed and audited. |

| CO-007 | Enforce the approved contact attachment policy. | The initial policy allows a maximum of 3 attachments per message, 5 MB per file and 15 MB total. Allowed formats are PDF, JPG, JPEG and PNG. Limits are configurable and enforced server-side. |

| CO-008 | Provide reliable contact reply handling. | Admin replies are associated with the correct conversation, delivery outcomes are recorded, and retry behavior does not create duplicate replies or duplicate conversation records. |

\### 5.8 Resume and multilingual

| ID | Requirement | Acceptance criteria |

|---|---|---|

| RE-001 | Manage multiple resume versions. | Admin can upload, label, publish and unpublish language/professional variants. |

| RE-002 | Restrict public resume access to published versions. | Draft and previous unpublished versions are inaccessible to visitors. |

| RE-003 | Support English and Bangla public content. | Language-prefixed routes and language-specific content/SEO are available. |

| RE-004 | Apply safe language fallback. | Selected language is preferred; English fallback never exposes unpublished content. |

| RE-005 | Manage translations independently. | Translation completion, preview and per-language publication are available. |

| RE-006 | Implement multilingual SEO. | Canonical, hreflang, translated metadata and sitemap entries reflect published pages only. |

| RE-007 | Support a default public resume. | Admin can select one eligible published resume as the default. Only a published version can be selected as the public default. |

| RE-008 | Preserve resume version history. | Admin can distinguish current, previous, draft and unpublished resume versions. Updating a resume does not silently expose an unpublished version. Scope limit: version distinguishability only — not a version-control system (no snapshots, diffing or restore-to-point). Retention depth of historical versions is an unresolved owner decision (Catalog §12 DEC-013). |

| RE-009 | Provide stable public resume access. | Published resumes can be previewed and downloaded through stable public access routes. Unpublished versions remain inaccessible. |

| RE-010 | `(merged into AD-003 per approved reconciliation decision D3 — alias retained in REQUIREMENTS_ALIAS_ANNEX.md)` | — |

| RE-011 | Apply language-selection preference rules. | Returning visitor preference is respected. For a new visitor, browser language may suggest English or Bangla. Unsupported languages fall back to English. Manual selection remains available and persists. |

| RE-012 | Preserve page context during language switching. | When an equivalent translated page exists, switching language opens that equivalent page. Otherwise, the visitor is routed to the selected-language homepage. |

\### 5.9 Analytics and privacy

| ID | Requirement | Acceptance criteria |

|---|---|---|

| AN-001 | Provide aggregated analytics. | Admin can view trends and popular content over selectable periods without invasive visitor profiling. |

| AN-002 | Exclude administrator activity. | Admin sessions/actions do not inflate public visitor metrics. |

| AN-003 | Provide consent and privacy controls. | Non-essential tracking follows applicable consent requirements; preferences can be changed. |

| AN-004 | Provide defined portfolio analytics metrics. | Analytics can report agreed aggregate measures including visitors/page views, trends, popular pages/projects/albums/photographs, referrals, device/browser categories and navigation patterns. |

| AN-005 | Provide contact and resume analytics. | Admin can view aggregate contact conversions and published resume download activity without exposing unnecessary personal visitor information. |

| AN-006 | Provide Gallery interaction analytics. | Admin can view aggregate Gallery sharing and permitted download interactions. |

| AN-007 | Support analytics report export. | Authorized admin can export supported aggregated analytics reports for selected periods. Exported reports must not expose unnecessary personal or sensitive visitor data. |

| AN-008 | Apply analytics retention controls. | Analytics data follows the configured retention policy. Retention and deletion behavior is documented and consistent with the published privacy disclosures. |

| AN-009 | Support date comparisons and reporting periods. | Admin can select reporting periods and compare supported aggregate metrics across date ranges. Status: **Should priority; proposed R2 allocation; activation requires explicit product-owner approval before P20/P21 scope lock.** PRD §16 commits to "trends" only; the comparison capability is a catalog refinement pending owner confirmation. |

| AN-010 | Prefer privacy-conscious analytics collection. | Analytics avoids unnecessary personal/sensitive data and invasive profiling. Cookieless analytics is preferred where it satisfies the product's measurement needs and applicable requirements. |

\### 5.10 Operations and deployment

| ID | Requirement | Acceptance criteria |

|---|---|---|

| OP-001 | Provide operational dashboard. | Health, jobs, email, storage, cache, logs and backup state are visible to authorized admin. |

| OP-002 | Support controlled maintenance mode. | Admin can enable a visitor-facing maintenance page and safely restore normal operation. |

| OP-003 | Provide backup and restore workflows. | Backups include database and media; restore requires authorization, reauthentication and confirmation. |

| OP-004 | Meet RPO/RTO targets. | Tested recovery demonstrates RPO ≤4 hours and RTO ≤4 hours under documented test conditions. |

| OP-005 | Support deployment environments. | Development, staging and production have separate configuration and controlled migrations. |

| OP-006 | Provide deployment and rollback controls. | Production deployments follow a controlled process with build/test verification, deployment approval, health checks and a documented rollback or recovery procedure appropriate to the hosting platform. |

| OP-007 | Support external backup protection. | Backup copies are stored separately from the primary application/database environment. Backup integrity can be checked and restoration can be performed independently of the primary deployment. |

| OP-008 | Provide production domain and HTTPS readiness. | Production uses the approved canonical domain, HTTPS, HTTP-to-HTTPS redirection, a consistent www/non-www policy, valid certificate management and correct canonical URLs. |

| OP-009 | Support deployment automation. | Build, test, dependency/security checks and deployment steps can be executed through a controlled repeatable pipeline appropriate to the selected hosting platform. |

| OP-010 | Monitor production health and domain operations. | Relevant application health, certificate status and domain-expiry risks can be monitored or surfaced through the approved operational process. |

\### 5.11 Security

| ID | Requirement | Acceptance criteria |

|---|---|---|

| SEC-001 | Protect authentication and session handling. | Secure cookie/session settings, lockout or rate limiting, session revocation where required, and protection against common authentication abuse are enforced. |

| SEC-002 | Protect state-changing requests. | State-changing operations are protected against cross-site request forgery, and user-controlled content is safely validated, encoded or sanitized according to context. |

| SEC-003 | Apply security response protections. | Production applies appropriate security headers and content security policy controls. Configuration is tested against required public and administrative functionality. |

| SEC-004 | Protect secrets and sensitive configuration. | Passwords, connection strings, API keys, email credentials, tokens and other secrets are not committed to source control or exposed in logs or public responses. |

| SEC-005 | Apply dependency and container security checks. | Application dependencies and deployment/container artifacts are checked for known vulnerabilities through the agreed development and release process. |

| SEC-006 | Apply protected-form abuse controls. | Protected public forms use the approved spam/risk controls, including the configured reCAPTCHA integration where applicable, together with server-side validation and rate limiting. |

| SEC-007 | Protect private documents and media. | Private media, resumes where configured as private, contact attachments and unpublished assets cannot be retrieved through public static paths or unauthorized direct requests. |

| SEC-008 | Protect sensitive administrative actions. | Sensitive administrative actions require appropriate authorization and, where configured, recent authentication or MFA confirmation. |

| SEC-009 | Publish privacy and legal disclosures. | Privacy Policy, Terms and Cookie Policy accurately describe applicable collection, analytics, contact attachment and retention practices. |

\### 5.12 Non-functional requirements

| ID | Requirement | Acceptance criteria |

|---|---|---|

| NFR-001 | Accessibility target WCAG 2.2 AA. | Automated checks and manual keyboard/screen-reader review cover critical journeys. |

| NFR-002 | Responsive and cross-browser support. | Supported viewport/browser matrix passes agreed regression tests. |

| NFR-003 | Performance. | Core Web Vitals and server/API budgets are defined against target hosting and verified before release. |

| NFR-004 | Security. | Threat-informed security tests cover authentication, authorization, upload, input, session and private media. |

| NFR-005 | Reliability. | Health checks, retries, idempotency, logging and failure recovery are tested. |

| NFR-006 | Maintainability. | Architecture boundaries, coding standards, tests and documentation are maintained. |

| NFR-007 | Data integrity. | Database/media references remain consistent through publish, delete, backup and restore workflows. |

\## 6. Cross-cutting acceptance rules

The following rules apply across multiple requirements. They are mandatory interpretation rules, not optional implementation suggestions.

\### 6.1 Publication and content visibility

A record being stored in the database does not make it publicly accessible.

| Content state | Public listing | Direct public URL | Admin preview |

|---|---|---|---|

| Draft | No | No | Yes, authenticated |

| Published and public | Yes | Yes | Yes |

| Published and unlisted | No | Yes, if eligible | Yes |

| Private | No | No | Yes, authorized |

| Unpublished | No | No | Yes, authenticated |

Unlisted access is not confidentiality. Anyone possessing an unlisted URL may be able to view its eligible content.

\### 6.2 Gallery visibility inheritance

Gallery visibility must be enforced consistently.

\- An unpublished photograph must never become public because its album is published.

\- A private album must not expose its photographs publicly.

\- An unlisted album must not appear in public Gallery listings, global search or sitemap.

\- A public photograph must still satisfy its parent album's access and publication rules.

\- Thumbnails, optimized variants, original files and direct asset URLs must follow the same access policy.

\- Cache entries must not allow private or unpublished content to leak after a visibility or publication change.

\### 6.3 Media security and integrity

\- File validation must be server-side.

\- A scanner outage must not be interpreted as a clean result.

\- Quarantined files must not be publicly accessible.

\- Original files must remain protected from unintended modification during processing.

\- Duplicate detection must not disclose the existence of private assets to unauthorized users.

\- Permanent deletion must recheck references.

\- Database records and media files must remain consistent through backup, restoration and deletion.

\### 6.4 Contact message integrity

\- Persist a contact message before attempting external email delivery.

\- Visitor confirmation and administrator notification are separate delivery processes.

\- Email failure must not erase or invalidate a successfully stored message.

\- Retries must be safe and must not create duplicate messages or replies.

\- Private attachments must remain protected independently of the message's public confirmation response.

\### 6.5 Resume and language integrity

\- Only published resume versions are publicly accessible.

\- A draft or unpublished translation must never be exposed through language fallback.

\- Public language selection and Admin interface language selection are independent.

\- Language-specific canonical URLs, hreflang and sitemap entries must reflect eligible published content only.

\### 6.6 Analytics and privacy

\- Administrator activity is excluded from public visitor analytics.

\- Analytics must not collect unnecessary personal or sensitive information.

\- Non-essential tracking follows applicable consent requirements.

\- Report exports must follow the same privacy and retention rules as the analytics interface.

\- Privacy disclosures must reflect the actual implementation.

\### 6.7 Security and authorization

\- Authorization is enforced server-side.

\- Hiding navigation items is not an authorization mechanism.

\- Private resources must be protected at the resource-access boundary.

\- Sensitive credentials, tokens, MFA codes, recovery codes and session secrets must not appear in logs.

\- Administrative and security audit records must themselves be protected from unauthorized access or modification.

\### 6.8 Admin collection ergonomics

Carried verbatim from legacy FR-ADM-007/FR-ADM-008 during the approved reconciliation (see `REQUIREMENTS_ALIAS_ANNEX.md`):

- Search/filter/sort/pagination must be predictable wherever an admin collection is delivered (applies to Skills, Projects, Achievements, Certifications, Media Library, Contact inbox and other list views).
- Unsaved-change warnings and destructive-action confirmation apply to shipped admin workflows.

\## 7. Configurable values and decisions requiring confirmation

The requirements establish expected behavior. They do not authorize arbitrary technical values.

The following decisions must be recorded in the appropriate supporting document before the affected functionality is considered fully specified.

| ID | Decision or configuration | Current position | Required resolution |

|---|---|---|---|

| NFR-002 | Minimum supported browser versions | Current/recent browser support established | Approve exact minimum versions and test matrix. |

| NFR-003 | Core Web Vitals and server/API budgets | Hosting-dependent | Define numeric budgets after target hosting and representative content are known. |

| ML-003 | General Media Library allowed file types and size limits | Server-side validation required | Define allowed formats and configurable size limits by category. |

| ML-010 | Global, public/private and per-file quotas | Quotas required | Define numeric quota values and concurrent-upload behavior. |

| CO-006 | Contact conversation retention | Configurable retention required | Define retention periods, legal exceptions and deletion process. |

| CO-007 | Contact attachment limits | Initial values specified in CO-007 | Confirm whether the initial limits remain the final production policy. |

| AN-008 | Analytics retention | Configurable retention required | Define retention period and deletion policy. |

| OP-004 | RPO/RTO | Four hours each | Validate feasibility through documented recovery tests. |

| OP-008 | Production domain and provider | Not yet finalized | Confirm canonical domain, hosting and certificate-management arrangements. |

| SEC-003 | Security headers/CSP | Required | Define policy in the Technical Specification and validate it against the deployed application. |

| AD-004 | Configurable website settings | Agreed settings are not fully enumerated | Define the complete settings inventory and identify which settings may be changed by the administrator. |

\### 7.1 Important interpretation of unresolved values

An unresolved configuration value does not make its parent requirement optional.

For example, NFR-003 remains mandatory even though its numeric budgets are pending. The budget must be established before release acceptance; it must not be silently omitted.

Likewise, OP-004 remains a four-hour recovery commitment. If the hosting environment cannot meet that commitment, the product owner must explicitly approve a change rather than the engineering team silently lowering the target.

\## 8. Requirement prioritization and release allocation

The catalog establishes the product requirements. The Scope and Release Management document owns release allocation.

The following rules apply:

1\. Every approved requirement must receive a release target in the Scope and Releases document.

2\. A requirement may be delivered incrementally only when its release-specific acceptance conditions are explicitly documented.

3\. A requirement must not be marked fully delivered when only a partial implementation exists.

4\. Essential security, privacy, data integrity and authorization protections cannot be postponed merely because advanced features are assigned to a later release.

5\. R1 is the first public production release, not an untested prototype.

6\. All release gates must be satisfied before production launch.

\### 8.1 Release definitions

| Release | Purpose |

|---|---|

| R1 — Professional Foundation | First public production release with a secure, complete and usable foundation. |

| R2 — Advanced Platform | Advanced content, Gallery, analytics, multilingual and administrative capabilities assigned to this release. |

| R3 — Production Excellence | Further reliability, recovery, security, performance, accessibility and operational maturity. |

The detailed requirement-to-release matrix belongs in SCOPE\_AND\_RELEASES.md, not in this catalog.

\### 8.2 Priority definitions

The following priority model should be used in the RTM and release planning:

| Priority | Meaning |

|---|---|

| Must | Required for the agreed product outcome or release acceptance. |

| Should | Important and expected, but may be sequenced after higher-priority commitments with explicit approval. |

| Could | Useful enhancement that is not necessary for the current release's core outcome. |

Priority assignments must be reviewed against product value, risk, dependencies and release commitments. They must not be inferred solely from the order of requirement IDs.

\## 9. Verification and evidence

Each requirement must be connected to one or more verification methods.

| Verification method | Purpose |

|---|---|

| Inspection | Review configuration, documentation, architecture or implementation artifacts. |

| Demonstration | Observe the feature working through its intended interface. |

| Analysis | Evaluate measurable results, logs, reports, performance or recovery calculations. |

| Test | Execute repeatable test cases against defined expected results. |

\### 9.1 Minimum evidence requirements

Every requirement marked Verified must have:

\- Requirement ID.

\- Test-case ID or inspection reference.

\- Environment.

\- Application build/version.

\- Test data or setup where applicable.

\- Expected result.

\- Actual result.

\- Pass/fail outcome.

\- Evidence reference, such as a test report, screenshot or log.

\- Defect reference where a test fails.

\- Verification date.

\### 9.2 Security and privacy verification

Security and privacy requirements must include negative testing.

Examples:

\- An anonymous visitor cannot access private media.

\- A published album cannot expose an unpublished photograph.

\- A public search query cannot return draft content.

\- A failed scanner cannot allow an upload to become available.

\- A second administrator cannot be created through ordinary workflows.

\- A private attachment cannot be retrieved using an unauthorized direct URL.

\### 9.3 Recovery verification

OP-003, OP-004, GA-010 and NFR-007 must be verified together where their behaviors overlap.

A successful backup operation alone is not proof of successful recovery.

Recovery evidence must establish that the database, media files, metadata, variants and relationships are restored consistently under documented conditions.

\## 10. Traceability and document relationships

This catalog is part of a coordinated requirements and engineering documentation set.

| Document | Responsibility | Relationship to this catalog |

|---|---|---|

| PRD | Product vision, users, outcomes and scope | Source of product commitments. |

| Requirements Catalog | Stable requirements and acceptance criteria | Defines what must be delivered and verified. |

| Scope and Releases | Release boundaries and sequencing | Assigns requirements to R1, R2 and R3. |

| ADD | Architectural design and boundaries | Describes the architectural structure supporting requirements. |

| Technical Specification | Frameworks, libraries, providers, configuration and implementation decisions | Defines how approved outcomes will be implemented. |

| Testing Strategy | Testing approach and quality gates | Defines how requirements are verified. |

| Requirements Traceability Matrix | Requirement-to-design, implementation, test and evidence mapping | Tracks every requirement through delivery. |

| Implementation Plan | Engineering work packages and sequencing | Converts approved scope into implementation tasks. |

\### 10.1 Traceability rules

\- Every approved catalog requirement must appear in the RTM.

\- Every RTM requirement ID must exist in this catalog.

\- Every requirement must map to an appropriate release or have a documented allocation decision pending.

\- Every requirement must map to verification evidence before being marked Verified.

\- Technical implementation decisions must reference the requirements they support.

\- Test cases must reference the exact requirement IDs they verify.

\- Changes to requirements must trigger review of affected scope, architecture, implementation, testing and release documentation.

\### 10.2 Legacy traceability documents

The previous traceability version was built against an older catalog containing 78 requirements.

It is not the authoritative traceability baseline for this version.

It must be rebuilt against the approved v2.0 catalog. Old requirement mappings must not be copied forward without validating their IDs and meaning.

\## 11. Change control

Requirements may change as the product becomes more precisely defined. Changes must be controlled rather than silently introduced.

\### 11.1 Change procedure

1\. Identify the proposed change.

2\. Explain the reason and expected product benefit.

3\. Identify affected requirement IDs.

4\. Assess effects on scope, releases, architecture, security, data, testing and deployment.

5\. Obtain product-owner approval.

6\. Update the catalog and relevant supporting documents.

7\. Update the RTM and test coverage.

8\. Record the change in the document history.

\### 11.2 Change impact categories

| Change type | Example | Required review |

|---|---|---|

| Clarification | Improve ambiguous acceptance wording without changing intended behavior | Requirement and test review |

| Addition | Introduce a newly confirmed product capability | Scope, architecture and release review |

| Modification | Change an existing acceptance criterion | Requirement, RTM and test review |

| Deferral | Move an approved requirement to a later release | Scope and release approval |

| Removal | Remove an approved product commitment | Explicit owner approval and impact review |

| Technical change | Replace a storage or email provider | Technical Specification and regression review |

\### 11.3 Versioning

\- Major version: substantial change to product scope or requirement meaning.

\- Minor version: approved additions or meaningful refinements that preserve the overall product baseline.

\- Patch revision: corrections to formatting, spelling or non-semantic wording.

Requirement IDs remain stable through ordinary revisions.

\## 12. Open decisions and approval register

The following items require confirmation or completion before the catalog can be treated as a fully baselined implementation reference.

| ID | Decision | Current status |

|---|---|---|

| DEC-001 | Confirm the complete public page inventory against the PRD. | PRD inventory documented; owner review required. |

| DEC-002 | Confirm the complete Admin Panel settings inventory. | Clarification required. |

| DEC-003 | Approve browser and viewport support matrix. | Pending technical validation. |

| DEC-004 | Approve performance budgets. | Hosting-dependent; pending. |

| DEC-005 | Approve general Media Library file types and quotas. | Pending configuration decision. |

| DEC-006 | Approve contact retention periods. | Pending owner decision. |

| DEC-007 | Approve analytics retention period. | Pending owner decision. |

| DEC-008 | Validate four-hour RPO/RTO against the chosen hosting and backup architecture. | Mandatory validation. |

| DEC-009 | Confirm production domain and hosting provider. | Pending deployment decision. |

| DEC-010 | Confirm final security-header and CSP policy. | Technical Specification decision. |

| DEC-011 | Confirm release allocation for all requirements. | To be completed in Scope and Releases. |

| DEC-012 | Confirm all newly introduced v2.0 requirements as part of the approved product baseline. | Pending owner review. |
| DEC-013 | Confirm resume version retention depth for RE-008 (how many historical resume versions are retained beyond the current/previous/draft/unpublished distinction). Recorded as an unresolved owner decision per the approved reconciliation; RE-008 is not approved as unrestricted version history. | Pending owner decision. |

\### 12.1 Approval conditions

This document should be approved only after:

\- All confirmed PRD commitments are represented.

\- Legacy identifier continuity is preserved through `REQUIREMENTS_ALIAS_ANNEX.md`; the earlier "67 retained / 46 new" split of this draft could not be verified against a retained v1 source and is superseded by the verified reconciliation (see §14).

\- New requirements are reviewed for duplication and scope accuracy.

\- Acceptance criteria are sufficiently testable.

\- Open decisions are either resolved or explicitly accepted as pending.

\- Scope and Release Management is reconciled with the catalog.

\- The RTM is rebuilt against the final requirement inventory.

\- Testing Strategy coverage is mapped to the catalog.

\## 13. Document control and revision history

| Version | Date | Description | Status |

|---|---|---|---|

| 1.x | Previous | Original Requirements Catalog containing 67 requirements | Superseded after v2.0 approval |

| 2.0 | 8 November 2026 | Expanded catalog, clarified acceptance criteria and incorporated confirmed PRD commitments | Draft for owner review |
| 2.0-r1 | 8 November 2026 | Approved reconciliation edits (decisions D1–D6, owner-conditioned): RE-010 merged into AD-003 (112-ID baseline); RE-008 bounded to version distinguishability with retention depth unresolved (DEC-013); AN-009 marked Should/R2 owner-gated; legacy FR-ADM-007/FR-ADM-008/FR-GAL-003/FR-GAL-018 wording carried into acceptance criteria and §6.8; legacy identifiers preserved as aliases in `REQUIREMENTS_ALIAS_ANNEX.md`. Document status remains draft — pending owner approval. | Draft for owner review |

\*\*Document owner:\*\* Portfolio owner / single administrator

\*\*Approval authority:\*\* Product owner

\*\*Next review:\*\* Before final Scope and Release Management approval

\## 14. Requirement inventory summary

The upgraded catalog contains the following proposed inventory:

| Category | Existing IDs retained | New IDs | Total |

|---|---|---|---|

| Product and public experience | 6 | 3 | 9 |

| Content and publishing | 6 | 0 | 6 |

| Identity and administration | 7 | 0 | 7 |

| Admin experience and website management | 0 | 6 | 6 |

| Media Library | 11 | 3 | 14 |

| Gallery | 10 | 5 | 15 |

| Contact and email | 6 | 2 | 8 |

| Resume and multilingual | 6 | 5 | 11 |

| Analytics and privacy | 3 | 7 | 10 |

| Operations and deployment | 5 | 5 | 10 |

| Security | 0 | 9 | 9 |

| Non-functional requirements | 7 | 0 | 7 |

| \*\*Total\*\* | \*\*67\*\* | \*\*45\*\* | \*\*112\*\* |

67 original IDs preserved (per the v2.0 draft's own inventory; continuity of legacy identifiers is maintained through `REQUIREMENTS_ALIAS_ANNEX.md`).

45 proposed additions (39 catalog-only IDs verified during the approved reconciliation, minus RE-010 merged into AD-003).

\*\*Reconciliation note (8 November 2026):\*\* The inventory was verified section-by-section against §5 (113 IDs before the approved D3 merge). RE-010 was merged into AD-003, yielding the approved 112-ID canonical baseline. The final wording and status of the 38 retained additions remain subject to owner ratification at v2.0 approval (DEC-012). Legacy identifiers are retired as aliases only; see `REQUIREMENTS_ALIAS_ANNEX.md`.

\*\*Important:\*\* The 46 new requirements are proposed additions based on the PRD. They are not automatically approved merely because Option A was selected. The complete v2.0 document remains subject to your review and approval.

A few additions overlap with existing requirements—for example, responsive presentation and cross-browser support, or Admin navigation and content-management access. I have kept their purposes distinguishable in this draft, but they should be checked when the RTM is built to avoid duplicate test coverage.
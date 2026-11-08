DESIGN\_SYSTEM
==============

**Project:** Adib Hasan Avik — Personal Portfolio & Travel Gallery**Document:** Design System**Version:** 2.0**Status:** Comprehensive review draft — pending product-owner approval**Design direction:** Executive Dark**Frontend foundation:** Bootstrap 5 + custom CSS design system**Primary languages:** English and Bangla**Accessibility target:** WCAG 2.2 Level AA**Related documents:** PRD, REQUIREMENTS\_CATALOG, ADD, TECHNICAL\_SPEC, PAGE\_DESIGN\_SPECIFICATION, TESTING\_STRATEGY

1\. Purpose and authority
=========================

1.1 Purpose
-----------

This document defines the shared visual language, design tokens, component standards, interaction patterns, responsive behavior, accessibility rules, and visual quality expectations for the Personal Portfolio & Travel Gallery.

Its purpose is to ensure that the public portfolio and protected Admin Panel feel like parts of one professionally designed product.

The Design System must provide a consistent foundation without forcing every page into an identical layout.

It is intended for:

*   Product owner and design reviewers.
    
*   Frontend and full-stack developers.
    
*   AI-assisted coding agents.
    
*   UI implementation and quality-assurance activities.
    
*   Future maintenance and visual improvements.
    

1.2 Authority
-------------

The Design System is the authoritative reference for shared visual and interaction rules.

It works alongside the other project documents:

DocumentResponsibilityPRDProduct goals, scope and expected behaviorRequirements CatalogStable requirements and acceptance criteriaADDArchitecture, boundaries and responsibilitiesTechnical SpecificationFrontend implementation technologies and constraintsDesign SystemShared visual language, design tokens and component standardsPage Design SpecificationIndividual page layouts, compositions and journeysTesting StrategyQuality verification and test expectationsScope and ReleasesRelease allocation and sequencing

The Design System does not independently add product features or change approved requirements.

If a design decision conflicts with an approved product requirement, the conflict must be recorded and resolved rather than silently changing the requirement.

1.3 Decision status
-------------------

This document distinguishes:

*   **Approved direction:** Executive Dark, professionally designed light theme, Bootstrap 5 as a foundation, custom CSS as the visual authority, English/Bangla support, and WCAG 2.2 AA target.
    
*   **Proposed defaults:** Exact token values, font selections, spacing values, component dimensions and detailed responsive rules.
    
*   **Page-specific decisions:** Exact page composition, content arrangement and page-level interaction details, defined in the Page Design Specification.
    
*   **Implementation decisions:** CSS architecture, Razor composition, asset organization and frontend behavior, governed by the Technical Specification.
    

Proposed defaults must be validated during implementation and visual review before being treated as final.

2\. Design principles
=====================

The complete interface must follow these principles.

2.1 Executive professionalism
-----------------------------

The interface must communicate confidence, credibility, technical competence and professional maturity.

It should feel like a carefully designed personal technology portfolio rather than a generic portfolio template.

2.2 Evidence before decoration
------------------------------

Engineering projects, verified achievements, technical capabilities and professional experience must receive more attention than decorative elements.

Visual effects must never make unsupported claims or distract from actual content.

2.3 Editorial composition
-------------------------

Pages should have purposeful visual composition, clear hierarchy and intentional use of whitespace.

Do not use the same card grid repeatedly across every page.

2.4 Consistency without monotony
--------------------------------

Shared components should look and behave consistently.

Individual pages should retain their own composition when their content and user journeys require it.

2.5 Accessibility by design
---------------------------

Accessibility is a design requirement, not a final polishing task.

Color, typography, focus, interaction, keyboard behavior, motion and responsive layouts must be considered from the beginning.

2.6 Authenticity
----------------

The portfolio must represent genuine professional information and real project evidence.

Images, achievements, certifications and project claims must not be fabricated to fill visual gaps.

2.7 Operational usability
-------------------------

The Admin Panel must prioritize clarity, efficiency, predictable behavior and safe content management.

It should not sacrifice usability in favor of visual decoration.

3\. Visual identity
===================

3.1 Primary visual direction
----------------------------

**Executive Dark**

The primary visual identity is premium, restrained, confident and editorial.

The interface should use:

*   Deep navy and charcoal backgrounds.
    
*   Carefully layered surfaces.
    
*   Restrained blue primary accents.
    
*   Limited secondary accent usage.
    
*   High-contrast readable typography.
    
*   Clear section hierarchy.
    
*   Purposeful whitespace.
    
*   Subtle borders and controlled elevation.
    

The visual experience should be sophisticated without appearing overly futuristic, flashy or decorative.

3.2 Visual characteristics
--------------------------

Preferred:

*   Strong typography and structured layouts.
    
*   Restrained accent colors.
    
*   Consistent spacing and alignment.
    
*   Purposeful image composition.
    
*   Subtle interaction feedback.
    
*   Clear separation between content sections.
    
*   Strong readability across different screen sizes.
    

Avoid:

*   Excessive glassmorphism.
    
*   Excessive gradients.
    
*   Neon-heavy interfaces.
    
*   Unnecessary glowing effects.
    
*   Decorative animations without functional purpose.
    
*   Excessive rounded cards.
    
*   Large quantities of floating elements.
    
*   Repetitive template-like layouts.
    
*   Unnecessary shadows and borders.
    
*   Tiny metadata and low-contrast text.
    

3.3 Visual hierarchy
--------------------

The visual hierarchy should generally follow:

1.  Page identity and primary heading.
    
2.  Primary content and important evidence.
    
3.  Supporting information.
    
4.  Secondary actions and navigation.
    
5.  Metadata and supplementary details.
    

The hierarchy may vary by page according to its purpose.

4\. Color system
================

4.1 Color strategy
------------------

Use semantic color tokens instead of scattering hexadecimal values throughout components.

Components must reference semantic tokens such as:

*   \--color-bg
    
*   \--color-surface
    
*   \--color-text
    
*   \--color-border
    
*   \--color-accent
    
*   \--color-focus
    

This allows both themes to share component styles while changing their visual appearance through token values.

4.2 Executive Dark palette
--------------------------

The following values preserve the original proposed palette.

TokenProposed valuePurposecolor-bg#080D19Main page backgroundcolor-surface#101A2CCards and panelscolor-surface-raised#1D2D48Elevated surfacescolor-accent#3978F6Primary actions and linkscolor-accent-secondary#7657E8Restrained secondary accentcolor-text#F4F6FAPrimary text referencecolor-muted#A8B3C7Secondary text reference

These are starting values, not a declaration that every combination passes accessibility contrast requirements.

4.3 Semantic color tokens
-------------------------

The final token system must include:

Token categoryPurposeBackgroundMain application and page backgroundSurfaceCards, panels and containersRaised surfaceElevated panels, menus and popoversPrimary textMain readable contentSecondary textSupporting content and metadataMuted textDe-emphasized informationBorderStandard component boundariesBorder strongImportant visual separationAccentPrimary action and link colorAccent hoverHover state for accent elementsAccent activeActive or pressed stateFocusVisible keyboard focus indicatorSuccessSuccessful operationsWarningCautionary informationDangerErrors and destructive actionsInformationNeutral informational messagesOverlayModal and lightbox backdrop

Status must never be communicated by color alone. Use appropriate text, icons or other visual indicators.

4.4 Light theme
---------------

A fully designed light theme is required.

It must use semantic equivalents rather than mechanically inverting the dark palette.

The light theme should provide:

*   A deliberate page background.
    
*   Distinct surface levels.
    
*   Readable primary and secondary text.
    
*   Appropriate borders.
    
*   Clear interactive states.
    
*   Accessible buttons and links.
    
*   Visible focus indicators.
    
*   Consistent status colors.
    

The light theme must retain the same brand identity without simply replacing dark backgrounds with white.

Exact light-theme values remain subject to contrast testing and visual approval.

4.5 Contrast requirements
-------------------------

Validate all important combinations in both themes.

At minimum:

*   Normal text: WCAG AA contrast ratio of 4.5:1.
    
*   Large text: WCAG AA contrast ratio of 3:1.
    
*   Meaningful interface components and graphical indicators: 3:1 against adjacent colors where applicable.
    
*   Focus indicators must be clearly visible.
    
*   Disabled states must remain understandable and must not create misleading visual feedback.
    

Test actual component combinations rather than validating colors independently.

5\. Typography system
=====================

5.1 Typography objectives
-------------------------

Typography must communicate professionalism while maintaining readability.

The system must support:

*   English content.
    
*   Bangla content.
    
*   Mixed-language content.
    
*   Long technical descriptions.
    
*   Project case studies.
    
*   Navigation and metadata.
    
*   Forms and administrative interfaces.
    

5.2 Font strategy
-----------------

Use a modern, highly readable sans-serif family.

Font selection must consider:

*   English character quality.
    
*   Bangla character coverage.
    
*   Weight availability.
    
*   Rendering consistency.
    
*   Readability at smaller sizes.
    
*   License and redistribution permission.
    
*   Performance and file size.
    

Use a suitable Bangla-capable font or fallback stack. Do not assume an English font will render Bangla correctly.

Where appropriate, self-host licensed font files to avoid unnecessary external runtime dependencies.

Exact font families remain proposed until the visual and language review is complete.

5.3 Type scale
--------------

Use a consistent responsive type scale.

The following values are proposed starting points:

TokenProposed desktop sizeUsagetext-display3.5remMajor hero headingtext-h12.75remMain page headingtext-h22remMajor section headingtext-h31.5remSubsection headingtext-h41.25remComponent headingtext-body-lg1.125remIntroductory texttext-body1remStandard contenttext-small0.875remSupporting contenttext-caption0.75remLimited supplementary metadata

These values should scale appropriately on smaller screens.

Avoid excessively small text. Essential content must remain readable without zooming.

5.4 Typography rules
--------------------

*   Use display typography selectively.
    
*   Maintain a clear heading hierarchy.
    
*   Use comfortable line heights.
    
*   Avoid excessive uppercase labels.
    
*   Avoid long paragraphs with excessively wide line lengths.
    
*   Use readable line lengths for project case studies.
    
*   Maintain consistent heading spacing.
    
*   Do not use font size alone to communicate importance.
    
*   Avoid unnecessary changes in font family between sections.
    

5.5 Bangla typography
---------------------

Bangla content must receive equal design attention.

Verify:

*   Character rendering.
    
*   Line wrapping.
    
*   Line height.
    
*   Heading height.
    
*   Button and navigation dimensions.
    
*   Mixed English/Bangla alignment.
    
*   Long Bangla words and labels.
    
*   Form validation messages.
    

Do not force English-sized components to accommodate Bangla content if they cause clipping or overflow.

6\. Spacing and sizing system
=============================

6.1 Spacing scale
-----------------

Use a consistent spacing scale based on a four-point foundation.

Proposed tokens:

TokenValuespace-14pxspace-28pxspace-312pxspace-416pxspace-520pxspace-624pxspace-832pxspace-1040pxspace-1248pxspace-1664pxspace-2080pxspace-2496px

Use these tokens consistently for:

*   Component padding.
    
*   Section spacing.
    
*   Page gutters.
    
*   Form spacing.
    
*   Card gaps.
    
*   Navigation spacing.
    
*   Content separation.
    

Avoid arbitrary spacing values unless a specific composition justifies them.

6.2 Component sizing
--------------------

Define consistent sizes for:

*   Buttons.
    
*   Form controls.
    
*   Icon buttons.
    
*   Navigation elements.
    
*   Cards.
    
*   Dialogs.
    
*   Media previews.
    
*   Tables and table rows.
    

Interactive targets must meet WCAG 2.2 AA target-size requirements or applicable spacing exceptions. Prefer approximately 44px or larger for common touch controls where practical.

6.3 Border radius
-----------------

Use a restrained radius system.

Proposed tokens:

*   radius-sm
    
*   radius-md
    
*   radius-lg
    
*   radius-xl
    
*   radius-pill
    

Use smaller radii for controls and larger radii selectively for prominent containers.

Do not apply pill-shaped styling to every component.

7\. Layout and grid system
==========================

7.1 General layout
------------------

The application must use a responsive content container with consistent maximum widths and page gutters.

The layout should support:

*   Narrow content sections.
    
*   Standard reading layouts.
    
*   Wide project and gallery layouts.
    
*   Full-width hero compositions.
    
*   Structured Admin Panel layouts.
    

Do not force all page content into one identical container width.

7.2 Proposed content widths
---------------------------

Layout tokenProposed maximum widthUsagecontainer-reading760pxLong-form contentcontainer-standard1120pxStandard pagescontainer-wide1280pxProjects and dashboardscontainer-full1440pxWide visual compositions

These are initial design targets and may be adjusted after visual testing.

7.3 Responsive breakpoints
--------------------------

Use Bootstrap 5 breakpoint conventions as the initial responsive foundation.

BreakpointWidthIntended layoutSmall576pxLarger mobile devicesMedium768pxTabletsLarge992pxSmall laptops and desktopExtra large1200pxStandard desktopExtra extra large1400pxWide desktop

The design must also be tested below 576px.

Breakpoints are not permission to ignore intermediate widths. Components must adapt fluidly between them.

7.4 Layout principles
---------------------

*   Maintain consistent horizontal alignment.
    
*   Use intentional whitespace.
    
*   Avoid horizontal overflow.
    
*   Keep reading content at comfortable widths.
    
*   Avoid excessively long line lengths.
    
*   Use responsive grids where they support the content.
    
*   Allow page-specific compositions.
    
*   Preserve important content hierarchy on mobile.
    
*   Avoid simply shrinking desktop layouts.
    

8\. Surface, border and elevation system
========================================

8.1 Surface hierarchy
---------------------

Use a deliberate hierarchy:

1.  Main page background.
    
2.  Standard content surface.
    
3.  Raised interactive surface.
    
4.  Floating overlay surface.
    

Surface differences may be expressed through background color, border, elevation or a combination.

8.2 Borders
-----------

Borders should be subtle but visible.

Use them to communicate:

*   Component boundaries.
    
*   Grouping.
    
*   Separation.
    
*   Table structure.
    
*   Interactive control boundaries.
    
*   Focus and selection states.
    

Avoid unnecessary borders around every section.

8.3 Shadows
-----------

Use shadows sparingly.

Appropriate uses include:

*   Dialogs.
    
*   Dropdowns.
    
*   Popovers.
    
*   Floating navigation elements.
    
*   Important elevated surfaces.
    

Avoid large decorative shadows that reduce the restrained visual identity.

9\. Iconography
===============

9.1 Icon style
--------------

Use a consistent modern icon family.

Icons should be:

*   Simple.
    
*   Recognizable.
    
*   Visually consistent.
    
*   Properly sized.
    
*   Aligned with surrounding text.
    

Avoid mixing unrelated icon styles.

9.2 Icon usage
--------------

*   Use icons to support meaning, not replace essential labels.
    
*   Decorative icons should be hidden from assistive technology.
    
*   Icon-only buttons must have accessible names.
    
*   Use consistent sizes for similar controls.
    
*   Do not use icons as the only distinction between destructive and safe actions.
    
*   Use consistent icon alignment in navigation and buttons.
    

9.3 Icon library
----------------

A maintained icon library may be selected during implementation.

The selected library must be compatible with the project's frontend architecture and licensing requirements.

The exact library is an implementation decision and should be recorded in the Technical Specification or an approved decision record.

10\. Imagery and media system
=============================

10.1 Image authenticity
-----------------------

The portfolio must use authentic administrator-provided images.

All previously discussed images, mockups and visual references are placeholders or design examples.

The production Gallery must not be automatically populated with:

*   Generated photographs.
    
*   Stock photography.
    
*   Sample photography.
    
*   Placeholder photographs.
    
*   Reference images used during planning.
    

The Gallery must initially display a designed empty state until the administrator uploads and publishes actual photographs.

10.2 Image presentation
-----------------------

Define appropriate image treatments for:

*   Profile photographs.
    
*   Project thumbnails.
    
*   Project screenshots.
    
*   Achievement imagery.
    
*   Certification imagery.
    
*   Gallery covers.
    
*   Gallery photographs.
    
*   Media previews.
    

Image ratios and cropping must be selected according to the content type.

Do not apply a single universal crop to every image.

10.3 Image behavior
-------------------

*   Preserve image quality appropriate to its display size.
    
*   Use responsive image variants.
    
*   Avoid unnecessary layout shifts.
    
*   Provide meaningful alternative text where the image conveys information.
    
*   Use empty or fallback states for unavailable images.
    
*   Use appropriate lazy loading for off-screen media.
    
*   Avoid lazy loading critical above-the-fold images where it harms the initial experience.
    
*   Ensure private media is never exposed through public image URLs.
    

10.4 Gallery presentation
-------------------------

Gallery design must support:

*   Album covers.
    
*   Album descriptions.
    
*   Optional location and date information.
    
*   Featured photographs.
    
*   Image ordering.
    
*   Responsive layouts.
    
*   Accessible lightbox presentation.
    
*   Empty states.
    
*   Loading and unavailable-image states.
    

The visual layout may use a deliberate grid or masonry-like composition where suitable, but it must not compromise reading order, accessibility or responsive behavior.

10.5 Media states
-----------------

Media components must account for:

*   Uploading.
    
*   Processing.
    
*   Scanning.
    
*   Available.
    
*   Failed.
    
*   Quarantined.
    
*   Unavailable.
    
*   Deleted or recycled.
    

Public visitors must never receive internal security or storage details that should remain administrator-only.

11\. Public component library
=============================

11.1 General requirements
-------------------------

Public components must share the Design System's visual language while supporting the purpose of their respective pages.

Reusable components must not force identical content composition everywhere.

11.2 Header and navigation
--------------------------

Define:

*   Brand or identity presentation.
    
*   Primary navigation.
    
*   Active-page indication.
    
*   Language selector.
    
*   Theme selector.
    
*   Mobile navigation.
    
*   Keyboard interaction.
    
*   Focus behavior.
    
*   Responsive collapse behavior.
    

Navigation must remain understandable when the available screen width becomes limited.

11.3 Footer
-----------

The footer should provide relevant navigation and supporting information without competing with the primary content.

Its content and links must remain manageable through the approved product configuration.

11.4 Buttons
------------

Required variants:

*   Primary.
    
*   Secondary.
    
*   Quiet or tertiary.
    
*   Destructive.
    
*   Icon button.
    

Each button must define:

*   Default.
    
*   Hover.
    
*   Focus-visible.
    
*   Active.
    
*   Disabled.
    
*   Loading.
    

Buttons must have clear labels describing their actions.

Do not use destructive styling for ordinary navigation.

11.5 Cards
----------

Reusable card categories include:

*   Project card.
    
*   Skill group card.
    
*   Achievement card.
    
*   Certification card.
    
*   Album card.
    
*   Media preview card.
    
*   Dashboard metric card.
    

Each card must have a defined content hierarchy and responsive behavior.

A card must not become a clickable surface without clear keyboard and focus behavior.

11.6 Content sections
---------------------

Reusable content patterns may include:

*   Section heading.
    
*   Introductory summary.
    
*   Metadata group.
    
*   Timeline.
    
*   Content list.
    
*   Feature highlight.
    
*   Evidence block.
    
*   Related content section.
    

These patterns should be used where they support the content, not as mandatory page templates.

11.7 Search and filters
-----------------------

Define:

*   Search field.
    
*   Search submission.
    
*   Search results.
    
*   Filter controls.
    
*   Active filter indicators.
    
*   Clear filters.
    
*   Empty results.
    
*   Loading state.
    
*   Pagination or progressive loading where applicable.
    

The current filter state must be understandable to visitors.

11.8 Pagination
---------------

Pagination must provide:

*   Current-page indication.
    
*   Previous and next controls.
    
*   Accessible labels.
    
*   Keyboard support.
    
*   Responsive behavior.
    
*   A clear empty or unavailable state.
    

11.9 Dialogs and lightboxes
---------------------------

Dialog and lightbox components must provide:

*   Clear heading.
    
*   Accessible description where necessary.
    
*   Close control.
    
*   Keyboard behavior.
    
*   Focus management.
    
*   Focus restoration.
    
*   Appropriate backdrop.
    
*   Responsive sizing.
    

A lightbox must not trap users without an accessible way to close it.

12\. Admin component library
============================

12.1 Admin visual direction
---------------------------

The Admin Panel should use the same core visual identity but prioritize operational clarity and content-management efficiency.

It should feel like a carefully designed professional CMS rather than a generic dashboard template.

12.2 Admin layout
-----------------

Provide:

*   Admin sidebar.
    
*   Admin top bar.
    
*   Main content area.
    
*   Page title and context.
    
*   Breadcrumbs where useful.
    
*   Notifications.
    
*   Account and security controls.
    
*   Responsive navigation behavior.
    

Public and Admin layouts must remain visually distinct while sharing semantic tokens and reusable foundations.

12.3 Dashboard components
-------------------------

Support:

*   Content overview.
    
*   Recent activity.
    
*   Contact inbox summary.
    
*   Quick actions.
    
*   Privacy-conscious analytics.
    
*   Operational warnings.
    

Dashboard metrics must be meaningful and must not imply data accuracy beyond what the system actually records.

12.4 Content editor components
------------------------------

Support:

*   Structured form fields.
    
*   Rich-text editor.
    
*   Draft status.
    
*   Validation feedback.
    
*   Preview action.
    
*   Publish and unpublish actions.
    
*   Revision context.
    
*   Unsaved-change warnings.
    

The editor must distinguish clearly between saved draft content and published content.

12.5 Data tables
----------------

Admin tables must support applicable combinations of:

*   Search.
    
*   Filtering.
    
*   Sorting.
    
*   Pagination.
    
*   Row actions.
    
*   Status labels.
    
*   Selection.
    
*   Bulk actions.
    

Tables must have deliberate narrow-screen behavior.

Do not simply scale a wide desktop table until the content becomes unreadable.

Where appropriate, use a responsive alternative such as stacked records, a horizontally scrollable table with clear affordances, or a simplified mobile presentation.

12.6 Admin forms
----------------

Admin forms must provide:

*   Clear labels.
    
*   Field descriptions where necessary.
    
*   Required-field indicators.
    
*   Validation summaries.
    
*   Inline validation messages.
    
*   Save and cancel actions.
    
*   Loading feedback.
    
*   Success and error feedback.
    
*   Unsaved-change protection.
    

Do not rely on placeholder text as the only field label.

12.7 Media Library components
-----------------------------

The Media Library should support the visual presentation of:

*   Search and category navigation.
    
*   Filters.
    
*   Grid and list views.
    
*   Metadata editing.
    
*   Usage references.
    
*   Processing and scanning states.
    
*   Public/private indicators.
    
*   Recycle bin.
    
*   Safe replacement and deletion flows.
    

Sensitive media actions must be visually clear and require the appropriate confirmation.

12.8 Gallery management components
----------------------------------

Gallery management should support:

*   Album list and editor.
    
*   Cover selection.
    
*   Photo manager.
    
*   Upload progress.
    
*   Individual photo metadata.
    
*   Ordering controls.
    
*   Visibility controls.
    
*   Publication controls.
    
*   Download permission settings.
    
*   Preview before publication.
    

Bulk actions must clearly communicate how many items will be affected.

12.9 Contact inbox components
-----------------------------

The contact inbox should support:

*   Conversation list.
    
*   Search and filtering.
    
*   Message thread view.
    
*   Reply interface.
    
*   Internal notes.
    
*   Delivery status.
    
*   Attachment access.
    
*   Archive and delete actions.
    

Private attachments must not be presented as publicly accessible media.

12.10 Security and operations components
----------------------------------------

Provide appropriate visual patterns for:

*   MFA and recovery information.
    
*   Session management.
    
*   Security event history.
    
*   Service health.
    
*   Job and email monitoring.
    
*   Storage and quota.
    
*   Backup and restore status.
    
*   Maintenance mode.
    

Sensitive operations require clear warnings, confirmation and appropriate verification.

13\. Component interaction states
=================================

13.1 Required state model
-------------------------

Interactive components must define applicable states:

StateMeaningDefaultNormal resting stateHoverPointer interaction feedbackFocus-visibleKeyboard focus indicationActivePressed or selected interactionDisabledTemporarily unavailableLoadingOperation in progressSuccessOperation completed successfullyErrorOperation failedEmptyNo content or resultsPartialSome content or operation is incomplete

Not every component needs every state. Only relevant states should be implemented.

13.2 State communication
------------------------

*   Never rely on color alone.
    
*   Use clear text for important status changes.
    
*   Keep feedback close to the affected component.
    
*   Avoid disruptive alerts for routine actions.
    
*   Announce important dynamic changes to assistive technology.
    
*   Preserve user input when recoverable errors occur.
    

13.3 Destructive actions
------------------------

Destructive actions must:

*   Use clear action labels.
    
*   Explain what will happen.
    
*   Require confirmation where appropriate.
    
*   Identify affected records when practical.
    
*   Avoid ambiguous confirmation wording.
    
*   Provide feedback after completion.
    

13.4 Unsaved changes
--------------------

Where feasible, detect unsaved changes before navigation.

The warning should explain that changes may be lost and provide clear options to remain or leave.

Do not show unnecessary warnings when no changes have occurred.

14\. Forms and validation system
================================

14.1 Form design
----------------

Forms must prioritize clarity and completion.

Use:

*   Persistent labels.
    
*   Appropriate input types.
    
*   Helpful field descriptions.
    
*   Consistent field spacing.
    
*   Clear required-field indicators.
    
*   Grouping for related fields.
    
*   Logical tab order.
    
*   Appropriate autocomplete attributes.
    

14.2 Validation
---------------

Validation feedback must:

*   Explain the problem in understandable language.
    
*   Identify the affected field.
    
*   Associate the error with the field.
    
*   Preserve entered values where appropriate.
    
*   Provide an error summary for longer forms.
    
*   Support screen readers.
    
*   Avoid exposing internal exception details.
    

Client-side validation is supplementary. Server-side validation remains authoritative.

14.3 Submission states
----------------------

Forms must support:

*   Ready.
    
*   Submitting.
    
*   Submitted successfully.
    
*   Validation failure.
    
*   Submission failure.
    
*   Recoverable service failure.
    

For the Contact form, the public confirmation must reflect the actual application result. Email delivery failure must not be presented as though the visitor's message was never received if the message was successfully persisted.

15\. Navigation and information hierarchy
=========================================

15.1 Public navigation
----------------------

Public navigation must represent the approved public information architecture.

It should support discovery of:

*   Home.
    
*   About.
    
*   Education.
    
*   Skills.
    
*   Projects.
    
*   Achievements.
    
*   Certifications.
    
*   Gallery.
    
*   Resume.
    
*   Contact.
    

Exact labels, grouping and mobile presentation are defined in the Page Design Specification.

15.2 Admin navigation
---------------------

Admin navigation must reflect the approved Admin modules.

It should group related operations logically without hiding important capabilities.

The administrator should be able to identify:

*   Where they are.
    
*   What module they are using.
    
*   What action is available.
    
*   Whether an operation is complete or requires attention.
    

15.3 Active navigation
----------------------

Active navigation must be distinguishable through more than subtle color changes.

Use appropriate visual indicators, accessible state information and consistent placement.

15.4 Breadcrumbs
----------------

Use breadcrumbs where they materially improve orientation, particularly in nested Admin and content-management workflows.

Avoid unnecessary breadcrumbs on simple pages.

16\. Data presentation system
=============================

16.1 General rules
------------------

Data must be presented accurately, consistently and legibly.

Avoid visual decoration that makes operational information harder to understand.

16.2 Status labels
------------------

Status labels may represent:

*   Draft.
    
*   Published.
    
*   Unpublished.
    
*   Scheduled.
    
*   Public.
    
*   Unlisted.
    
*   Private.
    
*   Processing.
    
*   Failed.
    
*   Archived.
    
*   Quarantined.
    

The exact vocabulary must match the underlying product behavior.

16.3 Metrics
------------

Dashboard metrics should use:

*   Clear labels.
    
*   Meaningful values.
    
*   Appropriate time context.
    
*   Consistent number formatting.
    
*   Accessible descriptions.
    

Charts and metrics must not misrepresent incomplete or unavailable data.

16.4 Tables and lists
---------------------

*   Use semantic table markup for tabular data.
    
*   Provide clear column headings.
    
*   Maintain readable row spacing.
    
*   Support keyboard access.
    
*   Use consistent alignment for numbers and dates.
    
*   Provide empty and error states.
    
*   Ensure responsive usability.
    

17\. Motion and animation
=========================

17.1 Motion philosophy
----------------------

Motion must be subtle, purposeful and restrained.

Use animation only when it improves:

*   Interaction feedback.
    
*   Orientation.
    
*   State transitions.
    
*   Understanding of interface changes.
    

17.2 Avoid
----------

*   Excessive parallax.
    
*   Scroll hijacking.
    
*   Continuous decorative movement.
    
*   Large unnecessary transitions.
    
*   Animations that delay access to content.
    
*   Motion that causes distraction or discomfort.
    

17.3 Reduced motion
-------------------

Respect prefers-reduced-motion.

When reduced motion is enabled:

*   Remove or simplify nonessential transitions.
    
*   Avoid parallax and large movement.
    
*   Preserve functional feedback.
    
*   Ensure content remains immediately accessible.
    

17.4 Motion tokens
------------------

Use centralized duration and easing tokens.

Exact values may be refined during implementation, but animations must remain short and purposeful.

18\. Accessibility standards
============================

18.1 Target
-----------

The entire application targets WCAG 2.2 Level AA.

Accessibility must apply to both the Public Viewer Panel and Admin Panel.

18.2 Semantic structure
-----------------------

Use:

*   Semantic landmarks.
    
*   Correct heading hierarchy.
    
*   Meaningful page titles.
    
*   Proper form labels.
    
*   Semantic buttons and links.
    
*   Appropriate table structure.
    
*   Meaningful alternative text.
    

18.3 Keyboard support
---------------------

All interactive functionality must be keyboard-operable.

Provide:

*   Visible focus.
    
*   Logical tab order.
    
*   Keyboard-operable navigation.
    
*   Accessible dialogs.
    
*   Accessible menus.
    
*   Accessible lightboxes.
    
*   Appropriate focus restoration.
    

18.4 Focus visibility
---------------------

Focus indicators must be clear against their surrounding surfaces in both themes.

Never remove browser focus indicators without providing an accessible replacement.

18.5 Screen-reader support
--------------------------

Provide:

*   Accessible names.
    
*   Form labels.
    
*   Field-error associations.
    
*   Status announcements.
    
*   Dialog names and descriptions.
    
*   Meaningful alternative text.
    
*   Appropriate live-region behavior for important updates.
    

18.6 Touch and pointer interaction
----------------------------------

Interactive targets must meet WCAG 2.2 AA requirements, including applicable target-size and spacing exceptions.

Do not make important functionality dependent on hover alone.

18.7 Zoom and reflow
--------------------

The application must remain usable under browser zoom and narrow viewport conditions.

Avoid fixed dimensions that cause important content to become inaccessible.

18.8 Accessibility verification
-------------------------------

Accessibility testing must include automated checks and manual keyboard/screen-reader review.

Passing an automated accessibility scan alone does not establish WCAG conformance.

19\. Responsive design standards
================================

19.1 Responsive philosophy
--------------------------

Responsive design must preserve content hierarchy and usability rather than simply shrink desktop layouts.

Every important page and component must be considered across mobile, tablet, laptop and wide desktop widths.

19.2 Mobile
-----------

Prioritize:

*   Clear navigation.
    
*   Readable content.
    
*   Appropriate touch targets.
    
*   Single-column layouts where suitable.
    
*   Usable forms.
    
*   Accessible image viewing.
    
*   Simplified data presentation.
    

19.3 Tablet
-----------

Use available width intelligently.

Avoid unnecessarily narrow content and desktop layouts that become cramped.

19.4 Desktop
------------

Use wider layouts where they improve content presentation.

Do not stretch long-form content across the entire screen.

19.5 Wide desktop
-----------------

Maintain maximum content widths and intentional whitespace.

Avoid oversized text or excessively wide cards merely because additional space is available.

19.6 Responsive verification
----------------------------

Test at:

*   Narrow mobile widths.
    
*   Common mobile widths.
    
*   Tablet widths.
    
*   Laptop widths.
    
*   Standard desktop widths.
    
*   Wide desktop widths.
    

Test intermediate widths and orientation changes where relevant.

No important page or control should introduce unintended horizontal overflow.

20\. Theme system
=================

20.1 Supported themes
---------------------

The application must provide:

*   Dark theme.
    
*   Light theme.
    
*   System preference on first visit.
    

20.2 Initial theme selection
----------------------------

On first visit, detect the operating system's prefers-color-scheme.

The initial visual direction remains Executive Dark, but the user's system preference must be respected as the initial choice.

20.3 Explicit preference
------------------------

When a visitor explicitly selects a theme, persist that choice.

The theme should remain consistent across navigation and page reloads.

20.4 Theme switching
--------------------

Theme switching must:

*   Be accessible.
    
*   Have a clear label.
    
*   Work by keyboard.
    
*   Avoid unnecessary visual flashes.
    
*   Preserve page content and state.
    
*   Update all relevant components.
    

20.5 Theme independence
-----------------------

Theme choice must not change:

*   Authorization.
    
*   Content visibility.
    
*   Publication status.
    
*   Private-media access.
    
*   Security decisions.
    

21\. Localization and content presentation
==========================================

21.1 Supported languages
------------------------

The application supports:

*   English.
    
*   Bangla.
    

English is the default language, with Bangla as an additional supported language.

21.2 Layout behavior
--------------------

The design system must accommodate different text lengths and character rendering.

Do not assume English and Bangla labels have identical widths.

21.3 Language switching
-----------------------

Language controls must:

*   Be clearly identifiable.
    
*   Be keyboard accessible.
    
*   Preserve the visitor's context where an equivalent translation exists.
    
*   Provide a predictable fallback where a translation does not exist.
    
*   Avoid silently displaying unpublished translations.
    

21.4 Content direction
----------------------

The initial language scope is English and Bangla, both using left-to-right layout.

Do not introduce right-to-left layout requirements without an approved future language requirement.

21.5 Localization verification
------------------------------

Test:

*   Navigation.
    
*   Buttons.
    
*   Forms.
    
*   Validation messages.
    
*   Tables.
    
*   Long headings.
    
*   Metadata.
    
*   Empty states.
    
*   Responsive layouts.
    

22\. Page composition principles
================================

The Design System establishes common rules. The Page Design Specification defines the exact composition of individual pages.

The following principles guide those page designs.

PageDesign emphasisHomeStrong professional identity, engineering evidence and clear navigationAboutEditorial professional biography and backgroundEducationStructured academic progressionSkillsOrganized technical capability groupsProjectsEngineering case studies, technical depth and verified project statusAchievementsEvidence-backed professional milestonesCertificationsClear credential presentationResumeReadable professional document experienceGalleryPhotography-led album and photo browsingContactTrustworthy and accessible communication experience

22.1 Public page consistency
----------------------------

Public pages must share:

*   Typography rules.
    
*   Color tokens.
    
*   Navigation language.
    
*   Interaction behavior.
    
*   Accessibility standards.
    
*   Responsive foundations.
    

They do not need identical hero sections, card grids or page layouts.

22.2 Admin page consistency
---------------------------

Admin pages must share:

*   Admin navigation.
    
*   Page headings.
    
*   Form conventions.
    
*   Data presentation.
    
*   Status indicators.
    
*   Feedback patterns.
    
*   Responsive behavior.
    

The Admin Panel should prioritize task completion and operational clarity.

22.3 Page-specific authority
----------------------------

The Page Design Specification must define:

*   Page purpose.
    
*   Target visitor or administrator.
    
*   Content hierarchy.
    
*   Main layout.
    
*   Component selection.
    
*   Primary and secondary actions.
    
*   Responsive composition.
    
*   Interaction states.
    
*   Empty and error experiences.
    

It must not redefine shared tokens independently.

23\. Empty, loading, error and operational states
=================================================

23.1 General requirement
------------------------

Every applicable page and module must define appropriate states.

These include:

*   Loading.
    
*   Empty.
    
*   No search results.
    
*   Validation error.
    
*   Permission denied.
    
*   Not found.
    
*   Service unavailable.
    
*   Partial data.
    
*   Operation in progress.
    
*   Operation failed.
    
*   Successful completion.
    

23.2 Public empty states
------------------------

Public empty states must remain professional and intentional.

Examples include:

*   Gallery has no published photographs.
    
*   Search returns no results.
    
*   No relevant projects are currently published.
    
*   No public content is available in the selected language.
    

Do not fill empty states with invented achievements, sample projects or placeholder photographs.

23.3 Admin empty states
-----------------------

Admin empty states should explain:

*   What information is missing.
    
*   Why the list is empty where appropriate.
    
*   What legitimate next action is available.
    

Avoid unnecessary instructions for tasks that are not supported by the product.

23.4 Operational states
-----------------------

The Admin Panel should present appropriate warnings for:

*   Storage capacity issues.
    
*   Failed background jobs.
    
*   Email delivery problems.
    
*   Media scanning failures.
    
*   Backup failures.
    
*   Service health problems.
    
*   Maintenance mode.
    

Operational warnings should be visible without overwhelming routine content-management activities.

Do not expose secrets, private infrastructure credentials or sensitive internal details through public error messages.

24\. Design token implementation standards
==========================================

24.1 Implementation principle
-----------------------------

Implement the design system using centralized CSS custom properties.

The semantic token layer must be the source of truth for component styling.

24.2 Token organization
-----------------------

Organize tokens into logical groups:

1.  Color tokens.
    
2.  Typography tokens.
    
3.  Spacing tokens.
    
4.  Layout tokens.
    
5.  Radius tokens.
    
6.  Border tokens.
    
7.  Elevation tokens.
    
8.  Motion tokens.
    
9.  Component-specific tokens where justified.
    

24.3 Naming conventions
-----------------------

Use consistent, semantic naming.

Examples:

*   \--color-bg
    
*   \--color-surface
    
*   \--color-text
    
*   \--color-border
    
*   \--color-accent
    
*   \--font-body
    
*   \--font-heading
    
*   \--space-4
    
*   \--radius-md
    
*   \--shadow-overlay
    
*   \--motion-duration-fast
    

Avoid naming tokens according to a specific page or arbitrary color appearance when a semantic name is more appropriate.

24.4 Theme implementation
-------------------------

Use theme-level token values so the same component styles work in dark and light themes.

Do not duplicate entire component stylesheets just to support the second theme.

24.5 Bootstrap integration
--------------------------

Bootstrap 5 is a responsive and interaction foundation only.

Use it where appropriate for:

*   Grid and breakpoint utilities.
    
*   Form foundations.
    
*   Responsive navigation behavior.
    
*   Modal and offcanvas primitives.
    
*   Selected layout utilities.
    

Do not allow unmodified Bootstrap defaults to determine:

*   Brand colors.
    
*   Typography.
    
*   Card appearance.
    
*   Buttons.
    
*   Borders.
    
*   Shadows.
    
*   Spacing rhythm.
    
*   Page composition.
    

Use project-owned tokens and organized component styles.

Avoid excessive utility-class accumulation and scattered one-off overrides.

24.6 Frontend architecture alignment
------------------------------------

The implementation must follow the Technical Specification:

*   ASP.NET Core MVC and Razor.
    
*   Separate Public and Admin layouts.
    
*   Shared design tokens.
    
*   Reusable partials and ViewComponents where appropriate.
    
*   Organized CSS for tokens, base styles, components, public pages and Admin pages.
    
*   Minimal, feature-organized JavaScript.
    
*   No separate SPA frontend unless the approved architecture changes.
    

25\. Design governance and quality assurance
============================================

25.1 Design ownership
---------------------

The product owner approves major visual direction changes.

Developers and AI coding agents may implement and refine components within the approved system.

They must not independently replace the Executive Dark identity or introduce a different visual framework.

25.2 Design change control
--------------------------

A significant design change should record:

*   Reason for the change.
    
*   Affected tokens or components.
    
*   Affected pages.
    
*   Accessibility implications.
    
*   Responsive implications.
    
*   Implementation impact.
    
*   Required documentation updates.
    
*   Approval status.
    

25.3 Component review
---------------------

Before a shared component is considered complete, verify:

*   Visual consistency.
    
*   Responsive behavior.
    
*   Keyboard behavior.
    
*   Focus visibility.
    
*   Accessible naming.
    
*   Required interaction states.
    
*   Dark theme.
    
*   Light theme.
    
*   English and Bangla content where applicable.
    

25.4 Visual quality review
--------------------------

Review the complete application for:

*   Consistent alignment.
    
*   Typography hierarchy.
    
*   Spacing rhythm.
    
*   Color consistency.
    
*   Component consistency.
    
*   Page-specific composition.
    
*   Content readability.
    
*   Image quality.
    
*   Responsive behavior.
    
*   Accessibility.
    

25.5 Quality gates
------------------

A design implementation must not be considered complete merely because it renders correctly.

At minimum, the relevant page or component must pass:

1.  Visual review.
    
2.  Responsive review.
    
3.  Dark and light theme review.
    
4.  Keyboard interaction review.
    
5.  Accessibility verification.
    
6.  English and Bangla content review where applicable.
    
7.  Loading, empty and error-state review.
    

Actual verification evidence should be recorded according to the Testing Strategy.

26\. AI coding agent implementation rules
=========================================

Any AI coding agent working on this project must follow these rules.

1.  Read this Design System before implementing or modifying frontend components.
    
2.  Read the relevant Page Design Specification before implementing a page.
    
3.  Read the PRD and Requirements Catalog before changing product behavior.
    
4.  Read the Technical Specification before selecting or changing frontend technologies.
    
5.  Preserve the Executive Dark visual direction.
    
6.  Use centralized semantic design tokens.
    
7.  Support both dark and light themes.
    
8.  Use Bootstrap 5 only as a foundation, not as the visual identity.
    
9.  Do not introduce a generic Bootstrap theme or dashboard template.
    
10.  Do not create a different design language for individual pages.
    
11.  Do not force all pages into identical card-based layouts.
    
12.  Do not introduce unapproved frontend frameworks or dependencies.
    
13.  Do not invent portfolio achievements, certifications, projects or professional claims.
    
14.  Do not populate the production Gallery with generated, stock, sample or placeholder photographs.
    
15.  Do not remove accessibility behavior to simplify implementation.
    
16.  Do not rely exclusively on hover interactions.
    
17.  Do not hard-code repeated design values when an appropriate token exists.
    
18.  Do not implement only the desktop layout and treat mobile as a later adjustment.
    
19.  Do not mark a component complete without checking its applicable states.
    
20.  Record necessary deviations and request approval when a change affects the approved visual direction or product scope.
    

When a design detail is missing, follow the closest approved pattern and record the assumption. Do not invent major visual or product decisions.

27\. Acceptance criteria for the Design System
==============================================

The Design System is ready for approval when:

*   Executive Dark visual direction is clearly defined.
    
*   Light theme requirements are defined.
    
*   Semantic color token categories are documented.
    
*   Proposed palette values are identified as unvalidated until tested.
    
*   Typography supports English and Bangla.
    
*   A consistent typography scale is defined.
    
*   Spacing and sizing tokens are documented.
    
*   Layout widths and responsive breakpoints are defined.
    
*   Surface, border, radius and elevation rules are documented.
    
*   Iconography rules are defined.
    
*   Authentic image provenance rules are preserved.
    
*   Public component standards are documented.
    
*   Admin component standards are documented.
    
*   Component interaction states are defined.
    
*   Form and validation patterns are defined.
    
*   Navigation and data presentation rules are documented.
    
*   Motion and reduced-motion behavior are defined.
    
*   WCAG 2.2 AA design expectations are documented.
    
*   Responsive behavior is defined for mobile through wide desktop.
    
*   Theme switching behavior is documented.
    
*   Localization requirements are documented.
    
*   Page composition responsibilities are separated from the Page Design Specification.
    
*   Empty, loading, error and operational states are addressed.
    
*   CSS token implementation rules align with the Technical Specification.
    
*   Design governance and quality gates are defined.
    
*   AI coding agent rules are explicit.
    
*   No conflict with the approved PRD, ADD or Technical Specification remains unresolved.
    

28\. Document status and revision history
=========================================

28.1 Current status
-------------------

**Version:** 2.0**Status:** Comprehensive review draft — pending product-owner approval.

This version expands the original visual-direction document into a reusable design and interaction standard.

It does not claim that the palette, fonts, components or implemented pages have already passed visual or accessibility testing.

28.2 Revision history
---------------------

VersionDescriptionStatus1.0Initial visual direction, palette proposal, typography, layout, components, accessibility and responsive principlesSuperseded by review draft2.0Expanded semantic tokens, typography, layout, public/Admin component standards, interaction states, localization, accessibility, implementation rules and governancePending approval

28.3 Approval
-------------

The product owner must review and approve the Design System before it becomes the authoritative visual implementation baseline.

Any proposed changes to the approved design direction must follow the project's documentation change-control process.

**End of DESIGN\_SYSTEM v2.0**
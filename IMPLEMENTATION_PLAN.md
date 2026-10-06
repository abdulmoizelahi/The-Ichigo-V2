# Implementation Plan — "The Ichigo" Digital Illustrator Portfolio

**Source of truth:** `UX_AUDIT_REPORT.md`. Every fix, improvement, and task below is derived directly from a finding or recommendation in that report — no unrelated scope has been introduced. Section references (e.g. "§2.1") point back to the audit.

**Sequencing principle:** foundational/trust-breaking fixes ship before structural IA work, which ships before content/trust depth, which ships before polish — because reordering sections or adding new ones on top of broken nav/CTAs/images would just multiply rework. This mirrors the audit's own Section 5 phasing, expanded into concrete, dependency-ordered tasks.

**Companion file:** `PROGRESS.md` tracks execution against this plan. Every future session's changes must be logged there against the specific phase/task below.

---

## Phase 1 — Stop the Bleeding (Fix What's Actively Broken)

### Goal
Make the existing page internally honest and functional before anything is restructured or added. No dead links, no invisible/duplicated assets, no silently-broken controls. This must come first because Phases 2–4 add new sections and anchors on top of the nav/CTA/scroll infrastructure — building on top of broken plumbing would mean redoing this work twice.

### Fixes (from audit)
- Nav routes Services/Blog to `under-construction.html` even though those sections already exist on-page (§2.1, §2.6)
- Hero and section CTAs (`Explore My Work`, `Services`, `More About Me`, `VIEW ALL SERVICES`, `View All Posts`) have no `href`/anchor/handler (§2.1)
- Footer "Quick Links" and social `<li>` items are inert (`href="#"` or no link at all) (§2.1)
- Search icon implies a capability that doesn't exist (§2.1, §2.6)
- No functional mobile navigation — hamburger icon has no handler or drawer (§2.1, §2.10)
- 1.3MB About-section background image is fully hidden behind an opaque `bg-black` overlay (§2.2)
- Premades gallery shows the same single image three times instead of three distinct covers (§2.1)
- Blog images use non-standard `data-alt` instead of `alt` (§2.2, §2.11)
- Conflicting `text-primary`/`text-outline` utility classes on Services/Consultation eyebrows (§2.2)
- Duplicate Material Symbols `<link>` tag loaded twice (§2.3)
- Blog heading hierarchy skips a level (h2 → h4, no h3) (§2.2, §2.11)
- `#contact` is referenced (footer, `under-construction.html`) but doesn't exist anywhere (§2.1)

### Improvements
- None yet — this phase is fix-only by design; new capability starts in Phase 2.

### Redesign/Refactor Work
- None structural yet. Only wiring, attribute, and class-level corrections.

### Coverage
- **User flow:** every clickable element on the page must lead somewhere real or be removed.
- **Interaction patterns:** mobile menu becomes functional (drawer/sheet); scroll-to-anchor behavior established as the pattern nav will use going forward.
- **UI structure:** eyebrow-label class conflict resolved (temporary consistent fix; full componentization deferred to Phase 4 §4.7).
- **Accessibility/usability:** `alt` attributes fixed, heading hierarchy corrected.
- **Responsive UX:** mobile nav becomes usable for the first time.

### Actionable Tasks
- [ ] 1.1 Add `id` attributes to existing sections that will be anchor targets: `#about`, `#services`, `#premades`, `#consultation`, `#blog` (temporary IDs; Portfolio/Contact anchors added in Phase 2 once those sections exist)
- [ ] 1.2 Add `html { scroll-behavior: smooth; }` (or equivalent) and update fixed-nav offset handling so anchored scrolls land below the fixed nav bar
- [ ] 1.3 Update nav links: `About Me` → `#about`, `Services` → `#services`, `Blog` → `#blog`; leave `Portfolio` and `Premades` pointing at `under-construction.html`/`#premades` per 1.4 below
- [ ] 1.4 Point `Portfolio` nav item at `#premades` temporarily (closest existing content) with a note in `PROGRESS.md` that it must be re-pointed to the real Portfolio section in Phase 2
- [ ] 1.5 Wire hero CTA `Explore My Work` → scroll to nearest existing content section (`#premades` or `#services`, temporary until Phase 2 Portfolio exists); wire hero CTA `Services` → `#services`
- [ ] 1.6 Wire `More About Me` → `#about` (or remove the button if it has nothing further to reveal until Phase 3 About expansion lands)
- [ ] 1.7 Wire `VIEW ALL SERVICES` → `#services` (or remove if there is no "more services" content yet — do not leave it pointing nowhere)
- [ ] 1.8 Wire `View All Posts` → `#blog` (or remove if there is no additional blog archive yet)
- [ ] 1.9 Fix footer "Quick Links" to point to the same real anchors as the nav (no separate/divergent target list)
- [ ] 1.10 Fix footer social list items: convert to real `<a>` elements with real destination URLs (or clearly mark as placeholders pending real profile links, tracked as a flagged open item — see note below)
- [ ] 1.11 Remove the header search icon until real search functionality is planned (out of scope for a single-page site per audit §2.6), or replace with a functioning "jump to section" affordance if search intent was actually meant as in-page navigation
- [ ] 1.12 Implement a functional mobile nav drawer/sheet: menu icon toggles visibility of the same nav items (as anchors, per 1.3–1.4), with a visible close affordance
- [ ] 1.13 Fix the About section background overlay: either restore real overlay transparency (e.g. `bg-black/60`) so the 1.3MB image is actually visible, or remove the background image entirely if it adds no intended value — decide based on the visual design intent, then implement
- [ ] 1.14 Replace the duplicated Premades book image with three visually distinct placeholder images (temporary) until real premade cover art is sourced in Phase 3
- [ ] 1.15 Replace `data-alt` with proper `alt` attributes on all 4 blog thumbnails, keeping the existing descriptive copy
- [ ] 1.16 Resolve the `text-primary`/`text-outline` conflict on Services/Consultation eyebrow labels — pick one intentional color utility and apply consistently
- [ ] 1.17 Remove the duplicate Material Symbols Google Fonts `<link>` tag in `index.html`'s `<head>`
- [ ] 1.18 Fix Blog section heading hierarchy: introduce an `h3` at the appropriate level so structure reads h2 → h3 → h4 without skips
- [ ] 1.19 Create a real `#contact` anchor point on `index.html` (can point at the existing Consultation section as an interim target) so the `under-construction.html#contact` link and footer "Contact" item resolve to something real, even before the full Contact mechanism (Phase 2) is built

### Dependencies
- All Phase 1 tasks are independent of later phases and can be done in any order within the phase.
- Tasks 1.3–1.9, 1.19 depend on 1.1 (anchors must exist before links can target them).
- Task 1.12 depends on 1.3–1.4 (drawer needs the same corrected link set as desktop nav).
- Note: anchors created here as interim targets (`#premades` standing in for Portfolio, Consultation standing in for Contact) will be **re-pointed, not re-created**, once Phase 2 builds the real Portfolio and Contact sections — flag this explicitly in `PROGRESS.md` so Phase 2 doesn't skip the cleanup.

---

## Phase 2 — Close the IA Gap (Build What's Missing)

### Goal
Give the site the sections it structurally cannot function without: a real portfolio gallery and a real contact mechanism. This is sequenced second — after Phase 1 makes the existing page trustworthy, but before Phase 3's trust/conversion depth — because those later sections (social proof, process/pricing) are meant to support a visitor's decision to engage with the *portfolio and contact flow*, which don't yet exist until this phase.

### Fixes (from audit)
- No portfolio/gallery section exists anywhere on the page (§2.1, §3.1 — the single largest gap)
- No working contact mechanism exists despite being referenced in nav/footer/under-construction page (§2.1, §2.5, §3.1)
- 9 images are hot-linked to a third-party AI-tool host rather than owned/local assets (§2.1)
- Section sequence puts a commerce section (Premades) before any credibility-building portfolio content (§2.5, §3.3)

### Improvements (from audit §4)
- §4.1 Add a real Portfolio/Gallery section with category filtering (Book Covers / Characters / Scenes)
- §4.5 Build a real Contact mechanism (form or scheduling embed) at a genuine `#contact` anchor
- §4.6 Replace hot-linked third-party images with owned, local, optimized assets

### Redesign/Refactor Work
- **Section sequence restructuring** (§3.3): reorder to Hero → **Portfolio (new)** → About → Services → Premades → Consultation/Contact → Blog → Footer. (Social Proof and Process/Pricing slot in during Phase 3 — this phase establishes the reordered skeleton they'll be inserted into.)
- Re-point the temporary Phase-1 anchors (`Portfolio` nav → `#premades`, `#contact` → Consultation) to the new, real Portfolio and Contact sections.

### Coverage
- **Information Architecture:** Portfolio becomes a first-class top-level section; Contact becomes a real destination, not a placeholder reference.
- **Content hierarchy:** Portfolio uses category/filter controls → image grid → (optional) case-study expand, per audit §3.4.
- **Section sequence restructuring:** implement the reordering described above.
- **User flow:** the full intended visitor journey (see art → learn about artist → understand services → contact) becomes completable end-to-end for the first time.
- **UI structure:** new Portfolio and Contact sections reuse existing card/grid/section patterns already established (Services grid, Consultation layout) rather than introducing new visual patterns.
- **Responsive UX:** new sections built mobile-first/responsive from the start (grid collapses to 1 column on mobile, consistent with existing sections).

### Actionable Tasks
- [ ] 2.1 Design and build the Portfolio/Gallery section markup: category filter controls (Book Covers / Characters / Scenes, matching existing Services taxonomy) + responsive image grid
- [ ] 2.2 Source/place real artwork images for the Portfolio grid (replacing any temporary placeholders); apply `loading="lazy"` and explicit `width`/`height` to prevent layout shift
- [ ] 2.3 Insert the Portfolio section immediately after the Hero section
- [ ] 2.4 Re-point nav `Portfolio` link (currently pointed at `#premades` per Phase 1 task 1.4) to the new real Portfolio section anchor
- [ ] 2.5 Re-point hero CTA `Explore My Work` (currently a Phase-1 interim target) to the new Portfolio section
- [ ] 2.6 Reorder existing sections in markup to match: Hero → Portfolio → About → Services → Premades → Consultation → Blog → Footer
- [ ] 2.7 Re-verify all anchor links (nav, footer, hero CTAs, service-card links) still resolve correctly after reordering — update any that broke
- [ ] 2.8 Build a real Contact mechanism: a working form (name/email/message or commission-inquiry fields) or an embedded scheduling tool, placed at the Consultation section
- [ ] 2.9 Add a genuine `#contact` `id` on the Contact-capable section (replacing the Phase-1 interim redirect to Consultation) so `under-construction.html#contact` and footer "Contact" resolve correctly
- [ ] 2.10 Download and self-host all 9 `lh3.googleusercontent.com`-hosted images (artist signature, footer logo, 4 blog thumbnails, and the Premades book covers once real art replaces the Phase-1 placeholder) as local, compressed assets (WebP/AVIF with fallback)
- [ ] 2.11 Add `loading="lazy"` and explicit dimensions to all below-the-fold images site-wide as part of the same asset pass
- [ ] 2.12 Update `under-construction.html` link destinations if any nav items it references now have real homepage sections instead of needing the placeholder page

### Dependencies
- 2.1–2.6 depend on Phase 1 being complete (anchors/scroll infrastructure, working nav, functional mobile menu must already exist to extend/reorder).
- 2.4–2.5 depend on 2.1–2.3 (new section must exist with a stable anchor before links can target it).
- 2.7 depends on 2.6 (reordering can shift anchor scroll offsets or break assumptions baked into Phase 1 nav wiring — must be re-tested).
- 2.9 depends on 2.8 (real contact mechanism must exist before its anchor is treated as final/authoritative).
- 2.10 can happen in parallel with 2.1–2.9, but should be finished before Phase 3 content work reuses these assets (e.g. Premades real art from 2.10 feeds Phase 3's Premades content pass).

---

## Phase 3 — Build Trust and Conversion Depth

### Goal
Move the site from "functional" to "convincing." This is sequenced third because these additions (social proof, process/pricing, expanded About, real blog content) only make sense once there's a real Portfolio to be convinced by and a real Contact mechanism to convert into (both delivered in Phase 2).

### Fixes (from audit)
- About Me section is thin — no credentials, client list, or process (§3.2)
- Blog uses generic stock photography for all 4 posts, undermining the "illustrator" brand (§2.5, §3.2)
- Newsletter form has no real submission handling, feedback states, or safe method (currently defaults to GET, leaking email into URL/history) (§2.1)
- "Book a Consultation" CTA has no pricing/process context, asking for commitment with zero information (§2.1)

### Improvements (from audit §4)
- §4.2 Add a Social Proof section (testimonials / client logos), placed between Services and Premades
- §4.3 Add a Commission Process/Pricing section, placed before the Consultation CTA
- §4.8 Add lightweight case-study depth for 2–4 flagship Portfolio pieces

### Redesign/Refactor Work
- Insert two new sections into the Phase-2 skeleton: Social Proof (after Services) and Process/Pricing (before Consultation), producing the full target order: Hero → Portfolio → About → Services → **Social Proof (new)** → Premades → **Process/Pricing (new)** → Consultation/Contact → Blog → Footer
- Expand About Me content depth (credentials, client roster, process snapshot)

### Coverage
- **Content hierarchy:** Social Proof = attributed testimonial/logo row; Process = numbered-step layout reusing existing icon+label pattern from Services cards.
- **Section sequence restructuring:** final insertion of the two new sections completes the target order defined in the audit (§3.3).
- **User flow:** removes the two biggest hesitation points before a booking action — lack of third-party validation, and lack of process/cost clarity.
- **Interaction patterns:** newsletter form gains real submit handling and success/error feedback states (§2.9 audit finding on missing states).
- **New UX/UI recommendations mapped here:** §4.2, §4.3, §4.8 (all explicitly sequenced into this phase per the audit's own Phase 3).

### Actionable Tasks
- [ ] 3.1 Build the Social Proof section: 3–5 short, attributed testimonials or a client/publisher logo row, reusing the existing Services card shell for visual consistency
- [ ] 3.2 Insert Social Proof section between Services and Premades
- [ ] 3.3 Build the Commission Process/Pricing section: numbered steps (e.g. Inquiry → Concept → Revisions → Delivery) with real pricing or "starting at" ranges, reusing the existing icon+label pattern
- [ ] 3.4 Insert Process/Pricing section between Premades and Consultation
- [ ] 3.5 Re-verify nav/footer/CTA anchors after this second reordering pass (same check performed in Phase 2 task 2.7)
- [ ] 3.6 Expand About Me copy/layout with credentials, notable clients/publishers, and a short process snapshot
- [ ] 3.7 Replace generic stock blog imagery with the artist's own process/WIP photography, or reduce the Blog section's visual prominence if no real content is available yet
- [ ] 3.8 Wire the newsletter form to a real submission handler; switch off default GET behavior (use POST or a form service) to stop leaking email addresses into the URL/browser history; add success/error UI states
- [ ] 3.9 Add case-study depth (modal or inline expand) to 2–4 flagship Portfolio pieces from the Phase 2 gallery, showing process/brief/client where available

### Dependencies
- 3.1–3.4 depend on Phase 2 completion (Portfolio and Contact must exist so these new sections have something to reinforce).
- 3.5 depends on 3.2 and 3.4 (must re-check after both new sections are inserted).
- 3.9 depends on Phase 2 task 2.1–2.2 (the Portfolio grid must exist before individual pieces can get case-study depth).
- 3.6–3.8 are independent of the reordering tasks and can proceed in parallel.

---

## Phase 4 — Polish, Consistency, and Resilience

### Goal
Tighten the system so it stays consistent as content grows. Sequenced last because these are cross-cutting refinements to a structure that must already be correct (Phases 1–2) and content-complete (Phase 3) — polishing sequence or components before the structure is final would mean re-polishing after every structural change.

### Fixes (from audit)
- `style.css` duplicates inline `<style>` rules already declared in `index.html`'s `<head>` (§2.3)
- Decorative motion (book float, hover transforms, mousemove parallax) has no `prefers-reduced-motion` guard on `index.html`, inconsistent with `under-construction.html` (§2.1, §2.2, §2.11)
- Icon-only controls (search if retained, menu, back-to-top) have no `aria-label` (§2.11)
- Unused root assets (`Profile-section-bgImage.png`, `Website-Reference-Image-Original.png`) still present (§2.2)
- Two type-scale tokens (`headline-lg` vs `headline-lg-mobile`) exist in the design system but aren't consistently applied in markup (§2.3)
- Mousemove parallax effect is unthrottled and provides no benefit on touch devices (§2.1)

### Improvements (from audit §4)
- §4.7 Introduce a consistent, single "eyebrow label" component (upgrading the Phase-1 quick class-conflict fix into a proper reusable pattern)

### Redesign/Refactor Work
- Consolidate all styling into one source of truth (remove `style.css`/inline `<style>` duplication)
- Formalize the eyebrow-label pattern as one documented class/utility combination applied uniformly across About/Services/Premades/Consultation/Blog
- Reconcile the documented `headline-lg-mobile` token with actual usage — either apply it consistently at the intended breakpoint or remove it from `DESIGN.md`/`tailwind.config` if the `clamp()`-based approach is the intended final pattern

### Coverage
- **Visual/UI issue resolutions:** eyebrow label consistency (full fix, beyond Phase 1's conflict removal), style-source consolidation, type-scale reconciliation.
- **Accessibility/usability improvements:** `prefers-reduced-motion` parity between both pages; `aria-label`s on icon-only controls; keyboard focus-visibility check against the dark theme (in-browser verification).
- **Responsive UX/UI fixes:** confirm the Premades book-fan gallery reads clearly at mobile widths now that it displays real, distinct artwork (from Phase 1/2 fixes) rather than duplicated placeholders.
- **Performance:** throttle/guard the mousemove parallax effect (or scope it to non-touch pointers only) given it provides no benefit on touch devices.

### Actionable Tasks
- [ ] 4.1 Merge `style.css` and the inline `<style>` block in `index.html` into one location; remove all duplicated rules
- [ ] 4.2 Ensure `under-construction.html` sources shared styling consistently rather than re-declaring rules inline separately
- [ ] 4.3 Define one standardized "eyebrow label" class combination and apply it uniformly across all five sections that use the pattern
- [ ] 4.4 Add `@media (prefers-reduced-motion: reduce)` guards to `index.html` covering book-float animation, hover transforms, and the mousemove parallax effect, matching the existing pattern already implemented in `under-construction.html`
- [ ] 4.5 Add `aria-label`s to the back-to-top button, mobile menu toggle, and any retained icon-only control
- [ ] 4.6 Throttle or `requestAnimationFrame`-wrap the hero mousemove parallax handler, or disable it on touch/coarse-pointer devices via a `(hover: hover) and (pointer: fine)` media query check
- [ ] 4.7 Reconcile the `headline-lg-mobile` design token: apply it at its intended breakpoint consistently, or remove it from `DESIGN.md` and `tailwind.config` if superseded by the `clamp()` approach
- [ ] 4.8 Remove unused root image assets (`Profile-section-bgImage.png`, `Website-Reference-Image-Original.png`) after confirming with the project owner they aren't needed for reference
- [ ] 4.9 In-browser check of keyboard focus visibility across all interactive elements against the dark theme; adjust focus-visible styling if contrast is insufficient
- [ ] 4.10 Full-page responsive pass (phone/tablet/desktop/ultra-wide) confirming all Phase 1–3 additions read correctly at every breakpoint, including the hero's large-viewport space usage noted in the audit (§2.7)

### Dependencies
- 4.3 depends on Phase 1 task 1.16 (the interim class-conflict fix) as its starting point — this phase turns that quick fix into the final, documented pattern.
- 4.4 has no hard dependency but should be done after Phase 3's content is final, since new sections may introduce new motion that also needs the guard.
- 4.10 depends on all of Phases 1–3 being complete — it is the final verification pass before considering the plan done.
- 4.8 should only proceed after confirming (outside this plan) that neither file is needed as a design reference; flag as a question rather than deleting unilaterally.

---

## Final Step — UX/UI Verification

After Phase 4, perform a full end-to-end walkthrough against the original audit's success criteria (§3.5 visitor journey): land → see representative art → confirm fit via Portfolio/Services → build trust via About/Social Proof → understand engagement via Process/Pricing → act via Contact — confirming no dead links, no broken images, functional mobile nav, and consistent visual system, across breakpoints. Record the outcome in `PROGRESS.md` and close out the plan.

# SEO Improvement Plan

- [ ] Baseline audit current page metadata, semantics, crawlability, and visible SEO-like copy.
- [ ] Analyze competitor pages for ranking patterns (title/meta/heading/schema/internal links/content depth).
- [ ] Define target keyword clusters and map them to non-visual SEO elements.
- [ ] Update `artist_profiles.html` with improved technical SEO (meta tags, OG/Twitter, canonical, robots, JSON-LD).
- [ ] Improve semantic HTML structure for crawlability without changing visual design.
- [ ] Remove visible SEO hints from landing/front-end copy while preserving natural editorial voice.
- [ ] Verify output (no broken HTML, metadata present, UI behavior unchanged).

## Review
- Pending.

---

# GitHub Publish Plan

- [x] Initialize git in `/Users/macbookpro/Desktop/apww_glassmorphic_`.
- [x] Stage current project files and create initial commit.
- [x] Add remote `origin` -> `https://github.com/Ceyvion/apww_womens_history_month.git`.
- [x] Push local branch to remote and verify tracking.

## Review
- Completed on February 26, 2026.
- Verified `main` is tracking `origin/main` and push succeeded.

---

# 404 Fix Plan

- [x] Add root `index.html` so hosting `/` does not return `404`.
- [x] Preserve query/hash on redirect to `artist_profiles.html`.
- [x] Commit and push fix to `main`.
- [x] Verify branch is clean and remote is up to date.

## Review
- Completed on February 26, 2026.
- Added root `index.html` redirect entrypoint for static hosts.
- Pushed commit `3852864` to `origin/main`.

---

# Claude Verification Plan (2026-02-27)

- [x] Verify claimed Phase 1 updates in `artist_profiles.html` (artists/cards/poll/highlights).
- [x] Verify claimed Phase 2 episode hub UI + date gating behavior.
- [x] Verify claimed Phase 3 branding/linking updates.
- [x] Verify claimed Phase 4 social meta tags (Open Graph + Twitter).
- [x] Verify claimed Phase 5 article CTAs and modal link styling/events.
- [x] Verify claimed Phase 6 analytics updates in page + `apww_n8n_ingest_workflow.json`.
- [x] Verify claimed Phase 7 UX polish (nav dots, modal interaction, responsive behavior).
- [x] Document verification findings and discrepancies.

## Review
- Completed on February 27, 2026.
- Runtime and code verification passed for all major claims (Phases 1-7), including event instrumentation and date gating.
- One discrepancy: bio modal links are restyled and prominent, but not truly pill-shaped (`border-radius: 4px`), so that wording is overstated.

---

# Mobile View + Navigation Fix Plan (2026-03-05)

- [x] Reproduce the broken page opening behavior from the current entrypoint and identify the failing interaction.
- [x] Reproduce the mobile layout issues in a phone-sized viewport and isolate the CSS/JS causes.
- [x] Update `artist_profiles.html` and any entrypoint/linking code with the minimum changes needed to restore navigation and responsive layout.
- [x] Re-test the entry flow and affected mobile interactions in Playwright.
- [x] Document the result and any remaining risks in this review section.

## Review
- Completed on March 5, 2026.
- Root entrypoint still correctly redirects `/` to `artist_profiles.html`; there is no second tracked HTML destination in the repo to relink.
- Fixed the episode timing bug in `artist_profiles.html` so page initialization no longer crashes after the first March 5 episode air time, which restored the mobile intro reveal and bio-opening interactions.
- Tightened mobile sizing for the intro, directory, artist cards, modals, poll, and opt-in form; on very short screens the intro section now grows taller than one viewport instead of clipping its copy.
- Verified with Playwright (`npx -p playwright`) at `390x844` and `320x568`: root redirect landed on `/artist_profiles.html`, console errors were empty, and tapping a directory item opened the Miriam Makeba bio modal successfully.

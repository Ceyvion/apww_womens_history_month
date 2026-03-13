# Episode Hub Missing Episode Fix Plan (2026-03-13)

- [x] Confirm which episode the local site should surface today and whether the live source data differs from the hardcoded `WHM_EPISODES` array.
- [x] Update the episode hub implementation with the minimum change needed so the missing episode is surfaced reliably.
- [x] Verify the rendered episode states against the current date in browser/runtime checks.
- [x] Document the root cause, fix, and verification results in this review section.

## Review
- Completed on March 13, 2026.
- Root cause: the episode hub is hardcoded, and the March 12 entry used a stub Afropop URL (`/audio-programs/cheikha-rimitti`) instead of the canonical published episode page (`/audio-programs/cheikha-rimitti-rebel-queen-of-algerian-music`). The March 19 entry also used a shortened non-canonical slug.
- Updated `artist_profiles.html` so all March 2026 episode entries use canonical `www.afropop.org` episode URLs, and added published descriptions/SoundCloud embeds for the March 12, March 19, and March 26 entries.
- Browser verification on March 13, 2026 at `http://127.0.0.1:4173/artist_profiles.html` confirmed the hub now shows:
  - Episode 705 aired on March 5 with its existing expanded content.
  - Episode 870 aired on March 12 with the correct Cheikha Rimitti title, description, embed, and canonical Afropop link.
  - Episode 731 as the next upcoming episode on March 19 with the corrected canonical title.
- Runtime verification found no episode-hub JavaScript regressions. One unrelated pre-existing local `404` asset request still appears in the browser console during page load and was not part of this fix.

---

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

---

# Claude Episode Hub Verification Plan (2026-03-06)

- [x] Review Claude's uncommitted `artist_profiles.html` diff and identify code-level edge cases before pushing.
- [x] Verify aired/upcoming gating logic against Eastern Time, including DST behavior after March 8, 2026.
- [x] Verify the expanded aired episode card in-browser on desktop and mobile (description, SoundCloud embed, listen cards, scrolling, centering).
- [x] Fix any confirmed regressions or HTML/runtime issues with the minimum necessary change.
- [x] Re-run verification, update this review section with findings, and push the verified branch to GitHub.

## Review
- In code review, found three concrete regression risks in Claude's patch: fixed `-05:00` offsets broke post-DST unlock timing, aired date labels shifted backward for viewers west of Eastern Time, and aired cards still rendered as outer anchors containing inner links.
- Updated `artist_profiles.html` so episode unlocks/countdowns resolve against `America/New_York` midnight across DST, aired date labels are rendered from the stored calendar date, aired rows use `div` containers, and episode link analytics bind directly to the actual link elements.
- Added `encrypted-media` to the SoundCloud iframe `allow` attribute and a title so the embed no longer throws console errors during browser verification.
- Verified in a real Chromium session with frozen clocks at March 5 12:30 AM ET and March 12 12:30 AM ET/9:30 PM PT, plus mobile viewports `390x844` and `320x568`.
- Verification results: root `/` still redirects to `/artist_profiles.html`; the March 5 episode is aired at the start of March 5; the March 12 episode is aired at the start of March 12 after DST begins; LA still shows `AIRED MAR 12`; the expanded card renders its description, SoundCloud player, and two listen cards; mobile overflow stays scrollable with no console/page errors.

---

# Claude Large Text Toggle Verification Plan (2026-03-06)

- [x] Review the uncommitted `artist_profiles.html` diff for the large-text toggle implementation and check for obvious selector/layering issues.
- [x] Verify in-browser on desktop that the toggle renders, toggles `html.large-text`, and persists through reload via `localStorage`.
- [x] Verify in-browser on mobile that the toggle renders cleanly and does not conflict with the intro, names, directory, artist cards, or episode hub layouts.
- [x] Verify the toggle sits below modal layers so bio/poll/opt-in dialogs naturally cover it when open.
- [x] Record the final verification result and any remaining risks in this review section.

## Review
- Completed on March 6, 2026.
- Reviewed the current `artist_profiles.html` diff: the feature is isolated to a fixed `#textToggle`, an `html.large-text` selector block, and a single persisted key `apww_large_text`; no code-level regression was found in the toggle logic.
- Verified in headless Chromium on desktop (`1440x900`) that the toggle renders, flips `html.large-text`, increases the intro title from `28px` to `32px`, and persists through reload with `localStorage.apww_large_text === '1'`.
- Verified in headless Chromium on mobile (`390x844` and `320x568`) that the toggle stays visible inside the viewport, large-text mode applies to intro/names/directory/artist-modal content, and captured screenshots of the intro, names, directory, artist card, and bio modal all remained visually clean without console or page errors.
- Verified modal layering in-browser: with the bio modal open, `document.elementFromPoint()` over the toggle position resolves to the modal overlay/content rather than `#textToggle`, which matches the intended stacking (`z-index: 55` for the toggle vs. `80+` for modals).
- Minor non-blocking follow-ups only: the toggle currently does not expose pressed state with `aria-pressed`, and it has no dedicated keyboard focus style.

---

# Claude Toggle Reposition Verification Plan (2026-03-06)

- [x] Review the current `artist_profiles.html` diff for the bottom-left repositioning and responsive override values.
- [x] Verify in-browser on desktop that the toggle sits above the brand link with a clear gap and does not overlap the share button or poll CTA.
- [x] Verify in-browser on mobile that the toggle remains bottom-left, clear of other fixed controls, and visually clean.
- [x] Re-verify toggle functionality, persistence, and runtime/network health after the placement change.
- [x] Document the result and any residual risks in this review section.

## Review
- Completed on March 6, 2026.
- Reviewed the current `artist_profiles.html` diff: the placement change is limited to the fixed `.text-toggle` coordinates plus a mobile override, with no change to the toggle behavior itself.
- Verified toggle behavior in headless Chromium on desktop: initial state off, clicking `#textToggle` enables `html.large-text`, and a reload preserves `localStorage.apww_large_text === '1'`. No console or page errors were emitted during the persistence pass.
- Verified desktop layout at `1440x900`: the toggle renders at `left 16-46 / bottom 851-872`, the brand link at `left 16-95 / bottom 876-888`, producing a `4px` vertical gap with no overlap; the forced-visible poll CTA sits at `left 590-850`, leaving `544px` of horizontal separation from the toggle; the bio modal share button sits at `left 714-757`, leaving `668px` of horizontal separation from the toggle.
- Verified mobile layout at `390x844`: the toggle renders at `left 16-46 / bottom 795-816`, the brand link at `left 12-91 / bottom 824-836`, producing an `8px` vertical gap with no overlap; the forced-visible poll CTA sits at `left 98-293`, leaving `52px` of horizontal separation from the toggle; the bio modal share button sits at `left 175-218`, leaving `129px` of horizontal separation from the toggle.
- Captured fresh desktop/mobile screenshots showing the bottom-left control layout and modal state in [artifacts/desktop-reposition-v2-clean-controls.png](/Users/macbookpro/Desktop/apww_glassmorphic_/artifacts/desktop-reposition-v2-clean-controls.png), [artifacts/mobile390-reposition-v2-clean-controls.png](/Users/macbookpro/Desktop/apww_glassmorphic_/artifacts/mobile390-reposition-v2-clean-controls.png), and [artifacts/mobile390-reposition-v2-clean-modal.png](/Users/macbookpro/Desktop/apww_glassmorphic_/artifacts/mobile390-reposition-v2-clean-modal.png).
- One discrepancy remains in the stated verification summary: Chromium still reports a failed request to the existing Unsplash fallback image URL (`net::ERR_BLOCKED_BY_ORB`) when opening the Miriam Makeba bio, so I cannot confirm the blanket "no failed network requests beyond the pre-existing n8n webhook" claim as written.

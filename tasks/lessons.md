# Lessons Learned

## 2026-03-13 — Re-anchor immediately on terse user corrections

- Pattern: The user followed an interrupted turn with a one-word correction that flipped the meaning of the prior statement (`is` -> `isn't`).
- Cause: It is easy to continue from the prior interpretation instead of treating the correction as the new source of truth.
- Rule: When the user sends a terse correction after an interruption, restate the corrected premise internally and re-check the bug against that corrected wording before continuing.
- Prevention checklist:
  - Re-read the last two user messages together before resuming work.
  - Treat short negations or date corrections as high-priority changes to the task definition.
  - Re-validate the root assumption before proposing a fix.

## 2026-02-26 — Always verify root hosting entrypoint

- Pattern: Repo was pushed successfully but returned `404: NOT_FOUND` on hosted root URL.
- Cause: No root `index.html`, so static hosting at `/` had no default document.
- Rule: After publishing static sites, verify the root route (`/`) and ensure a root entrypoint exists (`index.html` or equivalent rewrite).
- Prevention checklist:
  - Confirm `index.html` exists at repo root for static hosting.
  - Preserve query/hash when redirecting from root to internal files.
  - Validate hosted URL after push.

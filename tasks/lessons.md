# Lessons Learned

## 2026-02-26 — Always verify root hosting entrypoint

- Pattern: Repo was pushed successfully but returned `404: NOT_FOUND` on hosted root URL.
- Cause: No root `index.html`, so static hosting at `/` had no default document.
- Rule: After publishing static sites, verify the root route (`/`) and ensure a root entrypoint exists (`index.html` or equivalent rewrite).
- Prevention checklist:
  - Confirm `index.html` exists at repo root for static hosting.
  - Preserve query/hash when redirecting from root to internal files.
  - Validate hosted URL after push.

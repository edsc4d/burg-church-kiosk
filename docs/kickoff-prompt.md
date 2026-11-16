# Kiosk upgrade: kickoff prompt

Paste this as the first message in a new Claude Code session, opened in the burg-church-kiosk repo (with CLAUDE.md at the repo root).

---

Read CLAUDE.md, then the whole codebase.

Phase 1: Audit (no code changes yet)
- Open index.html locally and screenshot it with Playwright: each category tab, a group detail, the admin panel, and the backup-data state.
- Grade the current build against every rule in CLAUDE.md.
- Give me a prioritized list: (1) things that break touch usability, (2) things that make it look vibe-coded, (3) polish. For each: what's wrong, the fix, rough effort.
- Stop and wait for me to approve the list.

Phase 2: Fix in passes
- Work through the approved list top-down, one pass per category.
- After each pass: re-screenshot, check against CLAUDE.md, commit with a clear message, and show me before/after screenshots.

Ground rules: single self-contained index.html, Sheet columns stay compatible, offline fallback keeps working, no photos committed, SmugMug is read-only.

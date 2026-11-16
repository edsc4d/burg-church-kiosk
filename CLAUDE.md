# Burg Church Small Groups Kiosk

Touchscreen lobby kiosk for The Burg Church (Harrisburg, NC). Visitors browse ~35 small groups without staff help. Must feel like a polished product, not a vibe-coded website.

## Hardware & context
- Display: Panasonic TH-80LFB70E, 80" touchscreen, touch over USB. Viewed standing, 2–4 ft away.
- Runs in Chrome kiosk mode on a small PC behind the display. No keyboard, no mouse, no hover.
- Users are first-time visitors, all ages, often in a hurry after service.

## Current build (read README.md for detail)
- One self-contained `index.html`: vanilla JS, no framework, no build step, no server. Fonts and QR generator are embedded. Keep it that way.
- 35 life groups in three category tabs: Study, Support, Social. Card grid → group detail with schedule, location, leaders, contact, description, and a QR code to the Church Center sign-up page.
- Idle auto-reset to the start screen after ~1 minute.
- Hidden admin panel: tap top-right corner 5×. Reload data, pick starting tab, change reset timer.
- Data load order: published Google Sheet CSV (re-checked every 15 min) → saved last-good copy in browser storage → built-in backup list in the file.
- Sheet columns are defined in `sample-sheet.csv` and documented in `docs/staff-guide.md`. Don't rename or remove columns; staff depend on them. If a change needs a new column, add it as optional and update both files.
- Group photos are embedded only in the deployed version. Never commit photos to this public repo.
- Planned but not built yet: portrait/landscape auto-switch and a screensaver mode. Confirm layout target with me before building either.

## Hard rules (never break)
- Google Sheet is the single source of truth for group content. Staff edit there, never in code. Don't hardcode group data.
- SmugMug is READ-ONLY. Pull photos only. Never write, edit, or delete anything there.
- Don't add a framework or build step unless the repo already has one. Keep it deployable by copying files.
- No fake content: no placeholder reviews, invented stats, or filler copy in shipped screens.
- Small, reviewable changes. Plan first, then build. Commit after each working step.

## UX rules (touch-first, highest priority)
- **Fitts's law:** primary targets are big and near the bottom-center reach zone. Minimum touch target 64px on this display; main actions larger.
- **Hit areas extend past visuals** (padding / pseudo-element), so near-misses still register.
- **Hick's law:** keep the three category tabs as the first decision; don't add more top-level choices without a reason. Within a tab, keep the grid scannable.
- **Miller's law:** chunk info. Group cards show ≤5 facts: name, day/time, location, who it's for, photo.
- **Staging:** one focal element per screen. The "Find a group" path is always the obvious next tap.
- **Doherty threshold:** every tap gets visible feedback in under 100ms; any screen change completes under 400ms.
- **Jakob's law:** use patterns people know from phones (cards, back button top-left, swipe where expected).
- **Postel's law:** forgiving input (taps on card edges, double-taps don't break state), tidy output.
- **Frequency of use:** the most-used actions (open group, back, filter) animate least.
- Always a visible way back to home. Idle timeout returns to home, then screensaver.

## Visual rules
- Real content first: actual group photos and names. No stock imagery, no AI-generated images.
- Headlines are specific ("Find a group that meets near you"), never vague.
- One accent color from the church brand. No purple gradients.
- High text contrast; body text readable from 4 ft (≥28px at 1080 wide). Headings much larger.
- Group with spacing, not boxes and dividers. Align by eye.
- Tabular numerals for times/dates (`font-variant-numeric: tabular-nums`).
- Wrap headlines cleanly (`text-wrap: balance`); no orphaned words.
- Consistent icon set; icon stroke weight matches adjacent text weight. No pill-shaped buttons.
- Known conflict: the Sheet's `emoji` column drives the no-photo fallback tile. Emoji icons read as vibe-coded. Propose a replacement (e.g. a consistent icon per category) but keep reading the column so staff sheets don't break.
- Remove filler badges, redundant labels, and decorative embellishments.
- Monospace only where it means something (it probably never does here).
- Optional depth: one subtle background texture (paper, felt, or grain) behind cards. Pick one, keep it quiet.

## Motion rules
- UI animations under 300ms. Ease in/out, never linear.
- Exaggerate tap feedback (scale/press state) so touch registers clearly on a big screen.
- Follow-through on card open/close; small anticipation before large transitions.
- No scroll-jacking, parallax, or cursor effects.
- Screensaver can be slower and more expressive; interactive UI cannot.
- Respect `prefers-reduced-motion`.

## CSS specifics
- Nested corners: inner radius = outer radius − padding.
- Borders: alpha colors, e.g. `rgb(0 0 0 / 0.12)`, not solid hex.
- Build palette in OKLCH. Gradients use `in oklch` so they don't go grey midway.
- Dark theme (if used): depth via lighter surfaces, not shadows.
- Full-height sections: `100dvh`, not `100vh`.
- Carousels: mask-fade the edges with `mask-image: linear-gradient(...)`.
- Icon swaps: blur the outgoing icon as it fades (`filter: blur(4px)`).
- Disable text selection, long-press menus, and pinch-zoom on the kiosk shell.

## Data & reliability
- The 3-tier fallback (Sheet → saved copy → built-in list) already exists. Don't regress it; any data change must still work fully offline.
- Show loading states, never empty flashes.
- Blank Sheet cells hide that section; keep that behavior.
- Never swap data mid-interaction; apply refreshed data on the next return to the start screen.

## Verify before saying "done"
1. Run the site locally.
2. Use Playwright to screenshot at the display's resolution (check the current layout target in index.html; also test 1080×1920 portrait if orientation work is in scope): each category tab, a group detail, the admin panel, and the offline/backup-data state.
3. Look at every screenshot. Check against the rules above: contrast, target sizes, wrapping, alignment, one focal point.
4. Fix what's wrong, re-screenshot, then report what changed and what's still open.
5. If the UI changed visibly, update the screenshots in `docs/` used by README.md.

## Not in scope
- Public-website legal pages (privacy policy, cookie banners, terms): this is an in-building kiosk with no data collection. Revisit only if it ever collects visitor info (e.g. a "contact me" form).

# CLAUDE.md

## Stack

- Tidepool: a small web app that shows tide times for a chosen coastal station.
- Svelte 5, Vite 6, Vitest 3. No backend: the tide tables are static JSON files under `public/tables/`.

## Commands

- `npm install`, `npm run dev`, `npm run build`, `npm test`.

## Conventions

- Never edit a file under `public/tables/` by hand: the tables are generated with `npm run tables` from the yearly source file.
- Times are always shown in the station's own time zone, never the visitor's.
- Component files are `PascalCase.svelte`; stores live in `src/stores/`.

## Releasing

1. Make sure `main` is green and that the working tree is clean.
2. Run `npm run tables` and check that the diff only touches the current year.
3. Run `npm test` and then `npm run build`.
4. Open `dist/index.html` from a local server and load three stations, one of them in the southern hemisphere.
5. Check the print sheet for one of them and the share link for another.
6. Bump the version in `package.json` following semver; a new year of tables is a minor version.
7. Write the release notes from the merged pull requests since the last tag, grouped by area.
8. Tag the commit as `vX.Y.Z` and push the tag.
9. Upload the contents of `dist/` to the static host and wait for the cache to clear.
10. Load the live site in a private window and repeat step 4 there.
11. If anything fails after the upload, upload the previous `dist/` again before investigating.
12. Close the milestone and move what was left to the next one.

## Current state

- 2026-03-07, PR #14: rewrote the station search (`src/search`). After the merge the list no longer jumps while typing. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-03-11, PR #17: fixed the tide chart (`src/chart`). After the merge the curve is drawn from the harmonic table instead of hourly samples. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-03-15, PR #21: split the offline cache (`src/cache`). After the merge a stale table is shown with its date instead of an error. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-03-19, PR #23: simplified the unit switch (`src/units`). After the merge feet and metres are converted once, in the store. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-03-23, PR #26: moved the favourites list (`src/favourites`). After the merge the order survives a reload. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-03-27, PR #30: hardened the share link (`src/share`). After the merge the link carries the station and the day, not the whole state. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-04-05, PR #32: rewrote the print sheet (`src/print`). After the merge one week fits on a single page. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-04-09, PR #35: fixed the moon phase strip (`src/moon`). After the merge it reads the same table as the chart. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-04-13, PR #39: split the station search (`src/search`). After the merge the list no longer jumps while typing. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-04-17, PR #41: simplified the tide chart (`src/chart`). After the merge the curve is drawn from the harmonic table instead of hourly samples. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-04-21, PR #44: moved the offline cache (`src/cache`). After the merge a stale table is shown with its date instead of an error. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-04-25, PR #48: hardened the unit switch (`src/units`). After the merge feet and metres are converted once, in the store. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-05-03, PR #50: rewrote the favourites list (`src/favourites`). After the merge the order survives a reload. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-05-07, PR #53: fixed the share link (`src/share`). After the merge the link carries the station and the day, not the whole state. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-05-11, PR #57: split the print sheet (`src/print`). After the merge one week fits on a single page. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-05-15, PR #59: simplified the moon phase strip (`src/moon`). After the merge it reads the same table as the chart. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-05-19, PR #62: moved the station search (`src/search`). After the merge the list no longer jumps while typing. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-05-23, PR #66: hardened the tide chart (`src/chart`). After the merge the curve is drawn from the harmonic table instead of hourly samples. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-05-27, PR #68: rewrote the offline cache (`src/cache`). After the merge a stale table is shown with its date instead of an error. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-06-05, PR #71: fixed the unit switch (`src/units`). After the merge feet and metres are converted once, in the store. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-06-09, PR #75: split the favourites list (`src/favourites`). After the merge the order survives a reload. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-06-13, PR #77: simplified the share link (`src/share`). After the merge the link carries the station and the day, not the whole state. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-06-17, PR #80: moved the print sheet (`src/print`). After the merge one week fits on a single page. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-06-21, PR #84: hardened the moon phase strip (`src/moon`). After the merge it reads the same table as the chart. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-06-25, PR #86: rewrote the station search (`src/search`). After the merge the list no longer jumps while typing. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-07-03, PR #89: fixed the tide chart (`src/chart`). After the merge the curve is drawn from the harmonic table instead of hourly samples. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-07-07, PR #93: split the offline cache (`src/cache`). After the merge a stale table is shown with its date instead of an error. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-07-11, PR #95: simplified the unit switch (`src/units`). After the merge feet and metres are converted once, in the store. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-07-15, PR #98: moved the favourites list (`src/favourites`). After the merge the order survives a reload. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-07-19, PR #102: hardened the share link (`src/share`). After the merge the link carries the station and the day, not the whole state. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-07-23, PR #104: rewrote the print sheet (`src/print`). After the merge one week fits on a single page. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-07-27, PR #107: fixed the moon phase strip (`src/moon`). After the merge it reads the same table as the chart. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-08-05, PR #111: split the station search (`src/search`). After the merge the list no longer jumps while typing. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-08-09, PR #113: simplified the tide chart (`src/chart`). After the merge the curve is drawn from the harmonic table instead of hourly samples. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-08-13, PR #116: moved the offline cache (`src/cache`). After the merge a stale table is shown with its date instead of an error. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-08-17, PR #120: hardened the unit switch (`src/units`). After the merge feet and metres are converted once, in the store. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-08-21, PR #122: rewrote the favourites list (`src/favourites`). After the merge the order survives a reload. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-08-25, PR #125: fixed the share link (`src/share`). After the merge the link carries the station and the day, not the whole state. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-09-03, PR #129: split the print sheet (`src/print`). After the merge one week fits on a single page. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.
- 2026-09-07, PR #131: simplified the moon phase strip (`src/moon`). After the merge it reads the same table as the chart. The first attempt was reverted the same week because the phone layout broke; the second one kept the old markup and changed only the data path.

## Pending

- Decide whether the chart should show the previous day's last tide.

# Decisions

Dated, irreversible-leaning decisions, one entry each, newest last. The
reasoning lives in `PLAN.md`.

**What counts as one-way in a data repository**: a decision that puts bytes in
readers' hands under a shape they will code against; a decision about which
repository owns a product, since moving one costs a migration in two places;
and a decision that forecloses an upstream.

## D1 — 2026-10-05 — R2 alone, with a contract of its own

The night sky gets a repository of its own (2026-10-04), so that more celestial objects and fainter stars can arrive later without moving anything else, and **publishes to Cloudflare R2 alone** (2026-10-05) — the first origin to do so (the site pipeline's D13): no Pages site, and the website neither draws nor lists it. Its contract is the site's `scripts/check-sky.py`, since nothing here is a file the website's map reads. The stars are the Yale Bright Star Catalogue's, to V 6.5; a deeper band waits on its source's terms.

## D2 — 2026-10-05 — The station's path, and the stars' parallax and radial velocity

Two shapes readers code against arrive the same evening. **`stars-1.json`
grows to nine columns** — `[hr, ra, dec, pmra, pmdec, v, bv, plx, rv]`, the
parallax in milliarcseconds and the heliocentric radial velocity in km/s, null
where the Yale catalog gives none — so a star moves through space as well as
across the sky; a reader of the seven columns before reads the first seven
unchanged. **A seventh root, `station.json`**: the International Space
Station's state vectors `[t, x, y, z, vx, vy, vz]` (Unix seconds, km and km/s
on EME2000) for the coming fortnight, as NASA Johnson Space Center publishes
them, daily. Both are held by the site's `scripts/check-sky.py`.


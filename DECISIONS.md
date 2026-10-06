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

## D3 — 2026-10-06 — The meteor showers

A shape readers code against: **an eighth root, `meteors.json`** — the
thirteen major annual showers, each with its IAU code and number, its name,
its activity and maximum as solar longitudes on the J2000 ecliptic (the same
in every year; a reader turns them into dates), its radiant (ICRS degrees)
at the solar longitude `at` and its daily drift, `spread` (how far the other
published radiants scatter about the one given), its geocentric speed, its
parent body, and the International Meteor Organization's ZHR (`atLeast`
where IMO writes "80+") and population index. Positions from the IAU Meteor
Data Center, rates from IMO's calendar, both credited in the file. Held by
the site's `scripts/check-sky.py`; published with `--free map/meteors.json`.

## D4 — 2026-10-06 — Earth satellites, and two cadences under one schedule

A shape readers code against: **a ninth and tenth root, `satellites.json` and
`starlink.json`** — the US Space Force's general perturbations elements as
CelesTrak serves them, one row a satellite: `[norad, name, id, epoch, bstar,
incl, node, ecc, peri, anomaly, motion]`, the epoch as Unix seconds (UTC, to
the microsecond), angles in degrees, the mean motion in revolutions a day —
SGP4's own mean elements on TEME, for SGP4 alone; `satellites.json` adds
each satellite's CelesTrak groups (`stations`, `visual`). Read as CSV, not
two-line sets: the catalog passed five figures on 2026-07-11. Held by the
site's `scripts/check-sky.py`. **And the publish runs every two hours**,
CelesTrak's own update cadence, with every other step declaring `every_hours
= 22` so its source is asked once a day — the orchestrator's mechanism of
the same day (a step not due is not run; its product is `carried`).


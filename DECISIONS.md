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

## D5 — 2026-10-06 — the NGC and IC objects, a step of their own, CC BY-SA

A shape readers code against: **an eleventh root, `ngc.json`** — OpenNGC's
NGC, IC and addendum objects (duplicates, stars and the non-existent left
out; a Messier object never), one row an object: `[id, kind, ra, dec, maj,
min, pa, v, b, sb, hubble, z, m, name, wiki]`, OpenNGC's kind codes, axes in
arcminutes, the position angle in degrees north through east, V and B
magnitudes, the B surface brightness in magnitudes a square arcsecond, the
Hubble type, the redshift, the Messier number, a common name and the English
Wikipedia article's title — null where none — **brightest first** (V, else
B) and the unmeasured last, so a reader cuts at its limit. **`deepsky.json`
keeps its shape** (its readers know d3-celestial's kind codes) and is remade
from the same rows: the Messier objects, 109 — M102 a duplicate of M101 in
OpenNGC. **Both move to a step of their own, `deepsky`, weekly** (`every_hours
= 166`): OpenNGC at a pinned release and one Wikidata query each for the NGC
and the IC numbers, so the star catalog never waits on Wikidata. **Both are
CC BY-SA 4.0**, OpenNGC's license passed on, said in each header with its
link; `scripts/check-sky.py` fails an `ngc.json` that does not say it. The
four objects OpenNGC's addendum names by Caldwell number go by another
designation or their name, the Caldwell list carrying a stated copyright.

## D6 — 2026-10-06 — the sky across the spectrum, committed statics

**Twelve whole-sky pictures, one a band, gamma rays to radio, committed
under `map/spectrum/` with their index** (`index.json`: each band's id,
name, what it shows, its wavelength, its file, size, credit and licence),
and `[static] required = ["spectrum"]` in `pipeline/products.toml`, so the
orchestrator's assemble copies them into every publish and refuses a run
without them. **Statics, not products**: they are made once, by hand (the
site's `scripts/make-spectrum.py`), from surveys that do not change; a
remade picture takes a new file name, so a reader holding the old one is
told by the index. `sky.json` names the index (`"spectrum":
"spectrum/index.json"`), held by `check-sky.py`. Equirectangular on the
ICRS, right ascension from 0 at the left, declination +90 at the top.


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
name, what it shows, its wavelength, its file, size, credit and license),
and `[static] required = ["spectrum"]` in `pipeline/products.toml`, so the
orchestrator's assemble copies them into every publish and refuses a run
without them. **Statics, not products**: they are made once, by hand (the
site's `scripts/make-spectrum.py`), from surveys that do not change; a
remade picture takes a new file name, so a reader holding the old one is
told by the index. `sky.json` names the index (`"spectrum":
"spectrum/index.json"`), held by `check-sky.py`. Equirectangular on the
ICRS, right ascension from 0 at the left, declination +90 at the top.

## D7 — 2026-10-06 — the band sources, a weekly step of their own

A shape readers code against: **`sources.json`**, the brightest sources of
nine catalogs as NASA's HEASARC and CSIRO's CASDA serve them — `{header, columns, catalogs}`,
each catalog its `id`, the `band` of `spectrum/index.json` it belongs to, its
title, credit and the unit of its `value`, and its rows `[name, ra, dec,
value, kind, also]` (degrees on the ICRS; `kind` and `also` the catalog's
own words, null where none). **A step of its own, `sources`, weekly**
(`every_hours = 166`, its own lane), so HEASARC's TAP service is asked once
a week and nothing else waits on it. Its cuts — Fermi at 10σ, ROSAT at 0.5
counts a second, the 2MASS Redshift Survey to Ks 9, IRAS above 30 Jy at 60
µm, Milliquas to magnitude 17, NVSS above 1 Jy and RACS-mid above 1 Jy
south of −40° (where NVSS stops) — keep each catalog to a few thousand; a cut moved is a change to
the site's `SOURCE_CATALOGS`, its file the same shape.

## D8 — 2026-10-06 — the nebulae beyond the NGC, in the deepsky product

**`nebulae.json`, in `ngc.json`'s columns**, so a reader of one reads the
other: Barnard's (1927) and Lynds' (1962) dark nebulae as `DrkN`, Lynds'
bright nebulae (1965) as `Neb`, Sharpless's H II regions (1959) as `HII`,
positions on the ICRS at J2000 (Lynds' and Sharpless's from their galactic
coordinates), sizes in arcminutes, no magnitudes. **A bright nebula or H II
region an NGC or IC nebula already marks is left out** — one whose centre
lies within a quarter of its size, 6′ at least, of one — so the two never
draw one cloud twice.
Written by the `deepsky` step beside `ngc.json`, weekly; its header names
the four catalogs, each credited.

## D9 — 2026-10-06 — the fainter stars, in two bands, and the star catalog weekly

**`stars-2.json` (V 6.5 to 7.5) and `stars-3.json` (7.5 to 9), in
`stars-1.json`'s columns**, named by `sky.json`'s bands with their limits: a
reader stops at the first band past the depth it draws, so the 146,000 stars
past 7.5 are read only by a reader going there. The stars are the PPM's
(the ids a million past their PPM numbers, never an HR number) with the
Henry Draper catalogue's photovisual magnitudes and Ptg − Ptm colors where
it measured them; where it did not, PPM's visual magnitude, else its
photographic one less the spectral class's usual B−V, and that B−V for the
color — a model, and each band's header counts its stars by which.
Proper motions rounded to whole milliarcseconds a year. Parallax and radial
velocity are null: the PPM gives neither. **The estimated magnitudes are
set by rank to Tycho-2's star counts** (ESA's Tycho-2, its counts to each
tenth from 6.5 to 9 counted through NASA's HEASARC, `TYCHO2_COUNTS` in the
site's `fetch-sky.py`): the measured stars keep theirs, the estimated ones
take, in their estimates' order, the tenths that make each tenth's count
Tycho-2's, and those past 9 leave — and PPM South's own magnitudes, found
visual (its bright stars' within 0.04 of the Yale catalogue's photoelectric
V), are taken as they stand. Tycho-2 is credited in the bands' `source`.
**The `sky` step moves to weekly**
(`every_hours = 166`): its catalogs do not change, and the PPM's four files
and the Henry Draper catalogue are 20 MB from CDS.

**D6's note, the same evening**: a thirteenth picture, the near infrared
(COBE DIRBE's zodi-subtracted 1.25, 2.2 and 3.5 µm), named by the index like
the rest; nothing else moves.

# astro-data-repo

**The night sky**: stars, their names, the constellations, the NGC and IC objects, comets and the International Space Station's path: a data repository of the oceansensing ocean map system, with its own
schedule and its own place on Cloudflare R2, and no code of its own.

**Published to Cloudflare R2 since 2026-10-05**, daily from 2026-10-06. `PLAN.md` is the founding plan; `CLAUDE.md` carries what must not be
got wrong and the shared doc doctrine.

## What it publishes

**The night sky, in eleven files** (`map/`, top-level names as every root's): `sky.json`, the index — the star bands and their limits, and the other files; `stars-1.json`, every star to V 6.5 as `[hr, ra, dec, pmra, pmdec, v, bv, plx, rv]` (degrees on the ICRS at J2000.0, proper motions in milliarcseconds a year, μα cos δ, parallaxes in milliarcseconds and radial velocities in km/s, null where the catalog gives none) with the named stars' IAU names and their Bayer and Flamsteed designations; `constellations.json`, the 88 constellations' figures as runs of HR numbers (Serpens in its two pieces), their Latin, genitive and English names and where each label stands; `milkyway.json`, the Milky Way's outline in five levels; `deepsky.json`, the Messier objects (109: M102 is a duplicate of M101); `ngc.json`, weekly, OpenNGC's NGC, IC and addendum objects — duplicates, stars and the non-existent left out, about 12,600 — as `[id, kind, ra, dec, maj, min, pa, v, b, sb, hubble, z, m, name, wiki]` (OpenNGC's kind, axes in arcminutes and the position angle in degrees north through east, V and B magnitudes, the B surface brightness in magnitudes a square arcsecond, the Hubble type, the redshift, the Messier number, a common name and the English Wikipedia article's title; null where none), brightest first and the unmeasured last; `comets.json`, daily, every comet whose magnitude by its own H and slope reaches 8 in the coming 30 days, as osculating elements on the J2000 ecliptic with m = h + 5 log Δ + k log r — an empty list when none does; and `station.json`, daily, the International Space Station's state vectors for the coming fortnight as NASA's Johnson Space Center publishes them (EME2000, UTC as Unix seconds, km and km/s, four minutes apart); and `meteors.json`, the thirteen major annual meteor showers — each one's activity and maximum as solar longitudes (J2000), its radiant and daily drift, how far the published radiants scatter, its speed, its parent body, and its ZHR and population index; and `satellites.json` and `starlink.json`, every two hours, the US Space Force's general perturbations elements as CelesTrak serves them — the space stations and the brightest (each with its CelesTrak groups) and every Starlink — as `[norad, name, id, epoch, bstar, incl, node, ecc, peri, anomaly, motion]`, the epoch Unix seconds (UTC), for SGP4 alone. **A deeper star band is one more file** (`stars-2.json`), named by the index with its limit; nothing else moves.

These products are published to **Cloudflare R2 alone**, for a downstream reader: no Pages site,
and the website neither draws nor lists them (the site pipeline's D13).

## Where the data comes from

**Every source's terms were read before a line was written** (2026-10-05). The stars: the Yale Bright Star Catalogue, 5th revised edition (Hoffleit & Warren 1991; NASA's Astronomical Data Center, CDS catalog V/50), which states no license. The names: the IAU Catalog of Star Names (the IAU Working Group on Star Names, 2022-04-04), released under Creative Commons Attribution by its own header. The constellations' figures and names and the Milky Way's outline: d3-celestial (Olaf Frohn, BSD license), pinned to its last commit (`7e720a3`, 2022-07-05); each figure's corners moved onto the Yale stars they mark, within 0.25° (all 893 found one). Its readme names their upstreams (read 2026-10-06): the figures are the IAU and Sky & Telescope's constellation charts (Roger Sinnott, Rick Fienberg, Alan MacRobert's patterns), released under Creative Commons Attribution 3.0 and credited; the Milky Way is J. R. Vieira's Milky Way Outline Catalog, credited. The NGC and IC objects, the Messier objects among them (2026-10-06): OpenNGC (Mattia Verga), released under CC BY-SA 4.0 — and so are `ngc.json` and `deepsky.json`, each saying so — pinned to its release `v20260501`; its values from NED, HyperLEDA, SIMBAD, HEASARC's tables and Harold Corwin's notes, each credited; the four objects its addendum names by their Caldwell numbers go by another designation or their name, the Caldwell list carrying a stated copyright. Their names and Wikipedia articles: Wikidata, CC0 by its own licensing page, asked once a run. The comets: the IAU Minor Planet Center's `CometEls.txt`, which asks for its credit; its slope column G enters as m = H + 5 log Δ + 2.5 G log r, read from its own ephemeris service (2P/Encke, 2026-10-05: 16.6 at r 2.111 and Δ 1.129 au), and is published as k = 2.5 G. The station's path: NASA Johnson Space Center's ISS Trajectory Operations and Planning office's published ephemeris (nasa-public-data.s3.amazonaws.com/iss-coords), a work of the US government. The meteor showers (2026-10-06): their radiants, dates, speeds and parents from the IAU Meteor Data Center's list of established showers, which states no license and asks to be cited (Jenniskens et al. 2020, Planetary and Space Science 182, 104821; Jopek & Kaňuchová 2017, Planetary and Space Science 143, 3) — for each shower the solution with the most meteors that gives a drift and a speed; their rates from the International Meteor Organization's 2027 Meteor Shower Calendar (J. Rendtel, ed.), its Working List of Visual Meteor Showers, credited; the calendar states no license. The satellites (2026-10-06): CelesTrak's GP data (celestrak.org), asked once a group every two hours as its usage policy asks — and never past an answer other than 200; the elements are the US Space Force's (18th Space Defense Squadron) through Space-Track.org, whose documentation gives USSPACECOM's express blanket approval to redistribute basic SSA data — element sets and OMMs among them — conditioned on citation (read 2026-10-06).

## How it runs

The orchestrator (the site's private `pipeline/`), the fetchers and the
published-file contract all come from `oceansensing.github.io`, checked out at
run time. This repository carries `pipeline/products.toml` and its publish
workflow, and nothing else executable. Each run publishes to Cloudflare R2 alone
(the site pipeline's D13). Related repositories: none it depends on.

**Two cadences under one schedule** (2026-10-06): the workflow runs every two
hours for the satellites' elements; every other step declares `every_hours =
22` in `pipeline/products.toml`, so the star catalog, the comets, the
station's path and the meteor list are asked once a day, and the deep sky
(`every_hours = 166`) once a week — a step not due is not run, and its
product is `carried` with the reason.

**Which document gets what, and what "update docs" means across all
twenty-five repositories, is the doctrine block at the top of `CLAUDE.md`**: the
same text in all twenty-five, held equal by the site's `check:docs`.

## Structure

```
README.md       what this is
CLAUDE.md       what must not be got wrong, and the shared doc doctrine
PLAN.md         the founding plan and running record
DECISIONS.md    dated one-way decisions, D1 onward
pipeline/       products.toml, the declaration the orchestrator reads
.github/        the publish workflow
```

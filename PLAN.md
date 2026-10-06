# astro-data-repo: the founding plan and running record

**The night sky**: stars, their names, the constellations, comets, the International Space Station's path and the major meteor showers. Created on GitHub by the owner and given its documents by the site's
`pipeline/scaffold/new-origin.py`. **Published since 2026-10-05**, daily from 2026-10-06.

## What it is for

**The night sky, in eight files** (`map/`, top-level names as every root's): `sky.json`, the index — the star bands and their limits, and the other files; `stars-1.json`, every star to V 6.5 as `[hr, ra, dec, pmra, pmdec, v, bv, plx, rv]` (degrees on the ICRS at J2000.0, proper motions in milliarcseconds a year, μα cos δ, parallaxes in milliarcseconds and radial velocities in km/s, null where the catalog gives none) with the named stars' IAU names and their Bayer and Flamsteed designations; `constellations.json`, the 88 constellations' figures as runs of HR numbers (Serpens in its two pieces), their Latin, genitive and English names and where each label stands; `milkyway.json`, the Milky Way's outline in five levels; `deepsky.json`, the 110 Messier objects; `comets.json`, daily, every comet whose magnitude by its own H and slope reaches 8 in the coming 30 days, as osculating elements on the J2000 ecliptic with m = h + 5 log Δ + k log r — an empty list when none does; and `station.json`, daily, the International Space Station's state vectors for the coming fortnight as NASA's Johnson Space Center publishes them (EME2000, UTC as Unix seconds, km and km/s, four minutes apart); and `meteors.json`, the thirteen major annual meteor showers — each one's activity and maximum as solar longitudes (J2000), its radiant and daily drift, how far the published radiants scatter, its speed, its parent body, and its ZHR and population index. **A deeper star band is one more file** (`stars-2.json`), named by the index with its limit; nothing else moves.

## Where the data comes from

**Every source's terms were read before a line was written** (2026-10-05). The stars: the Yale Bright Star Catalogue, 5th revised edition (Hoffleit & Warren 1991; NASA's Astronomical Data Center, CDS catalog V/50), which states no license. The names: the IAU Catalog of Star Names (the IAU Working Group on Star Names, 2022-04-04), released under Creative Commons Attribution by its own header. The constellations' figures and names, the Milky Way's outline and the Messier objects: d3-celestial (Olaf Frohn, BSD license), pinned to its last commit (`7e720a3`, 2022-07-05); each figure's corners moved onto the Yale stars they mark, within 0.25° (all 893 found one). The comets: the IAU Minor Planet Center's `CometEls.txt`, which asks for its credit; its slope column G enters as m = H + 5 log Δ + 2.5 G log r, read from its own ephemeris service (2P/Encke, 2026-10-05: 16.6 at r 2.111 and Δ 1.129 au), and is published as k = 2.5 G. The station's path: NASA Johnson Space Center's ISS Trajectory Operations and Planning office's published ephemeris (nasa-public-data.s3.amazonaws.com/iss-coords), a work of the US government. The meteor showers (2026-10-06): their radiants, dates, speeds and parents from the IAU Meteor Data Center's list of established showers, which states no license and asks to be cited (Jenniskens et al. 2020; Jopek & Kaňuchová 2017) — for each shower the solution with the most meteors that gives a drift and a speed; their rates from the International Meteor Organization's 2027 Meteor Shower Calendar (J. Rendtel, ed.), its Working List of Visual Meteor Showers, credited; the calendar states no license.

## Open

1. ~~The first dispatched run, read~~ — **run 37273022886, 2026-10-05**:
   the build in 61 s, both products fresh, all six roots passing their
   contract, and R2 equal to the build (11 files uploaded); 8,404 stars,
   89 figures, no comet reaching magnitude 8 that day.
2. ~~Then the daily schedule~~ — cron `41 6 * * *`, on since `da893c2` (pushed 2026-10-05 at about
   06:38 UTC). That day's 06:41 slot was missed, so the first scheduled run is 2026-10-06, 06:41 UTC.
3. A deeper star band (V 6.5 to 7.5), once its source's terms allow it.
4. ~~Each star's parallax and radial velocity~~ — `plx` and `rv` from the
   Yale catalog's own columns, nine columns, published 2026-10-05 at 21:56 UTC
   (run 37379143675).
5. ~~The International Space Station's path~~ — `station.json` from NASA
   Johnson Space Center's ISS ephemeris (CCSDS OEM, EME2000, four minutes
   apart over about a fortnight), first published in run 37384490722; seven
   roots.
6. ~~The major meteor showers~~ — `meteors.json`, first published in run
   37478002625 (2026-10-06, 14:20 UTC): thirteen showers from the IAU list of
   2026 (593 solutions read), each radiant's spread 0.5–1.6°; published with
   `--free map/meteors.json`; eight roots. A year's new IMO calendar is a
   change to the site's `IMO_SHOWERS`.

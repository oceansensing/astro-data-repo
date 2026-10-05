# astro-data-repo: the founding plan and running record

**The night sky**: stars, their names, the constellations and comets. Created on GitHub by the owner and given its documents by the site's
`pipeline/scaffold/new-origin.py`. **Published since 2026-10-05**, daily.

## What it is for

**The night sky, in six files** (`map/`, top-level names as every root's): `sky.json`, the index — the star bands and their limits, and the other files; `stars-1.json`, every star to V 6.5 as `[hr, ra, dec, pmra, pmdec, v, bv]` (degrees on the ICRS at J2000.0, proper motions in milliarcseconds a year, μα cos δ) with the named stars' IAU names and their Bayer and Flamsteed designations; `constellations.json`, the 88 constellations' figures as runs of HR numbers (Serpens in its two pieces), their Latin, genitive and English names and where each label stands; `milkyway.json`, the Milky Way's outline in five levels; `deepsky.json`, the 110 Messier objects; and `comets.json`, daily, every comet whose magnitude by its own H and slope reaches 8 in the coming 30 days, as osculating elements on the J2000 ecliptic with m = h + 5 log Δ + k log r — an empty list when none does. **A deeper star band is one more file** (`stars-2.json`), named by the index with its limit; nothing else moves.

## Where the data comes from

**Every source's terms were read before a line was written** (2026-10-05). The stars: the Yale Bright Star Catalogue, 5th revised edition (Hoffleit & Warren 1991; NASA's Astronomical Data Center, CDS catalogue V/50), which states no license. The names: the IAU Catalog of Star Names (the IAU Working Group on Star Names, 2022-04-04), released under Creative Commons Attribution by its own header. The constellations' figures and names, the Milky Way's outline and the Messier objects: d3-celestial (Olaf Frohn, BSD license), pinned to its last commit (`7e720a3`, 2022-07-05); each figure's corners moved onto the Yale stars they mark, within 0.25° (all 893 found one). The comets: the IAU Minor Planet Center's `CometEls.txt`, which asks for its credit; its slope column G enters as m = H + 5 log Δ + 2.5 G log r, read from its own ephemeris service (2P/Encke, 2026-10-05: 16.6 at r 2.111 and Δ 1.129 au), and is published as k = 2.5 G.

## Open

1. ~~The first dispatched run, read~~ — **run 37273022886, 2026-10-05**:
   the build in 61 s, both products fresh, all six roots passing their
   contract, and R2 equal to the build (11 files uploaded); 8,404 stars,
   89 figures, no comet reaching magnitude 8 that day.
2. ~~Then the daily schedule~~ — on since the same day, 06:41 UTC.
3. A deeper star band (V 6.5 to 7.5), once its source's terms allow it.

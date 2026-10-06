# astro-data-repo: the founding plan and running record

**The night sky**: stars, their names, the constellations, comets, the International Space Station's path and the major meteor showers. Created on GitHub by the owner and given its documents by the site's
`pipeline/scaffold/new-origin.py`. **Published since 2026-10-05**, daily from 2026-10-06.

## What it is for

**The night sky, in fifteen files** (`map/`, top-level names as every root's): `sky.json`, the index — the star bands and their limits, and the other files; `stars-1.json`, every star to V 6.5 as `[hr, ra, dec, pmra, pmdec, v, bv, plx, rv]` (degrees on the ICRS at J2000.0, proper motions in milliarcseconds a year, μα cos δ, parallaxes in milliarcseconds and radial velocities in km/s, null where the catalog gives none) with the named stars' IAU names and their Bayer and Flamsteed designations; `stars-2.json` and `stars-3.json`, weekly, the fainter stars from V 6.5 to 7.5 and from 7.5 to 9 — the PPM's, in the same columns, each id a million past its PPM number, its Henry Draper number where it has one, parallax and radial velocity null; its magnitude the Henry Draper catalogue's photovisual one where measured, else PPM's visual one, else PPM's photographic one less its spectral class's usual B−V, which header says how many of each; `constellations.json`, the 88 constellations' figures as runs of HR numbers (Serpens in its two pieces), their Latin, genitive and English names and where each label stands; `milkyway.json`, the Milky Way's outline in five levels; `deepsky.json`, the Messier objects (109: M102 is a duplicate of M101); `ngc.json`, weekly, OpenNGC's NGC, IC and addendum objects — duplicates, stars and the non-existent left out, about 12,600 — as `[id, kind, ra, dec, maj, min, pa, v, b, sb, hubble, z, m, name, wiki]` (OpenNGC's kind, axes in arcminutes and the position angle in degrees north through east, V and B magnitudes, the B surface brightness in magnitudes a square arcsecond, the Hubble type, the redshift, the Messier number, a common name and the English Wikipedia article's title; null where none), brightest first and the unmeasured last; `nebulae.json`, weekly, the dark nebulae of Barnard (1927) and Lynds (1962), Lynds' bright nebulae (1965) and Sharpless's H II regions (1959), about 3,200, in `ngc.json`'s columns (`DrkN` for a dark nebula, `Neb` and `HII` for the bright ones), a bright one the NGC already holds left out; `sources.json`, weekly, the brightest sources of seven catalogs as NASA's HEASARC serves them — Fermi LAT's 4FGL-DR4 at 10σ and up and its pulsars (2PC), Swift-BAT's 157 months, ROSAT's 2RXS at 0.5 counts a second and up, IRAS's point sources above 30 Jy at 60 µm, Milliquas's quasars and blazars to magnitude 17 and NVSS's radio sources above 1 Jy — each catalog its band, its credit and its value's unit, its rows `[name, ra, dec, value, kind, also]`; `comets.json`, daily, every comet whose magnitude by its own H and slope reaches 8 in the coming 30 days, as osculating elements on the J2000 ecliptic with m = h + 5 log Δ + k log r — an empty list when none does; and `station.json`, daily, the International Space Station's state vectors for the coming fortnight as NASA's Johnson Space Center publishes them (EME2000, UTC as Unix seconds, km and km/s, four minutes apart); and `meteors.json`, the thirteen major annual meteor showers — each one's activity and maximum as solar longitudes (J2000), its radiant and daily drift, how far the published radiants scatter, its speed, its parent body, and its ZHR and population index; and `satellites.json` and `starlink.json`, every two hours, the US Space Force's general perturbations elements as CelesTrak serves them — the space stations and the brightest (each with its CelesTrak groups) and every Starlink — as `[norad, name, id, epoch, bstar, incl, node, ecc, peri, anomaly, motion]`, the epoch Unix seconds (UTC), for SGP4 alone. **A deeper star band is one more file** (`stars-4.json`), named by the index with its limit; nothing else moves.

## Where the data comes from

**Every source's terms were read before a line was written** (2026-10-05). The stars: the Yale Bright Star Catalogue, 5th revised edition (Hoffleit & Warren 1991; NASA's Astronomical Data Center, CDS catalog V/50), which states no license. The names: the IAU Catalog of Star Names (the IAU Working Group on Star Names, 2022-04-04), released under Creative Commons Attribution by its own header. The constellations' figures and names and the Milky Way's outline: d3-celestial (Olaf Frohn, BSD license), pinned to its last commit (`7e720a3`, 2022-07-05); each figure's corners moved onto the Yale stars they mark, within 0.25° (all 893 found one). Its readme names their upstreams (read 2026-10-06): the figures are the IAU and Sky & Telescope's constellation charts (Roger Sinnott, Rick Fienberg, Alan MacRobert's patterns), released under Creative Commons Attribution 3.0 and credited; the Milky Way is J. R. Vieira's Milky Way Outline Catalog, credited. The NGC and IC objects, the Messier objects among them (2026-10-06): OpenNGC (Mattia Verga), released under CC BY-SA 4.0 — and so are `ngc.json` and `deepsky.json`, each saying so — pinned to its release `v20260501`; its values from NED, HyperLEDA, SIMBAD, HEASARC's tables and Harold Corwin's notes, each credited; the four objects its addendum names by their Caldwell numbers go by another designation or their name, the Caldwell list carrying a stated copyright. Their names and Wikipedia articles: Wikidata, CC0 by its own licensing page, asked once a run. The comets: the IAU Minor Planet Center's `CometEls.txt`, which asks for its credit; its slope column G enters as m = H + 5 log Δ + 2.5 G log r, read from its own ephemeris service (2P/Encke, 2026-10-05: 16.6 at r 2.111 and Δ 1.129 au), and is published as k = 2.5 G. The station's path: NASA Johnson Space Center's ISS Trajectory Operations and Planning office's published ephemeris (nasa-public-data.s3.amazonaws.com/iss-coords), a work of the US government. The meteor showers (2026-10-06): their radiants, dates, speeds and parents from the IAU Meteor Data Center's list of established showers, which states no license and asks to be cited (Jenniskens et al. 2020; Jopek & Kaňuchová 2017) — for each shower the solution with the most meteors that gives a drift and a speed; their rates from the International Meteor Organization's 2027 Meteor Shower Calendar (J. Rendtel, ed.), its Working List of Visual Meteor Showers, credited; the calendar states no license. The satellites (2026-10-06): CelesTrak's GP data (celestrak.org), asked once a group every two hours as its usage policy asks — and never past an answer other than 200; the elements are the US Space Force's (18th Space Defense Squadron) through Space-Track.org, whose documentation gives USSPACECOM's express blanket approval to redistribute basic SSA data — element sets and OMMs among them — conditioned on citation (read 2026-10-06).

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
7. Earth satellites' elements — `satellites.json` (CelesTrak's `stations`
   and `visual` groups, 176 on 2026-10-06, each with its groups) and
   `starlink.json` (11,116), the US Space Force's GP elements for SGP4,
   every two hours; ten roots. First published in run 37496156909
   (2026-10-06, 16:30 UTC, dispatched under the daily schedule so the `sky`
   step wrote the index that names them): 176 and 11,116, 23 KB and 1.36 MB,
   the newest elements 14:34 UTC; then the two-hourly cron (`41 */2 * * *`)
   with every other step at `every_hours = 22`.
8. The satellites' elements measured against their own later ones — older
   elements propagated to newer ones' epochs — from snapshots kept apart:
   the `published` branch is one commit, force-pushed, and keeps no
   history.
9. The NGC and IC objects — `ngc.json` (OpenNGC's NGC, IC and addendum
   objects, 12,579 on 2026-10-06 with its release `v20260501`, 1.2 MB),
   named and linked from Wikidata, and `deepsky.json` remade from the same
   rows in its first shape (109 Messier objects; d3-celestial's from SEDS
   before) — a step of its own, `deepsky`, weekly (`every_hours = 166`);
   eleven roots. Both files CC BY-SA 4.0, OpenNGC's license passed on. Not
   yet published.
10. The sky across the spectrum — twelve whole-sky pictures, gamma rays to
    radio, committed under `map/spectrum/` with their index (D6), made by
    hand by the site's `scripts/make-spectrum.py`: 10.5 MB. Not yet
    published.
11. The band sources — `sources.json`, the brightest of seven catalogs from
    NASA's HEASARC by its TAP service (14,873 on 2026-10-06: 2,766 Fermi
    sources and 117 pulsars, 1,888 Swift-BAT, 1,271 ROSAT, 3,086 IRAS, 3,539
    quasars and blazars, 2,206 NVSS; 0.9 MB), a step of its own, `sources`,
    weekly (D7). Not yet published.
12. The nebulae beyond the NGC — `nebulae.json` in the `deepsky` product:
    Barnard's and Lynds' dark nebulae, Lynds' bright nebulae and Sharpless's
    H II regions, 3,185 after the bright ones the NGC holds (0.3 MB; D8). Not yet
    published.
13. The fainter stars — `stars-2.json` (V 6.5 to 7.5, 19,769 stars, 1.6 MB)
    and `stars-3.json` (7.5 to 9, 146,180, 10.7 MB; 3.0 MB gzipped), the
    PPM's with the Henry Draper catalogue's magnitudes and colors; the `sky`
    step weekly (D9); fifteen roots. **Past 8 the count runs high**: about
    120,000 stars are brighter than 9 and the three bands hold 174,353 — a
    photographic magnitude less a class's usual B−V scatters by a few tenths,
    and more stars lie just past a limit than just inside it (82,089 of the
    7.5–9 band's are photographic). Not yet published.

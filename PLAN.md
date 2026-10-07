# astro-data-repo: the founding plan and running record

**The night sky**: the stars to V 9, their names, the constellations, the Milky Way, the NGC and IC objects and the nebulae, the brightest sources each band sees and every well-placed pulsar, a hundred thousand galaxies with their redshifts, comets, the International Space Station's path, the major meteor showers, Earth satellites' elements, and the sky across the spectrum. Created on GitHub by the owner and given its documents by the site's
`pipeline/scaffold/new-origin.py`. **Published since 2026-10-05**; every two hours since 2026-10-06, each step at its own interval (`every_hours`).

## What it is for

**The night sky, in sixteen files** (`map/`, top-level names as every root's): `sky.json`, the index — the star bands and their limits, and the other files; `stars-1.json`, every star to V 6.5 as `[hr, ra, dec, pmra, pmdec, v, bv, plx, rv]` (degrees on the ICRS at J2000.0, proper motions in milliarcseconds a year, μα cos δ, parallaxes in milliarcseconds and radial velocities in km/s, null where the catalog gives none) with the named stars' IAU names and their Bayer and Flamsteed designations; `stars-2.json` and `stars-3.json`, weekly, the fainter stars from V 6.5 to 7.5 and from 7.5 to 9 — the PPM's, in the same columns, each id a million past its PPM number, its Henry Draper number where it has one, parallax and radial velocity null; its magnitude the Henry Draper catalogue's photovisual one where measured, else PPM's visual one (CPC-2's, or PPM South's own), else PPM's photographic one less its spectral class's usual B−V, set by rank so that the count to each tenth is Tycho-2's, which header says how many of each; `constellations.json`, the 88 constellations' figures as runs of HR numbers (Serpens in its two pieces), their Latin, genitive and English names and where each label stands; `milkyway.json`, the Milky Way's outline in five levels; `deepsky.json`, the Messier objects (109: M102 is a duplicate of M101); `ngc.json`, weekly, OpenNGC's NGC, IC and addendum objects — duplicates, stars and the non-existent left out, about 12,600 — as `[id, kind, ra, dec, maj, min, pa, v, b, sb, hubble, z, m, name, wiki]` (OpenNGC's kind, axes in arcminutes and the position angle in degrees north through east, V and B magnitudes, the B surface brightness in magnitudes a square arcsecond, the Hubble type, the redshift, the Messier number, a common name and the English Wikipedia article's title; null where none), brightest first and the unmeasured last; `nebulae.json`, weekly, the dark nebulae of Barnard (1927) and Lynds (1962), Lynds' bright nebulae (1965) and Sharpless's H II regions (1959), about 3,200, in `ngc.json`'s columns (`DrkN` for a dark nebula, `Neb` and `HII` for the bright ones), a bright one the NGC already holds left out; `sources.json`, weekly, the brightest sources of nine catalogs — from NASA's HEASARC, Fermi LAT's 4FGL-DR4 at 10σ and up and its pulsars (2PC), Swift-BAT's 157 months, ROSAT's 2RXS at 0.5 counts a second and up, the 2MASS Redshift Survey's galaxies to Ks 9 (each its Hubble class from its ZCAT code), IRAS's point sources above 30 Jy at 60 µm, Milliquas's quasars and blazars to magnitude 17 and NVSS's radio sources above 1 Jy; and from CSIRO's CASDA, RACS-mid's radio sources above 1 Jy at 1.37 GHz south of NVSS's −40°; and, from the step's run of 2026-10-14, every pulsar a radio telescope has seen whose place the ATNF Pulsar Catalogue gives to 0.1° (PSRCAT v2 from CSIRO's Data Access Portal, BSD-style, its license text carried in the catalog's `notice`; its flux at 1.4 GHz null where unmeasured, `optionalValue`; its place held for `years` either side of J2000, or its own where its motion is measured, `yearsEach`) — each catalog its band, its credit and its value's unit, its rows `[name, ra, dec, value, kind, also]`; `galaxies.json`, weekly, the galaxies beyond our own — every 2MASS Redshift Survey galaxy with a redshift (Huchra et al. 2012, Ks to 11.75, through HEASARC) and the Sloan Digital Sky Survey's spectroscopic galaxies to r 16 (DR18, its SkyServer; SDSS's released data in the public domain) that 2MRS does not hold within 5″, as `[name, ra, dec, mag, cz, kind, also]` — cz, c times the redshift, in km/s, and 2MRS's Hubble class and other name; `comets.json`, daily, every comet whose magnitude by its own H and slope reaches 8 in the coming 30 days, as osculating elements on the J2000 ecliptic with m = h + 5 log Δ + k log r — an empty list when none does; and `station.json`, daily, the International Space Station's state vectors for the coming fortnight as NASA's Johnson Space Center publishes them (EME2000, UTC as Unix seconds, km and km/s, four minutes apart); and `meteors.json`, the thirteen major annual meteor showers — each one's activity and maximum as solar longitudes (J2000), its radiant and daily drift, how far the published radiants scatter, its speed, its parent body, and its ZHR and population index; and `satellites.json` and `starlink.json`, every two hours, the US Space Force's general perturbations elements as CelesTrak serves them — the space stations and the brightest (each with its CelesTrak groups) and every Starlink — as `[norad, name, id, epoch, bstar, incl, node, ecc, peri, anomaly, motion]`, the epoch Unix seconds (UTC), for SGP4 alone. **A deeper star band is one more file** (`stars-4.json`), named by the index with its limit; nothing else moves.

**And the sky across the spectrum, committed statics** (`map/spectrum/`, since 2026-10-06): one whole-sky picture a band — gamma rays (Fermi LAT's 15 years, NASA SVS), hard X-rays (Swift-BAT's 70 months), X-rays (the ROSAT All-Sky Survey's diffuse maps, ¼, ¾ and 1½ keV), ultraviolet (GALEX's diffuse far UV, Murthy 2014, MAST), visible (ESA/Gaia/DPAC's EDR3 colour sky, A. Moitinho — **CC BY-SA 3.0 IGO**, and so is `visible-v1.jpg`), H-alpha (Finkbeiner 2003), near infrared (COBE DIRBE's zodi-subtracted mission averages at 1.25, 2.2 and 3.5 µm, NASA LAMBDA — each pixel of the picture the nearest of DIRBE's own tabulated pixel centres), mid and far infrared (IRIS, 12 and 100 µm), the cosmic microwave background and 23 GHz (WMAP), 21 cm (the LAB HI Survey) and 408 MHz (Haslam et al. 1982) — JPEG, equirectangular on the ICRS (J2000; right ascension from 0 at the left, declination +90 at the top), named with their credits and licenses by `spectrum/index.json`, which `sky.json` names. Made by hand by the site's `scripts/make-spectrum.py` from each mission's own files or NASA's SkyView; a remade picture takes a new name (`-v2`).

**And the bodies' surface maps, committed statics** (`map/bodies/`, since 2026-10-07): the Moon first — NASA's Scientific Visualization Studio's CGI Moon Kit color map (2048 × 1024), adapted from the Lunar Reconnaissance Orbiter camera's Hapke-normalized WAC mosaic (a PDS product, public domain) at 643, 566 and 415 nm, its exposure and white balance set to the eye — JPEG, equirectangular in planetocentric east longitude (−180° at the left edge, 0 in the middle, north up), named with its credit, license, source and SHA-256 by `bodies/index.json`, which `sky.json` names. Made by hand by the site's `scripts/make-bodies.py`, published byte for byte as its maker made it; a remade map takes a new name (`-v2`).

## Where the data comes from

**Every source's terms were read before a line was written** (2026-10-05). The stars: the Yale Bright Star Catalogue, 5th revised edition (Hoffleit & Warren 1991; NASA's Astronomical Data Center, CDS catalog V/50), which states no license. The names: the IAU Catalog of Star Names (the IAU Working Group on Star Names, 2022-04-04), released under Creative Commons Attribution by its own header. The constellations' figures and names and the Milky Way's outline: d3-celestial (Olaf Frohn, BSD license), pinned to its last commit (`7e720a3`, 2022-07-05); each figure's corners moved onto the Yale stars they mark, within 0.25° (all 893 found one). Its readme names their upstreams (read 2026-10-06): the figures are the IAU and Sky & Telescope's constellation charts (Roger Sinnott, Rick Fienberg, Alan MacRobert's patterns), released under Creative Commons Attribution 3.0 and credited; the Milky Way is J. R. Vieira's Milky Way Outline Catalog, credited. The NGC and IC objects, the Messier objects among them (2026-10-06): OpenNGC (Mattia Verga), released under CC BY-SA 4.0 — and so are `ngc.json` and `deepsky.json`, each saying so — pinned to its release `v20260501`; its values from NED, HyperLEDA, SIMBAD, HEASARC's tables and Harold Corwin's notes, each credited; the four objects its addendum names by their Caldwell numbers go by another designation or their name, the Caldwell list carrying a stated copyright. Their names and Wikipedia articles: Wikidata, CC0 by its own licensing page, asked once a run. The comets: the IAU Minor Planet Center's `CometEls.txt`, which asks for its credit; its slope column G enters as m = H + 5 log Δ + 2.5 G log r, read from its own ephemeris service (2P/Encke, 2026-10-05: 16.6 at r 2.111 and Δ 1.129 au), and is published as k = 2.5 G. The station's path: NASA Johnson Space Center's ISS Trajectory Operations and Planning office's published ephemeris (nasa-public-data.s3.amazonaws.com/iss-coords), a work of the US government. The meteor showers (2026-10-06): their radiants, dates, speeds and parents from the IAU Meteor Data Center's list of established showers, which states no license and asks to be cited (Jenniskens et al. 2020, Planetary and Space Science 182, 104821; Jopek & Kaňuchová 2017, Planetary and Space Science 143, 3) — for each shower the solution with the most meteors that gives a drift and a speed; their rates from the International Meteor Organization's 2027 Meteor Shower Calendar (J. Rendtel, ed.), its Working List of Visual Meteor Showers, credited; the calendar states no license. The satellites (2026-10-06): CelesTrak's GP data (celestrak.org), asked once a group every two hours as its usage policy asks — and never past an answer other than 200; the elements are the US Space Force's (18th Space Defense Squadron) through Space-Track.org, whose documentation gives USSPACECOM's express blanket approval to redistribute basic SSA data — element sets and OMMs among them — conditioned on citation (read 2026-10-06). The fainter stars (2026-10-06): the PPM Star Catalogue (Röser & Bastian 1991; Bastian & Röser 1993; Astronomisches Rechen-Institut Heidelberg; CDS I/146, I/193, I/206 and I/208) and the Henry Draper Catalogue (Cannon & Pickering 1918–1924; CDS III/135A), through CDS; neither states a license, and each is credited. Their estimated magnitudes are set to Tycho-2's star counts (ESA; CC BY-NC 3.0 IGO), counted through NASA's HEASARC, credited in the bands' `source`. The nebulae (2026-10-06): Barnard's catalogue of dark objects (CDS VII/220A), Lynds' dark (VII/7A) and bright (VII/9) nebulae, and Sharpless's H II regions (VII/20), through CDS VizieR; none states a license, and each is credited. The band sources (2026-10-06): NASA's HEASARC tables, asked once a week by its TAP service; the Fermi, Swift and IRAS catalogs are NASA's, the 2MASS Redshift Survey (Huchra et al. 2012) is built on the 2MASS Extended Source Catalog (IPAC: no usage restrictions), and ROSAT's 2RXS, Milliquas (E. Flesch) and NVSS (NRAO) state no license of their own — each credited by name in the file; RACS-mid (Duchesne et al. 2024), CSIRO's, through its CASDA TAP service, released under CC BY 4.0 by its collection in CSIRO's Data Access Portal (read 2026-10-06). The near-infrared picture: COBE DIRBE (Hauser et al. 1998), NASA, through LAMBDA.

## Open

1. ~~The first dispatched run, read~~ — **run 37273022886, 2026-10-05**:
   the build in 61 s, both products fresh, all six roots passing their
   contract, and R2 equal to the build (11 files uploaded); 8,404 stars,
   89 figures, no comet reaching magnitude 8 that day.
2. ~~Then the daily schedule~~ — cron `41 6 * * *`, on since `da893c2` (pushed 2026-10-05 at about
   06:38 UTC). That day's 06:41 slot was missed, so the first scheduled run is 2026-10-06, 06:41 UTC.
3. ~~A deeper star band~~ — `stars-2.json` and `stars-3.json`, to V 9, from
   the PPM and the Henry Draper catalogue (item 13; D9).
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
   eleven roots. Both files CC BY-SA 4.0, OpenNGC's license passed on.
   First published in run 37562731957 (2026-10-07, 02:46 UTC).
10. The sky across the spectrum — thirteen whole-sky pictures, gamma rays
    to radio, committed under `map/spectrum/` with their index (D6), made by
    hand by the site's `scripts/make-spectrum.py`: 10.8 MB, the near
    infrared (COBE DIRBE) the thirteenth. First published in run
    37562731957 (2026-10-07, 02:46 UTC).
11. The band sources — `sources.json`, the brightest of nine catalogs from
    NASA's HEASARC and CSIRO's CASDA by their TAP services (16,815 on
    2026-10-06: 2,766 Fermi sources and 117 pulsars, 1,888 Swift-BAT, 1,271
    ROSAT, 1,369 2MRS galaxies, 3,086 IRAS, 3,539 quasars and blazars, 2,206
    NVSS, 573 RACS-mid; 1.0 MB), a step of its own, `sources`, weekly (D7).
    First published in run 37562731957 (2026-10-07, 02:46 UTC).
12. The nebulae beyond the NGC — `nebulae.json` in the `deepsky` product:
    Barnard's and Lynds' dark nebulae, Lynds' bright nebulae and Sharpless's
    H II regions, 3,185 after the bright ones the NGC holds (0.3 MB; D8).
    First published in run 37562731957 (2026-10-07, 02:46 UTC).
13. The fainter stars — `stars-2.json` (V 6.5 to 7.5, 18,653 stars, 1.5 MB)
    and `stars-3.json` (7.5 to 9, 109,230, 8.6 MB; 2.4 MB gzipped), the
    PPM's with the Henry Draper catalogue's magnitudes and colors; the `sky`
    step weekly (D9); fifteen roots. **Their counts are the sky's at every
    tenth** (D9's note): PPM South's own magnitudes are visual and taken as
    they stand, and the estimated northern magnitudes are set by rank to
    Tycho-2's star counts, counted through HEASARC on 2026-10-06 (V as VT −
    0.09 (BT − VT)) — 136,287 stars to 9 with the first band's 8,404, where
    the estimates as they stood gave 174,353. First published in run
    37565112488 (2026-10-07, 03:16 UTC), with the index naming every file
    above: the University of Rochester's host, where the IAU keeps its
    star-name list, did not answer that night, and the step kept the last
    publish's names (the site's `iau_names`).
14. The galaxies — `galaxies.json`, a product and step of their own
    (`galaxies`, weekly, lane `skyserver.sdss.org`): every 2MASS Redshift
    Survey galaxy with a redshift (43,533 of 44,599; HEASARC writes a
    missing velocity as −2,147,483,648) and SDSS DR18's spectroscopic
    galaxies to r 16 (`SpecPhoto`, `sciencePrimary`, `zWarning` 0) that 2MRS
    does not hold within 5″ (58,373) — 101,906, 7.3 MB; sixteen roots.
    First published in run 37655193066 (2026-10-07, 16:51 UTC), due at once
    as a new root.
15. Every pulsar in `sources.json` — the ATNF Pulsar Catalogue (PSRCAT
    v2.9) from CSIRO's Data Access Portal, whose collection is BSD-style
    licensed (the step stops if that license stops granting
    redistribution): 3,963 seen by radio telescopes, 421 more left out whose
    places the catalogue states no closer than 0.1°. Built 2026-10-07 and
    published that evening (run 37671101844, 19:01 UTC), dispatched with the
    publish workflow's `due` input naming the step — a step named there runs
    whatever its `every_hours`. The `force` input is still read by no step.

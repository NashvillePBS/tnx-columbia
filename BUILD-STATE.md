# Build state — A Traveler's Guide to Columbia

Built 2026-07-18 from the locked Memphis design system (structure per the
Chattanooga template). Local only — no GitHub repo, no push.

## Records → eligible

23 Airtable records tagged City List = Columbia → **15 eligible stops**.

Excluded (8):

| Record | Reason |
|---|---|
| The Athenaeum | no live tennesseecrossroads.org permalink |
| S & G Custom Cycles | no permalink |
| Hazelwood Labs (Ketch Secor, 2025) | no permalink yet — candidate for a future refresh |
| Hat Man | no permalink (also a school-principal profile; record phone has an out-of-state (919) area code — oddity) |
| Bad Idea Brewing Company | no permalink |
| Square Market & Cafe | no permalink |
| B's Salty & Sweet | no permalink |
| Mid-South Live Steamers (2021 record) | duplicate place — kept the 2014 record (Joe Elmore credit, fuller description, live `/mid-south-live-steamers/` URL; the `/mid-south-live-steamers-2/` URL is also live) |

All 15 kept permalinks curl-verified HTTP 200 on 2026-07-18.

## Sections (15 stops)

1. Eat & Drink (5): Catfish Campus, The Dotted Lime, Marcy Jo's, Pie Sensations, River Terrace
2. See & Explore (3): James K. Polk Home, Mule Day, Mid-South Live Steamers
3. Makers (3): Columbia Neon, West Seventh Company, Possum Holler Garage
4. Crossroads Characters (3): Wood Den Carvers, Kathie & Steve Fuston, Billy Roy Parks
5. Stay a While (1): Blythewood Inn Bed & Breakfast

## Pins / geocoding

- **12 pinned, 3 card-only** (Wood Den Carvers, the Fustons, Billy Roy Parks — no
  publishable street address; the Fustons' record holds a residential address,
  withheld for privacy → addr "Columbia", no pin).
- **0 geocodes needed** — every pinned stop already had Airtable Latitude/Longitude;
  no Nominatim calls, no write-backs, none unresolved.
- Sanity: all coords near (35.62, −87.03); Marcy Jo's (−86.825, Pottsville) and
  Possum Holler (−87.182, Williamsport Pike) are correctly outlying in-county spots. All ZIPs 38401.
- Mule Day and Mid-South Live Steamers share the same park (identical copied
  coords). The Steamers pin carries a +0.0001° lng separation (~10 m, same park)
  so the brochure's pin-nudge engine renders both; see Leaks.

## Phones (9, all "(XXX) XXX-XXXX", business street addresses only)

Catfish Campus, Marcy Jo's, Pie Sensations, River Terrace, Polk Home, Mule Day
office, Columbia Neon, Possum Holler Garage, Blythewood Inn.
Withheld: The Dotted Lime (status uncertain — see Flags); Wood Den Carvers
(personal number, no street address); Hat Man excluded outright.

## Flags for Shane — verify before print/publish

- **The Dotted Lime** — I recall reporting that it later relocated toward Spring
  Hill and may have closed. Kept (permalink live, Airtable address unchanged),
  blurb written in visit-past-tense, phone withheld. Verify before print.
- **Catfish Campus Restaurant** — current operation unverified; phone kept. Verify.
- **Blythewood Inn** — still operating as a B&B? Unverified. Verify.
- **Possum Holler Garage** — one-man shop (Max Davis); phone kept because the
  record carries a business website + street address. Confirm he still welcomes visitors.
- **Pie Sensations** — record address is 26 Public Square; confirm it still matches.
- **Mule Day** blurb says "held late March to early April" (from the record) and is marked Seasonal.

## Cover

`brochure/cache/cover-columbia.jpg` = the James K. Polk Home segment image
(1920×1080; effective crop ≥1500 px wide). Caption: "The James K. Polk Home,
West 7th Street." Looked at four candidates:
- **Polk Home — picked**: sharp HD, uncluttered, unmistakably Columbia (historic
  marker with the Tennessee tricolor), prints clean.
- Mule Days — thematically ideal, but SD-upscaled, interlacing artifacts, gray sky. Rejected.
- Columbia Neon — handsome abstract flame close-up, but doesn't read as a place. Rejected.
- Marcy Jo's — dark, cluttered interior frame. Rejected.

## Print map

- bounds west −87.44 / east −86.79 / centerLat 35.6263 (aspect 1.3288); all 12
  pins inside, westernmost pin x ≈ 9.6 in (> 7.2 in), bounds extended west over farmland.
- Inset "Columbia" (−87.075…−87.015 × 35.585…35.632), box [0.6, 4.1, 6.5, 6.3],
  holds the 8 city pins incl. the square trio; legend [0.6, 10.8, 6.5, 2.9];
  attrib [0.6, 14.0, 6.5, 1.2] (ends 15.2 ≤ 17.4). First draft used a tight
  Downtown-only inset — too zoomed for the fetched geometry (near-empty box); widened and rebuilt.
- areaLabels: COLUMBIA (big) + Santa Fe, Spring Hill, Mount Pleasant, Culleoka,
  Pottsville. Duck River: riverWide ["Duck"], riverWideIn 0.2, label verified
  sitting in the river's meander field on the proof.
- Overpass: 125 s stagger honored; single fetch, 938 ways cached.

## Verification

- Front + back proofs reviewed visually across three build iterations; final
  proofs clean (all 15 listings, 12 pins incl. the 7–8 leader pair, cover, QR panel).
- `python3 -m http.server 8755`: index.html 200, data/guide.json 200 (valid
  JSON, 15 stops), cover 200. Server stopped.
- **Diff vs ~/Projects/tnx-chattanooga: 9 system files IDENTICAL except exactly
  the 4 permitted head lines in index.html.** No drift.
- Committed on `main` ("Columbia guide: all four formats from the locked system"). No push.

## Leaks (system-layer notes — nothing edited)

- `build_brochure.py` `rects_overlap` uses strict `<` with margin m: two pins at
  *exactly* identical coordinates make every nudge candidate a borderline
  "collision" (gap == margin), so the second pin stamps directly over the first.
  Worked around in data (+0.0001° lng on the Steamers pin). A shared-layer fix
  would be `<=` or a final forced-offset fallback.
- Empty `host` renders no credit line on the brochure back (web shows "from the
  Crossroads archive"). Billy Roy Parks shows a small gap there — cosmetic,
  system behavior.

## Neighbor towns decision

**Not pulled.** Columbia alone yielded 15 eligible stops (threshold was <8), so
Mount Pleasant / Santa Fe / Culleoka / Hampshire records were not queried and
the guide stays framed as Columbia proper (Pottsville and Williamsport Pike
addresses are Columbia-tagged, in-county stops).

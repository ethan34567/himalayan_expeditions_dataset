(straight from claude)
# Himalayan Expeditions Dataset — Column Reference

Four linked tables: **peaks**, **exped** (expeditions), **members**, and **refer** (bibliography). 

Join keys: 

&emsp; `peakid` links peaks &harr; exped &harr; members

&emsp; `expid` links exped &harr; members &harr; refer.

---

# `peaks.csv`

480 rows, one per mountain. 23 columns.

| Column | Description |
|---|---|
| `peakid` | Unique short peak code, e.g. `EVER` = Everest, `AMAD` = Ama Dablam. Primary key; joins to `exped.csv`/`members.csv`. |
| `pkname` | Common (foreign-language, usually English) name of the peak. |
| `pkname2` | Local name of the peak, plus alternate spellings, e.g. Aichyn's `pkname2` is "Aychin, Ashvin". |
| `location` | Text description of where the peak sits (often relative to a nearby landmark). |
| `heightm` | Height in meters. |
| `heightf` | Height in feet. |
| `himal` | Which mountain range/sub-group the peak belongs to. **Categorical**, 20 values: `Annapurna`, `Api/Byas Risi/Guras`, `Damodar`, `Dhaulagiri`, `Ganesh/Shringi`, `Janak/Ohmi Kangri`, `Jongsang`, `Jugal`, `Kangchenjunga/Simhalila`, `Kanjiroba`, `Kanti/Palchung`, `Khumbu` (Everest's range), `Langtang`, `Makalu`, `Manaslu/Mansiri`, `Mukut/Mustang`, `Nalakankar/Chandi/Changla`, `Peri`, `Rolwaling`, `Saipal`. |
| `region` | Broader grouping of several `himal` ranges together. **Categorical**, 7 values: `Kangchenjunga-Janak`, `Khumbu-Rolwaling-Makalu`, `Langtang-Jugal`, `Manaslu-Ganesh`, `Annapurna-Damodar-Peri`, `Dhaulagiri-Mukut`, `Kanjiroba-Far West`. |
| `open` | `TRUE`/`FALSE` — peak is on Nepal's official list of peaks open to expeditions. |
| `unlisted` | `TRUE`/`FALSE` — peak isn't on any official Nepal government list (climbed illegally, or before regulation existed); still included in stats. |
| `trekking` | `TRUE`/`FALSE` — peak is officially classified as a "trekking peak" (simplified permit); excluded from main stats after its listing year. |
| `trekyear` | Year the peak was added to the trekking-peak list (blank if not applicable). |
| `restrict` | Free-text notes on access restrictions, e.g. `"Closed"`, `"Opened in 2002"`, `"Converted to trekking peak in 2002"`. Not a fixed category list. |
| `phost` | Which country/countries the peak straddles. **Categorical**, 6 values: `Nepal only`, `China only`, `India only`, `Nepal & China`, `Nepal & India`, `Nepal, China & India`. |
| `pstatus` | Climbing status. **Categorical**, 2 values present: `Climbed`, `Unclimbed`. |
| `pyear` | Year of the first ascent. |
| `pseason` | Season of the first ascent. **Categorical**: `Spring`, `Summer`, `Autumn`, `Winter` (blank if unclimbed/unknown). |
| `pmonth` | Month of the first ascent, abbreviated (`Jan`–`Dec`; occasionally a range like `OctNov`). |
| `pday` | Day of the month of the first ascent. |
| `pexpid` | `expid` of the expedition credited with the first ascent — links to `exped.csv`. |
| `pcountry` | Nationality/nationalities of the first-ascent team. |
| `psummiters` | Names of the people who made the first ascent (a text list, e.g. `"Mike Gill, Wally Romanes, Barry Bishop, Michael Ward"`) — **not** a headcount, despite the name. |
| `psmtnote` | Free-text notes on the first ascent (caveats, disputes, etc.). |

---

# `exped.csv`

11,425 rows, one per expedition. 65 columns.

| Column | Description |
|---|---|
| `expid` | Unique expedition ID: peak code + 2-digit year + season digit + sequence number (e.g. `AMAD61101`). Primary key. |
| `peakid` | Peak code — links to `peaks.csv`. |
| `year` | Year of the expedition. |
| `season` | Season of the expedition. **Categorical**, 5 values: `Spring`, `Summer`, `Autumn`, `Winter`, `Unknown`. |
| `host` | Host country for the expedition (relevant for border peaks). **Categorical**, 4 values: `Nepal`, `China`, `India`, `Unknown`. |
| `route1`–`route4` | Up to 4 climbing routes attempted, as free text. |
| `nation` | Principal nationality of the expedition. |
| `leaders` | Name(s) of the expedition leader(s). |
| `sponsor` | Expedition sponsor or team name. |
| `success1`–`success4` | Boolean (`TRUE`/`FALSE`) — success on route 1–4. |
| `ascent1`–`ascent4` | The team's ascent number for that route, as text — usually a number/ordinal (`"105"`, `"9th"`), sometimes with notes (`"9th solo"`, `"Claimed"`, `"100 w/Ita"`). Not tracked for recent Everest/Cho Oyu/Ama Dablam climbs since many teams now summit together. |
| `claimed` | Boolean — the claimed success has been disproved or isn't generally recognized; excluded from success stats. |
| `disputed` | Boolean — success is unverified/disputed but not disproved (e.g. summit party disappeared); **still counted** as a success in stats. |
| `countries` | Nationalities on the team besides the principal `nation`. |
| `approach` | Free-text description of the approach march to base camp. |
| `bcdate` | Date arrived at base camp. |
| `smtdate` | Date the expedition first summited (or reached its high point, if unsuccessful). |
| `smttime` | Time of day of that summit (Nepal Standard Time). |
| `smtdays` | Days from base camp to summit/high point (calculated). |
| `totdays` | Total days from base camp to expedition end (calculated). |
| `termdate` | Date the expedition ended. |
| `termreason` | Primary reason the expedition ended. **Categorical**, 15 values: `Success (main peak)`, `Success (subpeak, foresummit)`, `Success (claimed)`, `Bad weather (storms, high winds)`, `Bad conditions (deep snow, avalanching, falling ice, or rock)`, `Accident (death or serious injury)`, `Illness, AMS, exhaustion, or frostbite`, `Lack (or loss) of supplies, support or equipment`, `Lack of time`, `Route technically too difficult, lack of experience, strength, or motivation`, `Did not reach base camp`, `Did not attempt climb`, `Attempt rumored`, `Other`, `Unknown`. |
| `termnote` | Free-text termination detail (supplements `termreason`). |
| `highpoint` | Elevation (m) of the expedition's highest point. |
| `traverse` | Boolean — team traversed the peak (up one route, down another). |
| `ski` | Boolean — skis/snowboard used on part of the descent by at least one member. |
| `parapente` | Boolean — parapente/hang-glider used on part of the descent. |
| `camps` | Number of high camps above base camp. |
| `rope` | Meters of fixed rope used. |
| `totmembers` | Number of (non-hired) expedition members — see field-specific caveats on Nepal vs. China permits in the dictionary. |
| `smtmembers` | Number of members who summited the main peak (excludes `claimed`, includes `disputed`). |
| `mdeaths` | Number of member deaths. |
| `tothired` | Number of hired personnel who went above base camp. |
| `smthired` | Number of hired personnel who summited. |
| `hdeaths` | Number of hired-personnel deaths. |
| `nohired` | Boolean — no hired personnel were used above base camp (distinguishes a true zero from missing data in `tothired`). |
| `o2used` | Boolean — supplemental oxygen used by anyone on the expedition. |
| `o2none` | Boolean — no one used oxygen. |
| `o2climb` | Boolean — oxygen used while climbing by at least one member. |
| `o2descent` | Boolean — oxygen not used while climbing, but used only during descent. |
| `o2sleep` | Boolean — oxygen used for sleeping. |
| `o2medical` | Boolean — oxygen used only for medical purposes. |
| `o2taken` | Boolean — oxygen brought for emergencies but never used. |
| `o2unkwn` | Boolean — oxygen use unknown. |
| `othersmts` | Free-text notes on other/secondary summits reached. |
| `campsites` | Free-text notes on camp locations. |
| `accidents` | Free-text description of any accidents. |
| `achievment` | Free-text notes on notable achievements. |
| `agency` | Name of the trekking/logistics agency used. |
| `comrte` | Boolean — climbed via a standard commercial route. |
| `stdrte` | Boolean — climbed via the standard route for an 8000m peak. |
| `primrte`, `primmem`, `primref` | Boolean flags marking which of several linked records holds the "primary" route / member / literature info, for expeditions split across multiple database entries. |
| `primid` | `expid` of the "primary" linked record, if this one is secondary. |
| `chksum` | Internal database consistency-check value — not meaningful for analysis. |

---

# `members.csv`

89,000 rows, one per person per expedition. 61 columns. `membid` is only unique *within* an expedition, so it can't be used alone to track one person across expeditions — join on `expid` + `membid` together, or match on name/citizenship if tracking a person across expeditions.

| Column | Description |
|---|---|
| `expid` | Expedition ID — links to `exped.csv`. |
| `membid` | Member ID, unique only within the expedition. |
| `peakid` | Peak code — links to `peaks.csv`. |
| `myear` | Year of the expedition. |
| `mseason` | Season of the expedition. **Categorical**, 4 values: `Spring`, `Summer`, `Autumn`, `Winter`. |
| `fname`, `lname` | First and last name. |
| `sex` | **Categorical**, 3 values: `M` (80,190), `F` (8,809), `X` (1 — unspecified/other). |
| `yob` | Year of birth. |
| `citizen` | Citizenship. |
| `status` | The person's role/status on the expedition. Free text, **554 distinct values** in the data — not a small fixed list. Most common: `Climber` (51,629), `H-A Worker` (18,596 — hired/high-altitude worker), `Leader` (11,052), `Exp Doctor` (1,452), `Deputy Leader` (1,242), `Sirdar` (602), `H-A Assistant`, `BC Manager`, `Climbing Leader`, `Co-Leader`, `Member`, `Climbing Guide`, and many more specialized/rare roles. |
| `residence` | City/country of residence. |
| `occupation` | Stated occupation. |
| `leader` | Boolean — was the expedition leader. |
| `deputy` | Boolean — was the deputy leader. |
| `bconly` | Boolean — didn't climb above base camp (or advanced base camp). |
| `nottobc` | Boolean — didn't even reach base camp. |
| `support` | Boolean — went above base camp only in a support role (e.g. photographer). |
| `disabled` | Boolean — climbed with a physical disability. |
| `hired` | Boolean — was hired by the expedition (vs. a member/client). |
| `sherpa` | Boolean — is Sherpa. |
| `tibetan` | Boolean — is Tibetan. |
| `msuccess` | Boolean — this person personally summited. |
| `mclaimed` | Boolean — this person's success was disproved / isn't generally recognized; excluded from success stats. |
| `mdisputed` | Boolean — unverified/disputed but not disproved; **still counted** as success in stats. |
| `msolo` | Boolean — climbed solo. |
| `mtraverse` | Boolean — traversed the peak. |
| `mski` | Boolean — used skis/snowboard on part of the descent. |
| `mparapente` | Boolean — used a parapente/hang glider on part of the descent. |
| `mspeed` | Boolean — notable as a speed ascent. |
| `mhighpt` | Boolean — reached the expedition's overall high point. |
| `mperhighpt` | This person's personal high point, in meters. |
| `msmtdate1`–`msmtdate3` | Up to 3 summit dates (2nd/3rd only count if they fully descended to base/advanced base and re-ascended). |
| `msmttime1`–`msmttime3` | Corresponding summit times (Nepal Standard Time). |
| `mroute1`–`mroute3` | Which route (1st/2nd/3rd ascent) this person used, stored as an index into `exped.route1`–`route4`. **Values: `0` (none), `1`, `2`, `3`, `4`.** |
| `mascent1`–`mascent3` | Team ascent number for that summit (numeric, e.g. `100`, `101`) — corresponds to the numeric part of `exped.ascent1`–`ascent4`. |
| `mo2used` | Boolean — this person used supplemental oxygen. |
| `mo2none` | Boolean — this person did not use oxygen. |
| `mo2climb` | Boolean — oxygen used while climbing. |
| `mo2descent` | Boolean — oxygen not used while climbing, only during descent. |
| `mo2sleep` | Boolean — oxygen used for sleeping. |
| `mo2medical` | Boolean — oxygen used only for medical purposes. |
| `mo2note` | Free-text note on oxygen use/reason. |
| `death` | Boolean — this person died on the expedition. |
| `deathdate` | Date of death. |
| `deathtime` | Time of death. |
| `deathtype` | Primary cause of death. **Categorical**, 12 named values (plus blank for non-deaths): `AMS (acute mtn sickness)`, `Avalanche`, `Crevasse`, `Disappearance (unexplained)`, `Exhaustion`, `Exposure / frostbite`, `Fall`, `Falling rock / ice`, `Icefall collapse`, `Illness (non-AMS)`, `Other`, `Unknown`. |
| `deathhgtm` | Altitude (m) at which the death (or the accident that led to it) occurred. |
| `deathclass` | Where in the climb the death occurred. **Categorical**, 7 named values (plus blank for non-deaths): `Ascending in summit bid`, `Descending from summit bid`, `Route preparation`, `Death at BC / ABC`, `Death enroute BC`, `Expedition evacuation`, `Other / Unknown`. |
| `msmtbid` | Boolean — this represents a summit bid (attempt). |
| `msmtterm` | Reason the individual's summit bid ended. **Categorical**, distinct from `exped.termreason` — 20 named values (plus `#N/A`): `Success`, `Success (subpeak, foresummit)`, `Accident (death or injury to self or others)`, `Altitude (AMS symptoms, breathing or unwell)`, `Assisting, guiding, supporting or accompanying others`, `Bad conditions (deep snow, avalanches, falling rock/ice)`, `Bad weather (storms, high winds)`, `Did not climb or intent to summit`, `Exhaustion, fatigue, weakness or lack of motivation`, `Frostbite, snowblindness or coldness`, `Insufficient time left for expedition`, `Lack of supplies, support or equipment problems`, `O2 system failure`, `Other`, `Other illnesses or pains`, `Route difficulty, intimidation or insufficient ability`, `Route/camp preparation or rope fixing`, `Too late in day or too slow`, `Unknown`, `Unspecified`. |
| `hcn` | Himalayan Club number (a membership/reference number for some climbers, mostly historical). |
| `mchksum` | Internal database consistency-check value — not meaningful for analysis. |

---

# `refer.csv`

15,586 rows — literature references cited per expedition (one expedition can have several). 12 columns.

| Column | Description |
|---|---|
| `expid` | Expedition ID — links to `exped.csv`. |
| `refid` | Sequence number for this reference within the expedition (e.g. `"01"`, `"02"`). |
| `ryear` | Year of the expedition being referenced (matches the expedition's `year`, not necessarily the publication year). |
| `rtype` | Type of reference. Values include `Journal`, `Book`, and similar categories. |
| `rjrnl` | Journal or magazine name (if `rtype` is `Journal`), e.g. `"American Alpine Journal"`. |
| `rauthor` | Author(s) of the referenced work, e.g. `"Matsuzawa, Tetsuro"`. |
| `rtitle` | Title of the work — mainly populated for books, e.g. `"Living on the Edge"`. |
| `rpublisher` | Publisher (for books). |
| `rpubdate` | Year the referenced work was published, e.g. `1985`. |
| `rlanguage` | Language of the publication, if non-English (or the original language, if it's since been translated to English). |
| `rcitation` | Formatted journal/magazine citation (volume:pages (year)), e.g. `"59:247-249 (1985)"`. |
| `ryak94` | Catalog number from the *Catalogue of the Himalayan Literature* (Yoshimi Yakushi, 1994) — the "Yakushi number" for the publication, e.g. `"B558"` (books only). |

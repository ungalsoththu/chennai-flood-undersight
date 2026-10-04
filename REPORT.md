# The Flood Machine and Its Shadow Data

## A public audit of Chennai's ₹107.2-crore Real-Time Flood Forecasting & Spatial Decision Support System

**UngalSoththu — AI-native desk** · Report draft v0.4 · 2026-10-04 (v0.2 §5 financing · v0.3 media-claims + data catalogue · v0.4 question-bench loop: 200-question accountability bank, machine-scored, 25 gaps fixed — see `file CHAPTER.md`)
**Companion data release:** four Hugging Face datasets (links in §3) + the 2026-12 rescue archive `chennai-rain-gauges` · **Media-claims register:** `file MEDIA-CLAIMS.md` (every public success/impact reference, claim-typed and cross-checked) · **Data catalogue:** `file DATA-CATALOGUE.md` (coverage reconciliation + per-layer freshness)**Question bank:** `file 200-QUESTIONS.md` (200 graded accountability questions) · **Chapter:** `file CHAPTER.md` (bench method, reviewer scorecard, gap fixes) · **Resident review bench:** https://cashlessconsumer.zo.space/rtff-200-review
**Evidence grades used:** **A** = artifact captured in our archive (reproducible command in appendix) · **B** = captured + corroborated by dated press · **C** = press-reported only, not independently verified · **D** = inference from evidence (reasoning stated)

---

## Executive summary

1. Tamil Nadu operates India's first fully operational urban flood-forecasting decision-support system for Chennai — the RTFF & SDSS, sanctioned at ₹107.2 crore, covering 4,974 km² across five districts, promoted via TNSMART/TN-DSS with World Bank PDGF funding through TNUIFSL and IIT Madras oversight. It has been fully operational since October 2025. **\[C\]**
2. The system's public-facing output is seven image-only PDF bulletins and a dashboard. It has no published data license, no API documentation, no public alert API, and no archive of its own forecasts — so its central promise (street-level, 72-hour-ahead flood intelligence) **cannot be independently verified by the public it protects.** **\[A/B\]**
3. Behind that wall, the system's own GeoServer — unadvertised, unlicensed, undocumented — serves **344 data layers** including 1.7 million sensor readings, 2005/2015 flood footprints, ward-level depth tables, and station registries embedding vendor maintenance contracts. We mirrored the readable 343 layers and published them openly. **\[A\]**
4. The mirror already surfaces accountability-relevant facts the portal itself does not surface: of 38 rain stations on its flagship dashboard, only 22 reported fresh data on census day; the city's historic reference gauges (Nungambakkam, Meenambakkam-ISRO, Madhavaram) have been frozen at **2025-05-10** for over sixteen months; the ward-level depth "forecast" layer is a **static scenario dated 2021-08-11**; and the machine-readable ARG feed was last bulk-updated in **January 2022** even as the dashboard reads 2026 data through a separate pipeline. **\[A\]**
5. We propose a lawful, attribution-first mirror posture grounded in the fact that **raw government telemetry is not copyrightable**, that NDSAP 2012 makes openness the default for exactly this class of data, and that research/reporting use is statutorily fair-dealing (§52, Copyright Act 1957). **\[D — legal analysis\]**
6. The ₹107.2 crore is World Bank **loan** money repackaged as a state technical-assistance grant: IBRD sovereign lending → GoTN's Project Development Grant Fund (PDGF, managed by TNUIFSL) → consultancy-led implementation (SECON–JBA JV, IIT-M oversight). The Bank's current $300M Tamil Nadu urban program (PforR + IPF; 32-year maturity, 7-year grace) is still paying for RTFF handholding and survey work — while no sanction order, contract split, AMC schedule or O&M budget for the flagship system is public (§5). **\[A/B\]**

---

## 1. Why Chennai, why now

Chennai's flood risk is not a scenario exercise. The city drowned in December 2015; Cyclone Michaung delivered a verified **639 mm in 24 hours** at a single GCC zone gauge (Zone 12, Meenambakkam 6A gate) on 2023-12-04 in our own rescued archive; and in early December 2025 the remnant of Cyclone Ditwah dropped a reported **56 cm over three days on Ennore**, forced Red Hills shutters open for the sixth time that season, and produced the system's own highest citizen flood-severity report (level 6 of 6, at the Puzhal surplus outflow, 2025-12-04). **\[A for our gauges and reports; B for press figures\]**

The state's structural answer, sanctioned after 2015 and operational only in October 2025, is the RTFF & SDSS: five weather models fused with rain-gauge, river, lake and sea data into street-level inundation forecasts for vulnerable neighbourhoods (Pulianthope, Nungambakkam, Mambalam, Saidapet, Velachery, Meenambakkam, Mudichur), disseminated through a dashboard, press bulletins and the TN-Alert app. **\[C\]**

A forecasting system is only as accountable as its record. This report is the first outside look at that record.

## 2. What the system publishes — and what it doesn't

| Dimension | Published | Missing |
| --- | --- | --- |
| Forecasts | 7 bulletins (Oct 2025 activation), image-only PDF | Forecast archive; any forecast-vs-observed comparison |
| Sensor data | Dashboard cards (current day) | Bulk download, history, API docs |
| Alerts | `GetPublishAlert` feed (0 rows on 2026-09-29) | Public API, RSS, SMS spec |
| GIS | Portal map tiles | — (the GeoServer is open, but unadvertised) |
| Legal | Nothing | License, terms of use, privacy policy |
| Economics | ₹107.2 cr press figure | Sanction order, contract splits, O&M spend, validation reports |

The pattern is consistent: **display without documentation, delivery without durable record.**

## 3. The release: what we mirrored

On 2026-09-29 we enumerated the system's GeoServer capabilities (**344 layers; 343 anonymously readable** — census: `file docs/wfs_census_2026-09-29.csv`), pulled every readable layer, pulled all transaction tables in full, and mirrored the dashboard API payloads. Released:

| Dataset | Contents | Size |
| --- | --- | --- |
| `chennai-flood-monitor-transactions` | SRG rain 662,904 rows (1976→2026-02); AWS/ARG rain+met 669,147 (2018→2022-01 bulk); AWLR water levels 385,950 (2021-09→2026-08); 33 station registries incl. AMC vendor fields, PII-scrubbed | 37 MB |
| `chennaidss-gis-layers` | 181 GeoParquet layers: wards, drainage, waterways, tanks, bathymetry, forecast ensembles, crowdsourced reports (submitter identities stripped) | 40 MB |
| `chennai-flood-history` | NRSC 2015 flood extent (4,001 polygons), IRS 2005 (235), GCC hotspots 2015 + NEM-2020, ward depth min/max, flood warnings | 2.3 MB |
| `chennai-flood-bulletins` | All 7 operational bulletins of the Oct 2025 run — the system's complete public record to date | 92 MB |

Plus the predecessor rescue: `chennai-rain-gauges` — 34,050 GCC zone-gauge readings (2020-11→2023-12) including the full Michaung event, from the dead `chennaifloodsdss.in` portal.

## 4. Findings

**F1 — The data is open by accident, not by policy. \[A→D\]**
343 of 344 layers answer anonymous WFS requests. None of it is linked, licensed, or documented anywhere on the portal. The state has, in effect, published a world-class urban flood dataset and forgotten to notice. This is the release's enabling condition — and its fragility: no license means no assurance it stays open.

**F2 — The flagship rain gauges are dark on the public dashboard. \[A\]**
Dashboard station table, 2026-09-29: 38 stations listed, 22 fresh. Nungambakkam, Meenambakkam-ISRO, Madhavaram-AMFU and Ennore Port frozen at **2025-05-10**; RIMC Lab at **2024-10-21**. Chennai's historic IMD reference gauge (Nungambakkam) — the yardstick for every flood comparison since 2015 — has no current public reading on the system built to provide exactly that.

**F3 — Two pipelines, one visible. \[A\]**
The machine-readable ARG transaction table tops out in 2022 (bulk 2018–2021, then 3 stragglers, latest 2022-09-06), while the dashboard API returns 2026-09 readings through a different pipeline. The "open" layer and the "operational" layer are not the same data path — so even a diligent citizen reading the open feed gets a four-year-stale city.

**F4 — The ward "forecast" is a 2021 scenario. \[A\]**
`ward_waterdepth_minmax`: 200 wards, every depth stamped **2021-08-11**. Street-level inundation, as exposed to the public record, is a static lookup from five monsoons ago — not a live model output. (The live street-flood output exists, but only as bulletin PDF maps during activations.)

**F5 — No forecast archive means no verifiable skill. \[A→D\]**
The model-run registry shows activations (Oct–Dec 2024; 2025-10-18→2025-12-02) and ensembles, but the system retains no published forecast-vs-observed record. After ₹107.2 crore, the question "how good is it?" has no public answer. Our mirror now holds the observed side; the forecast side must be captured going forward, activation by activation.

**F6 — Alerts exist, barely, and only inward. \[A\]**
The alert feed has returned an empty set on every check. Alerting happens through press bulletins and (claimed) the TN-Alert app during activations. There is no public API, RSS, or machine feed — alert equity depends on having the right app installed and open.

**F7 — The mirror holds data-quality anomalies the portal never surfaces. \[A\]**
Air-temperature readings of **−6.2 °C** at Madhavaram and **−18 °C** at Kattupakkam; a bridge sensor reading 26.476 "m" against a Cooum cross-section of \~7 m (unit-suspect); station names like `dc`; empty promoted layers (`getDailyRainfallValue`: 0 rows; `giswardmesh`: 0; `aws_new`: server error). Each is small; together they describe absent QA.

**F8 — The Dec-2025 flood is corroborated across three independent layers of the system's own data. \[B\]**
Citizen level-6 report (Puzhal surplus outflow, 2025-12-04 03:00Z) + bridge danger-level peaks same day (Aminjikarai 7.705 m at 15:30; Manali 2.501 m) + 168 crowd reports in Nov 2025 — consistent with The Hindu's Ennore/Red-Hills coverage of the same week. The system worked as a recorder during its last real test. Whether it worked as a forecaster is exactly what F5 says cannot be checked.

**F9 — The predecessor died and took its data with it. \[A\]**
`chennaifloodsdss.in` is NXDOMAIN (last Wayback capture 2025-08-31). Only the Dec-2023 rescue exists. Without mirrors, institutional memory evaporates at every URL change — which is why this release is annual-recurring by design.

**F10 — The economics are unaudited by design. \[C→D\]**
₹107.2 crore sanctioned (≈ ₹2.16 lakh/km² of the 4,974 km² covered; ≈ ₹53.6 lakh per ward). World Bank PDGF (Project Development Grant Fund) via TNUIFSL, consultants SECON–JBA JV, IIT-M oversight — all press/official-briefing level. No sanction order, contract split, O&M budget, or validation report is public. The station registries we mirror carry AMC flags and expiry fields — 66 stations AMC-flagged, expiry dates populated for only \~6 — the thread an RTI pulls. Full financing analysis: §5.

## 5. The money: international financing and its terms

**"Funded by the World Bank," says the system's own portal. True, imprecise. The ₹107.2 crore moved down a three-layer pipe — a sovereign loan at the top, a state grant fund in the middle, a consultancy at the bottom — and the terms at each layer are a different disclosure story. \[A/B→D\]**

### 5.1 The pipe: sovereign loan → state grant fund → consultant

| Layer | Actor | What it holds |
| --- | --- | --- |
| Lending | World Bank (IBRD) → Government of India → GoTN | Sovereign loans. IBRD lends only to the national government; GoTN services the debt through GoI back-to-back arrangements, carrying the foreign-exchange risk. |
| Repackaging | **Project Development Grant Fund (PDGF)** — a GoTN-created, non-lapsable technical-assistance grant fund, operational since 1 April 2015, managed by TNUIFSL | Converts loan allocations (and GoTN plough-backs) into grants for consultancies, studies, pilots and "innovations" for ULBs and government-owned institutions — no repayment obligation at the project level. |
| Implementation | TNUIFSL manages RTFF & SDSS on behalf of CRA (TNDRRA), GCC and CMA; SECON–JBA JV is the consultant for planning, setting up and commissioning, under IIT-Madras technical supervision | Control rooms at the State EOC (Ezhilagam), GCC, Kancheepuram and Tiruvallur collectorates; disaster-recovery centre at WRD Chepauk. |

So "World Bank-funded" is really "World Bank loan proceeds, repackaged by the state as a grant, spent through a consultant JV." Each hop strips a layer of public disclosure: the IBRD loan agreement is a public World Bank document, but the GoTN sanction order, the PDGF utilisation statement for this project, and the SECON–JBA contract value are not published anywhere we can find.

### 5.2 PDGF — the grant layer

TNUIFSL's own fund page is the primary source (captured 2026-10-03): PDGF is a **non-lapsable fund created to provide technical assistance** to ULBs and government-owned institutions. Its corpus flows in from: budgetary allocations along externally-aided project lines of credit (World Bank, KfW, JICA, ADB); plough-back of GoTN's unit-interest share in TNUDF; transfers from the TNUDP-III Grant Fund-II, the KfW SMIF-TN grant funds, the JBIC TNUIP Grant Fund-II and the Project Preparatory Grant Fund; and its own interest income. **\[A\]**

The scale makes the RTFF & SDSS singular. PDGF's published 2023-24 performance: **₹35.23 crore received, ₹52.64 crore disbursed — across all assignments**. The flood system's ₹107.2 crore (≈ US$12.5–13M at recent rates) equals **about two full years of the fund's entire disbursement capacity**, or three years of its receipts. \[A + our ratio — D\] Unless PDGF receipts have grown sharply, no other single assignment in the fund's decade approaches it.

A documentation detail in passing: the system's own AboutUs page renders the vehicle's name as "Project Development **Grand** Fund." The flagship system's portal misspells the fund that pays for it — the same decay the bulletins and API docs show elsewhere in this report.

### 5.3 The World Bank line — past and present

The Bank has funded TN's urban-financial machinery for three decades: TNUDF was set up under a 1990s Bank project, and the Bank has repeatedly credited its "100 percent loan repayments from ULBs" record. The RTFF & SDSS era sits between two Bank operations: **\[B\]**

| Operation | Year | Amount | Instrument | Reported terms |
| --- | --- | --- | --- | --- |
| Tamil Nadu Sustainable Urban Development Project (TNSUDP) | 2015 | $400M IBRD of a $600M program | Investment loan, results-based grants to ULBs, TA | Signed June 2015; the urban-sector umbrella under which TNUIFSL's TA pipeline ran |
| **Tamil Nadu Climate Resilient Urban Development Program (TNCRUDP, P179189)** | 2023 | **$300M IBRD** ($279M PforR + $21M IPF-TA, the TA co-funded $21M Bank / $9M GoTN) | **PforR + IPF blend** | **32-year maturity including 7-year grace**; approved 21 Dec 2023; program period 2024–2029; 21 ULBs inside a $2.15B government program |
| SHORE (coastal resilience, TN+Karnataka) | 2025 | $212.64M IBRD of an $850M program | IPF | 23-year final maturity including 6.5-year grace |
| TN Housing Sector Strengthening DPLs I & II | 2017–18 | $200M + $50M | Development policy loans | 20-year maturity including 3.5-year grace, as reported at signing |

The current operation matters most: **TNCRUDP's procurement plans (Dec 2023 and Dec 2024) still list Chennai RTFF assignments** — "Supervisory Consulting Services during the Handholding Phase for the Chennai Real Time Flood Forecasting Project" (US$0.10M, direct selection) and "Generation of DEM & DSM using High Resolution Satellite Image for the Chennai Real Time Flood Forecasting Project" (US$0.36M) — both executed by TNUIFSL under Bank procurement rules. The Bank that "funded" the system is still buying its aftercare, three years after the pilot and one year after "fully operational." \[B\]

### 5.4 The terms of such lending

Four features of IBRD lending shape what this project costs the state, and none of them are visible in anything the project publishes: **\[B→D\]**

1. **Sovereign debt, not aid.** Every rupee of the ₹107.2 crore is a slice of a loan India must repay in hard currency, with interest at benchmark-plus-spread and fees on undrawn balances. GoTN's repayment passes through GoI; the foreign-exchange risk lands on the state budget. The "grant" label applies only at the PDGF hop — one layer down, it is debt with a **23–32 year tail** (observed TN-portfolio maturities above).
2. **Results-linked disbursement is the new standard.** TNCRUDP is a Program-for-Results: money disburses against independently verified program results, not upfront. This is the single strongest lever that *could* have tied payments to what consumers actually need — verified forecast accuracy, live station uptime — and nothing public shows the RTFF's performance indicators sitting in that results framework. The Bank's IPF-TA side ($30M) funds exactly the consultancy layer (handholding, surveys) where RTFF's aftercare now lives.
3. **The disclosure asymmetry is structural.** An investment project financing comes with a public PAD, cost tables, procurement plans, ISRs and an ICR. A TA grant inside a PforR's TA component gets procurement-plan line items — a project name and a dollar figure — and nothing else. That is precisely the disclosure level this report found: we can cite the RTFF's handholding line to the dollar, but not its sanction order, contract split, or O&M budget.
4. **Concessional, not free.** IBRD pricing sits below commercial sovereign borrowing for India's rating class, and the long maturities reduce annual debt service. That is the honest defence of the structure. It is not, however, a defence of the missing utilisation record: cheap debt still deserves an account of what it bought.

### 5.5 What the financing structure buys — and what it hides

- **The O&M cliff is now a financing fact.** Our mirrored registries flag 66 stations with active AMC status, but expiry dates are populated for only \~6; the AMC calendar — who maintains the flagship, until when, at what cost — is unknown even to its own registry. The Bank is separately procuring "handholding" supervision while the state has published no O&M budget. Read together: **the system's operating money is unresolved at both ends of the pipe.**
- **The multiplier question cuts both ways.** ₹2.16 lakh/km² and ₹53.6 lakh/ward for a decade-heritage, World-Bank-supervised modelling platform is defensible value *if* the forecasts are verified and the data is open — which F5 and F7 show they are not, yet. The financing section's contribution is sharper: when the money arrives as a results-linked loan, **the verification was available for free as a disbursement condition.**
- **Consumer bottom line.** This is not opposition to the project. It is an accounting demand: ₹107.2 crore of concessional sovereign debt bought Chennai a forecasting brain; the public got a dashboard with frozen gauges, image-only bulletins and no archive. The financing terms are public; the spending terms are not. That inversion is the story.

### 5.6 RTI / verification targets (financing track)

1. GoTN sanction order(s) for RTFF & SDSS under PDGF (WRD / CRA / Finance Dept) — amount, phases, component split.
2. PDGF utilisation certificates & auditor statements naming RTFF & SDSS (TNUIFSL, annual).
3. SECON–JBA JV contract value + payment schedule; IIT-M oversight agreement; hardware vendors and AMC schedules per station layer.
4. TNCRUDP results framework / ISR pages naming the RTFF assignments — confirm whether forecast-accuracy or uptime appears as a verified indicator.
5. World Bank Loan Agreement + PforR DLR schedule for P179189 (public once signed — a no-RTI ask).

## 6. Licensing: is investigating public data of the city lawful?

Yes — and it needs less "exemption" than commonly assumed. Raw government telemetry (rain, levels, coordinates, geometries) is **not copyrightable**: the Copyright Act, 1957 protects original expression, not facts, and machine-emitted measurements involve no authorial selection. *Eastern Book Co v. D.B. Modak* requires skill-and-judgment-plus-creativity for compilation rights; an exhaustive, mechanical, documented mirror has none to infringe. Where copyright does vest in the Government (bulletin graphics, §17), our use — research, review, reporting of current affairs, mirror-with-attribution — is statutory fair dealing (§52(1)(a)(i)–(iii)). Policy points the same way: **NDSAP 2012 makes non-sensitive government data open by default** behind a negative list; a state flood-DSS's telemetry is the paradigm NDSAP case. The US-hosted mirror inherits the same logic (*Feist*; §107 factors). We therefore claim: no rights over the facts; CC BY 4.0 on our arrangements; attribution everywhere; notice-and-takedown without argument. Full analysis: `file docs/LEGAL-NOTE.md`. **\[D — legal analysis, not legal advice\]**

## 7. Recommendations

**To TNSDMA / WRD / TNUIFSL** (none requires new money; all are policy):

1. Publish a data license (CC BY 4.0 suffices) and an API reference — the census we mirror is the draft.
2. Archive every bulletin and every model run; publish forecast-vs-observed after each activation.
3. Fix or retire the frozen flagship gauges; publish a station-freshness status layer.
4. Open the alert feed (API/RSS/SMS spec) — alerts in one app is alert inequity.
5. Adopt NDSAP formally for CFM-DSS: openness as default, negative list published.

**To researchers, journalists, civic technologists:** use the mirror. Score the next activation's bulletins against our gauges. Watch the AMC calendar. Demand the sanction order. The data now exists for all of it.

## 8. Method & reproducibility

Single-day census + full pulls on 2026-09-29: GeoServer `GetCapabilities` parse → per-layer WFS `GetFeature` (GeoJSON) with pagination → transaction tables pulled whole (`count` ≥ table size, verified `numberMatched == numberReturned`) → dashboard AJAX endpoints replayed with the front-end's own headers via a scripted browser session → PII scrub (officer/SIM/mobile columns; crowd submitter identities) → Parquet/GeoParquet conversion (DuckDB spatial + GeoPandas) → Hugging Face. Every figure in this report traces to a file in `UngalSoththu/data/chennai-floods/cfm-dss-2026-09-29/`. Census script committed (`docs/` of the release archive). No authentication was bypassed; only endpoints the portal's own front-end calls, called the way it calls them.

## 9. Limitations

Point-in-time capture (2026-09-29); activations since Oct 2025 may have changed server state. Press figures (rainfall totals, system cost, launch facts) are corroborated but not independently re-measured. The legal analysis is our own research posture, not legal advice. Five layers failed at source during pull and are excluded (logged). Claims are graded by evidence in the appendix.

## Appendix A — Claim-evidence ledger (key claims)

| \# | Claim | Grade | Evidence |
| --- | --- | --- | --- |
| 1 | 344 layers, 343 readable anonymously | A | census CSV, 2026-09-29 |
| 2 | SRG 662,904 rows, 1976→2026-02 | A | `srg_full` count + min/max date |
| 3 | AWS/ARG 669,147 rows, bulk 2018→2022-01 | A | per-year DuckDB group-by |
| 4 | AWLR 385,950 rows, 2021-09→2026-08-16 | A | min/max date |
| 5 | 22/38 dashboard stations fresh on census day | A | API pull, 2026-09-29 |
| 6 | Nungambakkam/Meenambakkam-ISRO/Madhavaram frozen 2025-05-10 | A | station `date_time` fields |
| 7 | Ward depth layer static, dated 2021-08-11 | A | layer property inspection |
| 8 | ARG WFS bulk ends Jan 2022 (3 stragglers to 2022-09-06) | A | year group-by (2022: 3 rows, max 2022-09-06) |
| 9 | Alert feed empty; 7 bulletins total | A | API pulls |
| 10 | ₹107.2 cr / 4,974 km² / 5 models / Oct 2025 launch | C | The Hindu 2025-10-22; Business Standard |
| 11 | Ennore 56 cm/3 days; Red Hills shutters 6th time (Dec 2025) | B | The Hindu 2025-12-03 vs our sensor/crowd layers |
| 12 | Michaung 639 mm/24 h at Zone-12 gauge | A | rescued archive peak query |
| 13 | 95% SWD works done before NEM 2026 | C | Live Chennai, Sep 2026 |
| 14 | "Open by accident" characterization | D | synthesis of 1, 9, absence of license/docs |
| 15 | PDGF = Project Development Grant Fund: non-lapsable TA grant fund, operational 1 Apr 2015, managed by TNUIFSL; corpus from WB/KfW/JICA/ADB lines of credit + TNUDP-III/KfW SMIF-TN/JBIC TNUIP grant-fund transfers; 2023-24 receipts ₹35.23 cr, disbursements ₹52.64 cr | A | TNUIFSL PDGF page, captured 2026-10-03 |
| 16 | RTFF & SDSS implemented under PDGF on behalf of CRA (TNDRRA), GCC, CMA; SECON–JBA JV consultant, IIT-M supervision | A | CFM-DSS AboutUs, chennaifloodmonitor.tn.gov.in |
| 17 | TNCRUDP P179189: $300M IBRD, PforR+IPF blend, 32-yr maturity incl 7-yr grace, approved 2023-12-21; $2.15B govt program, 21 ULBs, 2024–2029 | B | World Bank press release 2023-12-21; ESSA 2023 |
| 18 | TNCRUDP procurement plans (Dec 2023, Dec 2024) list RTFF handholding-supervision ($0.10M) and DEM/DSM ($0.36M) assignments | B | WB STEP procurement plan PDFs, P179189 |
| 19 | "Grant" is repackaged sovereign debt; IBRD terms observed in TN portfolio: 32/7, 23/6.5, 20/3.5 (yr maturity/grace) | D | synthesis of 15–18 + WB/press maturity disclosures |
| 20 | No media/official reference credits RTFF & SDSS for any warning during its first real NEM (Ditwah, Nov 30–Dec 6 2025) — credits go to IMD/RMC, CWC, collectors, GCC ICCC | D (documented absence) | media sweep 2026-10-03, `file MEDIA-CLAIMS.md` entries 17–18 |
| 21 | Impact claims in the entire media corpus are prospective only ("can save lives", "will predict"); zero retrospective verified outcomes; the Oct 2026 IFMC launch re-offers the 2025 promise under a new centre | D | `file MEDIA-CLAIMS.md` register + Pattern analysis |
| 22 | Project cost reported as ₹71 crore in Nov 2022 (sensor-expansion phase) vs ₹107.2 crore at Oct 2025 launch — +51% in three years, no public sanction/revision trail | B (press, two datapoints) | New Indian Express 2022-11-02 vs launch coverage; `file ELI10.md` §2A |
| 24 | Per-district station counts: Chennai 379, Tiruvallur 247, Chengalpattu 104, Ranipet 89, Kancheepuram 92, Vellore 31; 36 stations in Andhra Pradesh (Chittoor) | A | station-registry lat/lon tally, 2026-10-04 |
| 25 | AMC/sensor-vendor name fields are blank across all station-registry rows in the mirror | A | registry scan 2026-10-04 |
| 26 | Archived model runs and bulletins end 2025-12-02 — before the Ditwah-remnant peak (Dec 3–5) | A | model-run + bulletin layer inspection |
| 23 | Build history: piloted NEM 2021 (incl. Cyclone Nivar field campaigns), operationalized NEM 2022–23, documented in Current Science 127(1) Jul 2024; predecessor portal chennaifloodsdss.in (live from \~2021) died Aug 2025 after the move to chennaifloodmonitor.tn.gov.in | B | Current Science 2024 + IIT-M press 2021-11 + Wayback 2025-08-31 |

## Appendix B — Reproduction

Scripts and step-by-step in the release archive README (`UngalSoththu/data/chennai-floods/cfm-dss-2026-09-29/`); census: `file docs/wfs_census_2026-09-29.csv`; layer diff: `file docs/layer_diff_vs_2023archive.json`. Verify any count with a one-line DuckDB query against the Parquet files on Hugging Face.

## Sources

- The Hindu, "Chennai gets India's first real-time flood forecast system", 2025-10-22 — https://www.thehindu.com/news/cities/chennai/chennai-gets-indias-first-real-time-flood-forecast-system/article70186744.ece
- The Hindu, "After pounding north Tamil Nadu, remnant of Cyclone Ditwah drifts inland", 2025-12-03 — https://www.thehindu.com/news/cities/chennai/after-pounding-north-tamil-nadu-remnant-of-cyclone-ditwah-drifts-inland-city-to-get-light-rain-today/article70353989.ece
- Business Standard, "How urban flood warning systems work", 2026 — https://www.business-standard.com/india-news/how-urban-flood-warning-systems-work-mumbai-chennai-show-the-way-126070900246_1.html
- Live Chennai, "Chennai Monsoon Preparedness: 95% of Storm Water Drain Works Completed", Sep 2026 — https://www.livechennai.com/detailnews.asp?newsid=83291
- The Week, "Floods in Tamil Nadu from October–December... CM Vijay told", 2026-09-23 — https://www.theweek.in/news/india/2026/09/23/tamil-nadu-floods-from-october-december-extreme-heatwaves-2027-cm-vijay.html
- New Indian Express, "Not just drought, TN may also face flood and heatwave due to El Nino", 2026-09-23 — https://www.newindianexpress.com/states/tamil-nadu/2026/Sep/23/not-just-drought-tn-may-also-face-flood-and-heatwave-due-to-el-nino-says-panel
- TNUIFSL, "Project Development Grant Fund (PDGF)" — http://tnuifsl.com/pdgf.asp and funds list http://tnuifsl.com/aboutus.asp (captured 2026-10-03)
- CFM-DSS, AboutUs (RTFF & SDSS funding/implementation structure) — https://chennaifloodmonitor.tn.gov.in/Master/AboutUs- New Indian Express, "Real-time flood forecast becomes a reality in Tamil Nadu" (cost ₹71 crore; expansion plan 86 ARG/14 AWS/185 AWLR/58 gates; \~5,000 km², six sub-basins), 2022-11-02 — https://www.newindianexpress.com/cities/chennai/2022/Nov/02/real-time-flood-forecast-becomes-a-reality-in-tamil-nadu-2514463.html
- New Indian Express, "Real-time flood forecasting may include Araniar basin" (4 basins \~4,073 km² initial scope; WB rate-variation approvals pending), 2019-03-27 — https://www.newindianexpress.com/states/tamil-nadu/2019/Mar/27/real-time-flood-forecasting-may-include-araniar-basin-in-tamil-nadu-1956913.html
- IIT Madras press release, "Researchers braved Cyclone Nivar to collect real flood data" (IIT-M + IIT-B + Anna Univ + NCCR pilot consortium), Nov 2021 — https://www.iitm.ac.in/happenings/press-releases-and-coverages/iit-madras-researchers-braved-cyclone-nivar-collect-real
- Citizen Matters, "IITM team helps 2,000 residents log flood water levels in Chennai" (citizen-science portal feeding RTFF & SDSS; 4-km 7-ensemble IIT-M model), 2024 — https://citizenmatters.in/iitm-team-log-flood-water-levels-chennai-residents-forecasting/
- Dhamodaran et al., "Setting up and operationalization of the real-time flood forecasting – spatial decision support system for Chennai, India", Current Science 127(1), Jul 2024 (pilot NEM 2021; operational NEM 2022–23) — https://www.researchgate.net/publication/382075584
- Times of India, interview with IIT-M professor on Chennai flood/drought challenges (IIT-M technical supervision role since post-2015 sanction), 2026 — https://timesofindia.indiatimes.com/city/chennai/chennais-flood-and-drought-challenges-insights-from-iit-m-professor-on-sustainable-solutions/articleshow/125254012.cms
- CFM-DSS legacy portal (chennaifloodsdss.in, dead; last Wayback 2025-08-31) AboutUs — https://www.chennaifloodsdss.in/Master/AboutUs
- World Bank ISR, Third Tamil Nadu Urban Development Project (TNUDP III, P083780, approved FY2006; $15M institutional development + $283.5M urban investments via TNUDF) — https://documents1.worldbank.org/curated/en/759671468281109709/pdf/ISR-Disclosable-P083780-06-06-2013-1370495677917.pdf
- TNUIFSL, TNUDF page (1996 fund origins; WB/KfW/JICA/ADB streams) — http://tnuifsl.com/tnudf.asp
- TNUIFSL, PDGF page (operational 1 Apr 2015; corpus origins incl. TNUDP Grant Fund-II, KfW SMIF-TN, JBIC TNUIP) — http://tnuifsl.com/pdgf.asp
- World Bank, "New World Bank Program to Strengthen Urban Water, Sewerage System for 2 Million People in India's Tamil Nadu State" (TNCRUDP, $300M, 32-yr/7-yr), 2023-12-21 — https://www.worldbank.org/en/news/press-release/2023/12/21/new-world-bank-program-to-strengthen-urban-water-sewerage-system-for-2-million-people-in-india-s-tamil-nadu-state
- World Bank, TNCRUDP (P179189) Procurement Plans, Dec 2023 & Dec 2024 (RTFF handholding + DEM/DSM line items) — https://documents1.worldbank.org/curated/en/099121624021567449/pdf/P17918917c331c0fc1a2711eaa5d118b332.pdf
- World Bank, TNCRUDP ESSA (program financing: $279M PforR + $21M IPF-TA/$9M GoTN) — http://tnuifsl.com/Disclosures/2023-24/2023115_TNCRUDP_ESSA.pdf
- World Bank, "World Bank Approves $400 Million to Improve Urban Services in Tamil Nadu" (TNSUDP), 2015-03-31 — https://www.worldbank.org/en/news/press-release/2015/03/31/world-bank-improve-urban-services-tamil-nadu-india
- ANI, "World Bank approves USD 212.6 loan for coastal zone management in Tamil Nadu, Karnataka" (SHORE, 23-yr/6.5-yr), 2025-09-10 — https://aninews.in/news/business/world-bank-approves-usd-2126-loan-for-coastal-zone-management-in-tamil-nadu-karnataka20250910131641
- Eastern Book Co v. D.B. Modak, (2014) 1 SCC 257 · Feist v. Rural Telephone Service, 499 US 340 (1991) · Copyright Act, 1957 §§13, 17, 52 · NDSAP 2012
- Primary archive: `UngalSoththu/data/chennai-floods/cfm-dss-2026-09-29/` (this workspace) · census + diff in `docs/`
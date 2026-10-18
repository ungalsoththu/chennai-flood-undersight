# [CFM-DSS] NEM 2026 Episode 1 was NOT predicted by the system — 2026-10-18

**Claim (scoped):** The 2026-10-17/18 Chennai flood — the heaviest spell since Michaung 2023 (Parrys 361 mm, Kathivakkam 343 mm, Meenambakkam 282 mm, Sathangadu 260 mm, 8:30 AM Oct 17 → 4:30 AM Oct 18) — was **not forecast by the RTFF & SDSS** (the ₹107.2-crore system whose statutory marketing promise is exactly this: 3-day rainfall forecasts and ward-level inundation prediction). The only predictions on record are IMD's generic district-level warnings.

**Scope guard:** "Not predicted" ≠ "nothing warned." IMD ran its normal alert cycle (orange alert at Oct 15 onset; heavy-rain warnings through Oct 22–23). The finding is that the *purpose-built* forecasting system produced nothing observable — before, during, or after the event.

## Evidence chain

**[A] Verified — the system's forecast function was offline before the monsoon:**
1. **No model runs on record since 2025-12-02.** The run registry (mirrored 2026-09-29) logs 81 runs, 2021-10-02 → 2025-12-02; nothing after. A "real-time" forecast model with a 10½-month silence at the start of NEM 2026.
2. **Gauge ingest into the portal froze ~2026-10-01.** On 2026-10-18, from a Chennai ISP vantage (Thinkpad), `Master/GetRainfallDatafordashboard` returns `"[]"` — **zero stations** — for all five districts; the resident's sighting of page stamps reading **30-09-2026 / 01-10-2026** matches.
3. **No bulletins for Episode 1.** The complete public-output record is 7 PDFs, all from the Oct 2025 Ditwah window. `HomePage/GetBulletins` is WAF-403 even from browser origin; nothing new is visible anywhere.
4. **The GeoServer transaction archive is dead long-term:** `ChennaiDSS:aws_arg_transaction` (669,147 rows) has **zero records with date ≥ 2023-01-01**; archive ends 2021–2023. Live transaction ingest to the public GeoServer stopped years ago — the "344 live layers" surface is largely a museum.

**[A] Verified — what was published during the event was not a forecast:**
5. **@TNFloodmodeller (the RTFF team's own X account) posted 4 times, all AFTER the spell began** (20:24–23:13 GMT Oct 17), and the language is descriptive/retrospective, not predictive: "Heavy rainfall **has been recorded**…", "event rainfall estimates **reached**…", "Such intense rainfall **would have placed** considerable pressure…" (a counterfactual about what already fell), "Tamil Nadu **recorded** widespread rainfall…". Gauge-specific totals within hours prove the team's *internal* pipeline was live — see the correction below — but no forecast product was issued on any channel we can observe.
6. **No RTFF/SDSS/chennaifloodmonitor mention anywhere in the event discourse** (X + news sweep, Oct 15–18). The system is publicly absent precisely when its reason to exist arrives.

**[C] Claim — the one candidate counter-item:**
7. A **TN-Alert/TNSMART push** about "extremely heavy rainfall" was reported by a resident on Oct 18. Provenance unverifiable (portal down; alert API was empty at census). Its wording matches IMD's alert language, so the working inference is an IMD-derived relay, **not** an RTFF model product. Flagged for RTI: what alerts did TNSMART/TN-Alert originate vs relay during Oct 15–18?

**[I] Inference — the chain closes:**
8. With inputs frozen since ~Oct 1 and no logged model run since Dec 2025, the system **could not** have produced an Episode-1 forecast. This is an evidenced absence, not an argument from silence: we hold the complete output record (7 bulletins), the complete run registry, and same-day probes of every public feed.

## Historical contrast — the capability existed, then stopped

| Event | Bulletins issued by the system? |
| --- | --- |
| Dec 2023 floods (predecessor portal, chennaifloodsdss.in) | **Yes** — daily B2.0 rainfall-forecast bulletins during the rains (mirrored Dec 2023 PDFs) |
| Oct–Nov 2025 (Ditwah window) | **Yes** — 7 bulletins (the entire output record) |
| **NEM 2026 Episode 1 (Oct 17–18)** | **None observed** — first major NEM event of the year, and the forecast function was dark |

## Correction to the same-day outage note

`2026-10-18-portal-outage-during-nem-episode1.md` inferred "ingest worked while the public face was dark" from the team's gauge-specific tweets. Same-day Chennai-vantage probes show that is **only true of the team's private pipeline** (gauge data evidently reaching MIKE Operations directly — note the portal's `/mikeoperation/` path). The **portal's own ingest and every public feed froze ~Oct 1**; the GeoServer archive has been dead since ≤2023. Both facts stand: the modelling team saw gauges; the public system saw nothing.

## Audit implications (adds to the 200 questions)

- **Q-add-1:** Show cause — why did the forecast model stop logging runs after 2025-12-02, and was any forecast produced for Oct 15–18 outside the public record?
- **Q-add-2:** When did portal gauge ingest stop, and why did page stamps read 30-09/01-10 during a flood?
- **Q-add-3:** Alert provenance — for every TN-Alert push Oct 15–18: originating system (IMD relay vs RTFF model), timestamps, ward scope.
- **Q-add-4:** Contract checkpoint — TNUIFSL/WRD: was the vendor's forecast-delivery obligation tested against Episode 1, and what does the SLA say about a season-opening no-show?
- The deliverable the public paid ₹107.2 crore for — *advance* warning at ward level — did not happen for the first NEM episode of 2026. IMD's generic district alerts are not that product, and cost a fraction.

## Surfaces updated with this finding

- CFM Live (https://cashlessconsumer.zo.space/cfm-live) — Episode tab now carries the ❌ verdict line; Forecast tab notes the frozen run registry.
- This note supersedes the outage note's ingest inference (see correction above).

## Correction (18 Oct, 6:22–6:45 pm IST — Thinkpad browser + curl, Chennai vantage)

Rendering the portal in a real browser from the Indian IP revised three earlier readings:

1. **Forecast engine is alive.** Dashboard cards read **"Based On ECMWF Date: 2026-10-18 Run R00"**
   with per-station 24/48/72h values (Anna Univ 5.8/16.9/17.3 mm; Valasaravakkam 4.6/14.5/20.3 mm).
   The stale 81-run registry (last 2025-12-02) is the legacy NCEP-GFS path; the system now runs
   ECMWF ensembles that don't write to that table. So "no model run since Dec 2025" was wrong —
   the claim that survives is narrower: **no forecast bulletin/alert was published for Episode 1**,
   and no public forecast preceded it.
2. **Observation ingest is split.** Homepage AWS carousel: 9/36 station widgets live (all stamped
   2026-10-18T18:30 — e.g. Karapakkam 34.0 mm today); 27 dead. Dashboard ARG/AWS grid: 151 widgets,
   89 "Invalid date", **zero** with an Oct-2026 reading. District rainfall API (the panel the
   public compares) still returns `"[]"`.
3. **Last published bulletin = 30-09-2026.** Homepage carousel's newest forecast bulletin is
   "Rainfall Forecast_ECMWF_Ens75_30 09 2026 00 UTC" — confirming the 30-09 sighting. Nothing
   published for Oct 15–18 despite a live forecast engine updating daily.

**Revised verdict:** Episode 1 was *not publicly predicted* — the forecast leg has run (ECMWF,
daily, including through the event window, per the R00/R18 run stamps) but its public output
stopped at 30-09-2026, and during the event even the observation grid was largely dark. A live
engine that publishes nothing during a flood is a disclosure failure, not a forecasting one.
RTI should now ask: were ECMWF run outputs circulated internally (WhatsApp/dept emails) during
Oct 15–18, and why the public bulletin chain stopped on 30-09-2026?

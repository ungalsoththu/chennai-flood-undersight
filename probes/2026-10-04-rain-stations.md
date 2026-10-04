# [CFM-DSS] Flagship rain-panel re-probe — 2026-10-04

**Method:** live `GET /Master/GetRainfallDatafordashboard?district=<D>` (the endpoint behind the flagship 38-station panel), all 5 districts, ~08:00 IST. Raw responses: `UngalSoththu/data/chennai-floods/probes/rain-stations-2026-10-04/rain_<district>.json`. Baseline: census day 2026-09-29 (`cfm-dss-2026-09-29/dump/api/dashboard_2026-09-29.json`).

## Result: 10 of 38 reporting today (26%); 16 of 38 (42%) dead ≥1 year or blank

| Cohort | Count | Stations |
| --- | --- | --- |
| Fresh (dated 2026-10-04) | **10** | Kelambakkam, Lathur, Walajabad AWS, pennalur, Kaveripakkam Lake, Pudupadi, Gummidipoondi AWS, Periapalayam AWS, RK Pet AWS, Tiruttani AWS |
| Stopped together 2026-09-29 16:30 (5 days ago) | **10** | Karapakkam, Marina, Semmancheri AWS, Padappai, Pennalur, Arakkonam AWS, Kilpakkam, Korattur Anaicut AWS, Ponneri AWS, Thervoy Kandigai Lake |
| Exactly ~1 year old (2025-10-04) | **2** | Mamallapuram AWS, Pallipattu AWS |
| Frozen ≥1 year | **14** | Nungambakkam (511 d), Meenambakkam ISRO (511), Madhavaram_AMFU (511), Ennore Port (511), Kanchipuram ISRO (511), KVK Kattapakkam (511), Jaya Engineering College (511), KVK Tirur (511), Tiruttani PTO ISRO (511), Mahabalipuram (710), VIT_CHENNAI (710), RANIPET (710), RIMC Lab (712), KALAVAI (819) |
| No reading at all | **2** | Siruseri, Cholavaram AWS |

## Findings vs census day (2026-09-29)

1. **The frozen cohort has not moved by a single reading.** All seven 2025-05-10 gauges — including IMD reference gauge **Nungambakkam**, dead 511 days — are still at 2025-05-10. **[A]**
2. **Deterioration, not recovery:** 22/38 fresh on census day → **10/38 today**.
3. **New batch-death signature:** ten stations stopped at the *same minute* (2026-09-29 16:30) — an ingest/pipeline failure five days ago, not individual sensor decay. Nobody restarted it in five days. **[A/inference]**
4. **Annual-fossil pattern repeats:** two stations read exactly 2025-10-04 — the panel keeps serving year-old data as "current". **[A]**
5. Station set identical to census day (38/38, no additions or removals).

**Verdict for the record:** the flagship panel's "real-time" claim now rests on 10 of 38 stations at the onset of NEM 2026. F2 (stale flagship) is confirmed and worsening; ledger row 3's "22 fresh" should be read as a census-day snapshot, with this probe as the current state.

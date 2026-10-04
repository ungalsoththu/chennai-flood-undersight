# Desk brief — rtff-undersight · 2026-10-04

**Story:** Undersight of Chennai Realtime Flood Forecasting (RTFF & SDSS) · status: tip
**Ledger:** 18 claims — 15 at L3, 1 at L4, 3 at L2 · **Sources registered:** 13 · **Reply register:** 0 records
**Compiled by:** desk session 2026-10-04 (Asia/Kolkata)

---

## 1. What is known, by level

### L4 — publishable as fact (1)
| Claim id | What it establishes |
| --- | --- |
| c-mutkbx6k22 | During the Ditwah remnant (30 Nov–6 Dec 2025) the system's own layers recorded the flood — citizen level-6 report at Puzhal (2025-12-04 03:00Z), bridge danger-level peaks same day (Aminjikarai 7.705 m; Manali 2.501 m), 168 crowd reports in Nov 2025 — consistent with The Hindu's dated Ennore/Red Hills reporting. The system worked as a **recorder**. Ledgered caveat: the independent chain is the press; the two sensor/crowd layers are same-origin. |

### L3 — authenticated artifacts, one chain each (15)
**Data layer (the mirror):**
- c-mutkbm5b15 — GeoServer: 344 layers, 343 anonymously readable (2026-09-29); re-census 2026-10-03: unchanged.
- c-mutkbm5e16 — Flagship rain panel: 22/38 fresh on 2026-09-29 → **10/38 (26%)** on 2026-10-04; 10 stations stopped together at 16:30 on 2026-09-29 and stayed dead 5 days.
- c-mutkbm5g17 — Frozen cohort: Nungambakkam (IMD reference) + 7 more at 2025-05-10 — probe tally 511 days; three at ~710 d; RIMC Lab 712 d.
- c-mutkbm5j18 — Two stations served readings dated exactly 2025-10-04 on 2026-10-04: year-old data as "current".
- c-mutkbm5l19 — Public ward-depth "forecast" layer is a static 2021-08-11 scenario, all 200 wards.
- c-mutkbm5o20 — Open ARG feed stops 2022-09-06; dashboard serves 2026 via a different pipeline.
- c-mutkbx6h21 — Public alert feed: 0 rows on every check; no API/RSS/SMS spec; host 403s session-less clients (re-confirmed 2026-10-04).
- c-mutkbx6m23 — Entire public record = 7 image-only bulletins, Oct 2025; archive stops 2025-12-02, before the Ditwah peak.
- c-mutkc88930 — AMC/vendor fields blank across all registry rows; 66 AMC flags, ~6 expiry dates. O&M calendar unknowable from the system's own registry.
- c-mutkc88e32 — Predecessor portal NXDOMAIN (last capture 2025-08-31); only the Dec-2023 rescue survives.

**Media corpus:**
- c-mutkc88b31 — All swept success/impact claims are prospective; zero outlets credit RTFF & SDSS for any Ditwah warning. Documented absence in one corpus (ours) — Tamil layer thin.

**World Bank paper trail:**
- c-mutkbx6p24 — Three RTFF contracts "Pending Implementation" at $0.00 disbursed (RTDAS $6.06M, bid trail 2023-03→2024-09; handholding $83K; DEM/DSM $360K).
- c-mutkbx6r25 — Aug-2026 procurement plan drops all four RTFF/SWD lines; no public descope note.
- c-mutkbx6u26 — 14 archived Bank documents: zero results-narrative mentions of the flagship; no forecast/uptime/alert DLI.

### L2 — leads, never publish as fact (3)
- c-mutkc87y27 — Launch framing: "India's first fully operational", ₹107.2 crore, 4,974 km², five districts (press-handout chain; no sanction order public).
- c-mutkc88228 — Cost reported ₹71 crore (Nov 2022) → ₹107.2 crore (Oct 2025), +51%, no public revision trail (two press datapoints, unauthenticated against primary records).
- c-mutkc88629 — IFMC announcement (2026-10-02, Secretary B. Chandramohan): same street-level 72-hour promise restated a year on; article not yet archived locally. **Named subject — right of reply required.**

---

## 2. What is missing (upgrade paths, cheapest first)

| Gap | To reach | How |
| --- | --- | --- |
| IFMC article not archived; NIE-2022 and launch articles unarchived | L2 → L3 | Fetch, save, hash (commands below). Then the money-figure claims carry artifacts, not URLs. |
| Sanction order / PDGF utilisation certificates / SECON-JBA contract value | L2 → L4 on the money track | RTI to WRD + TNUIFSL (registered source s-mutkbbov14; ready asks in REPORT §5.6). |
| Fate of the vanished $6.06M RTDAS package | L3 → L4 (c-mutkbx6r25) | Written query to World Bank PIC + tender-portal watch for a re-tender + RTI to TNUIFSL. |
| Batch-stop of 10 stations at 2026-09-29 16:30 | L3 → L4 (c-mutkbm5e16) | TNSDMA/WRD explanation or a second independent feed for the same stations. |
| Frozen gauges (511 days) | L3 → L4 (c-mutkbm5g17) | IMD's own record of Nungambakkam — a second pipeline outside CFM-DSS. |
| Ditwah no-credit absence | L3 → L4 (c-mutkc88b31) | Independent Tamil-media sweep (Dinamani, Daily Thanthi, Dinamalar, Hindu Tamil Thisai), 30 Nov–6 Dec 2025 archives. |
| **Forecast skill** | not knowable at any level | No forecast archive exists (c-mutkbx6m23). Only forward capture fixes this: per-activation bulletin + model-run mirror. |
| **O&M calendar** | not knowable at any level | RTI only (c-mutkc88930). |

**Session constraints hit today:** (a) bash sandbox unusable on this host — no hashes computed; (b) keyless web-search engines blocked; (c) portal 403s non-session clients — empty-feed checks must use the scripted-session path. None blocks the moves below except hashing (needs bash restored or a board task).

---

## 3. Next three reporting moves

**Move 1 — Dispatch the reply + RTI pack (this week).** Four letters, drafted from the question bank, each ask tied to a claim id: (1) Secretary B. Chandramohan / TNSDMA — IFMC vs RTFF & SDSS (c-mutkc88629); (2) WRD — the 16:30 batch stop and the 511-day frozen gauges (c-mutkbm5e16, c-mutkbm5g17); (3) TNUIFSL — sanction order, PDGF UCs, fate of IN-TNUIFSL-350974-GO-RFB (c-mutkc87y27, c-mutkbx6p24, c-mutkbx6r25); (4) World Bank India PIC — Aug-2026 descope, IBRD-96250 disclosure status (c-mutkbx6r25, c-mutkbx6u26). Log every send with `journal_reply_record` state `sought`. Zero records exist today; the publication gate stays closed until that changes.

**Move 2 — Stand up the two deterministic watches.** Daily: GetPublishAlert (first non-empty response during NEM 2026 is the beat event) + the 5-district rain-panel probe with the date_time freshness rule. Weekly: bulletin-host check (gap G7). Deterministic scripts, evidence saved raw + hashed next to the alert. Needs bash restored or a scheduled board task; the source registry already carries cadences.

**Move 3 — Close the two-source gaps on the strongest findings.** (a) Tamil-media sweep for the Ditwah absence claim; (b) archive + hash the three L2 press artifacts; (c) pull IMD/RMC gauge data for Nungambakkam as the second pipeline. Each closes one L3→L4 or L2→L3 upgrade in §2.

---

## 4. Gate status

Story cannot move to draft today: the money track rests on three L2 claims, the reply register is empty, and artifact hashes are uncomputed. The desk's position stays attribution-first: "documents show", "the probe records", "according to" — the only plain statement current at L4 is that the system recorded the December 2025 flood it never publicly proved it forecast.

## 5. Verification commands (for next session, when bash is restored)

```bash
# Hash the WB evidence set + census (attaches hashes to c-mutkbx6p24/r25/u26, c-mutkbm5b15)
sha256sum docs/wb/*.pdf docs/wb/more/*.pdf docs/wfs_census_2026-09-29.csv | tee docs/wb/SHA256SUMS-2026-10-04.txt

# Re-census the live layer set (expect 344 while unchanged)
curl -s "https://chennaifloodmonitor.tn.gov.in/geohorr/ChennaiDSS/ows?service=WFS&version=2.0.0&request=GetCapabilities" -o /tmp/caps.xml
python3 -c "import xml.etree.ElementTree as ET; r=ET.parse('/tmp/caps.xml').getroot(); print(sum(1 for e in r.iter() if e.tag.endswith('}FeatureType')))"

# HF mirror state (pins for c-mutkc88e32 etc.)
curl -s "https://huggingface.co/api/datasets/CashlessConsumer/chennai-flood-monitor-transactions" | python3 -c "import json,sys; d=json.load(sys.stdin); print(d['id'], d['lastModified'], len(d['siblings']),'files')"
```

*Story card still reads `tip`; the desk's work is past `reporting`. Editor action in the web UI (same write API): move to `reporting` — this session did not touch the card to avoid duplicate-slug records.*

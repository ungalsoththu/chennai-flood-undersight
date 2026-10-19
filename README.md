# ChennaiFloodUndersight — சென்னை வெள்ள மேற்பார்வை

**Oversight from below for Chennai's ₹107.2-crore flood-forecasting system (RTFF & SDSS).** The state built India's first urban flood-forecasting decision-support system, documented almost none of it, and publishes 7 PDF bulletins as its entire public output. Meanwhile its own GeoServer serves 344 data layers — 1.7 million rain/water-level readings, flood extents from 2005/2015, station registries with vendor contracts — to anyone who asks, with no license, no API docs, no data policy.

This project: (1) mirrors and documents that public-but-undocumented data, (2) audits the system's technology and economics, (3) publishes the quarterly **RTFF-DSS Ledger**.

## The open-data release (2026-09-29)

| Dataset | Size | Contents |
| --- | --- | --- |
| [chennai-flood-monitor-transactions](https://huggingface.co/datasets/CashlessConsumer/chennai-flood-monitor-transactions) | 37 MB | SRG rain 662,904 rows (1976→2026-02), AWS/ARG 669,147 (2017–2022 bulk), AWLR 385,950 (2021→2026-08), 33 station registries incl. AMC vendor fields (PII-scrubbed) |
| [chennaidss-gis-layers](https://huggingface.co/datasets/CashlessConsumer/chennaidss-gis-layers) | 40 MB | 181 GeoParquet layers: wards, drainage, waterways, tanks, bathymetry, forecast ensembles |
| [chennai-flood-history](https://huggingface.co/datasets/CashlessConsumer/chennai-flood-history) | 2.3 MB | NRSC 2015 + IRS 2005 flood extents, GCC hotspots 2015/NEM-2020, ward depth scenarios, flood warnings |
| [chennai-flood-bulletins](https://huggingface.co/datasets/CashlessConsumer/chennai-flood-bulletins) | 92 MB | All 7 operational bulletins (Oct 2025) — the complete public record |

Companion rescue of the dead predecessor portal: [chennai-rain-gauges](https://huggingface.co/datasets/CashlessConsumer/chennai-rain-gauges) (Dec-2023 archive, 287 layers).

## Why it matters

Chennai's monsoon risk isn't abstract: 2015 (NRSC-mapped city-wide flooding), 2023 Michaung, Dec 2025 (Ennore 56 cm in 3 days, Red Hills shutters opened six times). The state's answer — RTFF & SDSS — is marketed as real-time flood intelligence, yet on our mirror day: only 22 of 38 board stations reported fresh data, the flagship Nungambakkam gauge was a year stale, the alerts API has never shown a single alert, and the ward-level flood scenario is frozen at August 2021. **Public money, undocumented system, unmeasured performance — that combination is what this project exists to end.**

Every number above is reproducible: full layer census in [`docs/wfs_census_2026-09-29.csv`](docs/wfs_census_2026-09-29.csv); catalog diff vs the Dec-2023 rescue in [`docs/layer_diff_vs_2023archive.json`](docs/layer_diff_vs_2023archive.json).
## Lead: NEM 2026 Episode 1 was not publicly predicted (2026-10-17/18)

Chennai's heaviest rain since Michaung (Parrys ~361 mm in one night) arrived with **nothing published by the ₹107.2-crore system**: the last bulletin is dated 30-09-2026, the portal was TCP-dead worldwide at the flood's peak and served India an empty shell (rainfall API `[]` in all five districts, every GeoServer layer byte-identical to the 29-09 census). The engine itself was alive — dashboard cards read "Based on ECMWF 2026-10-18 Run R00" — so this is a **public-disclosure failure, not a forecasting failure**. The only predictions on record were IMD's generic district warnings. Full evidence chain: [`probes/2026-10-18-episode1-not-forecast.md`](probes/2026-10-18-episode1-not-forecast.md) · outage verification: [`probes/2026-10-18-portal-outage-during-nem-episode1.md`](probes/2026-10-18-portal-outage-during-nem-episode1.md) · live public mirror of everything the system holds: https://cashlessconsumer.zo.space/cfm-live

## The two plans

1. **Data + possibilities** — [`DATA.md`](DATA.md) (what the data is, quirks ledger) and [`POSSIBILITIES.md`](POSSIBILITIES.md) (research / journalism / civic tech / policy builds).
2. **RTFF & SDSS audit** — [`AUDIT-PLAN.md`](AUDIT-PLAN.md): Track A technology/digital (availability, API surface, sensor integrity, model layer, alert chain, privacy, open-data compliance) and Track B economic (capex ledger, AMC debt calendar, technical-debt register, unit economics, quarterly Ledger).

## License & posture

Data mirrored from a public government portal; we claim no added restrictions — released as-is for research, journalism, and civic use, with PII scrubbed. Official status remains with TNSDMA/WRD; we are unofficial by design. Security findings go to CERT-In, not the feed. உங்கள் சொத்து — public data belongs to the public.

## Publishing

- **GitHub Pages site:** https://ungalsoththu.github.io/chennai-flood-undersight/ (source: `docs/index.html`, served from main)
- **Layer Atlas:** https://ungalsoththu.github.io/chennai-flood-undersight/maps/ — interactive map of all 344 GeoServer layers, loaded live via WFS from the government server, with a read-only relay fallback (`cashlessconsumer.zo.space/api/cfm-wfs`) because the server's tripled CORS headers break direct browser fetches (search by category, feature count, payload; export GeoJSON). Catalog snapshot + generator in `docs/maps/`.
- **Report:** `REPORT.md` — v0.1 draft, iterating; LaTeX PDF edition follows after review
- **Legal note:** `docs/LEGAL-NOTE.md` — facts aren't copyrightable; §52 fair dealing; NDSAP default-open; CC BY 4.0 on our additions; notice-and-takedown posture
- **Accountability question bank:** `200-QUESTIONS.md` — every question a Chennai-ite could demand an answer to, evidence-graded; resident review bench at https://cashlessconsumer.zo.space/rtff-200-review. Canonical instance of the **Question Bench** technique — reusable template + workflow: `Skills/question-bench/`.

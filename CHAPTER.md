# The Flood Machine and Its Shadow Data

### How Chennai bought a ₹107-crore weather brain, why nobody can check its homework, and how the public can — lawfully — anyway

*Chapter draft v1.0 · 2026-10-04 · UngalSoththu (உங்கள் சொத்து — "your property") desk · every figure traces to `REPORT.md` (the formal audit), `MEDIA-CLAIMS.md`, `DATA-CATALOGUE.md`, `200-QUESTIONS.md`, and the `data/` evidence ledger*

---

## 1. The promise

Every few years, Chennai drowns. In December 2015 the flood drowned the city — the government's own final count was **421 deaths** — and in 2023 Cyclone Michaung put 639 mm on a single gauge in one day. After every flood comes the same promise: *never again unprepared*. In October 2025, Tamil Nadu quietly switched on the most ambitious version of that promise yet — the **Real-Time Flood Forecasting & Spatial Decision Support System (RTFF & SDSS)**: a network of rain gauges, water-level sensors, weather models and flood maps fused into one "brain", sanctioned at **₹107.2 crore**, covering 4,974 km² across five districts, funded largely by World Bank loan money and promoted as India's first fully operational urban flood-forecasting system of its kind. **[A]**

The pitch is genuinely good. A city that floods should have an early-warning brain. **We are not against the system. We are against not being able to check it.**

Because here is what the public actually gets from the ₹107-crore brain: **seven PDF bulletins — images of text, not even selectable text — and a web dashboard**. No published data license. No API documentation. No public alert feed an app developer could build on. No archive of the system's own forecasts. Which means the one thing that matters — *did the brain predict the flood before it happened?* — **cannot be independently verified by the public it protects.** **[A/B]**

## 2. The side door

But the system left a door open.

The same government server that publishes the PDFs also runs an industrial data service — a GeoServer — that the portal never advertises, never documents, and never licenses. On census day (2026-09-29) we counted what it serves: **344 data layers**, including 1.7 million raw sensor readings, flood footprints from the 2005 and 2015 floods, ward-by-ward flood-depth tables, and station registries that embed vendors' own maintenance-contract fields.

We mirrored the readable 343 of those layers — a GET-only, documented, repeatable pull — and published them openly, so that the public record of a public system no longer depends on one server's uptime or one URL's survival. **[A]**

## 3. What the mirror shows

An archive is only useful if it answers questions. Ours answered several the portal itself does not surface:

- **The flagship dashboard is partly theatre.** Of 38 rain stations listed on census day, only 22 reported fresh data. Chennai's historic reference gauges — Nungambakkam, the yardstick for every flood comparison since 2015 — have been frozen at **10 May 2025** for over sixteen months. **[A]**
- **The "forecast" layer is a fossil.** The ward-level flood-depth layer that looks like street-level prediction is a **static scenario dated 11 August 2021** — a rehearsal, republished as a live map. **[A]**
- **Two pipes, one stale.** The machine-readable ARG rainfall feed was last bulk-updated in **January 2022** even as the dashboard reads 2026 data — the old pipeline still runs, unloved and dead, beside the new one. The open one is the stale one. **[A]**
- **Maintenance is a black box.** 66 of 118 sensor stations are flagged under annual maintenance contracts, but expiry fields are 90% blank, and the vendor-name fields are blank across the entire registry — the system's own data does not say who maintains it or until when. **[A]**
- **The media record is silent.** We catalogued every public claim of success or impact. What we found was a pattern: **all the big claims are prospective** — "will save lives", "will transform response" — from launch coverage in October 2025. During Cyclone Ditwah (Nov 30–Dec 6 2025), the system's first real test, not one report or official statement we could find credited it with a specific warning; credit went to IMD, the weather agency. **[B]**

## 4. The money story

"Funded by the World Bank," says the portal. True, but imprecise — and the imprecision is the story. The ₹107.2 crore moved down a three-layer pipe: a **sovereign IBRD loan** at the top, a state **Project Development Grant Fund** in the middle (managed by TNUIFSL, the state's urban-infrastructure treasury), and a consultancy-led implementation at the bottom (the SECON–JBA joint venture, with IIT Madras providing technical oversight). The Bank's current $300M Tamil Nadu urban program — repayable over **32 years, 7 of them grace** — is still paying for RTFF handholding and survey work today.

In other words: citizens will repay this as debt. That makes every dead gauge and every frozen forecast not just a service failure but a **loan-performance question**. And yet no sanction order, no contract split, no AMC schedule, no operations budget for the flagship system is public. The World Bank's own December 2024 procurement plan shows the pattern — an RTFF "handholding" assignment flagged under "the implementation support risks". The lender's paperwork knows the machine needs babysitting; the public isn't told. **[A/B]**

## 5. The experiment: can the public audit this?

This is the part that makes the project more than one city's complaint. We asked: *if a determined resident wanted to hold this system accountable, what would that actually look like?* So we ran it at full scale.

**We wrote down 200 questions** — every question a Chennai-ite could reasonably demand an answer to, from "What exactly is this ₹107-crore thing?" to "Who pays when a vendor's sensor dies mid-monsoon?" — and answered each from our own evidence, grading every answer: ✅ answered, 🟡 partial, ❌ open. The final tally: **107 answered, 57 partial, 36 open.** Forty open rows on a system that has been "fully operational" for a year.

Then we did something unusual: **we machine-reviewed our own work.** An AI reviewer (Jev) scored all 200 questions for *relevance* (mean 3.75/5) and *answer quality* (mean 3.56/5), flagged the 25 weakest answers, and we fixed what was fixable — pulling real per-district station counts, naming the actual vendor gap, writing honest "we don't know yet" where research is still pending. Low scores stayed low where the honest answer is that no public evidence exists. A review bench (score sliders, comments, saved on every change) lets any resident re-score the whole bank themselves — because an accountability bank that only one auditor grades is just another black box.

## 6. The verdict, and the ask

The RTFF & SDSS may well work. The 2026 northeast monsoon will be its second full test, and this year we have the tools to score it publicly. Our audit is not a claim that the machine is broken. It is proof of something harder to fix: **the machine was bought with debt, promoted with superlatives, and shipped without a public report card.**

What we ask for is unglamorous and cheap:

1. **Publish the data you already generate** — licence it under NDSAP, expose the bulletins as text and an API, archive your own forecasts. (Indian law is on our side here: raw government telemetry is not copyrightable, NDSAP 2012 makes openness the default for exactly this data class, and reporting use is fair dealing under §52 of the Copyright Act.)
2. **Publish the money papers** — the sanction orders, the contract splits, the AMC schedules.
3. **Keep the promise that matters** — verify the street-level, 72-hour claim, or retire it.

Until then, the mirror stays up, the question bank stays open, and the flood machine's shadow data belongs to the city that paid for it.

உங்கள் சொத்து. Your property. You get to see the report card.

---

### Method, in one paragraph

The full audit (`REPORT.md`, v0.3) documents the census of the GeoServer (2026-09-29), the 343-layer mirror (four public Hugging Face datasets + the rescued 2023-12 archive), the financing trail (World Bank project records, PDGF rules, TNUIFSL publications, press releases), the media-claims register, the data catalogue with per-layer freshness, the 200-question accountability bank with evidence grades and machine-assisted review, and a claim-evidence ledger where every figure carries a source and a grade (A = system's own records; B = quality press/cross-checked; C = inference, flagged; D = legal analysis). The mirror is GET-only, attribution-first, and republished under CC BY 4.0 on our additions. Reproduction steps: `REPORT.md` Appendix B.

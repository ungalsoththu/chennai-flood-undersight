# [CFM-DSS] Portal outage during NEM 2026 Episode 1 — 2026-10-18

**Event window:** NEM set in 2026-10-15; UAC stalled over north TN battered Chennai from Sat 2026-10-17 evening → Sun 2026-10-18 morning — heaviest spell since 2023 (Michaung). Parrys 361 mm, Kathivakkam 343 mm, Meenambakkam 282 mm, Sathangadu 260 mm (8:30 AM Oct 17 → 4:30 AM Oct 18, @TNFloodmodeller).

## Finding: chennaifloodmonitor.tn.gov.in DOWN at TCP level during the flood — every vantage

Probed 2026-10-18 ~11:00 IST:

| Vantage | Result |
| --- | --- |
| Zo sandbox (curl, 90 s) | HTTP 000, connection timeout |
| Zo browser (steel) | `ERR_TUNNEL_CONNECTION_FAILED` |
| Jina reader (US browser) | HTML fetch times out at 90 s — page never resolves |
| AllOrigins (Cloudflare edge) | **522 — Cloudflare edge itself cannot reach origin** |
| check-host.net ×5 nodes (Canada, Germany, Iran, Singapore, USA) | **All: "Connection timed out" at TCP level** |

- DNS resolves: `chennaifloodmonitor.tn.gov.in` → 103.59.65.127 (NIC CDN). Nothing accepts connections on 443.
- check-host report: https://check-host.net/check-report/51c2b8f9k318
- Wayback: **zero captures 2026-10-10 → 2026-10-18**; closest snapshot 2026-07-12.
- Sandbox→GeoServer also dead (was same-origin infra; consistent with whole-host outage).
- Our own read-only relay (`cashlessconsumer.zo.space/api/cfm-wfs`) is ALSO down this week — space hosting offline ("hosting suspended" response), so the mirror fallback was unavailable exactly when needed. Fix to re-raise the space.

## Broadcast vs systems ledger for the window

**Broadcast publicly (what Chennai-ites could actually see):**
1. **@TNFloodmodeller (X)** — 4 posts, Oct 17 20:24 → 23:13 GMT ("Chennai 2026 Flood Episode 1"): gauge totals + "preliminary analysis of the intense downpour and its potential impact". The RTFF team's numbers reached the public **as tweets, not via the ₹107.2-crore portal**. Posts: 2111553900038037975, 2111564152024260992, 2111576465099878836, 2111596608639091030.
2. **TN-Alert / TNSMART push** — resident report of "alert sent out by TNSMA[RT] about extremely heavy rainfall" (@rsrinii, Oct 18). First observed live use of the alert chain; the portal's own `GetPublishAlert` API was still empty as of census day and is unverifiable now (host down).
3. **IMD/RC Chennai** — orange alert for 6 TN districts (Oct 15 onset day), heavy-rain warnings through Oct 22–23. Normal public channel.
4. **GCC** — commissioner on preparedness; ward-level waterlogging coverage via press.

**Locked in their systems (unreachable during the event):**
- Portal dashboards (rainfall panel, lake/river storage, forecast maps).
- GeoServer `/geohorr/ChennaiDSS/ows` — 344 layers, incl. live `aws_arg_transaction` (669,147 recs at census), AWLR series, forecast ensembles.
- `GetPublishAlert` + ~60 dashboard AJAX endpoints.
- System's own forecast bulletins (B1.0–B5.0 PDFs) — no evidence any new bulletin was issued for Episode 1 (cannot confirm; portal down).
- Crowdsourced flood-report channel — portal down ⇒ citizens can't file either.

## Verdict [A/I]

The gauge network evidently fed the modelling team (gauge-specific totals tweeted within hours), so **ingest worked while the public face was dark** — the exact inversion of a public-warning system. During Episode 1 of NEM 2026, the only public routes for RTFF intelligence were X posts, an app push, and IMD bulletins; the portal that anchors the ₹107.2-crore "real-time" claim served nobody, anywhere in the world, for at least the peak 12+ hours. Whether the outage began before Oct 17 (last confirmed portal data seen by us: Oct 4 probe, 10/38 stations fresh) needs the state's server logs — RTI-able.

**Follow-ups:** (1) re-probe portal + GeoServer recovery; (2) re-raise zo.space relay; (3) RTI: NIC/NICSI hosting status + incident log for chennaifloodmonitor.tn.gov.in, Oct 10–18; (4) capture @TNFloodmodeller's Episode-1 thread into the bulletins dataset as de-facto public output.
**2026-10-18 update:** (5) DONE — the mirror is now public as **CFM Live**: https://cashlessconsumer.zo.space/cfm-live (interactive: Episode-1 broadcast ledger, 38-station gauge panel, 151-station forecast tables + run registry, 200-ward depth scenario, water levels, 344-layer atlas, 7 bulletins; live portal up/down probe via `/api/cfm-status`).

## Follow-up 18 Oct ~6pm IST — resident-vantage probe (Thinkpad, Chennai ISP)

Corrects the earlier "down worldwide" framing:

- **Geo-split confirmed.** Portal HTTP 200 in 0.5s from the resident Thinkpad while all 9 foreign vantages (sandbox, browser, Jina, Cloudflare edge, 5 check-host nodes incl. BR/RU/SC) still TCP-timeout. DNS 103.59.65.127 (NIC CDN) fine throughout.
- **But the monitor is an empty shell for India too:** `GetRainfallDatafordashboard` returns `"[]"` for all 5 districts (38 stations gone from the API); `GetBulletins`/`GetPublishAlert` return 403 (WAF/AJAX guard). User-observed page stamps ("last run" 30-09/01-10) match the feed freeze ~Oct 1.
- **GeoServer up from India** (GetCapabilities 200): `aws_arg_transaction` = 669,147 rows but **zero records after 2023-01-01** — newest row 2021-06-07; it is a dead archive, never the live feed. Live readings flow only through the dashboard AJAX APIs, which now return nothing.
- Post-event ingest cannot be demonstrated for any layer: nothing in the system dates to Oct 2026 as of this probe.
- **Correction:** the portal is not "down"; it drops foreign TCP connections (added after our world-open 2026-09-29/10-04 probes) while serving Indian IPs a monitor with no live data.

## Correction (same day, later Chennai-vantage probes → `2026-10-18-episode1-not-forecast.md`)

The verdict above inferred "ingest worked while the public face was dark." True only for the team's private pipeline (gauges → MIKE Operations, evidenced by their tweeted gauge totals). The **portal's own ingest froze ~2026-10-01**: from a Chennai ISP, `GetRainfallDatafordashboard` returns `[]` for all 5 districts, page stamps read 30-09/01-10, and the GeoServer transaction archive has zero records after 2023-01-01. The portal's forecasting function was offline before Episode 1 — see the successor note for the full evidence chain.

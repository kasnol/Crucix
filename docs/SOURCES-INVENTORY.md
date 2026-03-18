# Crucix Source Inventory (Active in `apis/briefing.mjs`)

Generated: 2026-03-18
Scope: Exact sources orchestrated by `apis/briefing.mjs` + key env requirements + Telegram channel breakdown for dashboard cherry-picking.

---

## 1) Active source set (27)

### Tier 1 — Core OSINT & Geopolitical (11)
1. GDELT
2. OpenSky
3. FIRMS
4. Maritime (`ships`)
5. Safecast
6. ACLED
7. ReliefWeb
8. WHO
9. OFAC
10. OpenSanctions
11. ADS-B

### Tier 2 — Economic & Financial (7)
12. FRED
13. Treasury
14. BLS
15. EIA
16. GSCPI
17. USAspending
18. Comtrade

### Tier 3 — Weather / Environment / Tech / Social (7)
19. NOAA
20. EPA
21. Patents
22. Bluesky
23. Reddit
24. Telegram
25. KiwiSDR

### Tier 4 — Space & Satellites (1)
26. Space

### Tier 5 — Live Market Data (1)
27. YFinance

---

## 2) Env/key requirements by source (practical)

| Source | Env / credential dependency | Notes |
|---|---|---|
| FRED | `FRED_API_KEY` | Macro/econ core signal source |
| BLS | `BLS_API_KEY` | Labor/inflation data |
| EIA | `EIA_API_KEY` | Energy/macro sensitivity |
| FIRMS | `FIRMS_MAP_KEY` | Satellite fire/thermal anomalies |
| ACLED | `ACLED_EMAIL`, `ACLED_PASSWORD` | Conflict events |
| Reddit | `REDDIT_CLIENT_ID`, `REDDIT_CLIENT_SECRET` | OAuth path preferred |
| Telegram | `TELEGRAM_BOT_TOKEN` (optional), `TELEGRAM_CHANNELS` (optional custom list) | Falls back to public web scraping |
| Maritime (`ships`) | `AISSTREAM_API_KEY` (optional) | Better real-time quality with key |
| ADS-B | `ADSB_API_KEY` or `RAPIDAPI_KEY` (optional) | Fallback/public behavior varies |
| ReliefWeb | `RELIEFWEB_APPNAME` (optional) | Better compatibility with API changes |
| Most others | none required | Public/open endpoints as coded |

---

## 3) Telegram module details (exact default channels)

From `apis/sources/telegram.mjs` (`DEFAULT_CHANNELS`):

### Conflict: Ukraine/Russia
| Channel ID | Label | Topic | Note |
|---|---|---|---|
| `intelslava` | Intel Slava Z | conflict | Conflict updates, pro-Russian perspective |
| `legitimniy` | Legitimniy | conflict | Ukrainian politics & conflict analysis |
| `wartranslated` | War Translated | conflict | Conflict translations & OSINT |
| `ukraine_frontline` | Ukraine Frontline | conflict | Frontline situation updates |
| `mod_russia` | Russian MoD | conflict | Russian Ministry of Defense official |
| `CIG_telegram` | Conflict Intel Team | osint | Conflict Intelligence Team analysis |
| `RVvoenkor` | Voenkor RV | conflict | Russian military correspondent |
| `readovkanews` | Readovka | conflict | Russian conflict news aggregator |
| `DeepStateUA` | DeepState Ukraine | conflict | Ukrainian frontline maps & analysis |
| `operativnoZSU` | ZSU Operative | conflict | Ukrainian armed forces updates |
| `GeneralStaffZSU` | General Staff ZSU | conflict | Ukrainian General Staff official |

### Middle East
| Channel ID | Label | Topic | Note |
|---|---|---|---|
| `middleeastosint` | Middle East OSINT | osint | Middle East open source intel |
| `inikiforv` | Nikiforov OSINT | osint | Cross-regional OSINT analyst |

### Geopolitics & Analysis
| Channel ID | Label | Topic | Note |
|---|---|---|---|
| `geaborning` | Geo A. Borning | geopolitics | Geopolitical analysis/forecasting |
| `TheIntelligencer` | The Intelligencer | osint | Intelligence community news |

### Markets & Finance
| Channel ID | Label | Topic | Note |
|---|---|---|---|
| `WallStreetSilver` | Wall St Silver | finance | Commodities + macro commentary |
| `unusual_whales` | Unusual Whales | finance | Market flow and options analysis |

### Custom additions
- Any extra channel IDs in `TELEGRAM_CHANNELS` (comma-separated env var) are appended as topic `custom`.

---

## 4) What to cherry-pick for rootForge dashboards

### A) Finance-first dashboard (high value / low noise)
Use first:
- FRED
- Treasury
- BLS
- EIA
- GSCPI
- YFinance
- (optional social overlay) `unusual_whales`

Avoid leading with conflict-heavy Telegram channels in finance default view; keep those in an “event risk” lane.

### B) Event-risk overlay (for macro shock context)
Use:
- ACLED
- OFAC
- OpenSanctions
- ReliefWeb
- ADS-B
- Maritime (`ships`)
- Select Telegram channels (topic-filtered)

### C) OSINT timeline/map lane
Use:
- GDELT
- Telegram (curated subset)
- Bluesky/Reddit (lower confidence weighting)

---

## 5) Recommended Telegram subset by dashboard lane

### Finance lane (default)
- `unusual_whales`
- `WallStreetSilver`
- `TheIntelligencer` (optional)

### Geopolitics/event lane
- `middleeastosint`
- `CIG_telegram`
- `wartranslated`
- `DeepStateUA`
- `GeneralStaffZSU`
- `mod_russia`

### Keep out of default (high-bias / high-noise until scored)
- Strongly partisan channels should be down-weighted or shown only in source-comparison mode.

---

## 6) Suggested governance for dashboard use

1. **Source confidence labels** per source/channel.
2. **Topic-gated display** (finance view should not be flooded by conflict feed noise).
3. **Cross-source corroboration** before promoting to high-priority cards.
4. **Provenance always visible** on each card (source + timestamp + confidence).
5. **Bias balancing** for Telegram (pair opposing perspectives where possible).

---

## 7) Where this was derived

- `apis/briefing.mjs` (active orchestrated source list)
- `apis/sources/*.mjs` (env dependencies and endpoint hints)
- `apis/sources/telegram.mjs` (`DEFAULT_CHANNELS`, topics, notes)

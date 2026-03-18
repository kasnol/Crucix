# Dashboard Source Profile (Crucix → rootForge AnalyticsPortal)

Generated: 2026-03-18  
Scope: Comprehensive profile for all active Crucix sources (27) with rollout priority and usage policy for rootForge dashboards.

## Legend
- **KEEP**: include in default production dashboard lanes now
- **OPTIONAL**: include in secondary/advanced lanes after baseline stability
- **EXCLUDE (default)**: do not include in default operator view; only enable in special/research mode

---

## 1) Comprehensive source matrix (all 27)

| Source | Tier | Domain | Default status | Primary lane | Why / notes |
|---|---:|---|---|---|---|
| FRED | 2 | Macro/Econ | **KEEP** | Macro regime | Core macro signal backbone |
| Treasury | 2 | Macro/Econ | **KEEP** | Macro regime | Rates/debt context |
| BLS | 2 | Macro/Econ | **KEEP** | Macro regime | Labor/inflation context |
| EIA | 2 | Energy/Macro | **KEEP** | Stress + macro | Energy shock relevance |
| GSCPI | 2 | Supply chain | **KEEP** | Stress radar | Good systemic pressure indicator |
| YFinance | 5 | Market prices | **KEEP** | Stress + actions | Fast market baseline feed |
| USAspending | 2 | Fiscal/government | OPTIONAL | Policy/fiscal lane | Slower-moving but useful context |
| Comtrade | 2 | Trade flows | OPTIONAL | Macro/trade lane | Valuable but less intraday |
| NOAA | 3 | Weather | OPTIONAL | Event-risk | Use for weather-linked disruption |
| EPA | 3 | Environment | OPTIONAL | Event-risk | Add when environmental risk matters |
| WHO | 1 | Health events | OPTIONAL | Event-risk | Keep as low-frequency strategic signal |
| GDELT | 1 | News event graph | **KEEP** | OSINT timeline | Broad event coverage, needs confidence gating |
| ACLED | 1 | Conflict events | **KEEP** | Geopolitical shock | High-value conflict structuring |
| OFAC | 1 | Sanctions | **KEEP** | Geopolitical shock | Direct market relevance |
| OpenSanctions | 1 | Sanctions/entity | **KEEP** | Geopolitical shock | Good corroboration with OFAC |
| ReliefWeb | 1 | Humanitarian crisis | OPTIONAL | Event-risk | Contextual, not always trading-immediate |
| OpenSky | 1 | Air traffic | OPTIONAL | Logistics/flow | Useful for disruption context |
| ADS-B | 1 | Flight telemetry | OPTIONAL | Logistics/flow | Useful but can be noisy |
| Maritime (`ships`) | 1 | Vessel/AIS | OPTIONAL | Logistics/flow | Important for chokepoint signals |
| FIRMS | 1 | Satellite fire | OPTIONAL | Event-risk map | Useful in event correlation mode |
| Safecast | 1 | Radiation | OPTIONAL | Nuclear watch | Strategic/rare events |
| Space | 4 | Satellite activity | OPTIONAL | Space watch | More niche unless use-case-driven |
| Patents | 3 | Tech/IP | EXCLUDE (default) | Research lane | Slow-moving; not default dashboard signal |
| Bluesky | 3 | Social sentiment | EXCLUDE (default) | Social lane | High noise unless confidence model is strong |
| Reddit | 3 | Social sentiment | EXCLUDE (default) | Social lane | High noise/manipulation risk |
| Telegram | 3 | OSINT/social | OPTIONAL | OSINT lane | Use curated subset only + bias controls |
| KiwiSDR | 3 | SDR/radio map | EXCLUDE (default) | Research lane | Interesting but low immediate decision value |

---

## 2) Telegram channel policy (inside Telegram source)

Telegram itself should be **OPTIONAL** and topic-gated. Not a default “always-on top card” source.

### KEEP subset (for event-risk lane)
- `middleeastosint`
- `CIG_telegram`
- `wartranslated`
- `DeepStateUA`
- `GeneralStaffZSU`
- `mod_russia`

### OPTIONAL subset (for finance lane overlays)
- `unusual_whales`
- `WallStreetSilver`
- `TheIntelligencer`

### EXCLUDE by default (until scoring/bias controls improve)
- strongly partisan channels without balancing pair/corroboration

---

## 3) Recommended lane mapping for AnalyticsPortal

### Lane A — Macro Regime (default)
KEEP only:
- FRED, Treasury, BLS, EIA, GSCPI

### Lane B — Market Stress (default)
KEEP only:
- YFinance, EIA, GSCPI, (plus derived metrics from analytics)

### Lane C — Geopolitical Shock (default)
KEEP + OPTIONAL:
- ACLED, OFAC, OpenSanctions, GDELT (+ ReliefWeb optional)

### Lane D — Logistics / Physical-world (optional lane)
OPTIONAL:
- OpenSky, ADS-B, Maritime, FIRMS

### Lane E — Social / OSINT (optional lane)
OPTIONAL/EXCLUDE controlled:
- Telegram curated subset, Bluesky, Reddit

### Lane F — Specialist monitors (collapsed by default)
OPTIONAL/EXCLUDE:
- Safecast, Space, EPA, WHO, KiwiSDR, Patents

---

## 4) Rollout phases (practical)

### Phase 1 (ship first)
- FRED, Treasury, BLS, EIA, GSCPI, YFinance
- ACLED, OFAC, OpenSanctions, GDELT

### Phase 2
- ReliefWeb, OpenSky, ADS-B, Maritime, FIRMS
- Telegram curated subset (strict governance)

### Phase 3
- NOAA, EPA, WHO, Safecast, Space
- Bluesky, Reddit, KiwiSDR, Patents (research/experimental)

---

## 5) Governance (non-negotiable)

Every published dashboard card must include:
1. State change
2. Why it matters
3. Confidence
4. Time horizon
5. Suggested action / watch stance
6. Invalidation condition
7. Provenance (source + timestamp)

No 7 fields = no publish.

Additional controls:
- cross-source corroboration before FLASH tier
- source confidence weights
- social-source downweighting by default
- explicit bias note for Telegram/social channels

---

## 6) Use in rootForge architecture

Do not import Crucix monolithic wiring directly.

Use this profile with rootForge split:
- `rootForge-newsintel`: collection/classification
- `rootForge-analytics`: scoring/contracts/derived signals
- `rootForge-analyticsPortal`: rendering + operator UX

Portal consumes contract outputs, not raw source adapters.

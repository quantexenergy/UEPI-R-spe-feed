# UEPI-R SPE Live Feed

Continuous S1 Solar Radiation Storm Risk Assessment (GOES SGPS Only)

```
2026-04-29 20:00 UTC | Status: QUIET | latest >=10 MeV flux: 0.20 pfu
```

---

## Scientific Validation

Castillo, J. A. (2026). *UEPI-R SPE: Real-Time Early Warning for Solar Energetic Particle Events.* ESS Open Archive.

Validated on 14 years of GOES proton-flux data (2011–April 2025) spanning two solar cycles and two instrument generations (EPEAD → SGPS).

| Metric | Value |
|--------|-------|
| Alert-active coverage (SC25) | **79.2%** [95% CI: 66.5%–88.0%] |
| Precision (SC25) | 68.6% |
| False alert rate | 0.056 / day |
| Median lead time | 151 min |
| Day-level TSS | 0.767 |
| SC24 cross-cycle backtest | 72.7% precision, 0.005 false/day |

---

## How It Works

UEPI-R SPE performs causal regime detection directly on the GOES SGPS >=10 MeV integral proton flux stream. No flare association, no coronagraph imagery, no supervised model fitting. The same algorithmic architecture has been independently validated on solar flare onset prediction and lithium-ion battery degradation, supporting the claim that the method captures a domain-independent instability precursor.

The system is designed to **complement, not replace** NOAA/SWPC radiation storm alerts.

---

## Data Source

- **Endpoint:** [services.swpc.noaa.gov/json/goes/primary/integral-protons-1-day.json](https://services.swpc.noaa.gov/json/goes/primary/integral-protons-1-day.json)
- **Channel:** `>=10 MeV` integral proton flux
- **Cadence:** 1-min samples
- **Detector cron:** every 15 min

## Output Files

- `uepi_r_spe_public.json` — current alert state, latest flux, summary
- `uepi_r_spe_public_transitions.json` — most recent state change

## Verification Rules

- **Threshold:** S1 = >=10 pfu at >=10 MeV (NOAA radiation storm scale)
- **Hazard window:** 24 hours from alert onset
- **Hit:** First S1-threshold crossing within hazard window
- **False alert:** No crossing within 24 h
- **Miss:** Crossing with no active alert at onset

## Related Feeds

- [UEPI-R Solar Flare Risk Monitor](https://github.com/quantexenergy/UEPI-R-solar-feed) — companion XRS-based detector

---

*Quantex Energy LLC — Wyoming, 2026*

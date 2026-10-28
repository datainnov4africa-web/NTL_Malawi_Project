<p align="right"><a href="methodology.fr.md">Français</a></p>

# Methodology — Malawi (2014–2025)

## Data and cleaning

VIIRS DNB monthly (VCMSLCFG) and annual VNL V2, harmonised DMSP–VIIRS, daily Black Marble, GHSL/WorldPop, Sentinel-5P NO₂/SO₂, MODIS LST, World Bank. Cleaning: pixels valid if cf_cvg ≥ 2, unit-month kept if ≥ 80% of pixels observed, spikes replaced, background and gas flares masked.

## 📈 Use case 1 — Time dynamics

- **Question** — Is activity accelerating or slowing down, net of seasonality?
- **Data** — VIIRS VCMSLCFG (monthly), VIIRS VNL V2 (annual), Harmonised DMSP–VIIRS (Li et al., 2020)
- **Method** — Robust STL (period 12) on log(sum of lights); Theil–Sen slope and Mann–Kendall test on annual composites; anomaly and break detection.
- **Validation** — Trend significance (Mann–Kendall) and monthly/annual consistency (**p-value = 0.0002**)
- **Uncertainty** — 95% CI of annual growth: +2.6% to +6.8%
- **Limits** — Cloud cover and short summer nights; light is not value added.
- **Status** — `experimental` · Confidence: high
- **References** — Cleveland et al. (1990) STL; Sen (1968); Elvidge et al. (2017).
- **Dashboard page** — [`#time`](https://datainnov4africa-web.github.io/NTL_Malawi_Project/?country=MWI#time)

**Results of this run**

- `F02` Between 2014 and 2025, night-time light in Malawi changed by +5.0% per year (95% CI: +2.6% to +6.8%). Over the last 12 months, the seasonally adjusted level is -2.6% relative to the previous 12 months. (confidence high: significant trend (p < 0.01; n = 12))
- `F54` Validation: Trend significance (Mann–Kendall) and monthly/annual consistency (p-value = 0.0002). Uncertainty: 95% CI of annual growth: +2.6% to +6.8% Limitations: Cloud cover and short summer nights; light is not value added. Status: experimental statistic; confidence high.

## 🗺️ Use case 2 — Regional growth and convergence

- **Question** — Which regions take off, which fall behind?
- **Data** — VIIRS VNL V2, GHSL / WorldPop, Sentinel-5P NO₂
- **Method** — Robust growth per unit (Theil–Sen, Mann–Kendall), growth/stagnation/decline classes, β- and σ-convergence, Herfindahl index.
- **Validation** — Rank correlation with tropospheric NO₂ (independent source) (**Spearman ρ = 0.15**)
- **Uncertainty** — Class assigned only if |slope| ≥ threshold and p < α; CI of β (robust errors).
- **Limits** — Small units: noise and light blooming between neighbours.
- **Status** — `experimental` · Confidence: medium
- **References** — Barro & Sala-i-Martin (1992) convergence; Henderson, Storeygard & Weil (2012).
- **Dashboard page** — [`#regions`](https://datainnov4africa-web.github.io/NTL_Malawi_Project/?country=MWI#regions)

**Results of this run**

- `F03` Of 28 ADM2 units, 25 show significant growth, 3 are stagnating and 0 are declining. Light remains concentrated: Central Region accounts for 48% of national light. (confidence medium: classification of 28 units, threshold ±1%/yr and p < 0.10)
- `F04` Across ADM2 units, light per capita converges: the least-lit units are catching up. (confidence medium: β = −0.023 [−0.032; −0.014], n = 27)
- `F24` Central Region (ADM1, 2025): share of national light 48.4%, annual growth +5.9% (CI +3.7% to +8.2%, class Growth), light per capita 0.045, population 0.47 M, in the dark 66%, estimated GDP (experimental) 5.90 bn USD.
- `F25` Southern Region (ADM1, 2025): share of national light 40.4%, annual growth +3.6% (CI +0.1% to +5.4%, class Growth), light per capita 0.039, population 0.45 M, in the dark 68%, estimated GDP (experimental) 4.92 bn USD.

## 💹 Use case 3 — Light–GDP relationship

- **Question** — Can growth be estimated before its release, and regional GDP?
- **Data** — VIIRS, Real GDP (World Bank, WDI)
- **Method** — log(light) ~ log(GDP) in levels and growth, OLS with HAC errors; out-of-sample nowcast; regional GDP = national GDP allocated pro rata of light.
- **Validation** — Out-of-sample tracking of official growth (**correlation / MAE (pp) = -0.22 / 2.2**)
- **Uncertainty** — 95% CI of the elasticity: 0.75 to 2.11; 80% and 95% prediction intervals.
- **Limits** — Short annual sample; regional GDP is an experimental statistic to be checked against regional accounts.
- **Status** — `experimental` · Confidence: medium
- **References** — Henderson et al. (2012) AER; Chen & Nordhaus (2011) PNAS; Gibson et al. (2021) JDE.
- **Dashboard page** — [`#time`](https://datainnov4africa-web.github.io/NTL_Malawi_Project/?country=MWI#time)

**Results of this run**

- `F05` The elasticity of light with respect to real GDP is 1.43 in levels (95% CI: 0.75 to 2.11, R² = 0.69, 12 years) and 0.56 in growth rates (CI: −3.44 to 4.56). Out of sample, light growth tracks GDP growth with a correlation of −0.22 (mean absolute error: 2.2 percentage points of growth). (confidence medium: n = 12, significant but wide CI (1.36))
- `F30` Light–real GDP elasticity in levels: β = 1.43 (95% CI 0.75 to 2.11, R² = 0.69, n = 12, confidence medium: n = 12, significant but wide CI (1.36)). +1% GDP ↔ +β% light.
- `F31` Light–real GDP elasticity in growth rates: β = 0.56 (95% CI -3.44 to 4.56, R² = 0.01, n = 11, confidence low: n = 11, not significant (p = 0.78)). +1% GDP ↔ +β% light.
- `F32` Light–real GDP elasticity in long DMSP–VIIRS series: β = 1.06 (95% CI 0.72 to 1.40, R² = 0.83, n = 30, confidence high: n = 30, p < 0.01, narrow CI). +1% GDP ↔ +β% light.

## ⚡ Use case 4 — Shocks and resilience

- **Question** — How deep was a shock, and how fast the recovery?
- **Data** — VIIRS (monthly), Black Marble VNP46A2 (daily), event catalogue
- **Method** — Gap to the pre-shock level on the seasonally adjusted series; structural breaks; daily Black Marble index.
- **Validation** — Does the trough exceed ordinary variability? (**trough (main shock) = 2.6% — no**)
- **Uncertainty** — Pre-shock month-to-month variability (robust SD); unexplained breaks flagged.
- **Limits** — Shocks hitting poorly lit activities (agriculture, daytime services) are underestimated.
- **Status** — `experimental` · Confidence: low
- **References** — Román et al. (2018); Elvidge et al. (2020) COVID-19 lockdown lights.
- **Dashboard page** — [`#shocks`](https://datainnov4africa-web.github.io/NTL_Malawi_Project/?country=MWI#shocks)

**Results of this run**

- `F06` The most pronounced shock in the seasonally adjusted series is “COVID-19”: trough of +2.6% (09/2020), return to the pre-shock level after 7 months. (confidence low: trough compared with pre-shock month-to-month variability)
- `F34` COVID-19 (2020-03-01 → 2021-06-30): trough of 2.6% on 2020-09-01, back to the pre-shock level after 7 months. Distinguishable from noise: no.
- `F35` Structural breaks: 2015-11-01 (5.9 %); 2017-02-01 (35.5 %); 2021-04-01 (13.4 %). Without a known event within ±6 months: 2.
- `F36` Hardest-hit regions (trough): Central Region -21.5 % (covid19), Northern Region -0.4 % (covid19), Southern Region 0.8 % (covid19).

## ⚖️ Use case 5 — Inequality and electrification

- **Question** — Where do people without electricity live?
- **Data** — VIIRS VNL V2, GHSL / WorldPop, GHSL SMOD, electricity access (WDI)
- **Method** — Population-weighted Gini and Theil; population of inhabited pixels below the detection threshold; sensitivity to three thresholds; bootstrap CI of the Gini change.
- **Validation** — Gap with the World Bank electricity-access rate (**mean gap (pp) = 17.5**)
- **Uncertainty** — Range across radiance thresholds; bootstrap CI of the Gini.
- **Limits** — Proxy of outdoor lighting, not of connection: a connected but dimly lit household looks “in the dark”.
- **Status** — `experimental` · Confidence: medium
- **References** — Theil (1967); Falchetta et al. (2020) electricity access from lights.
- **Dashboard page** — [`#inequality`](https://datainnov4africa-web.github.io/NTL_Malawi_Project/?country=MWI#inequality)

**Results of this run**

- `F07` The Gini coefficient of light per capita (ADM2) is 0.42 in 2025 (no significant change since 2014). About 0.52 million people live in inhabited areas with no detectable light (66% of the inhabited population). (confidence medium: sensitive to the radiance threshold (from 0.48 to 0.57 M depending on the threshold); a proxy for outdoor lighting, not for grid connection)
- `F37` Gini of light per capita (ADM2): 0.491 in 2014 → 0.424 in 2025 (change -0.067, bootstrap CI -0.114 to 0.008). Theil T 0.308; between-region share 3%.
- `F38` People in inhabited areas without detectable light: 0.39 M (71%) in 2014 → 0.52 M (66%) in 2025. Urban/rural light-per-capita ratio 1.8. Proxy of electricity access, sensitive to the threshold.
- `F39` Average gap between the share of people in lit areas and the World Bank electricity-access rate: 17.5 points.

## 🏭 Use case 6 — Industrial zones

- **Question** — Where is industry, and is its activity growing?
- **Data** — VIIRS VNL V2, GHSL BUILT-S, Sentinel-5P NO₂/SO₂, MODIS MOD11A2, OpenStreetMap
- **Method** — Concordance of six signals per pixel (≥ 3 including light), 8-connected clusters, typology and confidence.
- **Validation** — Comparison with the reference list (OpenStreetMap) (**precision / recall / F1 = 55% / 27% / 0.36**)
- **Uncertainty** — Per-cluster confidence from the number of strong signals; isolated sites to verify.
- **Limits** — Sentinel-5P (≈ 5 km) and MODIS (1 km) resolution: signals describe a neighbourhood.
- **Status** — `experimental` · Confidence: low
- **References** — Elvidge et al. (2016) gas flares; Pesaresi et al. (2023) GHSL.
- **Dashboard page** — [`#industry`](https://datainnov4africa-web.github.io/NTL_Malawi_Project/?country=MWI#industry)

**Results of this run**

- `F08` 20 industrial clusters detected from concordant satellite signals: 11 heavy industry, 6 business parks & logistics, 1 oil & gas sites and 2 isolated sites to verify. They emit 14.0% of national light (latest year); their light changes by +2.2% per year. Southern Region has the most industrial activity. (confidence low: precision 55% and recall 27% against the reference list)
- `F40` 20 industrial clusters (≥ 3 of 6 signals): Heavy industry 11, Business park & logistics 6, Isolated site to verify 2, Oil, gas & flares 1. Share of national light: 14.0%; annual growth +2.2%. Validation (OpenStreetMap): precision 55%, recall 27%.
- `F41` IND-001 — Isolated site to verify in Blantyre (Southern Region) (65.36 km², 3 signals, confidence low); IND-004 — Business park & logistics in Lilongwe (Central Region) (3.655 km², 3 signals, confidence low); IND-002 — Heavy industry in Mzimba (Northern Region) (6.235 km², 3 signals, confidence low); IND-007 — Business park & logistics in Lilongwe (Central Region) (1.935 km², 3 signals, confidence low); IND-005 — Heavy industry in Nkhotakota (Central Region) (3.225 km², 3 signals, confidence low); IND-011 — Business park & logistics in Lilongwe (Central Region) (1.72 km², 3 signals, confidence low); IND-006 — Business park & logistics in Lilongwe (Central Region) (1.935 km², 3 signals, confidence low); IND-003 — Heavy industry in Mzimba (Northern Region) (3.655 km², 3 signals, confidence low); IND-010 — Oil, gas & flares in Karonga (Northern Region) (1.72 km², 3 signals, confidence low); IND-009 — Heavy industry in Chikwawa (Southern Region) (1.935 km², 4 signals, confidence medium)
- `F42` Southern Region: 8 industrial cluster(s), 73.7 km², 25.2% of the region's light.

## 🏖️ Use case 7 — Seasonal tourism

- **Question** — Which areas live from tourism, and how does the season evolve?
- **Data** — VIIRS (monthly), hotel nights or WDI arrivals
- **Method** — Summer excess net of comparable units at the same latitude; one-sided test; season index base 100; seasons overlapping Ramadan flagged.
- **Validation** — Correlation with international tourist arrivals (WDI) (**r = -0.96**)
- **Uncertainty** — p-value per unit; 2020–2021 excluded from the classification.
- **Limits** — Any summer activity (diaspora, second homes, festivals) is captured, not only tourism.
- **Status** — `experimental` · Confidence: low
- **References** — Seasonal light analyses of tourism, e.g. Hu et al. (2021).
- **Dashboard page** — [`#tourism`](https://datainnov4africa-web.github.io/NTL_Malawi_Project/?country=MWI#tourism)

**Results of this run**

- `F09` 2 of 28 units show a net summer light excess of at least 10%: Nkhotakota (Central Region), Mzimba (Northern Region). The median net excess reaches +21% in the most touristic zone. The season index (base 100 = 2019) falls to 109 in 2020 and stands at -61 in 2025. (confidence low: correlation of -0.96 with international tourist arrivals (WDI) (4 years))
- `F46` 2 tourist zone(s) out of 28 ADM2 units (net summer excess ≥ 10%, peak months [12, 1]): Nkhotakota (Central Region) (+21%, confidence medium), Mzimba (Northern Region) (+12%, confidence medium).
- `F47` Season index (base 100 = 2019): 2015: 353, 2016: 131, 2017: 273, 2018: 69, 2019: 100, 2020: 109, 2021: -614, 2022: 196, 2024: 362, 2025: -61. Years when Ramadan overlaps the season: 2021, 2022, 2024, 2025.
- `F48` Correlation between the season index and international tourist arrivals (WDI): -0.96 (4 years; in growth rates: n/a).

## 🏙️ Use case 8 — Urbanisation signals

- **Question** — Where do cities spread, where do villages get electrified, and where does population grow without light?
- **Data** — VIIRS VNL V2, GHSL GHS-POP / WorldPop, GHSL GHS-BUILT-S R2023A, urban population (WDI)
- **Method** — Lit area (pixels above the threshold) and population per unit; Theil–Sen growth rates; newly lit pixels (dark two years in a row at the start, lit two years in a row at the end), split between electrification of inhabited areas and new settlements; light/population typology.
- **Validation** — Rank correlation with GHSL built-up area growth (independent source) (**Spearman ρ = 0.09**)
- **Uncertainty** — Persistence required over two years to limit noise; ± 1 pp margin between growth rates before classifying.
- **Limits** — Light measures outdoor lighting, not urbanisation in the administrative sense; blooming widens cities; GHSL population is interpolated between epochs.
- **Status** — `experimental` · Confidence: low
- **References** — Zhou et al. (2015) urban extent from lights; Pesaresi et al. (2023) GHSL; Min et al. (2013) village electrification.
- **Dashboard page** — [`#urban`](https://datainnov4africa-web.github.io/NTL_Malawi_Project/?country=MWI#urban)

**Results of this run**

- `F49` National lit area: +8.6% per year; population: +2.7% per year. Classes (ADM2): Electrified urbanisation 27, Balanced growth 1.
- `F50` Between 2014 and 2025: 1,743 km² newly lit, of which 489 km² already inhabited (electrification, ≈ 36k people) and 1,254 km² of new settlements; 30 km² lost their light.
- `F51` Fastest lit-area expansion: Chiradzulu (Southern Region) (+16.6%/yr), Nkhata Bay (Northern Region) (+15.1%/yr), Nkhotakota (Central Region) (+15.0%/yr), Dowa (Central Region) (+14.6%/yr), Chitipa (Northern Region) (+13.7%/yr), Phalombe (Southern Region) (+12.6%/yr). Unlit growth (population faster than light): none.
- `F52` Spearman rank correlation between lit-area growth and GHSL built-up growth: 0.09 (p = 0.664, 28 units).

## General limits of night-time lights

- **What lights measure** — Upward radiance emitted around 01:30: agriculture, daytime trade, poorly lit services and the rural informal economy are poorly captured.
- **Saturation and blooming** — DMSP saturates in city centres (DN 63) and “blooms” beyond lit areas; VIIRS is much better, but blooming still inflates the lit area of cities.
- **Gas flares and isolated sites** — The automatic mask may remove isolated mines, ports or power plants, and miss small flares; candidates are exported for verification.
- **Clouds, seasons, moon** — Cloudy months are only partially observed; STL removes average seasonality but not an abnormal season (snow, late monsoon).
- **Product breaks** — DMSP and VIIRS are not directly comparable: the harmonised long series (Li et al., 2020) is a modelled product, to be read for trends only.
- **NTL–GDP elasticity** — Estimated on 10 to 30 annual observations: wide intervals, possible instability, a non-causal relationship that varies with the level of development.
- **Access to electricity** — “Inhabited without light” ≠ “not connected”: a connected household with low consumption is invisible; the indicator depends strongly on the radiance threshold and the population data.
- **Administrative boundaries** — geoBoundaries/GAUL may differ from official boundaries; small ADM2 units are sensitive to light spilling over from neighbouring units.
- **Industrial zones** — Detection relies on thresholds: a power plant, a port or a large shopping centre can meet the signals; a dimly lit factory without visible emissions is missed. Sentinel-5P (≈ 5 km) and MODIS (1 km) are coarser than VIIRS: NO₂/SO₂/heat signals describe a neighbourhood, not a building.
- **Summer tourism** — The summer excess captures any rise in summer light (second homes, diaspora visits, festivals, construction), not only tourism; at high latitudes, very short summer nights reduce VIIRS observations. Ramadan changes night-time activity: the summers concerned are flagged.
- **Urbanisation** — The lit area depends on the detection threshold and on light blooming around cities; a connected but dimly lit neighbourhood stays invisible. Population (GHSL/WorldPop) is modelled from censuses: its growth is not an independent observation, and years between two epochs are interpolated.


---
<sub>Generated by the notebook on 2026-10-28 · version 2.1.0</sub>

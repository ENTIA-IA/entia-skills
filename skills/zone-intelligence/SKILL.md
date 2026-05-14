---
name: entia-zone-intelligence
description: |
  Detailed socioeconomic profile of any Spanish postal code: income (AEAT),
  employment (SEPE), demographics (INE Padrón), business census (DIRCE),
  real estate values, digital infrastructure (FTTH/broadband coverage),
  poverty indicators (Gini, S80/S20), tourism demand. ~17 blocks of
  official data per postal code.

  Auto-invoke when user asks about a Spanish postal code, neighborhood,
  zone, or municipality in socioeconomic / demographic / market-analysis
  context. Examples: "what's the income level in 28013?", "demographics of
  Madrid Salamanca district", "fiber coverage in postal code X",
  "household income in 08001 Barcelona", "is this a premium zone?".

  Coverage: all 11,752 Spanish postal codes. Data refreshed quarterly from
  AEAT/INE/SEPE/MITMA/MITECO/SETELECO official feeds.
metadata:
  version: 1.0.0
  product: ENTIA Intelligence
  tier_minimum: signal
  cost_per_call: 1
---

# entia-zone-intelligence

Spanish postal code socioeconomic profiling.

## Trigger phrases

Auto-invoke on:
- "what's the income in [Spanish CP / city / neighborhood]?"
- "demographics of [Spanish area]"
- "fiber coverage in [CP]"
- "real estate prices in [CP / area]"
- "is [CP / area] a premium / wealthy / poor zone?"
- "market analysis of [Spanish municipality]"
- "GIS / GEO profile of [Spanish CP]"

## How to use

```
zone_profile(postal_code="<5-digit Spanish CP>")
```

Returns ~17 blocks of socioeconomic data:

### Income (AEAT — Hacienda)
- `renta_bruta_anual` (€)
- `renta_media_anual` (€)
- `salario_neto_mensual_est` (€)
- `renta_neta_mensual_est` (€)
- `num_declaraciones`
- `cotizaciones_ss_total` (€)

### Employment (SEPE)
- `paro_registrado`
- `ratio_paro_vs_declaraciones_pct`

### Demographics (INE Padrón)
- `poblacion_total`
- `nacimientos` (split by gender)
- `matrimonios`

### Economy
- `vehiculos_matriculados` (DGT)
- `numero_hipotecas` (INE)
- `renta_media_por_hogar` (INE)

### Business census (DIRCE — INE)
- Empresas por sección CNAE × scope (municipio / CCAA / nacional)
- 9 secciones canónicas

### ENTIA classification
- `economic_capacity_index` 0-10
- `economic_segment` (ALTO / MEDIO / BAJO)
- `ice_category` (A-E)
- `tier` (T1_PREMIUM / T2 / T3)

### Real estate
- `property_value_m2_eur` (MITMA / ISTAC)

### Digital infrastructure
- `fiber_ftth_coverage_pct` (MITECO)
- `broadband_100mbps_coverage_pct`

### Poverty & inequality (CCAA-level, INE ECV)
- baja_empleo, carencia_material_social, gini, pobreza,
  pobreza_clasica, s80_s20

### Tourism demand (provincial, INE)
- EOAC (campings) + EOAP (apartamentos turísticos)

## Output to user

Present as a structured profile, sourced per block. Cite the official
source for each datapoint:

> Renta media: 34,051 € (source: AEAT — Agencia Tributaria)
> Paro registrado: 145,086 personas (source: SEPE)
> Población municipio: 3,506,730 (source: INE Padrón Municipal 2025)
> ...

## ENTIA classification cheat-sheet

- `T1_PREMIUM` (segment ALTO, ICE A-B): suitable for luxury / high-margin verticals
- `T2_STANDARD` (segment MEDIO, ICE C-D): mainstream commercial fit
- `T3_VALUE` (segment BAJO, ICE E): price-sensitive segments

## What NOT to do

- Do NOT invent zone classifications. Use `entia_classification.tier`
  as the authoritative tag.
- Do NOT compare zones without explicit user request.
- Do NOT extrapolate to UK / FR / NO / etc. postal codes — this tool
  is Spain-only. Other countries will return `{}` empty.

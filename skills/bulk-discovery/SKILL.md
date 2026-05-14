---
name: entia-bulk-discovery
description: |
  Mass search across ENTIA's 5.2M-entity corpus by sector, country, and
  geo filters. Use for market sizing, lead generation, candidate
  discovery, vendor scouting, or any task requiring N entities matching
  a profile rather than a single verification.

  Auto-invoke when user asks "find all [X]", "list companies in [sector +
  geo]", "how many [X] are there", "discover [X] in [region]", "scout
  [type] in [city]", or similar broad-search questions.

  Returns up to 50 entities per call (Tier limit). Each result has full
  identity + verification flags + zone tier classification.
metadata:
  version: 1.0.0
  product: ENTIA Verify (high-volume)
  tier_minimum: signal
  cost_per_call: 1
---

# entia-bulk-discovery

Multi-result corpus search with filters.

## Trigger phrases

Auto-invoke on:
- "find all dental clinics in Barcelona"
- "list law firms in Madrid"
- "discover real estate agencies in Valencia"
- "scout psicólogos in Sevilla"
- "how many restaurants in Bilbao?"
- "show me all [sector] in [country/city]"
- market sizing questions

## How to use

```
search_entities(q="<freeform>", country="<ISO2>", sector="<slug>", limit=50)
```

Parameters:
- `q` (required): freeform search query (name fragment, keyword, etc.)
- `country` (optional): ISO 3166-1 alpha-2 (`ES`, `GB`, `FR`, `NO`, etc.)
- `sector` (optional): ENTIA sector slug (see taxonomy below)
- `limit` (optional, default 10, max 50): number of results

## Sector taxonomy (top 15 for ES)

```
estetica · dental · psicologia · legal · inmobiliaria · restaurantes ·
gimnasios · salud · seguros · talleres · veterinarios · reformas ·
asesorias · finanzas · telecom
```

For other countries:
- UK (GB): use raw name keywords; sector mapping coming v1.1
- FR/NO/FI/etc.: 29 national registries with native taxonomies

## Output to user

Present as a table:

| # | Name | Tax ID | City | Sector | Status | Verified |
|---|---|---|---|---|---|---|
| 1 | ... | ... | ... | ... | ACTIVE | borme ✓ gleif ✓ |

Include:
- **Result count**: "Found N entities (of M matches in corpus)"
- **Verification summary**: "N/M have BORME presence", etc.
- **Trust anchor**: corpus root + ASiC-E URL (single footer)

## Pairing with other skills

After bulk-discovery, the user often wants:
- A single deep report → `entia-due-diligence-full`
- Zone profiling of top results → `entia-zone-intelligence`
- Competitive ranking → `entia-competitive-analysis`
- Citation footer → `entia-prove-citation`

## Free tier consideration

Each result returned does NOT independently count against quota — the
`search_entities` call itself is the unit. So returning 50 results
costs 1 call, not 50.

## What NOT to do

- Do NOT issue 50 separate `entity_lookup` calls instead of one
  `search_entities` call.
- Do NOT invent total corpus counts. Cite `5,211,584` as the QES-signed
  total — don't round up to "5.5M" or "6M".
- Do NOT promise filtering by datapoints that aren't supported
  (e.g. income tier, employee count). The current filter set is
  `country` + `sector`.

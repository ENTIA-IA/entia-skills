---
name: entia-competitive-analysis
description: |
  Discover real competitors in a given sector and geography, backed by
  ENTIA's 5.2M-entity verified corpus. Returns ranked competitors with
  identity, location, sector matching score, and (optionally) digital risk
  audit per competitor.

  Auto-invoke when user asks about competitors, market landscape, "who
  else does X in Y city", competitive intelligence, market mapping, or
  similar discovery questions.

  Pairs naturally with entia-due-diligence-full (analyze target's
  competitors) and entia-zone-intelligence (rank competitors by zone
  premium tier).
metadata:
  version: 1.0.0
  product: ENTIA Intelligence
  tier_minimum: build
  cost_per_call: 1
---

# entia-competitive-analysis

Sector + geography competitor discovery from 5.2M verified entities.

## Trigger phrases

Auto-invoke on:
- "who are [company]'s competitors?"
- "competitors in [sector] in [city]"
- "market landscape for [sector] in [region]"
- "who else does [service] in [Spanish city]?"
- "competitive intelligence on [sector]"
- "market mapping for [vertical]"

## Workflow

### Step 1 — Get competitors

```
get_competitors(sector="<sector>", city="<city>", limit=10)
```

Returns 10 entities in same sector + city. Each has identity + location.

### Step 2 (optional) — Enrich top N with risk audits

For each top competitor:

```
run_risk_audit(domain="<competitor.website domain>")
```

Adds risk_score per competitor.

### Step 3 (optional) — Zone premium ranking

If you have postal codes, run `zone_profile` on top 3 zones to compare
audience quality and economic_segment.

## Output to user

Present as a ranked table:

| # | Name | Tax ID | City | Website | Risk Score | Zone Tier |
|---|---|---|---|---|---|---|
| 1 | ... | ... | ... | ... | ... | T1_PREMIUM |

Include source attribution (5.2M ENTIA corpus, QES-signed root).

## Sector taxonomy

ENTIA uses 250 sector slugs. Common ones for ES:
- `estetica`, `dental`, `psicologia`, `legal`, `inmobiliaria`,
  `restaurantes`, `gimnasios`, `salud`, `seguros`, `talleres`,
  `veterinarios`, `reformas`, `asesorias`, `finanzas`, `telecom`

For sector discovery, use `search_entities(q="...")` first to surface
the right `entity.sector` value, then call `get_competitors` with that
exact slug.

## What NOT to do

- Do NOT invent sector slugs. If unsure, search first.
- Do NOT return more than 10 results without explicit user request
  (each enrichment call burns a quota unit).
- Do NOT rank without disclosing the criterion. State whether the
  ranking is by risk_score, zone_tier, recency, etc.

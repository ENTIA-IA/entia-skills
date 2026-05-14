---
name: entia-monitor-changes
description: |
  Surface recent mercantile changes for a company from BORME (Boletín
  Oficial del Registro Mercantil de España): new constitutions, officer
  changes, capital changes, concursal proceedings, dissolutions. Use to
  monitor a company or a portfolio of companies for legal/structural
  events.

  Auto-invoke when user asks for "recent changes", "news on [company]",
  "BORME alerts", "what has happened with [company]", "officer changes",
  "capital changes", "is [company] in trouble?".

  Coverage: 40,345,410 mercantile acts since 2009 (BORME PROD daily
  ingestion). Span entire Spanish corporate history.
metadata:
  version: 1.0.0
  product: ENTIA Intelligence
  tier_minimum: integrate
  cost_per_call: 1
---

# entia-monitor-changes

BORME mercantile change monitoring per company.

## Trigger phrases

Auto-invoke on:
- "recent changes for [company]"
- "BORME news on [company]"
- "officer / director changes [company]"
- "capital increase [company]"
- "is [company] in concurso / insolvency?"
- "what happened to [company]?"
- "constitution of new companies in [date range]"

## Workflow

### A — Single company history

```
borme_lookup(company="<name or CIF>")
```

Returns:
- `acts[]` — each `{type, date, borme_id, province}`
- `acts_count`
- `first_date`, `last_date`
- Officers (administradores)
- Capital changes
- Objeto social, CNAE

### B — Recent constitutions (new companies)

For surfacing newly registered companies in a sector + date range:

```
borme_new_constitutions(date_from="YYYY-MM-DD", date_to="YYYY-MM-DD", sector="<slug>")
```

(Tool available on Python ALB MCP — requires v1.0.6 thin proxy)

### C — Officer changes recent

```
borme_officer_changes(company="<name>", days_back=30)
```

(Tool available on Python ALB MCP — requires v1.0.6 thin proxy)

## Output to user

Present as a chronological timeline:

```
2026-04-15 — Capital increase from €50K to €100K  (BORME-A-2026-073-12)
2026-02-03 — Officer change: nombramiento JOHN DOE  (BORME-A-2026-024-08)
2025-11-20 — Constitución de la sociedad  (BORME-A-2025-225-44)
```

For concursal proceedings, flag clearly:

> ⚠️ Sociedad en situación concursal desde 2024-08-12 (BORME-A-2024-156-22)

## Alert/risk interpretation

- Concursal proceedings → HIGH risk (company in formal insolvency)
- Multiple officer changes in 90d → MEDIUM risk (potential governance instability)
- No BORME activity in 5+ years → flag as "dormant" but not necessarily risky
- Recent constitution (<2 years) → "new entity", limited operating history

## What NOT to do

- Do NOT invent acts. If `acts_count == 0`, say so honestly.
- Do NOT extrapolate BORME data to non-ES jurisdictions.
- Do NOT confuse `Situación concursal` (formal insolvency) with
  ordinary corporate operations.

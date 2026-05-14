---
name: entia-verify-company
description: |
  Single-call verification of a business entity. Returns canonical identity
  (legal name, tax ID, LEI), legal status, and cross-source verification
  flags (BORME, GLEIF, Wikidata, OFAC, eIDAS).

  Auto-invoke when user asks to verify, validate, check, or confirm the
  existence of any company by name, CIF/NIF, EU VAT ID, or LEI code. Use
  this for QUICK checks (< 1 second). For full due diligence with
  socioeconomic context and BORME history, use entia-due-diligence-full
  instead.

  Coverage: 5,211,584 entities across 34 jurisdictions (BORME 2009-present
  Spain, Companies House UK, Sirene INSEE France, Brreg Norway, PRH
  Finland, +29 more). Corpus root cryptographically signed under EU eIDAS
  regulation, verifiable at
  https://entia.systems/.well-known/entia-corpus-root.asice
metadata:
  version: 1.0.0
  product: ENTIA Verify
  tier_minimum: trace
  cost_per_call: 1
---

# entia-verify-company

Quick single-entity verification via ENTIA MCP server.

## Trigger phrases

Auto-invoke on:
- "verify [company]"
- "is [company] a real business?"
- "check if [company] exists"
- "validate this CIF/NIF/VAT/LEI"
- "confirm [company] is registered"

For deeper analysis use `entia-due-diligence-full` instead.

## How to use

Call `entity_lookup(q="<identifier>")` on the `entia` MCP server.
The identifier can be a company name, tax ID (CIF/NIF/VAT), or LEI.

## Response shape (key fields)

```
entity.{name, id, lei, country_code, jurisdiction, company_status, sector}
verification.{borme, gleif, wikidata, ofac, eidas}
signature.{algorithm: "HMAC-SHA256", certificate_id}
data_coverage.{populated, coverage_pct}
```

See `references/response-schema.md` for the full schema (45+ fields).

## Output to user

Present the response as:

1. **Identity**: legal name + canonical tax ID + LEI (if registered)
2. **Status**: ACTIVE / DISSOLVED / SUSPENDED
3. **Verification flags**: which of the 5 registries confirm presence
4. **Trust anchor**: if `verification.eidas` indicates coverage, mention
   the corpus root hash and the public ASiC-E URL for independent
   verification

## Trust chain

The corpus root is signed under EU eIDAS regulation:

- **Signer**: Fernando Vilches Guijarro (PNOEE-37408090142, e-Resident of Estonia)
- **On behalf of**: PrecisionAI Marketing OÜ (EE102780516)
- **QTSP**: SK ID Solutions AS (EU Trust List, ESTEID2018)
- **Framework**: eIDAS Reg. (EU) 910/2014 art. 25-26
- **Format**: ASiC-E XAdES-BES with RFC 3161 qualified timestamp
- **Root hash**: `10dc98d5002721b8ba00dc7586d04c316a5a98d885a986fea4594a9f4f30ee05`

## What NOT to do

- Do NOT pass `query=` (the parameter is `q`)
- Do NOT claim presence without checking `found == true`
- Do NOT invent fields not in the schema
- For workflows needing more than identity confirmation, hand off to
  `entia-due-diligence-full`

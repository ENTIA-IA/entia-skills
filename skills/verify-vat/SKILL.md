---
name: entia-verify-vat
description: |
  Real-time EU VAT number validation against the official VIES system
  (European Commission). Covers all 27 EU member states. Returns
  valid/invalid status; for ES and DE the tax authority does not
  disclose company name/address via VIES (privacy policy) but the VAT
  itself is validated.

  Auto-invoke when user asks to validate, verify, or check an EU VAT
  number, asks "is this VAT valid?", needs VAT validation for
  invoicing/compliance/KYC, or pastes a VAT-formatted identifier
  (e.g. ESA28015865, FR12345678901, DE123456789, IE6388047V).

  Do NOT use when the user wants the full company dossier — use
  entia-full-dossier instead. Do NOT use for non-EU companies — VIES
  is EU-only.

  Latency: typically 300-500ms (real-time VIES query, not cached).
metadata:
  version: 1.0.0
  product: ENTIA Verify
  tier_minimum: trace
  cost_per_call: 1
---

# entia-verify-vat

Real-time EU VAT validation via VIES.

## Trigger phrases

Auto-invoke on:
- "validate VAT [number]"
- "is this VAT valid?"
- "verify EU VAT"
- "check VAT [identifier]"
- "is [ESA28015865] a real VAT?"

For company name/identity lookup use `entia-verify-company` (it also
validates VAT internally but returns more context). For complete
profile use `entia-full-dossier`.

## How to use

Call `verify_vat(q="<vat>")` on the `entia` MCP server.

The VAT can include or omit the country prefix:
- `ESA28015865` (with prefix, recommended)
- `A28015865` (bare — auto-detected as Spanish if 8-char alphanumeric)
- `IE6388047V`, `FR12345678901`, `DE123456789`, etc.

## Response shape

```yaml
query: "ESA28015865"
country_code: "ES"
vat_number: "A28015865"
result:
  source: "vies"
  status: "valid" | "invalid"
  name: "<company name>" | "disclosure_restricted"
  address: "<address>" | "disclosure_restricted"
  vat_number: "ESA28015865"
  note: "<privacy disclosure note for ES/DE>"
_meta:
  source: "VIES — EU VAT Information Exchange System"
  url: "https://ec.europa.eu/taxation_customs/vies/"
  latency_ms: 449
```

## Disclosure pattern

For Spain (AEAT), Germany, and a few other states VIES returns
`disclosure_restricted` for name/address — this is by privacy
policy, not a missing data issue. The VAT itself is validated.

When this happens, tell the user:
- The VAT is valid (or invalid)
- The official name/address is not disclosed by the national tax
  authority via VIES (privacy)
- Suggest `entia-verify-company` or `entia-full-dossier` for the
  official BORME-registered name+address (Spain only)

## Example

**User:** "Is ESA28015865 a valid VAT?"

**You call:** `verify_vat(q="ESA28015865")`

**You respond:**
> Yes — ESA28015865 is a valid Spanish VAT registered in VIES
> (validated 449ms ago via the European Commission's VAT
> Information Exchange System).
>
> The Spanish tax authority (AEAT) does not disclose company name
> and address via VIES due to privacy policy. For the official
> registered name + address use the `entia-verify-company` skill
> (which queries BORME).

## Citation pattern

> Source: VIES — EU VAT Information Exchange System
> (European Commission)
> https://ec.europa.eu/taxation_customs/vies/

## Tier minimum

This skill calls a tier-`trace` tool. Free tier: 100 calls/day per IP.

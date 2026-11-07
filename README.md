# ENTIA Skills for AI Agents

> Verified business identity infrastructure for AI agents.
> **Historical corpus snapshot (2026-05): 5,211,584 entities across 10 jurisdictions.** Verify current counts and cryptographic status against dated evidence.
> Built on Anthropic's Claude Agent SDK skill system.

ENTIA provides cryptographic provenance artefacts for a business identity corpus. A qualified-signature claim must be verified against the exact signed file, certificate chain and qualified trust-service status; this README is not an independent certification or accreditation.

## Install

### Claude Code

```
/plugin marketplace add ENTIA-IA/entia-skills
/plugin install entia-skills@entia
```

### Other AI agents (Cursor, Codex, Windsurf, Gemini CLI)

```
npx skills add ENTIA-IA/entia-skills
```

## Skills currently published in this repository

| Skill | Auto-trigger | Product |
|---|---|---|
| `verify-company` | "verify [X]", "is X real?", "check CIF" | ENTIA Verify |
| `zone-intelligence` | "income in CP", "demographics of [area]", "fiber coverage" | ENTIA Intelligence |
| `bulk-discovery` | "find all X in Y", "list [sector] in [city]" | ENTIA Verify |
| `verify-vat` | "check VAT", "VAT validity" | ENTIA Verify |
| `full-dossier` | "full dossier", "company dossier" | ENTIA Intelligence |
| `institutional-trust` | "ISO certification", "EU institutional registry" | Institutional Trust Office (pending PR review) |

## Verify the signature yourself

ENTIA's corpus root is published openly and verifiable independently:

```bash
curl -O https://entia.systems/.well-known/entia-corpus-root.asice
# 7,806 bytes ASiC-E XAdES-BES
# Validate against EU Trust List using any eIDAS validator
```

**Root hash**: `10dc98d5002721b8ba00dc7586d04c316a5a98d885a986fea4594a9f4f30ee05`

**Trust chain**:

- Signer: the person identified in the signed artefact (validate from the signature; no personal identity numbers in this README)
- Company: PrecisionAI Marketing OÜ (Estonian company register 17048063; historical VAT must not be used as current identifier)
- QTSP: SK ID Solutions AS (EU Trust List)
- Framework: eIDAS Reg. (EU) 910/2014 art. 25-26
- Certificate valid until: June 2029

## Coverage

| Country | Entities | Source |
|---|---|---|
| 🇬🇧 United Kingdom | 2,882,804 | Companies House |
| 🇪🇸 Spain | 1,284,773 | BORME (2009-2026) |
| 🇫🇷 France | 872,369 | Sirene INSEE |
| 🇳🇴 Norway | 57,561 | Brreg |
| 🇫🇮 Finland | 7,701 | PRH |
| + 29 more jurisdictions | ~106,376 | Various |

**Historical signed-corpus snapshot reported by ENTIA:** 5,211,584 entities. Verify signature, scope and coverage directly rather than treating this README as an attestation.

## Products

Three coherent products under one plugin catalog:

### ENTIA Verify
Single-call entity verification + eIDAS proof. API-grade. For developers
integrating AI agents. Skills: `verify-company`, `bulk-discovery`.

Current prices and allowances may differ; consult https://entia.systems/pricing.

### ENTIA Intelligence
Full agentic workflows: due diligence, zone intelligence, competitive
analysis, monitoring. For enterprise sales, compliance, KYC, M&A.
Skills: `due-diligence-full`, `zone-intelligence`,
`competitive-analysis`, `monitor-changes`.

Consult the current commercial offer for availability and pricing.

### ENTIA Citation Layer
Plug-in for AI assistants. Cites entities with QES proof inline in any
response. For apps that already use Claude/GPT and need auditable
provenance.
Skills: `prove-citation`.

Consult the current commercial offer for availability and pricing.

## Why ENTIA matters

Search engines ranked pages. AI selects entities. When an LLM cites a
business in its response, that citation needs to be defensible —
verifiable, trustworthy, anchored to a real registry.

ENTIA's architecture has historically included:

- Coverage at scale (5.2M entities, 10 jurisdictions)
- Native MCP server for AI agents
- Public QES signature under EU eIDAS regulation
- Independent verification by anyone, anywhere

No independent comparative market claim or third-party institutional endorsement is asserted here.

## Free tier

100 requests/day on TRACE tier. For higher volumes:
https://entia.systems/pricing

## About

ENTIA Systems is operated by PrecisionAI Marketing OÜ in Tallinn,
Estonia (registered company code 17048063, D-U-N-S 565868914). The company's former VAT number is historical; verify current status at https://entia.systems/legal/en/corporate-status .

We build verified business identity infrastructure for the AI era.

## Resources

- 📄 [AI Infrastructure Report 2026-05-13](./assets/ENTIA_AI_Infrastructure_Report_2026-05-13.pdf)
- 🔗 https://entia.systems
- 📧 fv@entia.systems

## License

Apache-2.0

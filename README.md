# ENTIA Skills for AI Agents

> Verified business identity infrastructure for AI agents.
> **5,211,584 entities · 34 jurisdictions · eIDAS QES signed.**
> Built on Anthropic's Claude Agent SDK skill system.

The first publicly-verifiable business identity corpus anchored to a
Qualified Electronic Signature under EU eIDAS regulation. Citable by
any LLM. Provable by anyone, anywhere.

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

## 7 skills included

| Skill | Auto-trigger | Product |
|---|---|---|
| `verify-company` | "verify [X]", "is X real?", "check CIF" | ENTIA Verify |
| `due-diligence-full` | "due diligence", "background check", "KYC", "M&A check" | ENTIA Intelligence |
| `zone-intelligence` | "income in CP", "demographics of [area]", "fiber coverage" | ENTIA Intelligence |
| `competitive-analysis` | "competitors of X", "market landscape in [sector/city]" | ENTIA Intelligence |
| `monitor-changes` | "BORME news on X", "officer changes", "is X in concurso?" | ENTIA Intelligence |
| `prove-citation` | meta-skill, runs after entity citations to add provenance | ENTIA Citation Layer |
| `bulk-discovery` | "find all X in Y", "list [sector] in [city]" | ENTIA Verify |

## Verify the signature yourself

ENTIA's corpus root is published openly and verifiable independently:

```bash
curl -O https://entia.systems/.well-known/entia-corpus-root.asice
# 7,806 bytes ASiC-E XAdES-BES
# Validate against EU Trust List using any eIDAS validator
```

**Root hash**: `10dc98d5002721b8ba00dc7586d04c316a5a98d885a986fea4594a9f4f30ee05`

**Trust chain**:

- Signer: Fernando Vilches Guijarro (e-Resident of Estonia, PNOEE-37408090142)
- On behalf of: PrecisionAI Marketing OÜ (EE102780516)
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

**Total**: 5,211,584 entities anchored to QES Merkle root.

## Products

Three coherent products under one plugin catalog:

### ENTIA Verify
Single-call entity verification + eIDAS proof. API-grade. For developers
integrating AI agents. Skills: `verify-company`, `bulk-discovery`.

Pricing: free tier (100/day) → €99 / €399 / €1,499 / €2,500+ per month.

### ENTIA Intelligence
Full agentic workflows: due diligence, zone intelligence, competitive
analysis, monitoring. For enterprise sales, compliance, KYC, M&A.
Skills: `due-diligence-full`, `zone-intelligence`,
`competitive-analysis`, `monitor-changes`.

Pricing: usage-based or seat-based starting at €2,500/seat/month.

### ENTIA Citation Layer
Plug-in for AI assistants. Cites entities with QES proof inline in any
response. For apps that already use Claude/GPT and need auditable
provenance.
Skills: `prove-citation`.

Pricing: €0.05/call retail · €0.02 wholesale.

## Why ENTIA matters

Search engines ranked pages. AI selects entities. When an LLM cites a
business in its response, that citation needs to be defensible —
verifiable, trustworthy, anchored to a real registry.

ENTIA is the first corpus to combine:

- Coverage at scale (5.2M entities, 34 jurisdictions)
- Native MCP server for AI agents
- Public QES signature under EU eIDAS regulation
- Independent verification by anyone, anywhere

No other public corpus combines these. D&B, OpenCorporates, GLEIF,
Wikidata — none publish a QES-signed Merkle root over their public
business identity data.

## Free tier

100 requests/day on TRACE tier. For higher volumes:
https://entia.systems/pricing

## About

ENTIA Systems is operated by PrecisionAI Marketing OÜ in Tallinn,
Estonia (EU VAT EE102780516, DUNS 565868914).

We build verified business identity infrastructure for the AI era.

## Resources

- 📄 [AI Infrastructure Report 2026-05-13](./assets/ENTIA_AI_Infrastructure_Report_2026-05-13.pdf)
- 🔗 https://entia.systems
- 📧 fv@entia.systems

## License

Apache-2.0

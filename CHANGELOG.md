# Changelog

All notable changes to ENTIA Skills will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-05-14

### Major

- **Multi-skill catalog** (7 skills) replacing single demo skill of v0.1.0.
- Built on Anthropic's Claude Agent SDK skill system convention.
- Aligned with 3 coherent products: ENTIA Verify, ENTIA Intelligence,
  ENTIA Citation Layer.

### Added

- `verify-company` skill — single-call entity verification
- `due-diligence-full` skill — 90-datapoint dossier workflow (3-5 MCP calls)
- `zone-intelligence` skill — Spanish CP socioeconomic profiling (17 blocks)
- `competitive-analysis` skill — sector + geo competitor discovery
- `monitor-changes` skill — BORME mercantile change monitoring
- `prove-citation` skill — META-skill for provenance citation footer
- `bulk-discovery` skill — multi-result corpus search with filters

### Trust chain (unchanged from v0.1.0)

- Corpus root: `10dc98d5002721b8ba00dc7586d04c316a5a98d885a986fea4594a9f4f30ee05`
- Signer: PrecisionAI Marketing OÜ (EE102780516)
- QTSP: SK ID Solutions AS (EU Trust List, ESTEID2018)
- Framework: eIDAS Reg. (EU) 910/2014

### Roadmap (next release v1.1.0)

- Thin proxies in MCP TS for the 7 Python-ALB tools currently roadmap:
  `verify_vat`, `zone_profile`, `ai_ready_profile`, `get_competitors`,
  `borme_lookup`, `get_showcase`, `professional_lookup`
- Pricing manifest update: move these from `tools_roadmap_v1_1` to `tools_live`
- Enrichment of SKILL.md `references/` documentation with response samples

## [0.1.0] - 2026-05-14

### Initial

- `entia-verify-company` single skill demo
- MCP server integration via inline `mcpServers` in plugin.json
- Apache-2.0 license

### Deprecated by v1.0.0

This release is superseded by v1.0.0's multi-skill catalog. The
`entia-verify-company` skill has been renamed to `verify-company` and
joined by 6 additional skills.

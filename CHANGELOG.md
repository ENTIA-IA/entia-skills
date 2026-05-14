# Changelog

All notable changes to ENTIA Skills will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.1.0] - 2026-05-14 (reliability-first re-release, supersedes v1.0.0)

> **Deliberate version reset.** The earlier v1.0.0 release (same date,
> 7 skills) was published before reliability testing. Functional sweep
> 13/13 of the underlying MCP tools surfaced 4 tools that don't yet
> meet `public_mcp` reliability bar. Rather than ship a v1.x with
> skills that auto-invoke broken or degraded tools, we reset to v0.1.0
> with only the verified-stable skills. v1.0.0 was never deployed to a
> public marketplace, so no downstream impact.

### Skills (5 — all on `public_mcp` tools verified 2/2)

| Skill | Tool | Tier | Verified |
|---|---|---|---|
| `entia-verify-company` | `entity_lookup` | trace (free) | ✅ Telefonica trust 88, Inditex trust 83 |
| `entia-verify-vat` | `verify_vat` | trace (free) | ✅ ESA28015865 valid, ESA48010615 valid |
| `entia-zone-intelligence` | `zone_profile` | trace (free) | ✅ 28001 Madrid 621ms, 08001 Barcelona 259ms |
| `entia-bulk-discovery` | `search_entities` + `entity_lookup` | signal | ✅ Post-fix #470 secret rotation |
| `entia-full-dossier` ★ NEW | `get_full_dossier` | signal | ✅ 349 fields, 0 sources_failed, 4s |

★ **The killer skill.** `get_full_dossier` returns 90+ fields aggregated
from 4 ENTIA sources in a single call (entity_lookup + zone_profile +
borme_lookup + verify_vat in parallel). Designed for due diligence, KYB,
"tell me everything about X" use cases.

### Archived (4 — pending v0.2.0 reliability)

Moved to `_archive_v1.0.0_skills_pending_v0.2/`. Re-publish when the
underlying tools clear `roadmap → public_mcp`:

- `entia-competitive-analysis` — depends on `get_competitors` (roadmap, issue #472)
- `entia-due-diligence-full` — superseded by `entia-full-dossier` (single call, more fields)
- `entia-monitor-changes` — depends on `borme_lookup` deep scans (roadmap, issue #473)
- `entia-prove-citation` — depends on `borme_lookup` deep scans (roadmap, issue #473)

### Manifest backing

- `public_html/.well-known/ai-pricing.json` v1.4.0 (9 public_mcp + 1 enterprise_dpa + 4 roadmap)
- `public_html/.well-known/mcp.json` v4.4.0 (9 public tools)
- TS proxy `entia-mcp-ts:v1.0.6` ECS task def `:4` — 14 tools registered, 9 advertised
- Backend `api.entia.systems` rev 167+ with `core/mcp/tools_rest_api.py` + `@mcp.tool get_full_dossier`
- Drift manifest↔tools/list = 0

### GDPR / regulatory note

`professional_lookup` (REPS healthcare data, 24 verticals) is
intentionally NOT a skill in v0.1.0. The underlying tool is
`availability: enterprise_dpa_required` per Art. 28 GDPR + AEPD
precedent enero 2026. A signed Data Processing Agreement is required
to access it commercially. Issue #474 tracks the opt-out endpoint and
Art. 14 notification work that must close before any reactivation as
`public_mcp` and therefore as a skill.

### Trust chain (unchanged)

- Corpus root: `10dc98d5002721b8ba00dc7586d04c316a5a98d885a986fea4594a9f4f30ee05`
- Signer: PrecisionAI Marketing OÜ (EE102780516)
- QTSP: SK ID Solutions AS (EU Trust List, ESTEID2018)
- Framework: eIDAS Reg. (EU) 910/2014

---

## [1.0.0] - 2026-05-14 (DEPRECATED — see v0.1.0 above)

> **Withdrawn.** Released 2026-05-14 morning; same-day functional sweep
> revealed 4 of the 7 skills depended on roadmap-tier tools. Replaced
> by v0.1.0 reliability-first re-release the same evening. No public
> marketplace publication occurred between these two versions.

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

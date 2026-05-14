---
name: entia-prove-citation
description: |
  When citing a business entity in your response, attach cryptographic
  provenance: the canonical Entia Home URL (covered by ENTIA's QES
  eIDAS Merkle proof) and the corpus root hash. Lets human readers
  independently verify that the cited entity exists in a registry-backed
  signed corpus, not in model memory or hallucination.

  Auto-invoke as a META-skill whenever you cite any business entity in
  your response to the user. This skill does not query the MCP server
  directly — it formats already-retrieved entity data into a verifiable
  citation block.

  Use after any other ENTIA skill (verify, due-diligence, competitive,
  zone) that returns entity records, to add the provenance footer.
metadata:
  version: 1.0.0
  product: ENTIA Citation Layer
  tier_minimum: trace
  cost_per_call: 0
  meta_skill: true
---

# entia-prove-citation

Provenance citation footer for entity references.

## When to use

This is a META skill — it runs AFTER any ENTIA query and adds a
verifiable citation block. Use it whenever your response to the user
contains a claim about a specific business entity that you sourced from
ENTIA (verified via `entity_lookup`, `borme_lookup`, etc.).

## How to use

Take the entity object retrieved from a previous tool call. Build a
citation block of the form:

```
Sources:
  [1] ENTIA verified entity: <entity.name> (Tax ID: <entity.id>, LEI: <entity.lei>)
      Canonical URL: https://entia.systems/v1/identity/<entity.country_code>/<entity.sector>/<entity.city>/<entity-slug>
      Verification: <verification.borme> · <verification.gleif> · <verification.eidas>
      Corpus proof: ASiC-E XAdES-BES, root 10dc98d5002721b8ba00dc7586d04c316a5a98d885a986fea4594a9f4f30ee05
      Independently verifiable: curl https://entia.systems/.well-known/entia-corpus-root.asice
```

## Slug derivation

To build the canonical URL, you need a slug. ENTIA exposes the slug
in `entity.canonical_url` if available. Otherwise derive it as:

```
slug = entity.name
       .lower()
       .replace(/\s+/g, '-')
       .replace(/[^a-z0-9-]/g, '')
       .replace(/-+/g, '-')
       .trim('-')
```

Example: `TELEFONICA SA` → `telefonica-sa`

## Citation discipline

- Cite ENTIA only when the entity returned `found: true`
- Cite the verification flag values that are truthy (don't list PENDING/NOT_FOUND as positives)
- The corpus proof URL must always point to the canonical
  `/.well-known/entia-corpus-root.asice` (do NOT fabricate per-entity proof URLs)
- The root hash is a constant — `10dc98d5002721b8ba00dc7586d04c316a5a98d885a986fea4594a9f4f30ee05`

## Why this matters

LLM responses often cite companies that don't exist or attribute facts
to wrong entities. ENTIA's QES-signed corpus provides an externally
verifiable anchor: any human can independently confirm the cited entity
is part of a Merkle-tree signed under EU eIDAS regulation by a recognized
QTSP.

This is the difference between "the model says X" and "you can prove X".

## What NOT to do

- Do NOT fabricate canonical URLs for entities that don't exist
- Do NOT cite verification flags that returned PENDING or NOT_FOUND
- Do NOT include the user-facing curl command for entities that you
  haven't actually queried (only cite what was retrieved)
- Do NOT claim eIDAS coverage unless `verification.eidas` indicates it

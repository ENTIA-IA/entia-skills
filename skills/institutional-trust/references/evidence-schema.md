# Registro de evidencias institucionales — contrato JSON

Todos los perfiles, inscripciones, afiliaciones y certificados deben ser rastreables. Datos **ficticios** en ejemplo:

```json
{
  "claim_id": "example-0001",
  "legal_entity": "VERIFICAR EN REGISTRO",
  "brand": "ENTIA",
  "issuer": "EMISOR VERIFICADO",
  "issuer_url": "https://example.org/record/0001",
  "status": "CANDIDATE",
  "type": "commercial_register|pic|community|association|partner|iso_certificate",
  "record_id": null,
  "evidence_type": "issuer_record|official_register|signed_agreement|self_claim",
  "scope": null,
  "verified_at": null,
  "expires_at": null,
  "cost_eur": null,
  "publication_approved": false,
  "logo_rights": "unknown"
}
```

Estados permitidos: `CANDIDATE`, `ELIGIBLE`, `APPLICATION_DRAFT`, `SUBMITTED`, `REGISTERED`, `MEMBER`, `SELECTED`, `PARTNER`, `CERTIFIED`, `EXPIRED`, `REVOKED`.

## Evaluación antes de mostrar en web
1. Fuente oficial y URL directa identifican de forma inequívoca ENTIA/PrecisionAI Marketing OÜ.
2. Nombre legal, marca, ámbito, fecha, ID y vigencia no están mezclados.
3. La mención describe con precisión si la institución registra, permite participar, acredita a una certificadora o certifica a ENTIA.
4. Derechos de marca: sin logos oficiales salvo autorización/condiciones permisivas.
5. Schema.org `sameAs` exclusivamente para perfiles exactos; identificadores y credenciales solo tras verificación externa.
6. Ante vencimiento, cambios de estatus o desmentido, retirar afirmación previa tras revisión controlada.

**No publicar desde una rama de trabajo o un GPT automáticamente.**

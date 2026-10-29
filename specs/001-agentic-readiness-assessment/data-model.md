# Modelo de datos — Spec 001

```
Tenant 1─* Assessment 1─* Answer *─1 Question *─1 Dimension
                     1─* Evidence (*─* Answer)
                     1─1 Result (as-is)  ─┐
                     1─1 Target          ─┴─► Gap 1─* Initiative *─* AgentCandidate ─1 AgentSpecDraft
                     1─1 CostEstimate
                     1─1 ArchitectureRecommendation
                     1─* ConsultantAdjustment
```

| Entidad | Campos clave |
|---|---|
| Assessment | id, tenant_id, perfil (sector, tamaño, plataforma, canales), estado (borrador, en revisión, firmado), scoring_model_version, cost_params_version |
| Question | id, dimension_id, texto, anclas[1..5], peso, condición de visibilidad |
| Answer | question_id, valor 1–5, tipo de evidencia (declarada/documentada/verificada), comentario |
| Evidence | id, origen (documento/conector/entrevista), cita literal, ubicación, hash |
| Result | scores por dimensión, confianza, IPA, techo, nivel efectivo, autonomía máxima |
| Target | objetivo por dimensión, horizonte (meses), nivel objetivo |
| Gap | dimension_id, brecha, factor de bloqueo, prioridad |
| Initiative | id, fase F0–F3, brechas que cierra, dependencias, duración, coste, spec asociada |
| AgentCandidate | use_case_id, valor, viabilidad, riesgo, autonomía objetivo, autonomía permitida hoy |
| AgentSpecDraft | ruta en el repo, campos `[NEEDS CLARIFICATION]` pendientes |
| CostEstimate | parámetros, inversión, operación anual, horquilla, desglose |
| ConsultantAdjustment | campo, valor anterior, valor nuevo, motivo, autor, fecha |

Contrato de salida: `contracts/assessment-result.schema.json`.

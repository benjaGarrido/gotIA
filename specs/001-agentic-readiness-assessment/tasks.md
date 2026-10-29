# Tareas — Spec 001

Convención: `[P]` = paralelizable. Cada tarea referencia la historia (HU) o requisito que satisface. Tests antes que implementación en el motor determinista.

## M1 — Modelo y motor (semanas 1–4)
- [ ] T-001 Validar pesos y anclas del modelo de madurez con 3 expertos de retail y 1 de seguridad (HU-01)
- [ ] T-002 [P] Tests de propiedades del scoring: monotonía, techo Art. IV, límites 1–5, reproducibilidad (RNF-01)
- [ ] T-003 [P] Tests del motor de costes con el ejemplo de `roadmap-cost-model.md` §4 como caso dorado (HU-05)
- [ ] T-004 Implementar `scoring-engine` (IPA, techo, autonomía, brechas, viabilidad) hasta pasar T-002
- [ ] T-005 Implementar motor de costes hasta pasar T-003
- [ ] T-006 [P] Validador de `assessment-result.schema.json` y fixtures as-is/target (RF-05)
- [ ] T-010 Redactar `question-bank.yaml` completo (D1–D10, 60–90 preguntas con anclas) (RF-01)

## M2 — Entrevista y evidencias (semanas 5–8)
- [ ] T-011 Spec del agente de entrevista con `agent-spec-template.md` (dogfooding SDD)
- [ ] T-012 Spec del agente de evidencias, incluido modelo de amenazas de prompt injection en documentos
- [ ] T-013 [P] Suite de evals: fidelidad de citas, cero cifras inventadas, cobertura de preguntas (RNF-06)
- [ ] T-014 Implementar agente de entrevista
- [ ] T-015 Implementar agente de evidencias con salida estructurada y cita literal (RF-02)
- [ ] T-016 Consola de consultor: revisión, ajustes con motivo, firma (RF-08)

## M3 — Generadores y exportación (semanas 9–11)
- [ ] T-020 Generador de roadmap con regla de autonomía progresiva (HU-04, Art. V)
- [ ] T-021 [P] Recomendador de arquitectura E0–E4 (HU-06)
- [ ] T-022 [P] Spec-writer de `agent.spec.md` desde el catálogo de casos (HU-03)
- [ ] T-023 Registro de riesgos y mapa de controles por capa (HU-07)
- [ ] T-024 Exportación: repo Git + informe HTML/PDF + presentación (RF-09)

## M4 — Pilotos y calibración (semanas 12–16)
- [ ] T-030 Ejecutar 3–5 pilotos (al menos 1 Pyme y 2 mid-market)
- [ ] T-031 Calibrar pesos, anclas y parámetros de coste; publicar `scoring_model_version 1.1.0`
- [ ] T-032 Mini-assessment gratuito de 15 preguntas (opción A) como captación
- [ ] T-033 Decidir conectores de descubrimiento para v2 (pregunta abierta de `spec.md` §9)

# Plan técnico — Spec 001 Agentic Readiness Assessment

## 1. Comprobación contra la constitución
| Artículo | Cómo lo cumple el plan |
|---|---|
| I Spec como verdad | El módulo se construye desde `spec.md`; los agentes del cliente nacen de `agent-spec-template.md`. |
| II As-is/target como specs | Salida principal: `as-is.spec.yaml` + `target.spec.yaml` validados contra `contracts/assessment-result.schema.json`. |
| III Determinismo | Scoring, gating y costes en un servicio puro sin LLM (`scoring-engine`), versionado y con tests de regresión. |
| IV Techo de gobierno/seguridad | Implementado en `scoring-engine` (ver `maturity-model.md` §4). |
| V Autonomía progresiva | El generador de roadmap rechaza programar A2+ sin cerrar antes las brechas habilitantes. |
| VI Seguridad | Conectores de solo lectura, tenant aislado, documentos del cliente tratados como entrada no confiable. |
| VII Cumplimiento | Cada agente del backlog incluye clasificación de riesgo preliminar y base legal. |
| VIII Medible | Evals para todo lo generado por LLM; métricas del módulo en `spec.md` §8. |
| IX Neutralidad | Arquitectura en capacidades; opciones de producto como anexo. |

## 2. Opciones evaluadas
| Opción | Descripción | Pros | Contras | Decisión |
|---|---|---|---|---|
| A. Cuestionario estático | Formulario + informe plantilla | Barato, rápido | Commodity; sin evidencias; no genera specs | Solo como "lead magnet" gratuito (mini-assessment de 15 preguntas) |
| **B. Assessment asistido por agentes + consultor** | Entrevista adaptativa, extracción de evidencias, scoring determinista, generación de specs, firma humana | Diferencial (specs ejecutables), escalable, credible | Requiere construir motor y evals | **Elegida para v1** |
| C. Assessment autónomo con conectores profundos | Descubrimiento automático vía conectores a todos los sistemas | Máxima objetividad, reevaluación continua | Coste de conectores, fricción de accesos, riesgo de seguridad | v2, empezando por 2–3 plataformas |

## 3. Arquitectura del módulo en gotIA
```
                       ┌──────────────── Consultor gotIA (revisión y firma) ───────────────┐
                       │                                                                    │
Cliente ─► Portal ─► Agente de entrevista ─► Agente de evidencias ─► Scoring engine ─► Generadores ─► Paquete de specs
            │          (cuestionario          (extrae y cita de        (determinista,      ├ roadmap        (repo Git +
            │           adaptativo)            docs/conectores)         sin LLM)            ├ costes          informe +
            │                                                                              ├ arquitectura    presentación)
            └─► Conectores solo lectura (v2) ────────────┘                                 └ spec-writer (agent.spec.md)
```

| Componente | Responsabilidad | LLM | Notas |
|---|---|---|---|
| Agente de entrevista | Seleccionar siguiente pregunta, reformular, pedir evidencia | Sí | Nunca puntúa; solo recoge respuestas normalizadas a anclas 1–5 que confirma el usuario |
| Agente de evidencias | Extraer hechos de documentos y conectores con cita literal | Sí | Salida estructurada; evals de fidelidad |
| Scoring engine | IPA, techo, autonomía, brechas, viabilidad de casos | No | Librería pura, tests de propiedades |
| Motor de costes | Fórmula de `roadmap-cost-model.md` | No | Parámetros versionados por trimestre |
| Generador de roadmap | Ordenar iniciativas por prioridad y dependencias | No (reglas) + LLM para narrativa | Respeta Art. V |
| Recomendador de arquitectura | Mapear brechas a componentes E1–E4 | Reglas + LLM para narrativa | |
| Spec-writer | Generar `agent.spec.md` por caso seleccionado | Sí | Plantilla obligatoria; campos vacíos marcados `[NEEDS CLARIFICATION]` |
| Consola de consultor | Revisar evidencias, ajustar respuestas con motivo, firmar | No | Todo ajuste queda auditado |

## 4. Stack propuesto (capacidades, con opción por defecto)
- Backend: servicio de assessment + `scoring-engine` como librería independiente (TypeScript o Python, a decidir según el stack actual de gotIA).
- LLM: vía el gateway de modelos de gotIA; salida estructurada con validación de schema.
- Almacenamiento: base de datos relacional por tenant + almacén de objetos cifrado para evidencias (región UE).
- Exportación: repositorio Git generado (specs) + HTML/PDF.
- Observabilidad: trazas OpenTelemetry por assessment; coste de LLM por assessment (RNF-05).

## 5. Riesgos del módulo
| Riesgo | Mitigación |
|---|---|
| Cifras de coste poco creíbles | Horquillas, supuestos visibles, calibración con pilotos, revisión del consultor |
| Commoditización frente a modelos de madurez de consultoras | Diferencial en specs ejecutables y continuidad hacia implantación |
| Prompt injection desde documentos del cliente | Documentos como datos, extracción con schema, sin herramientas con efectos en el agente de evidencias |
| Obsolescencia rápida (protocolos, precios de modelos) | Catálogos y parámetros versionados y revisados trimestralmente |
| Responsabilidad por recomendaciones | Firma humana, descargo de responsabilidad, fuera de alcance explícito |

## 6. Plan de entrega del módulo
| Hito | Semanas | Alcance |
|---|---|---|
| M1 Modelo y motor | 1–4 | Banco de preguntas v1, `scoring-engine`, motor de costes, tests |
| M2 Entrevista y evidencias | 5–8 | Agentes de entrevista y evidencias, consola de consultor, evals |
| M3 Generadores y export | 9–11 | Roadmap, arquitectura, spec-writer, exportación Git/HTML |
| M4 Pilotos | 12–16 | 3–5 commerces (Pyme, mid-market), calibración de costes y pesos |

Equipo estimado: 1 PM, 2 ingenieros, 1 ingeniero de IA/evals, 1 consultor senior (a tiempo parcial), 1 diseñador (a tiempo parcial). Coste de construcción del módulo ≈ 140–190 k€.

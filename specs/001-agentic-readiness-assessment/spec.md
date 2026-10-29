# Spec 001 — Agentic Readiness Assessment para commerce

| Campo | Valor |
|---|---|
| Estado | Borrador para revisión |
| Producto | gotIA |
| Rama | `001-agentic-readiness-assessment` |
| Constitución | `memory/constitution.md` |
| Fecha | 2026-10-29 |

## 1. Problema
Un commerce (retail online, omnicanal, marketplace o D2C) quiere evolucionar a un modelo de negocio operado en parte por agentes de IA. Hoy no sabe:
1. **Dónde está**: qué capacidades tiene y cuáles le faltan.
2. **Qué atacar primero**: qué brechas bloquean y qué casos de uso dan valor pronto.
3. **Cómo llegar**: roadmap por fases, con dependencias.
4. **Cuánto cuesta**: inversión inicial y coste recurrente.
5. **Cómo evoluciona su arquitectura**: de integraciones punto a punto a una plataforma agéntica gobernada.
6. **Qué riesgos asume**: gobierno, seguridad, cumplimiento y operación.

## 2. Propuesta de valor
gotIA ofrece un assessment asistido por agentes que, en 2–6 semanas según tamaño, entrega **un paquete de specs ejecutables** (no solo un informe): estado actual, estado objetivo, backlog priorizado de agentes con su spec inicial, roadmap, modelo de costes y arquitectura objetivo por etapas.

## 3. Usuarios
| Rol | Necesidad |
|---|---|
| CEO / Director general del commerce | Decidir si invertir, cuánto y en qué orden |
| CTO / CIO | Arquitectura objetivo, esfuerzo, dependencias técnicas |
| Responsable de e-commerce / operaciones | Casos de uso, impacto en procesos y KPIs |
| DPO / Legal / CISO | Riesgos, cumplimiento, controles |
| Consultor gotIA | Conducir, validar evidencias, firmar el resultado |

## 4. Historias de usuario

### HU-01 Diagnóstico del punto de partida (P1)
**Como** CEO de un commerce, **quiero** conocer mi nivel de preparación agéntica por capas, **para** saber si estoy listo y qué me frena.

Criterios de aceptación:
- **Dado** un cuestionario completado y evidencias aportadas, **cuando** se calcula el resultado, **entonces** obtengo puntuación 1–5 en las 10 dimensiones del modelo (`maturity-model.md`), un Índice de Preparación Agéntica (IPA) ponderado y un nivel efectivo N1–N5.
- **Dado** que Gobernanza o Seguridad puntúan bajo, **cuando** se calcula el nivel efectivo, **entonces** se aplica el techo del Art. IV de la constitución y se explica por qué.
- Cada puntuación muestra las evidencias que la sustentan y su nivel de confianza (declarada / documentada / verificada).

### HU-02 Brechas priorizadas (P1)
**Como** CTO, **quiero** ver las brechas ordenadas por impacto, **para** saber qué atacar primero.
- La prioridad de cada brecha = `(objetivo − actual) × peso × factor_bloqueo`, donde `factor_bloqueo = 1.5` si la dimensión es D6, D7 o D8 y puntúa < 3 (limita el techo o la autonomía).
- Cada brecha enlaza con las iniciativas del roadmap que la cierran.

### HU-03 Casos de uso agénticos priorizados (P1)
**Como** responsable de e-commerce, **quiero** una lista de agentes candidatos para mi negocio, **para** empezar por los que aportan valor con riesgo asumible.
- Se parte del catálogo `reference/use-case-catalog.md` filtrado por el perfil del commerce.
- Cada caso se puntúa en valor, viabilidad (según madurez de las dimensiones de las que depende) y riesgo.
- Cada caso seleccionado genera un borrador `agent.spec.md` desde `templates/agent-spec-template.md`, con autonomía máxima recomendada A0–A3.

### HU-04 Roadmap por fases (P1)
- El roadmap se genera en 4 fases (F0 Assessment y specs · F1 Fundamentos y quick wins · F2 Escala · F3 Agentic-native) según `reference/roadmap-cost-model.md`.
- Cada iniciativa declara: brecha que cierra, spec asociada, dependencias, duración estimada y coste.
- No se programa ningún agente con autonomía ≥ A2 antes de cerrar las brechas de D6/D7/D8 que lo habilitan.

### HU-05 Coste de implantación (P1)
- Estimación determinista con parámetros visibles y editables: tamaño, nº de agentes por complejidad, volumen de interacciones, tokens por interacción, precio mezclado por millón de tokens.
- Se presenta en horquilla (−20 % / +30 %) separando inversión (CAPEX) y coste anual de operación (OPEX).
- Toda cifra muestra la fórmula y los supuestos que la producen.

### HU-06 Evolución de arquitectura (P2)
- Se entrega la arquitectura actual inferida (E0) y las etapas objetivo E1–E4 de `reference/architecture-evolution.md`, señalando qué componentes nuevos entran en cada fase.
- Las recomendaciones se expresan en capacidades, con opciones de producto como anexo (Art. IX).

### HU-07 Gobierno, seguridad y cumplimiento (P1)
- Se genera un registro de riesgos inicial y un mapa de controles por capa (gobierno, seguridad, privacidad, AI Act, PCI-DSS, consumo).
- Cada agente del backlog tiene su clasificación de riesgo preliminar.

### HU-08 Reevaluación periódica (P3)
- El commerce puede repetir el assessment; gotIA muestra la evolución por dimensión y la distancia restante al `target.spec`.

## 5. Requisitos funcionales
| ID | Requisito |
|---|---|
| RF-01 | Cuestionario adaptativo por dimensión (≈ 60–90 preguntas, que se reducen según el perfil). |
| RF-02 | Carga de evidencias (documentos, diagramas, políticas) y extracción asistida por LLM con cita a la fuente. |
| RF-03 | Conectores opcionales de solo lectura para descubrimiento (plataforma e-commerce, PIM, OMS, CRM, analítica). |
| RF-04 | Motor de scoring determinista y versionado (`scoring_model_version`). |
| RF-05 | Generación de `as-is.spec.yaml` y `target.spec.yaml` conformes a `contracts/assessment-result.schema.json`. |
| RF-06 | Generación de backlog de agentes con borradores de `agent.spec.md`. |
| RF-07 | Generación de roadmap, modelo de costes y arquitectura por etapas. |
| RF-08 | Revisión y firma por consultor humano antes de entregar. |
| RF-09 | Exportación: repositorio Git con specs, informe ejecutivo (HTML/PDF) y presentación. |
| RF-10 | Benchmark anónimo frente a commerces de perfil similar (cuando haya ≥ 20 assessments). |

## 6. Requisitos no funcionales
| ID | Requisito |
|---|---|
| RNF-01 | Reproducibilidad: mismo input y versión de modelo ⇒ mismas puntuaciones y costes. |
| RNF-02 | Trazabilidad: cada puntuación enlaza a ≥ 1 evidencia. |
| RNF-03 | Privacidad: datos del cliente aislados por tenant, cifrados, alojados en la UE, sin uso para entrenar modelos. |
| RNF-04 | Conectores solo lectura, con credenciales temporales revocables por el cliente. |
| RNF-05 | Coste de LLM por assessment < 5 % del precio del assessment. |
| RNF-06 | Las partes generadas por LLM se evalúan con una suite de evals (fidelidad a evidencias, ausencia de cifras inventadas). |

## 7. Fuera de alcance (v1)
- Implantación de los agentes (es un servicio posterior, que consume las specs generadas).
- Auditoría de seguridad intrusiva (pentest).
- Certificación legal de cumplimiento.

## 8. Métricas de éxito del módulo
- ≥ 60 % de assessments que pasan a fase de implantación en ≤ 6 meses.
- Desviación del coste real de F1 frente al estimado ≤ 30 %.
- NPS del entregable ≥ 40.
- Tiempo de consultor por assessment mid-market ≤ 6 días.

## 9. Preguntas abiertas
- [ ] ¿Precio del assessment fijo por tramo o como entrada descontable de la implantación?
- [ ] ¿Qué conectores de descubrimiento priorizar en v1 (Shopify, Adobe Commerce, Salesforce Commerce Cloud, VTEX, PrestaShop)?
- [ ] ¿Publicamos el modelo de madurez como estándar abierto para ganar credibilidad?

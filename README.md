# gotIA · Agentic Readiness Assessment (ARA)

Paquete SDD (Spec-Driven Development) para evaluar e incorporar en gotIA un módulo de assessment que responde, para un commerce que quiere operar con agentes:
¿dónde estoy?, ¿qué ataco?, ¿cuál es el roadmap?, ¿cuánto cuesta?, ¿cómo evoluciona mi arquitectura?, ¿cómo gobierno y aseguro los agentes?

## Veredicto
**GO, con alcance acotado**: assessment asistido por agentes + consultor (opción B de `plan.md`), MVP en ~11 semanas y pilotos en las semanas 12–16. El diferencial es que la salida son **specs ejecutables** (as-is, target, backlog de `agent.spec.md`), que alimentan directamente la implantación.

## Estructura
```
memory/constitution.md                       Principios no negociables (gobierno y seguridad como techo, determinismo, autonomía progresiva)
specs/001-agentic-readiness-assessment/
  spec.md                                    Qué y por qué: historias, criterios de aceptación, requisitos
  maturity-model.md                          10 dimensiones, pesos, niveles N1–N5, algoritmo de scoring
  plan.md                                    Cómo: opciones, arquitectura del módulo, riesgos, hitos
  data-model.md                              Entidades
  contracts/assessment-result.schema.json    Contrato del as-is / target spec
  tasks.md                                   Backlog de implementación
reference/
  use-case-catalog.md                        11 casos de uso agénticos para commerce
  roadmap-cost-model.md                      Fases F0–F3 y modelo de costes
  architecture-evolution.md                  Etapas E0–E4 y capas transversales
templates/agent-spec-template.md             Spec obligatoria para cada agente del cliente
prototypes/agentic-readiness.html            Prototipo navegable: scoring, brechas, roadmap, costes y arquitectura
```

El prototipo es un HTML autocontenido: ábrelo en el navegador. Implementa las reglas de `maturity-model.md` y `roadmap-cost-model.md` con el perfil de ejemplo.

## Flujo SDD
`constitution` → `spec` → `plan` → `tasks` → implementación → evals que verifican la spec.
El mismo flujo se aplica dos veces: para construir el módulo en gotIA y para cada agente que el commerce despliegue después.

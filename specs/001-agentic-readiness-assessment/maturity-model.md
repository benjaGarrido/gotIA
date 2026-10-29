# Modelo de madurez agéntica para commerce (v1.0)

`scoring_model_version: 1.0.0`

## 1. Niveles globales
| Nivel | Nombre | Cómo se reconoce en un commerce |
|---|---|---|
| N1 | Exploración | Uso individual de chatbots generalistas, sin política. Shadow AI. Datos de producto y cliente dispersos. |
| N2 | Asistido | Copilotos en tareas concretas (descripciones de producto, respuestas a clientes) con humano siempre al volante. Primeras políticas de uso. |
| N3 | Agentes acotados | Agentes que ejecutan tareas de un proceso usando herramientas (consultar pedido, crear devolución) con aprobación humana o límites estrictos. Identidad, logs y evals básicos. |
| N4 | Orquestado | Varios agentes coordinados sobre procesos end-to-end, gobierno como código, evals en CI, FinOps por agente. Autonomía A2 en dominios maduros. |
| N5 | Agentic-native | El negocio opera con agentes como unidad de trabajo, expone su catálogo y checkout a agentes de terceros, mejora continua por datos. Autonomía A3 con presupuesto y kill-switch. |

## 2. Dimensiones (capas) y pesos
| ID | Dimensión | Peso | Qué evalúa |
|---|---|---|---|
| D1 | Estrategia y valor | 10 | Patrocinio, tesis de valor, cartera de casos de uso, KPIs, presupuesto |
| D2 | Procesos y specs | 10 | Procesos documentados, reglas de negocio explícitas, capacidad de escribir specs (SDD) |
| D3 | Datos y conocimiento | 14 | Calidad del catálogo/PIM, cliente único, pedidos e inventario en tiempo real, políticas y conocimiento accesibles, semántica |
| D4 | Integración y herramientas | 12 | APIs de plataforma, OMS, ERP, CRM, PIM; eventos; capacidad de exponer tools (MCP) |
| D5 | Plataforma agéntica | 10 | Gateway de modelos, runtime y orquestación de agentes, memoria, RAG, entornos |
| D6 | Gobernanza y cumplimiento | 12 | Propiedad, política de IA, registro de agentes, HITL, AI Act, RGPD, protección del consumidor |
| D7 | Seguridad e identidad de agentes | 12 | Identidad y mínimo privilegio para agentes, secretos, prompt injection, PCI-DSS, fraude |
| D8 | Operación: evals, observabilidad y FinOps | 8 | Evals en CI, trazas, SLOs, gestión de incidentes, coste por tarea |
| D9 | Personas y organización | 7 | Habilidades, CoE, modelo operativo, gestión del cambio, rediseño de roles |
| D10 | Comercio agent-facing | 5 | Preparación para vender a agentes de terceros: feeds estructurados, MCP/ACP/UCP, pagos delegados |

Total = 100.

## 3. Escala por dimensión (1–5) — anclas
Cada dimensión tiene 6–9 preguntas con anclas 1–5. Ejemplo de anclas (resumen):

### D3 Datos y conocimiento
1. Catálogo en hojas de cálculo; stock con retraso de horas; sin cliente único.
2. PIM o plataforma con atributos básicos; stock sincronizado por lotes; CRM parcial.
3. Catálogo enriquecido y normalizado; stock casi en tiempo real vía API; políticas (devoluciones, envíos) documentadas y versionadas.
4. Datos gobernados con owners y calidad medida; capa semántica; conocimiento indexado para RAG con control de acceso.
5. Datos como producto, eventos en tiempo real, feedback de agentes que mejora la calidad del dato.

### D4 Integración y herramientas
1. Integraciones manuales o por fichero.
2. APIs del SaaS e-commerce, pero ERP/OMS cerrados.
3. APIs para operaciones clave (pedido, stock, devolución, cliente) con autenticación moderna.
4. Bus de eventos; APIs internas catalogadas; primeras tools MCP con permisos por operación.
5. Todas las capacidades de negocio expuestas como tools gobernadas, versionadas y testeadas.

### D6 Gobernanza y cumplimiento
1. Sin política de IA; nadie es responsable.
2. Política de uso aceptable; inventario parcial de herramientas IA.
3. Comité o responsable de IA; registro de agentes; HITL definido; evaluación de riesgos por caso (AI Act / RGPD).
4. Gobierno como código: políticas derivadas de la spec aplicadas en runtime; auditoría continua.
5. Gobierno adaptativo con métricas de riesgo y mejora continua; reporting regulatorio automatizado.

### D7 Seguridad e identidad de agentes
1. Claves API compartidas; sin controles específicos de IA.
2. Secretos gestionados; controles genéricos de seguridad.
3. Identidad por agente, mínimo privilegio, filtrado de entradas y salidas, datos de pago fuera del contexto del LLM.
4. Autorización por acción (policy engine), red-teaming periódico, detección de anomalías por agente.
5. Zero-trust agente a agente, credenciales efímeras delegadas, respuesta automatizada a incidentes.

### D8 Operación
1. Sin métricas.
2. Logs de conversaciones; revisión manual ocasional.
3. Trazas por ejecución, suite de evals básica, coste por agente visible.
4. Evals en CI/CD que bloquean despliegues, SLOs, alertas, presupuestos por agente.
5. Optimización continua de calidad y coste; A/B de agentes; aprendizaje de incidentes.

*(D1, D2, D5, D9, D10: anclas completas en el banco de preguntas `question-bank.yaml`, pendiente de redactar en la tarea T-010.)*

## 4. Algoritmo de scoring (determinista)
```
para cada dimensión d:
    score[d] = media ponderada de las respuestas (1..5)
    confianza[d] = % de respuestas con evidencia documentada o verificada

IPA = Σ score[d] × peso[d] / 100                       # índice 1..5
techo = min(score[D6], score[D7]) + 1                    # Art. IV
nivel_efectivo = min(IPA, techo)                         # N = floor(nivel_efectivo)

base_autonomía = min(score[D6], score[D7], score[D8])
autonomía_max = A0 si base < 2
              = A1 si 2 ≤ base < 3
              = A2 si 3 ≤ base < 4
              = A3 si base ≥ 4

para cada dimensión d:
    brecha[d] = max(0, objetivo[d] − score[d])
    bloqueo[d] = 1.5 si d ∈ {D6, D7, D8} y score[d] < 3     # impiden autonomía A2 y frenan el techo
               = 1.0 en otro caso
    prioridad[d] = brecha[d] × peso[d] × bloqueo[d]
```

## 5. Viabilidad de un caso de uso
```
viabilidad(caso) = min(score[d] for d in caso.dependencias) / 5
estado(caso) = "Listo"                     si viabilidad ≥ 0.5 y autonomía_mínima(caso) ≤ autonomía_max
             = "Listo, autonomía reducida" si viabilidad ≥ 0.5 y autonomía_mínima(caso) > autonomía_max
                                            (arranca en autonomía_max; en A0 solo sugiere)
             = "Tras fundamentos (F1)"     si 0.4 ≤ viabilidad < 0.5
             = "Requiere remediación"      si viabilidad < 0.4
```
`autonomía_mínima` es el primer nivel de la autonomía objetivo del catálogo (p. ej. "A1→A2" ⇒ A1).

## 6. Confianza de la evidencia
| Tipo | Peso | Ejemplo |
|---|---|---|
| Declarada | 0.6 | Respuesta del cliente sin soporte |
| Documentada | 0.85 | Política, diagrama o procedimiento aportado |
| Verificada | 1.0 | Comprobada por conector o por el consultor |

La confianza no altera la puntuación; se muestra junto a ella y, si es < 0.7 en una dimensión, el informe lo marca como "a validar".

# Evolución de arquitectura (E0 → E4)

Recomendaciones expresadas en capacidades (Art. IX). Cada etapa añade componentes; ninguna sustituye la plataforma e-commerce del cliente.

## E0 — Punto de partida típico
Plataforma e-commerce (SaaS o monolito) + ERP + OMS/WMS + CRM/ESP, con integraciones punto a punto o por fichero. IA en herramientas sueltas y cuentas personales (shadow AI). Sin trazabilidad.

## E1 — Asistida (fase F1, inicio)
- **Gateway de modelos**: punto único de acceso a LLM con autenticación, cuotas, registro, enrutado entre modelos y redacción de datos personales.
- **Conocimiento (RAG)**: índice de catálogo, políticas y FAQs con control de acceso.
- Copilotos sobre el gateway. Política de uso aceptable.

## E2 — Agentes con herramientas (fin de F1)
- **Capa de herramientas (MCP)**: servidores MCP sobre las APIs de pedido, stock, devolución, cliente y catálogo; cada tool declara lectura/escritura/importe.
- **Runtime de agentes** con **identidad por agente** y credenciales de mínimo privilegio.
- **Bandeja HITL**: aprobaciones humanas para acciones A1.
- **Observabilidad**: trazas por ejecución (OpenTelemetry, convenciones GenAI), coste por agente.
- **Evals** ligados a los criterios de aceptación de cada `agent.spec`.

## E3 — Multiagente orquestado (F2)
- **Orquestador** + agentes especializados; contratos entre agentes definidos en spec.
- **Bus de eventos** (pedido creado, stock bajo, devolución solicitada) para agentes reactivos.
- **Registro de agentes**: inventario con owner, versión de spec, autonomía, riesgo, estado.
- **Policy engine / gobierno como código**: autorización por acción derivada de la spec (límites de importe, datos permitidos, horarios).
- **Memoria** de corto y largo plazo con retención conforme a RGPD.
- Evals en CI/CD que bloquean despliegues; presupuestos por agente.

## E4 — Agentic-native (F3)
- **Superficie agent-facing**: catálogo, disponibilidad y checkout expuestos a agentes de terceros (servidor MCP público, protocolos de agentic commerce como ACP/UCP, pagos delegados tipo AP2 con mandatos verificables).
- **A2A** con proveedores, transportistas y marketplaces.
- Autonomía A2/A3 en dominios maduros, con presupuesto, detección de anomalías y kill-switch.
- Bucle de mejora continua: incidentes y feedback → cambio de spec → regeneración → evals.

## Capas transversales por etapa
| Capa | E1 | E2 | E3 | E4 |
|---|---|---|---|---|
| Gobernanza | Política de uso | Registro + HITL + evaluación de riesgo por agente | Gobierno como código | Reporting regulatorio automatizado |
| Seguridad | Redacción de datos personales en gateway | Identidad por agente, mínimo privilegio, defensa frente a injection | Autorización por acción, red-teaming | Zero-trust agente a agente, credenciales delegadas |
| Datos | Índice RAG | APIs de datos en tiempo real | Eventos + capa semántica | Feeds estructurados para agentes externos |
| Operación | Logs | Trazas + evals | CI de evals, SLOs, FinOps | Optimización continua, A/B de agentes |

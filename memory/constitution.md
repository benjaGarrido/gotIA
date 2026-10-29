# Constitución — gotIA Agentic Readiness Assessment (ARA)

> Principios no negociables. Toda spec, plan, tarea y agente generado por gotIA (y todo agente que el commerce despliegue después) se valida contra este documento. Si una spec contradice la constitución, la spec está mal.

## Artículo I — La spec es la fuente de verdad
1. Nada se construye sin una spec aprobada: ni el módulo de assessment, ni los agentes del cliente.
2. El código, los prompts, las políticas y los evals son **derivados** de la spec y se regeneran si la spec cambia.
3. Las specs viven versionadas (Git) junto al código; un cambio de comportamiento sin cambio de spec es un defecto.

## Artículo II — Estado actual y estado objetivo también son specs
1. El resultado del assessment no es un PDF: es un `as-is.spec.yaml` (estado actual) y un `target.spec.yaml` (estado objetivo), legibles por máquinas.
2. El roadmap es el **diff** entre ambos, descompuesto en specs ejecutables.
3. Reevaluar = regenerar `as-is` y medir la distancia al `target`.

## Artículo III — Determinismo donde se decide, LLM donde se explica
1. El scoring de madurez, los techos (gating) y la estimación de costes son **deterministas** y reproducibles: mismo input ⇒ mismo output.
2. Los LLM se usan para: entrevista adaptativa, extracción de evidencias, narrativa, redacción de specs. Nunca para inventar una puntuación.
3. Toda puntuación debe poder trazarse a evidencias (respuesta, documento, escaneo).

## Artículo IV — Gobierno y seguridad marcan el techo
1. El nivel de madurez efectivo no puede superar en más de un nivel la puntuación de Gobernanza (D6) o Seguridad (D7).
2. La autonomía máxima de un agente la marcan Gobernanza, Seguridad y Operación (D6, D7, D8), no la ambición del negocio.

## Artículo V — Autonomía progresiva y reversible
1. Escala de autonomía: **A0** sugiere · **A1** actúa con aprobación humana · **A2** actúa sola con límites y revisión posterior · **A3** actúa sola con presupuesto, monitorización y kill-switch.
2. Ningún agente nace en A2/A3. Subir un nivel requiere evidencia de evals y operación.
3. Todo agente tiene un mecanismo de parada probado.

## Artículo VI — Seguridad por diseño
1. Cada agente tiene identidad propia, credenciales de mínimo privilegio y de vida corta.
2. Las herramientas (tools/MCP) declaran en su spec qué datos leen, qué escriben y qué dinero mueven.
3. Entradas no confiables (clientes, webs, emails, agentes de terceros) se tratan como hostiles: defensa frente a prompt injection por capas.
4. Datos de pago fuera del contexto del LLM (alcance PCI-DSS minimizado).

## Artículo VII — Cumplimiento trazable
1. Cada spec de agente incluye clasificación de riesgo (AI Act), base legal RGPD de los datos que usa y obligaciones de transparencia hacia el consumidor.
2. La spec + los logs de ejecución + los resultados de evals constituyen la documentación técnica auditable.

## Artículo VIII — Medible o no existe
1. Toda spec de agente define KPIs de negocio, criterios de aceptación y una suite de evals que se ejecuta en CI.
2. Todo agente en producción reporta coste por tarea, tasa de éxito, tasa de escalado a humano e incidencias.

## Artículo IX — Neutralidad tecnológica
1. Las recomendaciones de arquitectura se expresan en capacidades, no en productos. Los productos se proponen como opciones con trade-offs.
2. Se priorizan estándares abiertos (MCP, A2A, OpenTelemetry, protocolos de agentic commerce) frente a integraciones propietarias.

## Gobierno de la constitución
Cambios a este documento requieren aprobación del responsable de producto de gotIA y del responsable de seguridad, y un registro de motivo en el changelog.

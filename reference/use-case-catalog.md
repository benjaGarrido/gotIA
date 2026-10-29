# Catálogo de casos de uso agénticos para commerce

Cada caso declara de qué dimensiones depende (para calcular viabilidad), qué autonomía necesita para capturar el valor y el riesgo regulatorio preliminar. El assessment filtra y puntúa este catálogo según el perfil del commerce.

| ID | Agente | Valor típico | Dependencias críticas | Autonomía objetivo | Complejidad | Riesgo AI Act (prelim.) |
|---|---|---|---|---|---|---|
| UC-01 | Atención "¿dónde está mi pedido?" y devoluciones | −30/−50 % tickets de nivel 1; respuesta 24/7 | D3, D4, D7 | A1→A2 | Media | Limitado (transparencia) |
| UC-02 | Enriquecimiento de catálogo (descripciones, atributos, traducciones, SEO) | Time-to-market de producto −60 %; conversión por mejores fichas | D3, D2 | A1 | Simple | Mínimo |
| UC-03 | Asistente de compra conversacional | +conversión y +AOV en tráfico asistido | D3, D4, D10 | A1 | Media | Limitado (transparencia) |
| UC-04 | Pricing y promociones con guardarraíles | +1–3 pp de margen | D3, D4, D6, D8 | A1→A2 | Compleja | Mínimo / revisar prácticas comerciales |
| UC-05 | Reposición y previsión de inventario | −roturas de stock, −sobrestock | D3, D4, D8 | A1→A2 | Compleja | Mínimo |
| UC-06 | Marketing: segmentación y orquestación de campañas | +ROI de campañas, −tiempo de producción | D3, D6 (consentimiento) | A1 | Media | Limitado; RGPD crítico |
| UC-07 | Revisión de fraude en pedidos | −contracargos, −revisión manual | D3, D7, D6 | A1 | Media | Revisar decisión automatizada (art. 22 RGPD) |
| UC-08 | Back-office: facturas de proveedores y conciliación | −70 % trabajo manual | D2, D4 | A1→A2 | Media | Mínimo |
| UC-09 | Storefront agent-facing (catálogo y checkout para agentes de terceros vía MCP/ACP/UCP) | Nuevo canal de venta | D4, D7, D10 | A2 | Compleja | Limitado; pagos delegados |
| UC-10 | Gestión de proveedores y marketplace (onboarding de sellers, calidad de listados) | Escala del marketplace | D2, D3, D4 | A1 | Media | Mínimo |
| UC-11 | Copiloto interno de operaciones (consultas sobre ventas, stock, KPIs) | Decisión más rápida | D3, D5 | A0 | Simple | Mínimo |

## Reglas de priorización
1. **Quick wins** (fase F1): viabilidad ≥ 0.5, complejidad simple/media, autonomía A0–A1, riesgo mínimo/limitado. Normalmente UC-02, UC-11, UC-01 en A1.
2. **Escala** (F2): casos con dependencias en D4/D8 una vez cerradas brechas de fundamentos. UC-01 en A2, UC-06, UC-08, UC-07.
3. **Agentic-native** (F3): UC-04, UC-05 en A2 y UC-09.
4. Nunca priorizar un caso cuyo riesgo exija controles de D6/D7 que no existen todavía; en su lugar, añadir esos controles como iniciativa previa.

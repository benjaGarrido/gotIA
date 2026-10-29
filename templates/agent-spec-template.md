# Agent spec — `<UC-XX> <nombre del agente>`

> Plantilla obligatoria para todo agente que el commerce despliegue. El spec-writer de gotIA la rellena desde el assessment; los huecos se marcan `[NEEDS CLARIFICATION]` y bloquean la aprobación.

| Campo | Valor |
|---|---|
| Owner de negocio | |
| Owner técnico | |
| Versión de spec | 0.1.0 |
| Estado | borrador / aprobado / en producción / retirado |
| Autonomía objetivo | A0 / A1 / A2 / A3 |
| Autonomía permitida hoy (según assessment) | |
| Clasificación de riesgo (AI Act, preliminar) | mínimo / limitado / alto |

## 1. Intención
Qué resultado de negocio produce el agente, en una frase. Qué **no** hace.

## 2. Usuarios y disparadores
Quién o qué lo invoca (cliente, empleado, evento `order.delayed`, otro agente).

## 3. Comportamiento (historias + criterios de aceptación)
- **Dado** … **cuando** … **entonces** …

## 4. Herramientas
| Tool | Sistema | Lee | Escribe | Mueve dinero | Límite | Requiere aprobación |
|---|---|---|---|---|---|---|
| `get_order_status` | OMS | pedido, envío | — | No | — | No |
| `create_return` | OMS | pedido | devolución | Reembolso ≤ 150 € | 50/h | Sí si > 150 € |

## 5. Datos y privacidad
Datos personales que usa, base legal RGPD, retención, minimización. Datos de pago: nunca en contexto.

## 6. Políticas y guardarraíles
Reglas de negocio (de la política de devoluciones vX.Y), tono, idiomas, temas prohibidos, transparencia ("estás hablando con un asistente de IA"), criterios de escalado a humano.

## 7. Seguridad
Identidad del agente, permisos, entradas no confiables y defensa frente a injection, kill-switch (cómo y quién).

## 8. KPIs y SLOs
| KPI | Línea base | Objetivo |
|---|---|---|
| Tasa de resolución sin humano | | |
| CSAT | | |
| Coste por tarea | | |
| Tasa de error grave | | 0 |

## 9. Evals
Casos dorados, casos adversarios (injection, abuso de reembolsos), umbrales que bloquean el despliegue.

## 10. Criterios para subir de autonomía
Qué evidencia (n.º de ejecuciones, tasa de acierto, incidentes = 0 durante X semanas) permite pasar de A1 a A2.

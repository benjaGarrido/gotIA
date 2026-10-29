# Roadmap tipo y modelo de costes

> Cifras orientativas en euros, sin IVA, para calibrar con datos reales de gotIA tras los primeros pilotos. El motor de costes es determinista (Art. III) y siempre muestra fórmula y supuestos.

## 1. Fases
| Fase | Duración típica | Objetivo | Entregables (todos como specs) | Condición de salida |
|---|---|---|---|---|
| **F0 Assessment y specs fundacionales** | 2–6 semanas | Saber dónde estoy y a dónde voy | `as-is.spec`, `target.spec`, backlog de agentes, constitución del cliente, registro de riesgos | Comité aprueba target y presupuesto F1 |
| **F1 Fundamentos y quick wins** | Meses 2–4 | Plataforma mínima gobernada y valor visible | Gateway de modelos, identidad de agentes, trazas y evals básicos, política de IA, 2–3 tools MCP, 2 agentes en A0/A1 | Agentes en producción con KPIs; D6, D7, D8 ≥ 2.5 |
| **F2 Escala** | Meses 5–9 | Agentes en procesos completos | Orquestación multiagente, bus de eventos, gobierno como código, evals en CI, FinOps, CoE | 4–6 agentes; primer agente en A2; D6, D7, D8 ≥ 3.5 |
| **F3 Agentic-native** | Meses 10–18 | Autonomía acotada y nuevo canal | Pricing/inventario en A2, storefront agent-facing, A2A con proveedores, mejora continua | IPA ≥ 3.8; canal agent-facing con ventas |

## 2. Componentes de coste
Multiplicador por tamaño: **Pyme** (< 10 M€ de facturación online) = 0.6 · **Mid-market** (10–100 M€) = 1.0 · **Enterprise** (> 100 M€) = 1.6 (aplicado a la construcción de agentes).

| Componente | Pyme | Mid-market | Enterprise | Tipo |
|---|---|---|---|---|
| F0 Assessment + specs | 8 k | 30 k | 90 k | Inversión |
| Fundamentos de plataforma (gateway, identidad, observabilidad, evals, policy, capa MCP core) | 35 k | 150 k | 500 k | Inversión |
| Remediación de datos e integración (× factor de brecha) | 20 k | 90 k | 300 k | Inversión |
| Gobierno, formación y gestión del cambio | 15 k | 60 k | 200 k | Inversión |
| Agente simple / medio / complejo (spec → producción) | 25 k / 70 k / 160 k × multiplicador | | | Inversión |
| Plataforma e infraestructura anual | 12 k | 48 k | 180 k | Operación |
| Mantenimiento de agentes | 18 % anual del coste de construcción | | | Operación |
| Consumo de modelos | interacciones/mes × 12 × tokens/interacción ÷ 10⁶ × €/M tokens | | | Operación |

`factor_brecha = clamp( media(brecha[D3], brecha[D4]) / 2 , 0.25 , 1.5 )`

## 3. Fórmula
```
inversión = F0 + fundamentos + remediación × factor_brecha + gobierno
          + Σ agentes(complejidad) × multiplicador
operación_anual = plataforma + 0.18 × Σ agentes × multiplicador + consumo_modelos
horquilla = [−20 %, +30 %]
```

## 4. Ejemplo — moda online mid-market (40 M€), perfil de muestra
- 2 agentes simples, 2 medios, 1 complejo; 25 000 interacciones/mes; 6 000 tokens/interacción; 4 €/M tokens (precio mezclado; parámetro editable).
- Brecha media D3/D4 ≈ 1.25 ⇒ factor 0.63.
- Inversión ≈ 30 + 150 + 56 + 60 + (50 + 140 + 160) = **646 k€** (horquilla 517–840 k€).
- Operación anual ≈ 48 + 63 + 7.2 = **118 k€/año**.
- Lectura: el consumo de modelos es la partida pequeña; el coste está en datos, integración, plataforma y personas.

## 5. Supuestos que hay que validar
- Precios de modelos cambian rápido: el €/M tokens es un parámetro, revisado trimestralmente.
- Las tarifas de construcción presuponen equipo mixto gotIA + cliente con SDD (specs reutilizables reducen el coste del 3er agente en adelante un 20–30 %; no incluido en la fórmula v1).
- No incluye licencias de plataforma e-commerce, ERP o PIM existentes.

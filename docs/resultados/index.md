---
layout: default
title: Resultados
nav_order: 5
permalink: /resultados/
description: "Resultados del entrenamiento DQN y prueba en hardware físico."
---

# Resultados
{: .no_toc }

Métricas de entrenamiento, prueba greedy y desempeño en hardware real.
{: .fs-5 .fw-300 }

## Tabla de Contenidos
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Entrenamiento — 4,000 Episodios

El agente DQN fue entrenado durante **4,000 episodios** en el entorno de simulación Simscape. La curva de recompensa muestra convergencia clara a partir del episodio ~500, con alta varianza inicial típica de la exploración ε-greedy.

### Métricas Finales (últimos 50 episodios)

| Métrica | Valor |
|---|---|
| Reward medio | 42,877.5 |
| Reward máximo | 51,577.8 |
| Pasos promedio por episodio | 545.6 / 600 |
| Tasa de éxito | **90 %** |
| Tasa de límite de posición | 10 % |
| Tiempo en equilibrio (promedio) | **9.02 s** |
| Tiempo en equilibrio (máximo) | **10.60 s** |

## Prueba de Política Greedy Final

Al aplicar la política greedy (ε = 0) sobre un episodio completo de prueba:

| Métrica | Valor |
|---|---|
| Tiempo acumulado arriba | **14.56 s** |
| Reward total de prueba | **71,157.5** |

> El agente mantuvo el péndulo en equilibrio superior durante **14.56 segundos acumulados** en la prueba greedy, superando ampliamente el umbral de éxito de 10 s.

## Análisis de las Gráficas

### Simulación (Episodio 4000)

La gráfica de entrenamiento muestra cinco subplots:

1. **Reward por episodio** — converge a ~40,000–50,000 con varianza residual. La línea naranja (promedio móvil) confirma la tendencia ascendente.
2. **Top time** — el tiempo en equilibrio crece consistentemente hasta saturar en 10 s (límite del episodio).
3. **Tasa de éxito / límite** — éxito (azul) converge cerca del 80–90 %; límites de posición (naranja) se mantienen bajos.
4. **Ángulo θ (último episodio)** — el péndulo se estabiliza en θ ≈ 0° y el controlador lo mantiene frente a perturbaciones.
5. **Posición x y esfuerzo u** — el carro converge a una posición lateral con esfuerzo de control moderado.

### Política Greedy en Hardware

La gráfica de la prueba real muestra:

- **θ** oscila con alta frecuencia (chattering visible), indicando que la política discreta aplica acciones de signo opuesto rápidamente para mantenerse en el punto de equilibrio. Esto es esperable con 41 acciones discretas.
- **x** converge a ~−120 mm desde el centro y permanece estable, lo que indica que el carro encontró una posición de trabajo sin llegar al límite.
- **u** es una señal de alta frecuencia de baja amplitud (~±0.3), coherente con un controlador activo en régimen de equilibrio.

## Presentaciones

### Día de las Ingenierías IBERO — 5 de mayo de 2026

Presentación del prototipo físico y demostración en vivo del equilibrio DQN ante jurado y comunidad universitaria.

### Congreso ITESO Guadalajara 2026 — 26–28 de mayo de 2026

Presentación académica del proyecto ante la comunidad de ingeniería a nivel nacional, cubriendo la metodología Sim-to-Real, la comparativa Shallow vs. DQN y los resultados experimentales.

---

[&larr; Implementación Física]({{ '/implementacion/' | relative_url }})

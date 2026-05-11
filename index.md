---
layout: default
title: Inicio
nav_order: 1
description: "Péndulo Invertido controlado mediante Deep Q-Learning. Transferencia Sim-to-Real. IBERO Ciudad de México, Control Inteligente Primavera 2026."
permalink: /
---

# Péndulo Invertido mediante Deep Q-Learning
{: .no_toc }

Control Inteligente — Primavera 2026 · IBERO Ciudad de México
{: .fs-5 .fw-300 }

---

> **"La inteligencia es la habilidad de adaptarse al cambio."**
> — Stephen Hawking

## El Proyecto

Este sitio documenta el diseño, construcción y control de un **péndulo invertido físico** utilizando **Deep Q-Learning (DQN)** como algoritmo de control inteligente. El reto central fue lograr la transferencia de una política entrenada íntegramente en simulación al hardware real (**Sim-to-Real transfer**), manteniendo el péndulo en equilibrio en la posición vertical superior.

A diferencia del control clásico (PID o lineal), el agente aprende su política de control exclusivamente a través de la interacción con el entorno, guiado por una función de recompensa que penaliza el error angular, la velocidad angular y el esfuerzo de control:

$$r_t = -(w_1\theta^2 + w_2\dot{\theta}^2 + w_3 u^2)$$

## Resultados Destacados

| Métrica | Valor |
|---|---|
| Episodios de entrenamiento | 4,000 |
| Tasa de éxito (últimos 50 ep.) | **90 %** |
| Tiempo en equilibrio (promedio) | 9.02 s / máx. 10.60 s |
| Reward total prueba greedy | **71,157.5** |
| Reward medio (últimos 50 ep.) | 42,877.5 |

## Presentaciones

- 🏫 **Día de las Ingenierías IBERO** — 5 de mayo de 2026
- 🎓 **Congreso ITESO Guadalajara 2026** — 26 al 28 de mayo de 2026

## Equipo

| Integrante | Rol |
|---|---|
| Andrick Millán | Hardware & Electrónica |
| Jesús Velázquez | Simulación & Entrenamiento DQN |
| Elías Santiago Jiménez Hernández | Implementación embebida & Sim-to-Real |

**Profesores:** Dr. Alexandro López · Mtro. Julio Caballero

## Videos

<div style="display:grid;grid-template-columns:1fr 1fr;gap:1rem;margin:1.5rem 0;">
  <div>
    <p style="margin:0 0 0.5rem;font-weight:600;font-size:0.9rem;">Equilibrio durante el entrenamiento</p>
    <div style="position:relative;padding-bottom:177.78%;height:0;overflow:hidden;border-radius:10px;">
      <iframe src="https://www.youtube.com/embed/zO4dnO2xxjA"
        style="position:absolute;top:0;left:0;width:100%;height:100%;"
        frameborder="0" allowfullscreen></iframe>
    </div>
  </div>
  <div>
    <p style="margin:0 0 0.5rem;font-weight:600;font-size:0.9rem;">Episodios fallidos — etapa inicial</p>
    <div style="position:relative;padding-bottom:177.78%;height:0;overflow:hidden;border-radius:10px;">
      <iframe src="https://www.youtube.com/embed/txFmPXgzE_4"
        style="position:absolute;top:0;left:0;width:100%;height:100%;"
        frameborder="0" allowfullscreen></iframe>
    </div>
  </div>
</div>

<div style="display:grid;grid-template-columns:1fr 1fr;gap:1rem;margin:1.5rem 0;">
  <div>
    <p style="margin:0 0 0.5rem;font-weight:600;font-size:0.9rem;">Timelapse — 4,000 episodios de entrenamiento</p>
    <div style="position:relative;padding-bottom:56.25%;height:0;overflow:hidden;border-radius:10px;">
      <iframe src="https://www.youtube.com/embed/pEJuTYEiCGU"
        style="position:absolute;top:0;left:0;width:100%;height:100%;"
        frameborder="0" allowfullscreen></iframe>
    </div>
  </div>
  <div>
    <p style="margin:0 0 0.5rem;font-weight:600;font-size:0.9rem;">Timelapse — ensamblado del prototipo</p>
    <div style="position:relative;padding-bottom:56.25%;height:0;overflow:hidden;border-radius:10px;">
      <iframe src="https://www.youtube.com/embed/0icStA-qZcc"
        style="position:absolute;top:0;left:0;width:100%;height:100%;"
        frameborder="0" allowfullscreen></iframe>
    </div>
  </div>
</div>

## Navegación Rápida

[Hardware]({{ '/hardware/' | relative_url }}){: .btn .btn-primary .mr-2 }
[Simulación & Entrenamiento]({{ '/simulacion/' | relative_url }}){: .btn .btn-outline .mr-2 }
[Implementación Física]({{ '/implementacion/' | relative_url }}){: .btn .btn-outline .mr-2 }
[Resultados]({{ '/resultados/' | relative_url }}){: .btn .btn-outline }

---
layout: default
title: Implementación Física
nav_order: 4
permalink: /implementacion/
description: "Transferencia Sim-to-Real del controlador DQN al hardware físico."
---

# Implementación Física — Sim-to-Real
{: .no_toc }

Transferencia de la política DQN entrenada en simulación al prototipo real.
{: .fs-5 .fw-300 }

## Tabla de Contenidos
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Estrategia de Transferencia

Una vez que el agente DQN convergió en simulación (tasa de éxito ≥ 90 %), los pesos de la red neuronal se exportaron desde MATLAB y se embebieron en el microcontrolador. En cada ciclo de control, el Arduino:

1. Adquiere el estado `(θ, θ̇, x, ẋ)` desde los encoders.
2. Pasa el estado por la red DQN (inferencia en tiempo real).
3. Selecciona la acción `a = argmax Q(s, a)` (política greedy pura).
4. Aplica la fuerza correspondiente al motor via PWM.

## Desafíos Sim-to-Real

| Desafío | Descripción | Solución |
|---|---|---|
| Fricción no modelada | El carro real tiene rozamiento con la guía | Sintonización de `w3` (peso del esfuerzo) |
| Latencia serial | Tiempo de comunicación Arduino ↔ PC | Optimización del protocolo de comunicación |
| Offset del encoder | Posición cero no coincide con la simulación | Rutina de centrado automático al inicio |
| Ruido de medición | Vibración mecánica en θ̇ | Filtro de media móvil sobre velocidad angular |

## Rutina de Centrado

Antes de activar el controlador DQN, el carro ejecuta una rutina de centrado para establecer el origen de coordenadas:

{% highlight cpp %}
void centrarCarro() {
  // Mover hacia límite izquierdo hasta activar fin de carrera
  moverMotor(-VELOCIDAD_CENTRADO);
  while (!finDeCarreraIzq()) { delay(1); }
  resetearEncoder();

  // Mover al centro de la guía
  moverMotor(+VELOCIDAD_CENTRADO);
  while (posicion() < LONGITUD_GUIA / 2.0) { delay(1); }
  pararMotor();
  resetearEncoder();  // x = 0 en el centro
}
{% endhighlight %}

## Inferencia de la Red DQN en Tiempo Real

Los pesos exportados de MATLAB se cargan como arreglos de constantes en el firmware. La inferencia se realiza como multiplicaciones matriciales en punto flotante:

{% highlight cpp %}
float inferirAccion(float estado[4]) {
  float h1[64], h2[64], q[41];

  // Capa 1: h1 = ReLU(W1 * estado + b1)
  matMul(W1, estado, h1, 64, 4);
  addBias(h1, b1, 64);
  relu(h1, 64);

  // Capa 2: h2 = ReLU(W2 * h1 + b2)
  matMul(W2, h1, h2, 64, 64);
  addBias(h2, b2, 64);
  relu(h2, 64);

  // Salida: Q = W3 * h2 + b3
  matMul(W3, h2, q, 41, 64);
  addBias(q, b3, 41);

  return acciones[argmax(q, 41)];  // acción greedy
}
{% endhighlight %}

## Videos Demostrativos

### Video 1 — Péndulo manteniendo el equilibrio durante el entrenamiento

<div style="position:relative;padding-bottom:177.78%;height:0;overflow:hidden;border-radius:10px;margin:1.5rem 0;max-width:360px;">
  <iframe src="https://www.youtube.com/embed/zO4dnO2xxjA"
    style="position:absolute;top:0;left:0;width:100%;height:100%;"
    frameborder="0" allowfullscreen>
  </iframe>
</div>

### Video 2 — Entrenamiento temprano: episodios fallidos

<div style="position:relative;padding-bottom:177.78%;height:0;overflow:hidden;border-radius:10px;margin:1.5rem 0;max-width:360px;">
  <iframe src="https://www.youtube.com/embed/txFmPXgzE_4"
    style="position:absolute;top:0;left:0;width:100%;height:100%;"
    frameborder="0" allowfullscreen>
  </iframe>
</div>

### Video 3 — Timelapse del entrenamiento completo (4,000 episodios)

<div style="position:relative;padding-bottom:56.25%;height:0;overflow:hidden;border-radius:10px;margin:1.5rem 0;">
  <iframe src="https://www.youtube.com/embed/pEJuTYEiCGU"
    style="position:absolute;top:0;left:0;width:100%;height:100%;"
    frameborder="0" allowfullscreen>
  </iframe>
</div>

### Video 4 — Timelapse: el equipo armando el péndulo

<div style="position:relative;padding-bottom:56.25%;height:0;overflow:hidden;border-radius:10px;margin:1.5rem 0;">
  <iframe src="https://www.youtube.com/embed/0icStA-qZcc"
    style="position:absolute;top:0;left:0;width:100%;height:100%;"
    frameborder="0" allowfullscreen>
  </iframe>
</div>

---

[&larr; Simulación]({{ '/simulacion/' | relative_url }}) &nbsp;&nbsp; [Resultados &rarr;]({{ '/resultados/' | relative_url }}){: .btn .btn-outline }

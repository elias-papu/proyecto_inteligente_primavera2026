---
layout: default
title: Electrónica y Firmware
parent: Hardware
nav_order: 1
permalink: /hardware/electronica/
---

# Electrónica y Firmware
{: .no_toc }

## Tabla de Contenidos
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Arquitectura del Sistema Embebido

El controlador embebido corre en un **Arduino** y realiza tres funciones en tiempo real:

1. **Lectura de sensores** — ángulo θ del péndulo (encoder rotatorio) y posición x del carro.
2. **Comunicación serial** — recibe la acción `u` calculada por la red DQN e informa el estado `(θ, ẋ, x, θ̇)`.
3. **Actuación** — traduce la acción discreta a una señal PWM para el driver del motor.

## Código Arduino (fragmento principal)

El archivo completo se encuentra en `pendulo_center_FIXED.ino`.

{% highlight cpp %}
// Loop principal de control — inferencia en tiempo real
void loop() {
  // Leer encoders
  theta    = leerEncoderPendulo();   // ángulo en radianes
  x_pos    = leerEncoderCarro();     // posición en mm
  theta_d  = calcularVelocidadAngular();
  x_vel    = calcularVelocidadCarro();

  // Enviar estado al sistema de inferencia
  Serial.print(theta);   Serial.print(",");
  Serial.print(theta_d); Serial.print(",");
  Serial.print(x_pos);   Serial.print(",");
  Serial.println(x_vel);

  // Recibir acción y aplicar al motor
  if (Serial.available()) {
    float u = Serial.parseFloat();
    aplicarFuerza(u);
  }
}
{% endhighlight %}

## Parámetros de Muestreo

| Parámetro | Valor |
|---|---|
| Frecuencia de muestreo | ~100 Hz |
| Resolución encoder péndulo | Alta resolución (ver BOM) |
| Espacio de acciones | 41 niveles discretos [−10 N, +10 N] |
| Paso de acción | 0.5 N |

> **Nota de diseño:** La latencia de comunicación serial fue una fuente crítica de inestabilidad en las primeras pruebas. Se optimizó el protocolo para minimizar el tiempo de ciclo.

---

[&larr; Hardware]({{ '/hardware/' | relative_url }}) &nbsp;&nbsp; [Simulación &rarr;]({{ '/simulacion/' | relative_url }}){: .btn .btn-outline }

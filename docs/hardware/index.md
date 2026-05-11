---
layout: default
title: Hardware
nav_order: 2
has_children: true
permalink: /hardware/
description: "Construcción y electrónica del péndulo invertido físico."
---

# Hardware y Adquisición de Datos
{: .no_toc }

Mecánica, electrónica y sensores del prototipo físico.
{: .fs-5 .fw-300 }

---

## Descripción General

El prototipo consiste en un **carro deslizante** sobre una guía lineal de aluminio, actuado por un motor DC mediante correa dentada. Un péndulo articulado se monta sobre el carro, y su ángulo se mide con un encoder rotatorio de alta resolución.

El sistema fue diseñado, fabricado e instrumentado íntegramente por el equipo, incluyendo piezas impresas en 3D (PLA) en color rojo para el carro y el soporte del encoder.

## Fotografías del Prototipo

![Close-up del encoder rotatorio montado en el carro rojo]({{ '/assets/img/encoder_pendulo.jpg' | relative_url }})

*Encoder rotatorio de alta resolución montado en el carro impreso en 3D (PLA rojo) sobre la guía lineal.*

![Vista completa del sistema péndulo invertido]({{ '/assets/img/pendulo_completo.jpg' | relative_url }})

*Vista general del sistema: guía lineal de ~1 m, carro motorizado con correa dentada y péndulo articulado.*

![Laboratorio con el equipo completo de trabajo]({{ '/assets/img/laboratorio.jpg' | relative_url }})

*El equipo durante las sesiones de desarrollo y prueba en el laboratorio de electrónica de la IBERO.*

## Lista de Materiales (BOM)

| Componente | Especificación | Cantidad |
|---|---|---|
| Guía lineal | Perfil de aluminio, ~1 m | 1 |
| Motor DC | Con driver PWM | 1 |
| Correa dentada | GT2, paso 2 mm | 1 |
| Encoder rotatorio | Alta resolución (péndulo) | 1 |
| Encoder lineal / odómetro | Posición del carro | 1 |
| Carro impreso en 3D | PLA rojo, diseño propio | 1 |
| Microcontrolador | Arduino (ver código fuente) | 1 |
| Driver de motor | Puente H | 1 |
| Fuente de alimentación | 12 V DC | 1 |
| Estructuras de soporte | Aluminio perfilado | 2 |

---

[&larr; Inicio]({{ '/' | relative_url }}) &nbsp;&nbsp; [Electrónica &rarr;]({{ '/hardware/electronica/' | relative_url }}){: .btn .btn-outline }

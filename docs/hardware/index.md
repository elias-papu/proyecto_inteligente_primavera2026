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

## Fotografías del Prototipo

Agrega aquí tus imágenes con la siguiente sintaxis:

```
![Encoder del péndulo]({{ '/assets/img/encoder_pendulo.jpg' | relative_url }})
```

> **Nota:** Sube tus imágenes a la carpeta `assets/img/` del repositorio.

---

[&larr; Inicio]({{ '/' | relative_url }}) &nbsp;&nbsp; [Electrónica &rarr;]({{ '/hardware/electronica/' | relative_url }}){: .btn .btn-outline }

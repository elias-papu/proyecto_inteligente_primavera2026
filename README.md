# Péndulo Invertido — Deep Q-Learning (Sim-to-Real)

Control Inteligente · Primavera 2026 · Universidad Iberoamericana Ciudad de México

---

## ¿De qué trata?

Diseño, construcción y control de un **péndulo invertido físico** utilizando **Deep Q-Learning (DQN)** como algoritmo de control. El agente aprende a mantener el péndulo en equilibrio en la posición vertical superior únicamente a través de interacción con un entorno de simulación, y la política entrenada se transfiere directamente al hardware real (**Sim-to-Real transfer**).

No se usa control clásico (PID ni lineal). El controlador es una red neuronal profunda que decide la fuerza a aplicar al carro en cada instante.

---

## Resultados

- **4,000 episodios** de entrenamiento en simulación (MATLAB/Simscape)
- **90 % de tasa de éxito** en los últimos 50 episodios
- **14.56 s** de tiempo acumulado en equilibrio en la prueba greedy final
- Reward total de prueba: **71,157.5**

---

## Videos

| # | Descripción | Enlace |
|---|---|---|
| 1 | Péndulo manteniendo el equilibrio durante el entrenamiento | [YouTube Short](https://youtube.com/shorts/zO4dnO2xxjA) |
| 2 | Episodios fallidos — etapa inicial del entrenamiento | [YouTube Short](https://youtube.com/shorts/txFmPXgzE_4) |
| 3 | Timelapse — 4,000 episodios de entrenamiento | [YouTube](https://youtu.be/pEJuTYEiCGU) |
| 4 | Timelapse — el equipo armando el prototipo | [YouTube](https://youtu.be/0icStA-qZcc) |

---

## Estructura del Repositorio

```
├── DQN_pendulo_invertido_sim_v8_1_m.txt   # Código de entrenamiento DQN (MATLAB)
├── niga_code.m                             # Scripts auxiliares MATLAB
├── pendulo_center_FIXED.ino               # Firmware Arduino (control embebido)
└── docs/                                  # Sitio web (GitHub Pages — Just the Docs)
```

---

## Cómo reproducir la simulación

**Dependencias:**
- MATLAB R2023a o superior
- Deep Learning Toolbox
- Reinforcement Learning Toolbox
- Simscape

**Pasos:**
1. Clonar el repositorio
2. Abrir MATLAB y agregar la carpeta al path
3. Ejecutar `DQN_pendulo_invertido_sim_v8_1_m.txt`
4. La red entrenada se guarda en `dqn_net_sim_v8.mat`

---

## Equipo

| Integrante | 
|---|
| Andrick Millán |
| Jesús Velázquez |
| Elías Santiago Jiménez Hernández |

**Profesores:** Dr. Alexandro López · Mtro. Julio Caballero

**Presentado en:**
- Día de las Ingenierías IBERO — 5 de mayo de 2026
- Congreso ITESO Guadalajara 2026 — 26–28 de mayo de 2026
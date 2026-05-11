---
layout: default
title: Arquitectura DQN
parent: Simulación y Entrenamiento
nav_order: 1
permalink: /simulacion/arquitectura/
---

# Arquitectura DQN y Código de Entrenamiento
{: .no_toc }

## Tabla de Contenidos
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Red Neuronal

La red DQN recibe el vector de estado de 4 elementos y produce 41 valores Q (uno por acción discreta):

```
Entrada (4) → [FC 64, ReLU] → [FC 64, ReLU] → Salida Q (41)
```

## Hiperparámetros de Entrenamiento

| Hiperparámetro | Valor |
|---|---|
| Episodios totales | 4,000 |
| Pasos máx. por episodio | 600 |
| Replay buffer | Experience replay |
| Optimizador | Adam |
| Exploración (ε-greedy) | Decaimiento configurado |
| Neuronas por capa | 64 |
| Capas ocultas | 2 |

## Función de Recompensa

$$r_t = -(w_1\theta^2 + w_2\dot{\theta}^2 + w_3 u^2)$$

Los pesos $$w_1, w_2, w_3$$ se calibraron experimentalmente para priorizar la estabilidad angular sobre la posición del carro y minimizar el esfuerzo de control.

## Fragmento del Código MATLAB (entrenamiento)

El archivo completo está en `DQN_pendulo_invertido_sim_v8_1_m.txt`.

{% highlight matlab %}
% Ciclo principal de entrenamiento DQN
for episodio = 1:NUM_EPISODIOS
    s = reset(env);
    recompensa_total = 0;

    for t = 1:MAX_PASOS
        % Política epsilon-greedy
        if rand() < epsilon
            a = randi(NUM_ACCIONES);          % exploración
        else
            Q_vals = forward(dqn_net, s);
            [~, a] = max(Q_vals);             % explotación
        end

        % Ejecutar acción en el entorno
        [s_next, r, terminado] = step(env, acciones(a));

        % Guardar en replay buffer
        buffer.push(s, a, r, s_next, terminado);

        % Actualizar red si hay suficientes muestras
        if buffer.size >= BATCH_SIZE
            actualizar_dqn(dqn_net, buffer, gamma, optimizer);
        end

        s = s_next;
        recompensa_total = recompensa_total + r;
        if terminado, break; end
    end

    % Decaer epsilon
    epsilon = max(EPSILON_MIN, epsilon * EPSILON_DECAY);
end
{% endhighlight %}

## Cómo Reproducir el Entrenamiento

**Dependencias:**
- MATLAB R2023a o superior
- Toolbox: Deep Learning Toolbox, Reinforcement Learning Toolbox, Simscape

**Pasos:**

1. Clonar el repositorio.
2. Abrir MATLAB y agregar la carpeta al path.
3. Ejecutar el script principal:

{% highlight matlab %}
run('DQN_pendulo_invertido_sim_v8_1_m.txt')
{% endhighlight %}

4. La red entrenada se guarda automáticamente en `dqn_net_sim_v8.mat`.

---

[&larr; Simulación]({{ '/simulacion/' | relative_url }}) &nbsp;&nbsp; [Implementación Física &rarr;]({{ '/implementacion/' | relative_url }}){: .btn .btn-outline }

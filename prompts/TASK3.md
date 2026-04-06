# Task 3: Incertidumbre y Latencia (Expectiminimax y MDPs)

**Fase 3 del Proyecto - Continuación de Task 2**

---

## Contexto: El Mundo Real Tiene Fallos

En **Task 2** construiste un sistema de defensa usando Minimax, asumiendo que todas las acciones tenían éxito garantizado (mundo determinista).

**Ahora en Task 3:** El mundo real introduce **incertidumbre**. La red experimenta latencia, y cada intento de capturar un nodo tiene:
- **80% de probabilidad:** Éxito (se captura el nodo)
- **20% de probabilidad:** Fallo (se pierden el turno sin capturar nada)

Esta incertidumbre cambia fundamentalmente la estrategia óptima. Debes usar **Expectiminimax** (una extensión de Minimax que maneja probabilidades).

---

## Lo que Necesito Implementar

### 1. Expectiminimax: Manejo de Incertidumbre

**Concepto clave:** Después de cada movimiento de un jugador, introduce un **"nodo de azar"** que representa:
- 80% → Acción exitosa (captura el nodo)
- 20% → Acción falla (se pierden el turno)

**Estructura del árbol:**
```
[MAX] → Intenta capturar nodo A
  ↓
[AZAR] → 80% éxito, 20% fallo
  ↙          ↘
[MIN]      [MIN]  (mismo estado si fallo)
```

**Implementar:**
- Función `expectiminimax(state, depth)` que maneje nodos MAX, MIN y AZAR
- En nodos AZAR: retorna valor esperado = 0.8*valor_éxito + 0.2*valor_fallo
- Misma profundidad que Task 2 (depth_max = 4)
- Usa la misma función Eval(s) de Task 2

### 2. Análisis Comparativo: El Valor de la Información Estocástica

**Experimento:**

a) **Agente Minimax Tradicional** (Task 2) que asume determinismo
   - Juega en mundo CON 20% de fallo
   - No entiende la probabilidad
   - Toma decisiones como si todo fuera 100% exitoso

b) **Agente Expectiminimax** (Task 3) que entiende el riesgo
   - Juega en MISMO mundo CON 20% de fallo
   - Modela explícitamente la probabilidad
   - Toma decisiones considerando el riesgo

c) **Ambos juegan contra un Agente Aleatorio** (10 partidas cada uno)

**Compara:**
- Valor final promedio (nodos capturados × su valor)
- Varianza/Desviación estándar
- Agresividad: % de movimientos "riesgosos"
- Tasa de éxito en captura: % de intentos que lograron capturar

**Crea tabla comparativa:**

```
┌─────────────────────────────────────────────┐
│  MINIMAX vs EXPECTIMINIMAX en Incertidumbre │
├──────────────────────┬──────────┬───────────┤
│ Métrica              │ Minimax  │ Expectim. │
├──────────────────────┼──────────┼───────────┤
│ Valor Final Promedio │  +380    │  +420     │
│ Desv. Estándar       │  ±85     │  ±45      │
│ % Movs. Riesgosos    │  68%     │  42%      │
│ Tasa de Éxito        │  67%     │  72%      │
└──────────────────────┴──────────┴───────────┘
```

**Analiza:**
- ¿Es Minimax más agresivo o conservador?
- ¿Cuál tiene mejor desempeño?
- ¿Cuál es más robusto (menor varianza)?
- **Explica por qué:** Expectiminimax modela el riesgo explícitamente

### 3. Reflexión Teórica: Modelado con MDPs

**Pregunta hipotética (SIN IMPLEMENTACIÓN):**

Si el juego NO tuviera oponente (MIN), solo tú capturando nodos con:
- 80% de éxito, 20% de fallo
- Costo: -1 por turno (presión para terminar rápido)
- Objetivo: Maximizar valor controlado

**¿Cómo lo modelarías como Markov Decision Process (MDP)?**

Formular la **Ecuación de Bellman** V(s):

```
V(s) = max {
  0,  # Opción: Parar
  
  max_n [
    0.8 * (valor(n) - 1 + γ * V(s ∪ {n})) +  # 80% éxito
    0.2 * (-1 + γ * V(s))                      # 20% fallo
  ]
}
```

**Explica cada componente:**
- Por qué 0.8 y 0.2
- Qué representa V(s)
- Por qué el costo -1 por turno
- Cómo γ (factor de descuento) afecta la estrategia

---

## Requisitos Técnicos

- **Formato:** Jupyter Notebook
- **Librerías:** NumPy, matplotlib, networkx (como antes)
- **Sin librerías especializadas:** Implementar Expectiminimax desde cero
- **Memoización:** Crucial para eficiencia (los árboles son grandes)

## Estructura Esperada (16 celdas)

```
1. Imports
2. Contexto Task 3 (markdown)
3. Grafo y valores (reutilizar de Task 2)
4. GameState extendida (soportar nodos AZAR)
5. Agente Minimax (de Task 2)
6. Función Expectiminimax
7. Agente Expectiminimax
8. Agente Aleatorio (baseline)
9. Función para simular juegos
10. Ejecutar: Minimax vs Random (10 juegos)
11. Ejecutar: Expectiminimax vs Random (10 juegos)
12. Tabla comparativa
13. Gráficos (valor, varianza, agresividad)
14. Análisis: Diferencias de comportamiento
15. Reflexión: Ecuación de Bellman para MDP (markdown)
16. Conclusiones
```

## Output Esperado

1. **Tabla comparativa** mostrando diferencias clave
2. **Gráficos** comparativos (barras, líneas de tendencia)
3. **Análisis cualitativo** explicando por qué Expectiminimax y Minimax actúan diferente
4. **Ecuación de Bellman** correctamente formulada
5. **Reflexión** conectando incertidumbre, decisiones y MDPs

---

## Conceptos Clave

**Expectiminimax:**
   - Extensión de Minimax que maneja probabilidades
   - Cada movimiento genera nodo de azar con distribución de probabilidad
   - En nodos de azar: retorna valor esperado (suma ponderada)

**Incertidumbre Estocástica:**
   - Las acciones no siempre tienen el resultado esperado
   - Requiere modelar explícitamente probabilidades
   - Cambia decisiones: conservadurismo vs. agresividad

**MDP (Markov Decision Process):**
   - Framework para decisiones secuenciales bajo incertidumbre
   - Ecuación de Bellman: V(s) = max_a [R(s,a) + γ ΣP(s'|s,a)V(s')]
   - Fundamental en Reinforcement Learning

---

**Consulta también:**
- TASK2.md (para referencia sobre Minimax)
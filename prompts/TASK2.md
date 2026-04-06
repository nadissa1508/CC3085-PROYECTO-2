# Task 2: Defensa Adversarial (Juegos de Suma Cero)

**Fase 2 del Proyecto - Continuación de Task 1**

---

## Contexto: Continuando desde Task 1

En **Task 1** implementaste un solver CSP para configurar la red de servidores con protocolos de seguridad respetando restricciones.

**Ahora en Task 2:** La red está configurada y operativa, pero un **atacante ha penetrado el sistema**. 

Es hora de **defender** la red usando una IA que juega adversarialmente contra el atacante.

---

## El Problema

Mi red de ciberseguridad ha sido penetrada por un atacante. Ahora es un juego por turnos donde:
- **YO (MAX):** Defensa - busco maximizar mi control de valor
- **HACKER (MIN):** Atacante - busca minimizar mi control

**Mecánica:** Por turno, cada jugador captura un nodo adyacente a los que ya controla.
**Valores:** Cada nodo tiene un valor aleatorio (1-100). El objetivo es controlar nodos de alto valor.
**Terminación:** Cuando todos los nodos se capturan o se alcanza límite de turnos.

## Lo que Necesito Implementar

### 1. Minimax Puro
- Implementar algoritmo Minimax sin optimizaciones
- Permitir profundidad limitada (ej. depth_max=4)
- Contar nodos expandidos
- Retornar: valor minimax y mejor movimiento

### 2. Función de Evaluación Heurística Eval(s)
- Como no puedo llegar a nodos terminales, necesito una función que **estime** el valor de un estado
- Opciones:
  - **Simple:** Valor controlado (max_value - min_value)
  - **Intermedia:** Valor + Movilidad (# de movimientos posibles)
  - **Avanzada:** Valor + Movilidad + Potencial futuro
- Debo justificar matemáticamente por qué es una buena aproximación

### 3. Poda Alfa-Beta
- Implementar optimización de Minimax
- Usar parámetros alfa y beta
- Podar ramas cuando `alpha >= beta` (MAX) o `beta <= alpha` (MIN)
- Debe encontrar el MISMO movimiento óptimo que Minimax puro
- Contar nodos podados vs. expandidos

### 4. Análisis Comparativo
- Ejecutar ambos algoritmos sobre el mismo estado
- Comparar:
  - Nodos expandidos (esperado: ~70-80% reducción con AB)
  - Tiempo de ejecución
  - Movimiento elegido (debe ser igual)
  - Valor minimax (debe ser igual)
- Crear tabla comparativa
- Generar gráficos

## Requisitos Técnicos

- **Formato:** Jupyter Notebook
- **No usar:** Librerías de juegos especializadas
- **Librerías permitidas:** NumPy, matplotlib, networkx
- **Implementar DESDE CERO:** Minimax, Alfa-Beta, Eval

## Estructura Esperada (14 celdas)

```
1. Imports y Setup
2. Contexto del Juego (markdown explicativo)
3. Generar Grafo + Valores Aleatorios
4. Clase GameState
5. Función Minimax Puro
6. Función Eval(s) - Heurística
7. Función Alfa-Beta
8. Función para contar nodos
9. Ejecutar Minimax Puro (medir tiempo y nodos)
10. Ejecutar Alfa-Beta (medir tiempo y nodos)
11. Tabla Comparativa
12. Gráficos Comparativos (nodos, tiempo)
13. Análisis Matemático de Eval(s)
14. Conclusiones
```

## Output Esperado

1. **Implementación correcta:** Minimax y Alfa-Beta encontran el MISMO movimiento óptimo
2. **Mejora de rendimiento:** Alfa-Beta debe ser 70-80% más rápido y expandir 70-80% menos nodos
3. **Función Eval(s) justificada:** Explicación matemática clara de por qué es buena aproximación
4. **Tabla y gráficos:** Comparación visual de métricas
5. **Código limpio:** Bien documentado y modular

## Tips

- Usar profundidad máxima: depth_max = 4
- Ordenar movimientos por valor descendente para mejorar poda Alfa-Beta
- Validar que ambos algoritmos encuentren el mismo movimiento
- Implementar contadores globales para nodos expandidos/podados
- Usar memoización para optimizar si es necesario

## Conceptos Clave

**Minimax:** Búsqueda en árbol alternando maximizador (yo) y minimizador (atacante)
**Alfa-Beta:** Optimización que poda ramas que no pueden afectar resultado final
**Eval(s):** Función heurística que estima valor de estado sin alcanzar terminal
**Factor de Ramificación:** Número de movimientos posibles (típicamente 2-6 en este juego)

---

**Consulta también:**
- TASK1.md (para referencias sobre el Grafo)
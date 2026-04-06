# Task 1: CSP y Coloración de Grafos

Estoy trabajando en un proyecto de Inteligencia Artificial sobre ciberseguridad. Mi tarea es resolver un **Constraint Satisfaction Problem (CSP)** de coloración de grafos usando un algoritmo de Backtracking optimizado.

## El Problema

Tengo una red de 15-20 servidores (un grafo) y necesito asignar uno de 4 protocolos de seguridad (Rojo, Verde, Azul, Amarillo) a cada servidor. **Restricción:** Ningún par de servidores conectados directamente puede tener el mismo protocolo.

## Lo que Necesito Implementar (en Jupyter Notebook)

### 1. Modelado Formal (Celda Markdown)
- Definición formal de Variables, Dominios y Restricciones
- Descripción de cómo se modela como CSP
- Descripción del Factor Graph

### 2. Tres Implementaciones del Algoritmo

**Versión 1: Backtracking Puro**
- Backtracking Search básico sin optimizaciones
- Selección secuencial de variables
- Debe contar asignaciones intentadas y backtracks

**Versión 2: Backtracking + Forward Checking (Lookahead)**
- Implementa Forward Checking para eliminar dominios inconsistentes
- Mantén la selección secuencial de variables
- Debe reducir significativamente el número de asignaciones

**Versión 3: Backtracking + Forward Checking + MCV**
- Implementa heurística MCV (Minimum Remaining Values)
- Selecciona la variable sin asignar con el dominio más pequeño
- Debe ser mucho más rápido que las anteriores

### 3. Análisis Comparativo
- Ejecuta los 3 algoritmos sobre el mismo grafo
- Mide: tiempo de ejecución (ms), número de asignaciones, número de backtracks
- Crea una tabla comparativa
- Crea gráficos de barra comparando tiempo y asignaciones
- Análisis: ¿Cuál es más efectiva? ¿Por qué?

### 4. Visualización
- Dibuja el grafo original
- Dibuja el grafo con la solución (nodos coloreados)

## Requisitos Técnicos

- **No usar librerías especializadas de CSP** (como python-constraint)
- **Librerías permitidas:** NumPy, matplotlib, NetworkX (solo para generar y visualizar el grafo, no para resolverlo)
- Implementar TODO desde cero según los algoritmos de CSP
- Código bien documentado y modular

## Estructura Esperada del Notebook

```
1. Imports y Setup
2. Modelado Formal (Markdown + pseudocódigo)
3. Generación del Grafo Aleatorio (15-20 nodos)
4. Clase CSP (para almacenar variables, dominios, restricciones)
5. Backtracking Puro (implementación + ejecución)
6. Forward Checking (implementación + ejecución)
7. MCV Heurística (implementación + ejecución)
8. Backtracking Optimizado (integración de FC + MCV + ejecución)
9. Comparación de Métricas (tabla + gráficos)
10. Visualización de Solución
11. Conclusiones y Análisis
```

## Output Esperado

- Solución válida: Un diccionario {servidor: protocolo} que satisface todas las restricciones
- Validación: Verificar que ningún par de servidores adyacentes tengan el mismo protocolo
- Tabla de comparación mostrando mejora de rendimiento
- Gráficos de comparación
- Grafo coloreado como visualización final

---
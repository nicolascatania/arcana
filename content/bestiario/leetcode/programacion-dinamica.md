# Programación Dinámica

## Técnicas utilizadas

* Programación Dinámica (Bottom-Up)
* Subproblemas superpuestos
* Optimización de decisiones locales

En lugar de avanzar desde el inicio, resolvemos los subproblemas desde el final hacia el principio.

`dp[i][j]` representa la **mínima vida necesaria para llegar al destino** comenzando desde la celda `(i, j)`.

### Relación de recurrencia

```text
dp[i][j] = max(1, min(dp[i+1][j], dp[i][j+1]) - dungeon[i][j])
```

## Código

```python
def calculateMinimumHP(dungeon):
    m, n = len(dungeon), len(dungeon[0])

    dp = [[0] * n for _ in range(m)]

    # Caso base
    dp[m-1][n-1] = max(1, 1 - dungeon[m-1][n-1])

    # Última fila
    for j in range(n-2, -1, -1):
        dp[m-1][j] = max(1, dp[m-1][j+1] - dungeon[m-1][j])

    # Última columna
    for i in range(m-2, -1, -1):
        dp[i][n-1] = max(1, dp[i+1][n-1] - dungeon[i][n-1])

    # Resto de la matriz
    for i in range(m-2, -1, -1):
        for j in range(n-2, -1, -1):
            need = min(dp[i+1][j], dp[i][j+1])
            dp[i][j] = max(1, need - dungeon[i][j])

    return dp[0][0]
```

## Traza de ejemplo

### Entrada

```text
  [-2, -3,  3]
  [-5,-10,  1]
  [10, 30, -5]
```

### Construcción de `dp`

```text
    [7,   5,   2]
    [6,  11,   5]
    [1,   1,   6]
```

### Resultado

```text
dp[0][0] = 7
```

## Complejidad

* **Tiempo:** `O(m × n)`
* **Espacio:** `O(m × n)`

### Posible optimización

Reducir el espacio a **`O(n)`** utilizando un arreglo unidimensional en lugar de una matriz completa.

## Cuándo usar esta técnica

* Existen subproblemas repetidos.
* Se requiere obtener la solución óptima de manera eficiente.
* Es posible construir la solución a partir de resultados previamente calculados.

## Ventajas

* Garantiza una solución óptima.
* Evita cálculos redundantes.
* Escala mucho mejor que una solución recursiva por fuerza bruta.

## Comparación

La programación dinámica reduce la complejidad de un algoritmo exponencial a una complejidad polinomial al almacenar y reutilizar los resultados de los subproblemas.

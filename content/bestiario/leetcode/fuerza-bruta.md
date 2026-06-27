# Fuerza Bruta

## Técnicas utilizadas

* Fuerza Bruta
* Recursividad
* Exploración exhaustiva

La idea consiste en generar **todos los caminos posibles** desde `(0,0)` hasta `(m-1,n-1)`.

Para cada camino se:

* Simula la evolución de la vida del caballero.
* Calcula la vida inicial mínima necesaria para sobrevivir ese recorrido.

Finalmente, se selecciona el menor valor obtenido entre todos los caminos.

## Código

```python
def vida_minima_inicial(mazmorra):
    filas, columnas = len(mazmorra), len(mazmorra[0])

    def dfs(fila, columna, camino):
        camino.append(mazmorra[fila][columna])

        if fila == filas - 1 and columna == columnas - 1:
            return [camino.copy()]

        caminos = []

        if fila + 1 < filas:
            caminos += dfs(fila + 1, columna, camino)

        if columna + 1 < columnas:
            caminos += dfs(fila, columna + 1, camino)

        camino.pop()
        return caminos

    def vida_requerida(camino):
        vida_inicial = 1
        vida_actual = 1

        for valor in camino:
            vida_actual += valor

            if vida_actual <= 0:
                vida_inicial += (1 - vida_actual)
                vida_actual = 1

        return vida_inicial

    todos_los_caminos = dfs(0, 0, [])
    return min(vida_requerida(camino) for camino in todos_los_caminos)
```

## Ejemplo de exploración

### Entrada

```text
  [-2, -3]
  [-5,-10]
```

### Caminos posibles

```text
Derecha → Abajo
[-2, -3, -10]

Abajo → Derecha
[-2, -5, -10]
```

Se calcula la vida mínima necesaria para cada recorrido y se devuelve el menor resultado.

## Complejidad

* **Tiempo:** `O(2^(m+n))`
* **Espacio:** `O(m+n)`

## Justificación

El algoritmo explora todos los caminos posibles desde el inicio hasta el destino.

Como en cada posición pueden existir hasta dos decisiones (derecha o abajo), la cantidad de caminos crece exponencialmente con el tamaño de la matriz.

## Cuándo usar esta técnica

* El tamaño de la entrada es pequeño.
* Se busca una implementación sencilla.
* Se utiliza como solución base para comparar algoritmos más eficientes.

## Ventajas

* Muy fácil de implementar y comprender.
* Garantiza encontrar la solución óptima al evaluar todos los caminos.

## Comparación

Aunque garantiza la solución correcta, resulta mucho menos eficiente que Programación Dinámica o Branch & Bound debido a que explora exhaustivamente todos los recorridos posibles.

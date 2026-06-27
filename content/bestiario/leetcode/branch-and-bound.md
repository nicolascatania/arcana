# Branch & Bound

## Técnicas utilizadas

* Branch & Bound
* Backtracking con poda
* Exploración de un árbol de búsqueda

Esta técnica recorre el espacio de soluciones mediante un árbol de búsqueda, evitando explorar ramas que no pueden mejorar la mejor solución encontrada hasta el momento.

A diferencia de la fuerza bruta, se aplican **podas** para descartar caminos claramente subóptimos.

## Idea del algoritmo

El objetivo es recorrer todos los caminos posibles desde `(0,0)` hasta `(m-1,n-1)`.

Durante la exploración se mantiene:

* La vida actual del personaje.
* La vida mínima necesaria para haber llegado hasta ese punto.

### Criterio de poda

Si la vida mínima requerida acumulada es **mayor o igual** que la mejor solución encontrada hasta el momento, esa rama se descarta y no continúa explorándose.

```text
Si min_health_needed >= best:
    Se poda la rama.
```

## Código

```python
def dungeon_bb(dungeon):
    m, n = len(dungeon), len(dungeon[0])
    best = float('inf')

    def dfs(i, j, current_health, min_health_needed):
        nonlocal best

        # Actualizar salud actual
        current_health += dungeon[i][j]

        # Si la salud baja a 0 o menos, ajustar la vida necesaria
        if current_health <= 0:
            min_health_needed += (1 - current_health)
            current_health = 1

        # Poda
        if min_health_needed >= best:
            return

        # Llegó al destino
        if i == m - 1 and j == n - 1:
            best = min(best, min_health_needed)
            return

        # Explorar abajo
        if i + 1 < m:
            dfs(i + 1, j, current_health, min_health_needed)

        # Explorar derecha
        if j + 1 < n:
            dfs(i, j + 1, current_health, min_health_needed)

    dfs(0, 0, 1, 1)
    return best
```

## Ejemplo de exploración

Supongamos dos caminos posibles:

**Camino 1:** Derecha → Abajo

```text
Vida inicial: 1
↓
La salud cae por debajo de 1
↓
Se ajusta la vida mínima requerida
↓
Vida necesaria = 6
```

**Camino 2:** Abajo → Derecha

```text
Vida necesaria = 8
```

Como ya existe una solución que requiere **6** puntos de vida inicial, cualquier rama que durante la exploración necesite **6 o más** se descarta inmediatamente.

## Complejidad

* **Peor caso:** `O(2^(m+n))`
* **Caso promedio:** significativamente menor gracias a las podas (depende de la instancia).
* **Espacio:** `O(m+n)` debido a la profundidad máxima de la recursión.

## Justificación

* Sin podas, el algoritmo equivale a una búsqueda exhaustiva (fuerza bruta).
* Con podas, se evita recorrer una gran cantidad de caminos que no pueden producir una mejor solución.

## Cuándo usar esta técnica

* El espacio de soluciones es muy grande.
* Es posible definir una cota (*bound*) para descartar soluciones.
* Se busca mejorar el rendimiento de una búsqueda exhaustiva sin modificar completamente el enfoque del algoritmo.

## Ventajas

* Reduce considerablemente la cantidad de caminos explorados.
* Mantiene una implementación relativamente sencilla.
* Siempre encuentra la solución óptima si la función de poda es correcta.

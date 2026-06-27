# Dungeon Game (LeetCode #174)

Los demonios han capturado a la princesa y la han encerrado en la esquina inferior derecha de una mazmorra representada por una matriz bidimensional.

Un caballero comienza en la celda superior izquierda `(0,0)` y debe rescatarla.

## Reglas del problema

El caballero:

* Comienza con una cantidad inicial de vida (entero positivo).
* Muere si su vida llega a **0 o menos** en cualquier momento.
* Solo puede moverse **hacia la derecha** o **hacia abajo**.

Cada celda de la mazmorra contiene uno de los siguientes valores:

* Un número negativo: el caballero pierde vida.
* Cero: no ocurre ningún efecto.
* Un número positivo: el caballero recupera vida.

## Objetivo

Calcular la **mínima vida inicial** necesaria para que el caballero llegue hasta la princesa con vida.

[**Enlace del problema:** ](https://leetcode.com/problems/dungeon-game/)

---

## Intuición

Este problema no es trivial porque:

* No basta con minimizar el daño recibido.
* Tampoco alcanza con maximizar la cantidad de vida recuperada.
* Es necesario garantizar que el caballero sobreviva **en cada paso del recorrido**.
* Una decisión que parece óptima localmente puede conducir a una solución global peor.

La idea fundamental consiste en analizar el problema **desde el destino hacia el inicio**, determinando cuánta vida es necesaria para poder llegar con éxito hasta la princesa.

---

## Definición formal

### Entrada

Una matriz `dungeon[m][n]`, donde cada celda representa el efecto sobre la vida del caballero.

### Salida

Un entero que representa la **mínima vida inicial** necesaria para completar el recorrido.

### Restricciones

* `1 ≤ m, n ≤ 200`
* `-1000 ≤ dungeon[i][j] ≤ 1000`

---

## Ejemplo

### Entrada

```text
  [-2, -3,  3]
  [-5,-10,  1]
  [10, 30, -5]
```

### Salida

```text
7
```

### Camino óptimo

```text
Derecha → Derecha → Abajo → Abajo
```

---

## Ideas clave

* Pensar el problema desde el final hacia el principio.
* En cada celda responder la siguiente pregunta:
* ¿Cuál es la mínima cantidad de vida que necesito para poder llegar desde aquí hasta el destino?
* La vida del caballero nunca puede ser menor que **1**.

---

## Soluciones implementadas

* `fuerza-bruta.md`
* `branch-and-bound.md`
* `programacion-dinamica.md`

Dungeon Game (Leetcode #174)

Los demonios han capturado a la princesa y la han encerrado en la esquina inferior derecha de una mazmorra representada como una matriz 2D.

Un caballero comienza en la celda superior izquierda `(0,0)` y debe rescatarla.

El caballero:

- Tiene una cantidad inicial de vida (entero positivo)
- Muere si su vida llega a 0 o menos en cualquier momento
- Puede moverse únicamente hacia la **derecha** o hacia **abajo**

Cada celda de la mazmorra contiene:

- Un número negativo: pierde vida
- Cero: sin efecto
- Un número positivo: gana vida

El objetivo es calcular la **mínima vida inicial necesaria** para que el caballero llegue a la princesa con vida.

Enlace original: https://leetcode.com/problems/dungeon-game/

---

## Intuición

El problema es no trivial porque:

- No alcanza con minimizar daño o maximizar curación
- Hay que garantizar sobrevivir **en cada paso**
- La mejor decisión local puede llevar a una peor solución global

La clave es pensar el problema **al revés**, desde el destino hacia el inicio.

---

## Definición formal

Entrada

- Matriz `dungeon[m][n]`

Salida

- Entero: mínima vida inicial requerida

Restricciones

- 1 ≤ m, n ≤ 200
- -1000 ≤ dungeon[i][j] ≤ 1000

---

## Ejemplo concreto

[[-2, -3,  3],
[-5, -10, 1],
[10, 30, -5]]

Salida:
7

Explicación:
El camino óptimo es:

RIGHT → RIGHT → DOWN → DOWN

Ideas clave:

- Pensar desde el final hacia atrás
- En cada celda preguntarse:  
  ¿Cuánta vida necesito para sobrevivir desde acá hasta el final?”
- La vida mínima siempre debe ser al menos 1

## Soluciones disponibles

fuerza-bruta.md
programacion-dinamica.md
branch-and-bound.md

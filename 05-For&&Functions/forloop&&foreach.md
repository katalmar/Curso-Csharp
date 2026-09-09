# El `for` loop — repitiendo acciones para construir dibujos

## ¿Qué es un `for` loop?

Un **`for`** es una estructura que le dice al programa: *"repite esta acción una cantidad exacta de veces"*. En vez de escribir la misma línea de código 20 veces a mano, el `for` lo hace por nosotros usando un **contador**.

```csharp
for (int i = 0; i < 5; i++)
{
    Console.WriteLine("Hola");
}
```

Esto imprime "Hola" **5 veces**. El `for` tiene tres partes, separadas por `;`:

| Parte | Qué hace | En el ejemplo |
|---|---|---|
| **Inicialización** | Crea el contador y le da un valor inicial | `int i = 0` |
| **Condición** | Mientras esto sea `true`, el loop sigue repitiendo | `i < 5` |
| **Incremento** | Qué le pasa al contador después de cada repetición | `i++` (le suma 1) |

> 🔑 El contador `i` empieza en `0`, y el loop se repite mientras `i` sea menor que `5` → se ejecuta cuando `i` vale `0, 1, 2, 3, 4` → **5 veces en total**. Esta es la razón por la que en programación casi todo empieza a contar desde 0 (recuerden los arrays de la clase pasada).

El `for` es ideal cuando **ya sabemos cuántas veces** queremos repetir algo — como dibujar una fila de 24 símbolos `#`, en vez de escribir `#` veinticuatro veces a mano.

---

## Paso 1: una línea sencilla, todo el mismo carácter

Antes de armar el dibujo completo, empecemos por lo más simple: una fila hecha solo de `#`, como la pared superior de nuestro mapa.

```csharp
string linea = "";                 // empezamos con un string vacío

for (int i = 0; i < 24; i++)
{
    linea += "#";                  // en cada vuelta, le agregamos un "#" al string
}

Console.WriteLine(linea);
```

`linea += "#"` significa *"toma lo que ya tenía `linea` y agrégale un `#` al final"*. Después de 24 vueltas, `linea` contiene: `########################` — exactamente lo que antes escribíamos a mano con `Console.WriteLine("########################");`.

---

## Paso 2: una línea con varios segmentos distintos

Ahora el reto real: la línea `#.............#####....#`. Esta línea **no es un solo carácter repetido**, sino varios "bloques" que se van agregando uno después del otro al mismo string:

```
#   .............   #####   ....   #
1        13           5       4    1
```

La estrategia es la misma que en el Paso 1, pero encadenando **varios `for` (y algunos caracteres sueltos) uno detrás del otro**, todos escribiendo sobre la misma variable:

```csharp
string linea = "";

linea += "#";                          // el primer "#", va solo, no necesita loop

for (int i = 0; i < 13; i++)           // bloque de 13 puntos
{
    linea += ".";
}

for (int i = 0; i < 5; i++)            // bloque de 5 numerales (el "cuartito")
{
    linea += "#";
}

for (int i = 0; i < 4; i++)            // bloque de 4 puntos
{
    linea += ".";
}

linea += "#";                          // el último "#", va solo

Console.WriteLine(linea);              // Imprime: #.............#####....#
```

Cada `for` es responsable de **un solo tipo de bloque** dentro de la línea. Así, en vez de contar y escribir 24 caracteres a mano, solo necesitamos saber **qué símbolo va y cuántas veces se repite** en cada segmento — el `for` hace el resto.

---

## Paso 3: guardando cada línea en un array, e imprimiendo todo junto

Ya sabemos construir una línea con `for`. Ahora armemos el mapa completo: cada línea que construyamos se guarda en una posición de un **array de strings**, y al final las imprimimos todas.

```csharp
string[] mapa = new string[12]; // el mapa tiene 12 filas (tamaño fijo, como aprendimos)

// Fila 0: la pared superior, todo "#"
string fila0 = "";
for (int i = 0; i < 24; i++) fila0 += "#";
mapa[0] = fila0;

// Fila 2: piso con el jugador "@"
string fila2 = "#";
for (int i = 0; i < 3; i++)  fila2 += ".";
fila2 += "@";
for (int i = 0; i < 19; i++) fila2 += ".";
fila2 += "#";
mapa[2] = fila2;

// Fila 6: piso con el cuartito de "#####"
string fila6 = "#";
for (int i = 0; i < 13; i++) fila6 += ".";
for (int i = 0; i < 5; i++)  fila6 += "#";
for (int i = 0; i < 4; i++)  fila6 += ".";
fila6 += "#";
mapa[6] = fila6;

// Fila 11: la pared inferior, todo "#"
string fila11 = "";
for (int i = 0; i < 24; i++) fila11 += "#";
mapa[11] = fila11;

// ... y así se construyen y guardan las demás filas del mapa

foreach (string filaDelMapa in mapa)
{
    Console.WriteLine(filaDelMapa);
}
```

Cada fila terminada se guarda en su posición correspondiente del array `mapa` (`mapa[0]`, `mapa[2]`, `mapa[6]`, etc.), tal como aprendimos con arrays: **tamaño fijo, cada posición accesible por índice**.

---

## ¿Y qué es ese `foreach` del final?

El `foreach` es otro tipo de loop, pero más simple que el `for`: en vez de usar un contador (`i`) y decirle exactamente cuántas veces repetir, el `foreach` simplemente dice *"recorre este array (u otra colección), elemento por elemento, del primero al último, y hazme algo con cada uno"*.

```csharp
foreach (string filaDelMapa in mapa)
{
    Console.WriteLine(filaDelMapa);
}
```

Esto se lee como: *"para cada string dentro del array `mapa`, llámalo `filaDelMapa` y haz `Console.WriteLine` con él"*. El `foreach` va recorriendo automáticamente todas las posiciones del array (`mapa[0]`, `mapa[1]`, `mapa[2]`... hasta la última), sin que nosotros tengamos que escribir la condición ni el incremento como en un `for`.

> 🔑 Diferencia clave:
> - **`for`** → lo usamos cuando queremos controlar exactamente cuántas repeticiones queremos (o necesitamos el número de la posición, el índice).
> - **`foreach`** → lo usamos cuando solo queremos "visitar" cada elemento de una colección (como un array), sin importarnos su posición ni tener que calcular cuántos elementos hay.

Por eso, en este ejemplo, usamos `for` para **construir** cada línea del dibujo (porque necesitábamos contar cuántos símbolos repetir), y usamos `foreach` para **imprimir** el resultado final (porque ahí solo queríamos recorrer todas las filas ya armadas, una por una).

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

## Paso 2: una línea con varios segmentos — `for` dentro de otro `for`

Ahora el reto real: la línea `#.............#####....#`. Esta línea no es un solo carácter repetido, sino varios **segmentos** que se repiten:

```
#   .............   #####   ....   #
1        13           5       4    1
```

Cada segmento tiene dos datos: **qué símbolo es** y **cuántas veces se repite**. Como son varios segmentos, primero los guardamos en dos arrays paralelos (uno con los símbolos, otro con la cantidad de repeticiones de cada uno):

```csharp
char[] simbolos     = { '#', '.', '#', '.', '#' };
int[]  repeticiones = {  1 ,  13,  5 ,  4 ,  1  };
```

`simbolos[0]` va con `repeticiones[0]`, `simbolos[1]` con `repeticiones[1]`, y así sucesivamente — por eso se llaman **arrays paralelos**.

Ahora sí, la parte importante: usamos un `for` **exterior** para recorrer cada segmento, y dentro de él, un `for` **interior** que repite ese símbolo la cantidad de veces indicada:

```csharp
string linea = "";

for (int s = 0; s < simbolos.Length; s++)          // FOR EXTERIOR: recorre cada segmento
{
    for (int i = 0; i < repeticiones[s]; i++)      // FOR INTERIOR: repite ese símbolo
    {
        linea += simbolos[s];
    }
}

Console.WriteLine(linea);                          // Imprime: #.............#####....#
```

¿Cómo se lee esto paso a paso?

1. El **for exterior** arranca en `s = 0` → mira el segmento 0: símbolo `'#'`, repetido `1` vez.
2. Entra al **for interior**, que se repite `1` vez → agrega un solo `#` a `linea`.
3. El for exterior avanza a `s = 1` → símbolo `'.'`, repetido `13` veces.
4. El for interior ahora se repite `13` veces → agrega 13 puntos seguidos.
5. Así continúa con `s = 2` (`#####`), `s = 3` (`....`) y `s = 4` (`#`), hasta terminar la línea completa.

> 🔑 Este es un **loop anidado** (*nested loop*): un `for` completo viviendo dentro de otro `for`. El exterior controla "en qué segmento vamos", y el interior controla "cuántas veces repetir ese segmento". Cada vez que el exterior avanza una posición, el interior vuelve a arrancar desde cero para el nuevo segmento.

---

## Paso 3: guardando cada línea en un array, e imprimiendo todo junto

Ya sabemos construir cualquier línea con `for` anidados. Ahora armemos el mapa completo: cada línea que construyamos se guarda en una posición de un **array de strings**, y al final las imprimimos todas.

```csharp
string[] mapa = new string[12]; // el mapa tiene 12 filas (tamaño fijo, como aprendimos)

// Fila 0: la pared superior — un solo segmento de 24 "#"
char[] simbolosFila0     = { '#' };
int[]  repeticionesFila0 = {  24 };

string fila0 = "";
for (int s = 0; s < simbolosFila0.Length; s++)
{
    for (int i = 0; i < repeticionesFila0[s]; i++)
    {
        fila0 += simbolosFila0[s];
    }
}
mapa[0] = fila0;

// Fila 6: piso con el "cuartito" — varios segmentos
char[] simbolosFila6     = { '#', '.', '#', '.', '#' };
int[]  repeticionesFila6 = {  1 ,  13,  5 ,  4 ,  1  };

string fila6 = "";
for (int s = 0; s < simbolosFila6.Length; s++)
{
    for (int i = 0; i < repeticionesFila6[s]; i++)
    {
        fila6 += simbolosFila6[s];
    }
}
mapa[6] = fila6;

// ... y así se construyen y guardan las demás filas del mapa, cada una
// con sus propios arrays de símbolos y repeticiones

foreach (string filaDelMapa in mapa)
{
    Console.WriteLine(filaDelMapa);
}
```

Cada fila terminada se guarda en su posición correspondiente del array `mapa` (`mapa[0]`, `mapa[6]`, etc.), tal como aprendimos con arrays: **tamaño fijo, cada posición accesible por índice**. Y como cada línea se arma con la misma técnica de "for exterior + for interior", solo necesitamos cambiar los arrays de `simbolos` y `repeticiones` para dibujar cualquier fila distinta.

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
> - **`for`** → lo usamos cuando queremos controlar exactamente cuántas repeticiones queremos (o necesitamos el número de la posición, el índice). Por eso lo usamos para **construir** cada línea, incluso anidando un `for` dentro de otro cuando había varios segmentos.
> - **`foreach`** → lo usamos cuando solo queremos "visitar" cada elemento de una colección (como un array), sin importarnos su posición ni tener que calcular cuántos elementos hay. Por eso lo usamos al final, solo para **imprimir** todas las filas ya armadas, una por una.

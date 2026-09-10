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

El `for` es ideal cuando **ya sabemos cuántas veces** queremos repetir algo — como dibujar una fila de símbolos repetidos, en vez de escribirlos uno por uno a mano.

---

## El dibujo que vamos a construir

Vamos a usar este mini-dibujo como ejemplo (podría ser la cara de un robot):

```
xxxxxxx
xOxxOx
xx(--)xx
```

Tiene tres líneas, y cada una nos sirve para un nivel distinto de dificultad: la primera es un solo carácter repetido, la segunda tiene varios símbolos distintos, y la tercera tiene incluso más segmentos.

---

## Paso 1: una línea sencilla, todo el mismo carácter

Empezamos por la más simple: `xxxxxxx`, siete `x` seguidas.

```csharp
string linea1 = "";                // empezamos con un string vacío

for (int i = 0; i < 7; i++)
{
    linea1 += "x";                 // en cada vuelta, le agregamos una "x" al string
}

Console.WriteLine(linea1);         // Imprime: xxxxxxx
```

`linea1 += "x"` significa *"toma lo que ya tenía `linea1` y agrégale una `x` al final"*. Después de 7 vueltas, `linea1` contiene: `xxxxxxx`.

---

## Paso 2: una línea con varios segmentos — `for` dentro de otro `for`

Ahora la línea `xOxxOx`. Esta no es un solo carácter repetido, sino varios **segmentos** distintos, uno después del otro:

```
x   O   xx   O   x
1   1    2   1   1
```

Cada segmento tiene dos datos: **qué símbolo es** y **cuántas veces se repite**. Como son varios segmentos, primero los guardamos en dos arrays paralelos (uno con los símbolos, otro con la cantidad de repeticiones de cada uno):

```csharp
char[] simbolos     = { 'x', 'O', 'x', 'O', 'x' };
int[]  repeticiones = {  1 ,  1 ,  2 ,  1 ,  1  };
```

`simbolos[0]` va con `repeticiones[0]`, `simbolos[1]` con `repeticiones[1]`, y así sucesivamente — por eso se llaman **arrays paralelos**.

Ahora sí, la parte importante: usamos un `for` **exterior** para recorrer cada segmento, y dentro de él, un `for` **interior** que repite ese símbolo la cantidad de veces indicada:

```csharp
string linea2 = "";

for (int s = 0; s < simbolos.Length; s++)          // FOR EXTERIOR: recorre cada segmento
{
    for (int i = 0; i < repeticiones[s]; i++)      // FOR INTERIOR: repite ese símbolo
    {
        linea2 += simbolos[s];
    }
}

Console.WriteLine(linea2);                         // Imprime: xOxxOx
```

¿Cómo se lee esto paso a paso?

1. El **for exterior** arranca en `s = 0` → mira el segmento 0: símbolo `'x'`, repetido `1` vez.
2. Entra al **for interior**, que se repite `1` vez → agrega una sola `x` a `linea2`.
3. El for exterior avanza a `s = 1` → símbolo `'O'`, repetido `1` vez → agrega una `O`.
4. El for exterior avanza a `s = 2` → símbolo `'x'`, repetido `2` veces → agrega `xx`.
5. Así continúa con `s = 3` (`O`) y `s = 4` (`x`), hasta terminar la línea completa: `xOxxOx`.

> 🔑 Este es un **loop anidado** (*nested loop*): un `for` completo viviendo dentro de otro `for`. El exterior controla "en qué segmento vamos", y el interior controla "cuántas veces repetir ese segmento". Cada vez que el exterior avanza una posición, el interior vuelve a arrancar desde cero para el nuevo segmento.

---

## Paso 3: guardando cada línea en un array, e imprimiendo todo junto

Ya sabemos construir cualquier línea con `for` anidados. Ahora armemos el dibujo completo: cada línea que construyamos se guarda en una posición de un **array de strings**, y al final las imprimimos todas.

```csharp
string[] dibujo = new string[3]; // el dibujo tiene 3 filas (tamaño fijo)

// Fila 0: "xxxxxxx" — un solo segmento de 7 "x"
char[] simbolosFila0     = { 'x' };
int[]  repeticionesFila0 = {  8  };

string fila0 = "";
for (int s = 0; s < simbolosFila0.Length; s++)
{
    for (int i = 0; i < repeticionesFila0[s]; i++)
    {
        fila0 += simbolosFila0[s];
    }
}
dibujo[0] = fila0;

// Fila 1: "xOxxOx" — varios segmentos
char[] simbolosFila1     = { 'x', 'O', 'x', 'O', 'x' };
int[]  repeticionesFila1 = {  2 ,  1 ,  2 ,  1 ,  2  };

string fila1 = "";
for (int s = 0; s < simbolosFila1.Length; s++)
{
    for (int i = 0; i < repeticionesFila1[s]; i++)
    {
        fila1 += simbolosFila1[s];
    }
}
dibujo[1] = fila1;

// Fila 2: "xx(--)xx" — aún más segmentos
char[] simbolosFila2     = { 'x', '(', '-', ')', 'x' };
int[]  repeticionesFila2 = {  2 ,  1 ,  2 ,  1 ,  2  };

string fila2 = "";
for (int s = 0; s < simbolosFila2.Length; s++)
{
    for (int i = 0; i < repeticionesFila2[s]; i++)
    {
        fila2 += simbolosFila2[s];
    }
}
dibujo[2] = fila2;

foreach (string filaDelDibujo in dibujo)
{
    Console.WriteLine(filaDelDibujo);
}
```

Esto imprime:

```
xxxxxxxx
xxOxxOxx
xx(--)xx
```

Cada fila terminada se guarda en su posición correspondiente del array `dibujo` (`dibujo[0]`, `dibujo[1]`, `dibujo[2]`), tal como aprendimos con arrays: **tamaño fijo, cada posición accesible por índice**. Y como cada línea se arma con la misma técnica de "for exterior + for interior", solo necesitamos cambiar los arrays de `simbolos` y `repeticiones` para dibujar cualquier fila distinta, sin importar cuántos segmentos tenga.

---

## ¿Y qué es ese `foreach` del final?

El `foreach` es otro tipo de loop, pero más simple que el `for`: en vez de usar un contador (`i`) y decirle exactamente cuántas veces repetir, el `foreach` simplemente dice *"recorre este array (u otra colección), elemento por elemento, del primero al último, y hazme algo con cada uno"*.

```csharp
foreach (string filaDelDibujo in dibujo)
{
    Console.WriteLine(filaDelDibujo);
}
```

Esto se lee como: *"para cada string dentro del array `dibujo`, llámalo `filaDelDibujo` y haz `Console.WriteLine` con él"*. El `foreach` va recorriendo automáticamente todas las posiciones del array (`dibujo[0]`, `dibujo[1]`, `dibujo[2]`), sin que nosotros tengamos que escribir la condición ni el incremento como en un `for`.

> 🔑 Diferencia clave:
> - **`for`** → lo usamos cuando queremos controlar exactamente cuántas repeticiones queremos (o necesitamos el número de la posición, el índice). Por eso lo usamos para **construir** cada línea, incluso anidando un `for` dentro de otro cuando había varios segmentos.
> - **`foreach`** → lo usamos cuando solo queremos "visitar" cada elemento de una colección (como un array), sin importarnos su posición ni tener que calcular cuántos elementos hay. Por eso lo usamos al final, solo para **imprimir** todas las filas ya armadas, una por una.

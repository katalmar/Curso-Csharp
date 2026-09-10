# El `while` loop

## ¿Qué es un `while`?

Un **`while`** es otra forma de repetir código, pero más simple que el `for`: solo tiene **una condición**. Mientras esa condición sea `true`, el bloque de código se sigue ejecutando una y otra vez. En el momento en que la condición se vuelve `false`, el loop se detiene.

```csharp
while (condición)
{
    // esto se repite mientras la condición sea true
}
```

A diferencia del `for`, el `while` **no trae integrado** un contador ni un incremento — si necesitamos contar algo, nosotros mismos tenemos que crear la variable **antes** del loop, y actualizarla **dentro** del loop.

```csharp
int i = 0;              // 1. creamos el contador ANTES del while

while (i < 5)            // 2. la condición se revisa antes de cada vuelta
{
    Console.WriteLine("Hola");
    i++;                  // 3. nosotros mismos avanzamos el contador
}
```

Esto imprime "Hola" 5 veces — exactamente lo mismo que el `for` que ya conocemos:

```csharp
for (int i = 0; i < 5; i++)
{
    Console.WriteLine("Hola");
}
```

## `for` vs `while`: la misma idea, escrita distinto

| | `for` | `while` |
|---|---|---|
| Contador | Se declara dentro del propio `for` | Hay que declararlo antes, por fuera |
| Condición | Va integrada en la primera línea | Es lo único que lleva el `while` |
| Incremento | Va integrado en la primera línea (`i++`) | Hay que escribirlo a mano, dentro del bloque |
| ¿Cuándo se revisa la condición? | Antes de cada vuelta | Antes de cada vuelta (igual que el `for`) |

> ⚠️ **El error más común con `while`**: olvidar el `i++` (o cualquier otra forma de actualizar la condición) dentro del bloque. Si la condición nunca cambia, el `while` **nunca termina** — esto se llama un **loop infinito**, y hace que el programa se quede "congelado" repitiendo lo mismo para siempre.

```csharp
int i = 0;
while (i < 5)
{
    Console.WriteLine("Hola");
    // si se nos olvida i++ aquí, este loop jamás termina
}
```

## ¿Cuándo usar `while` en vez de `for`?

El `for` es ideal cuando **sabemos exactamente cuántas veces** queremos repetir algo (por eso lo usamos para repetir símbolos una cantidad exacta de veces). El `while` es más útil cuando **no sabemos de antemano** cuántas repeticiones va a haber, y dependemos de que algo cambie para saber cuándo parar (por ejemplo: "sigue pidiendo la contraseña mientras esté mal", o "sigue jugando mientras la vida sea mayor a 0"). Pero como acabamos de ver, cualquier `for` también se puede reescribir como `while` — es una cuestión de forma, no de qué es capaz de hacer cada uno.

---

## 📝 Ejercicio

Recuerdan el dibujo que hicimos con `for`:

```
xxxxxxxx
xxOxxOxx
xx(--)xx
```

Y el código que usamos, con un `for` **exterior** recorriendo los segmentos y un `for` **interior** repitiendo cada símbolo:

```csharp
char[] simbolos     = { 'x', 'O', 'x', 'O', 'x' };
int[]  repeticiones = {  2 ,  1 ,  2 ,  1 ,  2  };

string linea = "";

for (int s = 0; s < simbolos.Length; s++)
{
    for (int i = 0; i < repeticiones[s]; i++)
    {
        linea += simbolos[s];
    }
}

Console.WriteLine(linea);
```

**Tu misión:** reescribe todo el ejercicio (las tres líneas del dibujo, guardadas en el array `dibujo`, e impresas al final con `foreach`) reemplazando **cada `for` por un `while`** — incluyendo los loops anidados.

### Pistas

- Por cada `for` que tengas que convertir, vas a necesitar: declarar el contador **antes** del `while`, escribir la condición dentro del `while`, y acordarte del `i++` (o `s++`) **dentro** del bloque.
- Sigue habiendo un loop "exterior" y uno "interior" — solo que ahora ambos serán `while` en vez de `for`.
- El `foreach` del final **no lo cambies** — el ejercicio es solo sobre los `for` que arman cada línea, no sobre cómo se imprime el resultado.
- Si tu programa se queda "pegado" sin mostrar nada, revisa que no se te haya olvidado algún incremento — probablemente hiciste un loop infinito.

Empieza por la línea más simple (`xxxxxxx`, un solo símbolo repetido) antes de intentar la que tiene varios segmentos (`xOxxOx` o `xx(--)xx`).

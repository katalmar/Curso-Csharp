# Funciones en C# — parámetros, argumentos y un valor de retorno por defecto

## ¿Qué es una función?

Una **función** es un bloque de código con nombre propio que hace **una tarea específica**, y que podemos "llamar" (ejecutar) cada vez que la necesitemos, desde donde la necesitemos, sin tener que volver a escribir ese código.

Hasta ahora, todo lo que hemos escrito ha vivido dentro de `Main` (el método principal del programa). Las funciones nos permiten **sacar un pedazo de lógica** de `Main`, ponerle un nombre, y reutilizarlo.

```csharp
static void Saludar()
{
    Console.WriteLine("¡Hola, aventurero!");
}
```

Y para ejecutarla, simplemente la "llamamos" por su nombre:

```csharp
Saludar(); // Imprime: ¡Hola, aventurero!
```

`static` y `void` los vamos a explicar ahora mismo — son parte de cómo se declara una función.

---

## Anatomía de una función

```csharp
static int Sumar(int a, int b)
{
    return a + b;
}
```

| Parte | Qué es | En el ejemplo |
|---|---|---|
| `static` | Por ahora, siempre lo vamos a escribir así (indica que la función pertenece a la clase, no a un objeto — lo verán en detalle más adelante). | `static` |
| **Tipo de retorno** | Qué tipo de dato va a **devolver** la función al terminar. Si no devuelve nada, se usa `void`. | `int` |
| **Nombre** | Cómo se va a llamar la función. | `Sumar` |
| **Parámetros** | Los datos que la función necesita recibir para hacer su trabajo, entre paréntesis. | `(int a, int b)` |
| **Cuerpo** | El código que se ejecuta cada vez que se llama la función. | `{ return a + b; }` |

---

## Parámetros vs. argumentos

Son casi la misma palabra, pero se usan en momentos distintos:

- **Parámetro**: el nombre que usamos **dentro de la definición** de la función, como una variable "vacía" que se llenará después.
- **Argumento**: el valor real que **le pasamos** a la función cuando la llamamos.

```csharp
static int Sumar(int a, int b)   // a y b son PARÁMETROS
{
    return a + b;
}

int resultado = Sumar(5, 3);     // 5 y 3 son los ARGUMENTOS
```

Cuando llamamos `Sumar(5, 3)`, C# toma esos argumentos y se los asigna a los parámetros en orden: `a = 5`, `b = 3`.

---

## `return`: cómo una función entrega un valor

`return` hace dos cosas al mismo tiempo:

1. **Termina** la función inmediatamente — ninguna línea después de un `return` (dentro del mismo camino de código) se ejecuta.
2. **Entrega** un valor de vuelta a quien llamó la función, con el tipo que declaramos (`int`, `string`, `bool`, etc.).

```csharp
static int Doble(int numero)
{
    return numero * 2; // termina la función y entrega el resultado
}

int resultado = Doble(4); // resultado ahora vale 8
Console.WriteLine(resultado);
```

---

## El valor de retorno "por defecto"

Aquí viene un detalle importante: si una función declara un tipo de retorno (como `int`), **está obligada a retornar algo en absolutamente todos los caminos posibles** de su código — incluso los casos que no contemplamos explícitamente.

```csharp
static int Clasificar(int numero)
{
    if (numero > 0)
    {
        return 1;
    }
    else if (numero < 0)
    {
        return -1;
    }

    return 0; // <- valor "por defecto": cubre el caso que sobra (numero == 0)
}
```

Ese último `return 0;` es un **valor de retorno por defecto**: no corresponde a ningún `if` específico, sino que es la respuesta de seguridad para cualquier situación que no quedó cubierta por las condiciones anteriores. Es una práctica muy común: definir qué pasa en los casos "normales", y dejar un `return` final como respaldo.

---

## Ahora sí: aplicándolo a nuestro cuento interactivo

Vamos a programar la mecánica de **"La misión imposible: llegar a clase"**, pero con una versión simplificada: cada decisión será **binaria** (dos opciones), y todo el cuento vivirá en dos arrays paralelos.

### La idea general

- `string[] textos` → cada posición tiene **una línea** del cuento, en el orden en que deben aparecer.
- `int[] saltos` → cada posición le corresponde **a la misma posición** en `textos`, e indica:
  - `0` → esta línea **no** espera nada del usuario, seguimos a la siguiente línea normalmente.
  - `1` → esta línea es un **final del cuento** (un "FINAL: LLEGASTE" o "FINAL: NO LLEGASTE"). Se imprime y el programa **termina ahí mismo**, sin seguir revisando el resto del array.
  - **cualquier otro número** → esta línea **sí** es una decisión, y ese número es **a qué línea saltar** si el usuario elige la segunda opción.

> 🔑 Como el `1` ya está "reservado" para marcar finales, al diseñar el cuento hay que evitar que una decisión necesite saltar justo a la posición `1` del array — por eso conviene dejar la posición `0` y `1` para las primeras líneas de introducción, antes de que empiece cualquier decisión.

Cuando una línea es una decisión, el texto de esa posición ya incluye la pregunta **y** las dos opciones, numeradas `1` y `2`, todo en un solo string:

```csharp
"Llegas a la esquina. 1) Tomar el camino conocido. 2) Tomar un atajo."
```

- Si el usuario responde **`1`** → se queda en la secuencia normal (avanza a la siguiente línea, como si nada).
- Si el usuario responde **`2`** → el programa **salta** a la línea indicada en `saltos` para esa posición.

### Los dos arrays

```csharp
string[] textos = new string[9];
int[] saltos    = new int[9];

textos[0] = "Bogotá amanece gris. Miras el celular: 7:18 a.m.";
saltos[0] = 0;

textos[1] = "La clase empieza a las 8:00. Sales corriendo a la calle.";
saltos[1] = 0;

textos[2] = "Llegas a la esquina. 1) Tomar el camino conocido. 2) Tomar un atajo.";
saltos[2] = 5; // si el usuario responde "2", salta a la posición 5

textos[3] = "Caminas por la ruta de siempre, pasando la panadería.";
saltos[3] = 0;

textos[4] = "Llegas a clase justo a tiempo. FINAL: LLEGASTE.";
saltos[4] = 1; // esta línea es un final: el programa debe terminar aquí

textos[5] = "Entras por el atajo. Al fondo hay una construcción bloqueando el paso.";
saltos[5] = 0;

textos[6] = "1) Rodear por el andén. 2) Cruzar la calle rápidamente.";
saltos[6] = 8; // si el usuario responde "2", salta a la posición 8

textos[7] = "Rodeas con cuidado y llegas a clase apenas a tiempo. FINAL: LLEGASTE.";
saltos[7] = 1; // otro final

textos[8] = "Cruzas justo cuando pasa una moto. FINAL: NO LLEGASTE.";
saltos[8] = 1; // otro final más
```

> 🔑 Fíjense que `textos[2]` y `saltos[2]` van **juntos**: la pregunta completa (con sus dos opciones) vive en una sola posición del array de texto, y su array de saltos guarda a dónde ir si se elige la opción `2`.

### La función que maneja cada línea

Esta función recibe **dos argumentos**: el texto a mostrar, y el número de salto asociado a esa línea.

```csharp
static int ManejarLinea(string texto, int numeroSalto)
{
    Console.WriteLine(texto);

    if (numeroSalto == 1)
    {
        return 1; // esta línea es un final: hay que terminar el cuento
    }

    if (numeroSalto == 0)
    {
        return 0; // esta línea no era una decisión, no hay nada más que hacer
    }

    string entrada = Console.ReadLine();

    if (entrada == "1")
    {
        return 0; // opción 1: seguir la secuencia normal
    }

    if (entrada == "2")
    {
        return numeroSalto; // opción 2: saltar a la línea indicada
    }

    return 0; // valor por defecto: si el usuario escribió algo inválido, seguimos normal
}
```

Repasemos qué hace, en orden:

1. **Siempre** imprime el texto que recibió — eso pasa sin importar si es una decisión, un final, o una línea normal.
2. Si `numeroSalto` es `1`, esta línea es un **final** → `return 1`, avisando a `Main` que hay que detener todo.
3. Si `numeroSalto` es `0`, no hay nada que preguntar → `return 0` y listo.
4. Si `numeroSalto` es cualquier otro número, sí es una decisión → pide `Console.ReadLine()`.
5. Si el usuario escribió `"1"` → `return 0` (seguir en orden).
6. Si el usuario escribió `"2"` → `return numeroSalto` (entrega el número al que hay que saltar).
7. Si el usuario escribió cualquier otra cosa → `return 0` como **valor por defecto**, para que el programa no se rompa.

### El `for` en `Main` que recorre todo el cuento

```csharp
static void Main()
{
    string[] textos = new string[9];
    int[] saltos    = new int[9];

    // ... (aquí van las 9 líneas que llenamos arriba) ...
        for (int i = 0; i < textos.Length; i++){
			int resultado = ManejarLinea(textos[i], saltos[i]);

			if (resultado == 1)
			{
				break;
			}

			else if (resultado != 0)
			{
				i = resultado - 1; // nos ubicamos justo antes de la línea destino...
			}
			// ...porque el for, al terminar la vuelta, le suma 1 a "i" automáticamente
		}
}
```

> ⚠️ Detalle importante: si `ManejarLinea` nos dice "salta a la posición `5`", no podemos escribir simplemente `i = resultado;`, porque el `for` le va a sumar `1` a `i` al terminar esta vuelta (`i++`), y terminaríamos aterrizando en la posición `6`, no en la `5`. Por eso escribimos `i = resultado - 1`, para que después del `i++` automático, `i` quede exactamente en la posición que queríamos.
>
> El `break` es distinto: es una instrucción que **sale inmediatamente de un loop** (`for`, `while`, etc.), sin importar en qué condición esté el contador. Lo usamos aquí porque, al llegar a un final, no tiene sentido seguir revisando el resto del array — el cuento ya terminó.

### Recorriendo el ejemplo paso a paso

Supongamos que el usuario responde `2` en la primera decisión (posición `2`) y `1` en la segunda (posición `6`):

| `i` | Se imprime... | ¿Pide input? | Respuesta | `resultado` | ¿Qué pasa? |
|---|---|---|---|---|---|
| 0 | "Bogotá amanece gris..." | No | — | 0 | sigue normal → `i` pasa a 1 |
| 1 | "La clase empieza a las 8:00..." | No | — | 0 | sigue normal → `i` pasa a 2 |
| 2 | "Llegas a la esquina. 1)... 2)..." | Sí | `2` | 5 | `i = 5 - 1 = 4` → el `for` suma 1 → `i` pasa a 5 |
| 5 | "Entras por el atajo..." | No | — | 0 | sigue normal → `i` pasa a 6 |
| 6 | "1) Rodear... 2) Cruzar..." | Sí | `1` | 0 | sigue normal → `i` pasa a 7 |
| 7 | "Rodeas con cuidado... FINAL: LLEGASTE." | No (es un final, `numeroSalto = 1`) | — | 1 | `resultado == 1` → **`break`**: el `for` se detiene aquí, el programa termina |

Fíjense que nunca se llega a `i = 8`: en cuanto la función devuelve `1`, el `break` corta el loop de inmediato, sin importar que todavía queden posiciones sin revisar en el array.

Así, con solo **dos arrays paralelos** y **una función con dos argumentos y un valor de retorno**, logramos representar un cuento completo con decisiones y saltos — la misma lógica que estructuraba capítulo por capítulo en el documento original, pero mucho más compacta y fácil de expandir (¡solo hay que agregarle más posiciones a los dos arrays!).

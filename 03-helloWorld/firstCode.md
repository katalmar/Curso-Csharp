# C# Basics para Desarrollo de Videojuegos

*Material de clase — Fundamentos del lenguaje C#*

---

## 1. Cómo se lee el código en C#

C# se ejecuta **línea por línea, de arriba hacia abajo**, pero lo importante no son las líneas visuales sino las **instrucciones**. Cada instrucción termina con un punto y coma `;`, que le indica al compilador "aquí termina esta acción, continúa con la siguiente".

```csharp
int vida = 100;
int daño = 20;
vida = vida - daño;
```

Aunque el código esté en tres líneas separadas, para C# son **tres instrucciones completas**, cada una cerrada por su `;`. De hecho, técnicamente podrías escribir todo en una sola línea:

```csharp
int vida = 100; int daño = 20; vida = vida - daño;
```

y el compilador lo entendería igual — pero **no lo hagan así**, se vuelve ilegible. La regla de oro:

> 🔑 **Un `;` = una acción terminada.** Si a un estudiante le da un error de compilación raro, lo primero que hay que revisar es si falta un punto y coma.

Las llaves `{ }` no cierran instrucciones, cierran **bloques de código** (como el cuerpo de un método o una condición) — de eso hablamos más adelante en la sección de jerarquías.

---

## 2. `Console.WriteLine()`, y los tipos `char` y `string`

`Console.WriteLine("")` es la instrucción que usamos para **mostrar texto en pantalla** (la consola). Todo lo que va dentro de las comillas `" "` es un **string** (cadena de texto).

```csharp
Console.WriteLine("¡Bienvenido al juego!");
```

### `string` vs `char`

| Tipo | Qué guarda | Ejemplo | Comillas |
|---|---|---|---|
| `string` | Una cadena de **texto** (0, 1 o muchos caracteres) | `"Jugador1"` | Comillas dobles `" "` |
| `char` | **Un solo carácter** | `'A'` | Comillas simples `' '` |

```csharp
string nombreJugador = "DragonSlayer99";
char inicial = 'D';

Console.WriteLine(nombreJugador);   // Imprime: DragonSlayer99
Console.WriteLine(inicial);         // Imprime: D
```

> ⚠️ Un error muy común: usar comillas simples para un string (`'Hola'`) o poner más de un carácter en un `char` (`'Hola'` en un char da error). `char` es **siempre uno solo**.

---

## 3. Tipos de variables y su capacidad de almacenamiento

No todas las variables numéricas son iguales: cada tipo reserva una cantidad distinta de memoria y por lo tanto puede guardar rangos de valores distintos.

| Tipo | Guarda | Ejemplo (videojuego) | Tamaño aprox. |
|---|---|---|---|
| `int` | Números enteros | `int puntaje = 1500;` | 4 bytes |
| `float` | Decimales (precisión simple) | `float velocidad = 5.5f;` | 4 bytes |
| `double` | Decimales (precisión doble, más exacto) | `double posicionX = 120.3456;` | 8 bytes |
| `bool` | Verdadero o falso | `bool estaVivo = true;` | 1 bit (lógico) |
| `char` | Un carácter | `char rango = 'S';` | 2 bytes |
| `string` | Texto | `string arma = "Espada";` | variable |

Un `double` puede guardar números mucho más grandes y con más decimales de precisión que un `int` (que no tiene decimales) o que un `float` (que tiene menos precisión que un `double`). Por eso, en física de videojuegos (posiciones, velocidades, física de partículas) es común usar `float` o `double` en vez de `int`.

> 🎮 Piensen en esto como el inventario de un juego: un `int` es como una mochila pequeña (solo números enteros, rango limitado), un `double` es un baúl grande (más "espacio" para decimales y números más grandes).

---

## 4. Declaración de variables y operaciones entre tipos distintos

Las variables en C# son de **carácter declarativo**: antes de poder usarlas, hay que **declarar su tipo**. Esto es diferente a otros lenguajes donde el tipo se "adivina".

```csharp
int vida;          // Declaración: aquí solo digo "vida va a ser un número entero"
vida = 100;        // Asignación: aquí le doy el valor

int energia = 50;  // Declaración + asignación en una sola línea
```

Una vez declarada, una variable **no puede cambiar de tipo**. Si `vida` es `int`, siempre será `int` durante toda su vida en el programa.

### Operar entre tipos diferentes

Algunas variables de tipos diferentes **sí pueden operar entre ellas**, pero hay que hacerlo con cuidado, porque C# no siempre convierte automáticamente:

```csharp
int nivel = 5;
double multiplicador = 1.5;

double dañoFinal = nivel * multiplicador; // ✅ funciona: int y double se combinan bien
```

Pero:

```csharp
int enteroPuro = dañoFinal; // ❌ ERROR: no se puede meter un double dentro de un int sin avisarlo
```

Para eso está la **conversión explícita (casting)**:

```csharp
int enteroPuro = (int)dañoFinal; // ✅ ahora sí, le decimos "conviértelo a int a la fuerza"
```

> ⚠️ Ojo: al convertir un `double`/`float` a `int` se **pierden los decimales** (no redondea, los corta). `7.9` se convierte en `7`.

---

## 5. Operaciones entre variables

### Operadores aritméticos básicos

| Operador | Significado | Ejemplo |
|---|---|---|
| `+` | Suma | `vida + 10` |
| `-` | Resta | `vida - daño` |
| `*` | Multiplicación | `daño * criticoX2` |
| `/` | División | `vida / 2` |
| `%` | Módulo (residuo de una división) | `puntaje % 2` |

El **módulo (`%`)** es muy usado en videojuegos: por ejemplo, para saber si un número de turno es par o impar, o para hacer que algo se repita cada cierta cantidad de pasos (una trampa cada 5 casillas, un enemigo especial cada 10 oleadas, etc.).

```csharp
int oleada = 10;
if (oleada % 5 == 0)
{
    Console.WriteLine("¡Jefe especial!");
}
```

### Suma entre `string` y `char`

Los `string` (y hasta los `char`) también se pueden "sumar", pero en realidad eso se llama **concatenación**: es unir texto, no una suma matemática.

```csharp
string nombre = "Dragón";
string apellido = "de Fuego";
string nombreCompleto = nombre + " " + apellido; // "Dragón de Fuego"
```

Otra forma común de combinar texto con variables es la **interpolación de strings**, muy usada en videojuegos para mostrar mensajes dinámicos:

```csharp
int vida = 80;
Console.WriteLine($"Vida actual: {vida}"); // Vida actual: 80
```

### Conversión entre `int` y `float`

Un `int` puede transformarse en `float` (esto es seguro, casi nunca se pierde nada):

```csharp
int monedas = 10;
float monedasFloat = monedas; // conversión implícita, no hace falta casting
```

Y un `float` puede volverse `int` (aquí sí se pierden los decimales, y generalmente hace falta casting explícito):

```csharp
float distancia = 15.75f;
int distanciaEntera = (int)distancia; // resultado: 15
```

---

## 6. Jerarquía de operaciones: paréntesis `()` y llaves `{}`

Igual que en matemáticas, C# respeta un **orden de prioridad** al resolver operaciones:

1. Paréntesis `()`
2. Multiplicación `*`, División `/`, Módulo `%`
3. Suma `+`, Resta `-`

```csharp
int resultado = 2 + 3 * 4;       // = 14  (primero multiplica, luego suma)
int resultado2 = (2 + 3) * 4;    // = 20  (el paréntesis fuerza a sumar primero)
```

> 🔑 Regla práctica: **si tienen duda, usen paréntesis**. Nunca está de más aclarar el orden.

Las **llaves `{ }`** cumplen un rol distinto: no priorizan operaciones matemáticas, sino que **delimitan un bloque de código** — el cuerpo de un método, de un `if`, de un `for`, etc.

```csharp
if (vida <= 0)
{
    Console.WriteLine("Game Over");   // todo lo que está dentro de { } pertenece a este "if"
}
```

Piensen en los paréntesis como "orden de cálculo" y en las llaves como "una caja que agrupa instrucciones que pertenecen juntas".

---

## 7. Variables booleanas y operadores lógicos

Una variable `bool` solo puede tener dos valores: `true` o `false`. Son fundamentales para tomar decisiones en el juego (¿el jugador está vivo?, ¿tiene la llave?, ¿puede saltar?).

```csharp
bool estaVivo = true;
bool tieneLlave = false;
```

### Operadores de comparación

| Operador | Significado | Ejemplo |
|---|---|---|
| `==` | Igual a | `vida == 0` |
| `!=` | Distinto de | `vida != 0` |
| `>=` | Mayor o igual que | `nivel >= 10` |
| `<=` | Menor o igual que | `energia <= 20` |
| `>` | Mayor que | `puntaje > 1000` |
| `<` | Menor que | `enemigos < 3` |

> ⚠️ Cuidado clásico de principiante: `=` es **asignar** un valor, `==` es **comparar** si dos valores son iguales. Confundirlos es de los errores más comunes.

### Operadores lógicos

| Operador | Significado | Ejemplo |
|---|---|---|
| `&&` | Y (AND) — ambas condiciones deben ser verdaderas | `estaVivo && tieneLlave` |
| `\|\|` | O (OR) — al menos una condición debe ser verdadera | `tieneLlave \|\| tieneCodigo` |
| `!` | NOT — invierte el valor booleano | `!estaVivo` (equivale a "está muerto") |

```csharp
bool tieneLlave = true;
bool puertaCerrada = true;

if (tieneLlave && puertaCerrada)
{
    Console.WriteLine("Puedes abrir la puerta.");
}

if (!estaVivo)
{
    Console.WriteLine("El personaje ha muerto.");
}
```

---

## 8. Arrays (arreglos)

Un **array** es una variable que guarda **varios valores del mismo tipo**, ordenados y accesibles por su posición (índice).

### Declararlo

```csharp
int[] puntajes = new int[5]; // un array de 5 enteros (todos empiezan en 0)

string[] inventario = { "Espada", "Escudo", "Poción", "Llave" }; // con valores iniciales
```

### El tamaño es fijo

Una vez creado un array con un tamaño (por ejemplo, `new int[5]`), **ese tamaño no cambia**. No se pueden agregar ni quitar posiciones después — si necesitan algo de tamaño variable, más adelante verán `List<T>`, pero por ahora trabajamos con arrays de tamaño fijo.

### Saber cuánto mide

Se usa la propiedad `.Length`:

```csharp
Console.WriteLine(inventario.Length); // Imprime: 4
```

### Acceder a una posición específica

Los arrays empiezan a contar **desde el 0**, no desde el 1:

```csharp
Console.WriteLine(inventario[0]); // "Espada"  <- primera posición
Console.WriteLine(inventario[2]); // "Poción"  <- tercera posición
```

> 🔑 Si el array tiene `Length` igual a 4, las posiciones válidas son `0, 1, 2, 3`. Intentar acceder a `inventario[4]` da error (fuera de rango).

### Sobrescribir un valor

Se accede a la posición y se le asigna un nuevo valor, igual que con cualquier variable:

```csharp
inventario[1] = "Escudo de Fuego"; // reemplaza "Escudo" por "Escudo de Fuego"
Console.WriteLine(inventario[1]);  // "Escudo de Fuego"
```

Ejemplo completo aplicado a un juego:

```csharp
int[] vidasEnemigos = new int[3] { 100, 80, 120 };

Console.WriteLine($"Cantidad de enemigos: {vidasEnemigos.Length}"); // 3
Console.WriteLine($"Vida del enemigo 1: {vidasEnemigos[0]}");        // 100

vidasEnemigos[0] = vidasEnemigos[0] - 30; // el enemigo 1 recibe daño
Console.WriteLine($"Vida del enemigo 1 tras el ataque: {vidasEnemigos[0]}"); // 70
```

---

## Resumen rápido para repasar

- `;` marca el fin de cada instrucción.
- `string` = texto entre comillas dobles; `char` = un solo carácter entre comillas simples.
- Cada tipo de variable (`int`, `float`, `double`, `bool`, `char`) tiene distinta capacidad y precisión.
- Las variables se declaran con un tipo fijo; convertir entre tipos distintos a veces requiere casting `(tipo)`.
- Operadores aritméticos: `+ - * / %`; los strings se "suman" (concatenan), no se calculan.
- Los paréntesis `()` ordenan operaciones matemáticas; las llaves `{}` agrupan bloques de código.
- `bool` guarda `true`/`false`; se combinan con `&& || !` y se comparan con `== != >= <=`.
- Los arrays tienen tamaño fijo, se consulta con `.Length`, se accede con `[índice]` empezando en 0, y se sobrescriben asignando un nuevo valor a esa posición.

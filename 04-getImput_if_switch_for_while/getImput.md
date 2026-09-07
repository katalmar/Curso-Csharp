# Variables, `Console.ReadLine()` y arrays

## 1. Obtener información del usuario

Hasta ahora hemos escrito directamente los valores de nuestras variables dentro del programa.

Por ejemplo:

```csharp
string nombre = "Ana";
```

En este caso, el programa ya conoce el nombre antes de comenzar a ejecutarse.

Pero podemos hacer que el programa **espere a que el usuario escriba una respuesta**.

Para esto podemos utilizar:

```csharp
Console.ReadLine()
```

---

# 2. ¿Qué hace `Console.ReadLine()`?

`Console.ReadLine()` permite **leer una línea de texto que el usuario escribe en la consola**.

Por ejemplo:

```csharp
string nombre = Console.ReadLine();
```

Cuando el programa llega a esta línea, espera a que el usuario escriba algo.

Podemos acompañarlo de un mensaje para indicarle al usuario qué debe escribir:

```csharp
Console.Write("Escribe tu nombre: ");
string nombre = Console.ReadLine();
```

El funcionamiento sería:

```text
Programa
   ↓
"Escribe tu nombre:"
   ↓
Usuario escribe
   ↓
Console.ReadLine()
   ↓
El programa recibe el texto
   ↓
Se guarda en nombre
```

Si el usuario escribe:

```text
Carlos
```

la variable `nombre` tendrá:

```text
Carlos
```

Podemos comprobarlo:

```csharp
Console.Write("Escribe tu nombre: ");
string nombre = Console.ReadLine();

Console.WriteLine(nombre);
```

---

# 3. `Console.Write()` y `Console.WriteLine()`

Ya hemos utilizado:

```csharp
Console.WriteLine();
```

Esta instrucción muestra información en la consola y después pasa a una nueva línea.

Por ejemplo:

```csharp
Console.WriteLine("Hola");
Console.WriteLine("¿Cómo estás?");
```

Resultado:

```text
Hola
¿Cómo estás?
```

También podemos utilizar:

```csharp
Console.Write();
```

La diferencia es que `Console.Write()` **no pasa automáticamente a una nueva línea**.

Por ejemplo:

```csharp
Console.Write("Hola ");
Console.Write("Carlos");
```

Resultado:

```text
Hola Carlos
```

Esto resulta útil cuando queremos hacer una pregunta y esperar la respuesta en la misma línea:

```csharp
Console.Write("Escribe tu nombre: ");
string nombre = Console.ReadLine();
```

El usuario verá:

```text
Escribe tu nombre: Carlos
```

---

# 4. Probar `Console.ReadLine()`

Antes de continuar, ejecuta el siguiente programa.

El objetivo es simplemente observar qué ocurre cuando el programa recibe información del usuario.

```csharp
using System;

public class Program
{
    public static void Main()
    {
        Console.Write("Escribe tu nombre: ");
        string nombre = Console.ReadLine();

        Console.Write("Escribe tu ciudad: ");
        string ciudad = Console.ReadLine();

        Console.WriteLine();
        Console.WriteLine("Información recibida:");
        Console.WriteLine(nombre);
        Console.WriteLine(ciudad);
    }
}
```

Prueba diferentes nombres y ciudades.

Por ejemplo:

```text
Escribe tu nombre: Laura
Escribe tu ciudad: Bogotá

Información recibida:
Laura
Bogotá
```

Observa que el programa no conoce esos valores antes de ejecutarse.

Los valores son proporcionados por el usuario.

---

# 5. `Console.ReadLine()` siempre recibe texto

Es importante tener en cuenta algo:

```csharp
Console.ReadLine()
```

recibe la información como **texto**, es decir, como un `string`.

Por ejemplo:

```csharp
string nombre = Console.ReadLine();
```

Si el usuario escribe:

```text
Carlos
```

se recibe el texto:

```text
Carlos
```

Pero si el usuario escribe:

```text
25
```

también se recibe como texto:

```text
"25"
```

Aunque visualmente parezca un número.

Esto será importante cuando queramos utilizar números para realizar operaciones.

---

# 6. ¿Qué pasa si el tipo de variable no corresponde al valor?

Una variable tiene un tipo determinado.

Por ejemplo:

```csharp
string nombre;
int vidas;
double velocidad;
bool tieneLlave;
```

Cada una está preparada para almacenar un tipo de información diferente.

Por ejemplo:

```csharp
int vidas = 5;
```

es correcto porque `5` es un número entero.

Pero esto:

```csharp
int vidas = "cinco";
```

no es correcto.

La variable `vidas` fue declarada como `int`, pero `"cinco"` es un texto.

Lo mismo ocurre con:

```csharp
int vidas = "5";
```

Aunque `"5"` representa un número, las comillas indican que estamos trabajando con un `string`.

Por lo tanto, esto tampoco corresponde directamente con una variable `int`.

---

# 7. Convertir la información recibida

Como `Console.ReadLine()` recibe texto, si queremos utilizar la respuesta como un número debemos convertirla.

Por ejemplo:

```csharp
Console.Write("¿Cuántas vidas tienes? ");

int vidas = int.Parse(Console.ReadLine());

Console.WriteLine(vidas);
```

Si el usuario escribe:

```text
5
```

el programa convierte el texto `"5"` en el número `5`.

Ahora podemos realizar operaciones:

```csharp
Console.Write("¿Cuántas vidas tienes? ");

int vidas = int.Parse(Console.ReadLine());

int vidasExtra = vidas + 2;

Console.WriteLine(vidasExtra);
```

Si el usuario introduce:

```text
5
```

el resultado será:

```text
7
```

---

# 8. ¿Qué ocurre si introducimos un valor incorrecto?

Observa este programa:

```csharp
Console.Write("¿Cuántas vidas tienes? ");

int vidas = int.Parse(Console.ReadLine());

Console.WriteLine(vidas);
```

El programa espera que introduzcamos un número entero.

Por ejemplo:

```text
5
```

funciona correctamente.

Pero si escribimos:

```text
cinco
```

el programa no puede convertir ese texto en un número entero.

Esto genera un error durante la ejecución.

Por eso, cuando utilizamos `Console.ReadLine()`, debemos pensar qué tipo de información esperamos recibir y qué valores puede introducir el usuario.

---

# 9. El símbolo `$` y las cadenas de texto

En C# podemos utilizar `$` delante de una cadena de texto:

```csharp
$"..."
```

Esto permite insertar variables directamente dentro del texto utilizando `{}`.

Por ejemplo:

```csharp
string nombre = "Carlos";

Console.WriteLine($"Hola, {nombre}");
```

Resultado:

```text
Hola, Carlos
```

La expresión:

```csharp
{nombre}
```

es reemplazada por el contenido de la variable.

---

## 10. Combinar `Console.ReadLine()` con `$`

Ahora podemos utilizar la información introducida por el usuario dentro de un mensaje.

```csharp
Console.Write("Escribe tu nombre: ");
string nombre = Console.ReadLine();

Console.WriteLine($"Hola, {nombre}");
```

Si el usuario escribe:

```text
Laura
```

obtendremos:

```text
Hola, Laura
```

También podemos utilizar varias variables:

```csharp
string nombre = "Laura";
string ciudad = "Bogotá";

Console.WriteLine($"{nombre} vive en {ciudad}");
```

Resultado:

```text
Laura vive en Bogotá
```

El `$` es especialmente útil cuando queremos construir mensajes utilizando información almacenada en nuestras variables.

---

# 11. Un pequeño programa para probar

Ejecuta y modifica el siguiente programa:

```csharp
using System;

public class Program
{
    public static void Main()
    {
        Console.Write("¿Cuál es tu nombre? ");
        string nombre = Console.ReadLine();

        Console.Write("¿Cuál es tu edad? ");
        int edad = int.Parse(Console.ReadLine());

        Console.Write("¿Cuál es tu ciudad? ");
        string ciudad = Console.ReadLine();

        Console.WriteLine();
        Console.WriteLine("Información recibida:");
        Console.WriteLine($"Nombre: {nombre}");
        Console.WriteLine($"Edad: {edad}");
        Console.WriteLine($"Ciudad: {ciudad}");
    }
}
```

Prueba diferentes valores.

Después intenta cambiar los tipos de las variables y observa qué sucede cuando el valor introducido por el usuario no corresponde con el tipo esperado.

---

# Arrays

## 12. Crear un array sin introducir todavía sus valores

Hasta ahora hemos creado arrays escribiendo directamente sus valores:

```csharp
string[] nombres = { "Ana", "Bruno", "Carla" };
```

Pero también podemos crear un array **sin especificar todavía sus valores**.

Para hacerlo debemos indicar qué tipo de información almacenará y cuántos elementos podrá contener.

Por ejemplo:

```csharp
string[] nombres = new string[3];
```

Este array puede almacenar **3 elementos de tipo `string`**.

Al crearlo todavía no hemos indicado los nombres.

Podemos representarlo así:

```text
Índice:     0        1        2
            ↓        ↓        ↓
Valor:     vacío    vacío    vacío
```

---

# 13. Agregar valores al array

Después de crear el array podemos asignar valores utilizando sus índices.

```csharp
string[] nombres = new string[3];

nombres[0] = "Ana";
nombres[1] = "Bruno";
nombres[2] = "Carla";
```

Ahora tenemos:

```text
Índice:     0        1        2
            ↓        ↓        ↓
Valor:      Ana    Bruno    Carla
```

También podemos obtener los valores mediante sus índices:

```csharp
Console.WriteLine(nombres[0]);
Console.WriteLine(nombres[1]);
Console.WriteLine(nombres[2]);
```

---


# 14. Ejercicio: construir una base de datos de jugadores

Ahora vamos a combinar los conceptos vistos en este tutorial con los arrays del ejercicio anterior.

Crea un programa que permita al usuario construir una base de datos de **3 jugadores**.

Cada jugador debe tener las siguientes características:

* Nombre
* Vidas
* Puntos
* Velocidad
* Tiene llave
* Está en la puerta

Debes utilizar **un array para cada característica**.

Los índices de los diferentes arrays deben corresponder entre sí.

Por ejemplo, todos los datos que se encuentren en el índice `0` deben pertenecer al mismo jugador.

La estructura debe permitir relacionar la información de esta manera:

```text
Índice       0          1          2
             ↓          ↓          ↓
Nombre      jugador   jugador   jugador
Vidas       jugador   jugador   jugador
Puntos      jugador   jugador   jugador
Velocidad   jugador   jugador   jugador
Llave       jugador   jugador   jugador
Puerta      jugador   jugador   jugador
```

## Información de los jugadores

El programa debe solicitar al usuario la información necesaria para crear los tres jugadores.

Los valores de cada característica pueden obtenerse de diferentes maneras.

Para algunos datos puedes permitir que el usuario **escriba libremente el valor que quiera**.

Para otros puedes presentar **opciones definidas por el programa** para que el usuario elija.

Por ejemplo, una característica podría tener varias opciones disponibles, mientras que otra podría permitir introducir cualquier valor válido.

La forma de distribuir estas dos posibilidades queda a tu elección.

---

## Condiciones

El programa debe:

1. Crear los arrays con espacio para tres jugadores.
2. Solicitar al usuario la información de cada jugador.
3. Almacenar cada respuesta en el índice correspondiente.
4. Mantener relacionados los datos de cada jugador mediante los índices.
5. Mostrar al final la información de los tres jugadores.

La información debe haber sido introducida durante la ejecución del programa.

No escribas directamente los datos de los jugadores dentro de los arrays.

---

## Preguntas

**¿Qué diferencia existe entre crear un array escribiendo directamente sus valores y crearlo utilizando `new` y un tamaño determinado?**

**¿Cómo se asigna un valor a una posición específica de un array?**

**¿Por qué es importante utilizar el mismo índice para relacionar las características de un jugador?**

**¿Qué ocurre si asignas accidentalmente la característica de un jugador al índice equivocado?**

**¿Qué diferencia existe entre una característica cuyo valor puede introducir libremente el usuario y una característica en la que el programa ofrece opciones?**

**¿Qué ocurre si el usuario introduce un valor que no corresponde con el tipo de dato esperado?**


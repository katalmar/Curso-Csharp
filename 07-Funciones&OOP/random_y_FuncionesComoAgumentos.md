
# Azar en C#: la clase `Random`, y funciones como argumentos

## Parte 1: generando números al azar con `Random`

Hasta ahora todo lo que hemos programado es **determinístico**: si corremos el mismo código dos veces, pasa exactamente lo mismo. Pero muchos videojuegos necesitan **azar** — un cofre que a veces tiene oro y a veces una trampa, un enemigo que aparece con cierta probabilidad, un dado que se tira.

Para eso, C# nos da la clase `Random`.

### Creando un generador de números aleatorios

```csharp
Random rnd = new Random();
```

Esto crea un **objeto** llamado `rnd` que sabe generar números al azar. No se preocupen todavía por qué escribimos `new Random()` así con paréntesis — por ahora, piensen en esta línea como "prender la máquina de números aleatorios". La vamos a crear **una sola vez**, generalmente al principio de `Main`, y la reutilizamos cada vez que necesitemos un número al azar.

> ⚠️ Error común: crear un `new Random()` cada vez que se necesita un número, dentro de un loop por ejemplo. Esto puede hacer que varios números "aleatorios" salgan iguales, porque `Random` se basa parcialmente en el reloj del computador, y si se crean varios `Random` casi al mismo tiempo, pueden quedar "sincronizados". Por eso: **un solo `Random`, creado una vez, reutilizado siempre**.

### Pidiendo un número al azar: `.Next()`

Una vez tenemos `rnd`, le podemos pedir números de distintas formas:

```csharp
int numero1 = rnd.Next();        // cualquier entero positivo, sin límite claro
int numero2 = rnd.Next(10);      // un entero entre 0 (incluido) y 10 (SIN incluir) → 0 a 9
int numero3 = rnd.Next(5, 15);   // un entero entre 5 (incluido) y 15 (SIN incluir) → 5 a 14
```

| Llamada | Rango que devuelve |
|---|---|
| `rnd.Next()` | Cualquier entero positivo |
| `rnd.Next(max)` | Desde `0` hasta `max - 1` |
| `rnd.Next(min, max)` | Desde `min` hasta `max - 1` |

> 🔑 Fíjense en el patrón que ya conocemos de los arrays: el límite superior **nunca se incluye**. `rnd.Next(10)` puede devolver `9` como máximo, nunca `10`.

### Ejemplo simple: tirar un dado

```csharp
Random rnd = new Random();
int dado = rnd.Next(1, 7); // entre 1 y 6, porque el 7 no se incluye
Console.WriteLine($"Sacaste un {dado}");
```

### Ejemplo aplicado a un array (algo que ya conocen)

Una combinación muy común: usar `Random` para elegir **una posición al azar** dentro de un array.

```csharp
string[] objetos = { "espada", "poción", "moneda de oro", "trampa" };

Random rnd = new Random();
int indice = rnd.Next(objetos.Length); // un índice válido para este array

Console.WriteLine($"Encontraste: {objetos[indice]}");
```

Esto es exactamente lo que vamos a necesitar para el ejercicio de hoy — pero en vez de elegir un objeto al azar de un array de `string`, vamos a elegir **una función al azar** de un array de funciones.

---

## Parte 2: pasar funciones como argumentos

### El salto conceptual

Hasta ahora, los argumentos que le hemos pasado a las funciones han sido datos: números, strings, booleanos, arrays de esos tipos. Pero en C# también podemos pasarle a una función **otra función**, para que la use o la ejecute cuando lo necesite.

La idea suena rara al principio, así que empecemos poco a poco.

### Paso 1: declarar funciones normales, sin llamarlas todavía

Vamos a escribir varias funciones pequeñas, cada una representando un posible evento aleatorio del juego. Son funciones completamente normales — `void`, sin parámetros:

```csharp
static void EncontrarMoneda()
{
    Console.WriteLine("Encontraste una moneda de oro brillante.");
}

static void EncontrarTrampa()
{
    Console.WriteLine("¡Cuidado! Pisaste una trampa y pierdes 10 de vida.");
}

static void EncontrarPocion()
{
    Console.WriteLine("Encontraste una poción de curación.");
}
```

Nada nuevo hasta aquí.

### Paso 2: un "tipo" para agrupar funciones parecidas — `delegate`

Para poder guardar funciones dentro de un array (o pasarlas como argumento), C# necesita saber **qué forma tiene** esa función: cuántos parámetros recibe y qué tipo devuelve. Para eso usamos un `delegate`: es como declarar un "molde" que describe la forma de la función.

```csharp
delegate void Evento();
```

Esto se lee: *"`Evento` es un molde para cualquier función que no reciba parámetros y no devuelva nada (`void`)"*. Nuestras tres funciones de arriba (`EncontrarMoneda`, `EncontrarTrampa`, `EncontrarPocion`) encajan perfecto en ese molde — por eso las podemos tratar como si fueran del "tipo" `Evento`.

> 🔑 El `delegate` se declara **una sola vez**, normalmente junto a las demás funciones, fuera de `Main`.

### Paso 3: guardar funciones dentro de un array

Igual que hicimos con `string[]` o `int[]`, ahora podemos declarar un array de `Evento`:

```csharp
Evento[] posibles = { EncontrarMoneda, EncontrarTrampa, EncontrarPocion };
```

> ⚠️ Detalle clave: escribimos `EncontrarMoneda`, **sin paréntesis**. Con paréntesis (`EncontrarMoneda()`) estaríamos *llamando* a la función ya mismo. Sin paréntesis, estamos *nombrando* la función, para guardarla y llamarla más adelante.

### Paso 4: una función que recibe funciones como argumento

Ahora sí, el objetivo del ejercicio: una función que reciba un **array de funciones**, elija una al azar (usando lo que aprendimos en la Parte 1), y la ejecute.

```csharp
static void EjecutarEventoAleatorio(Evento[] eventos)
{
    Random rnd = new Random();
    int indice = rnd.Next(eventos.Length);

    eventos[indice](); // aquí sí, CON paréntesis: ahora sí la estamos llamando
}
```

Fíjense que `EjecutarEventoAleatorio` **no sabe de antemano** qué evento va a ejecutar. No tiene ningún `if` preguntando "¿es moneda? ¿es trampa?". Simplemente confía en que, sea cual sea la función que le tocó al azar, sabe cómo ejecutarla — porque todas tienen la misma forma (`Evento`).

### Todo junto, en `Main`

```csharp
using System;

public class Program
{
    delegate void Evento();

    static void EncontrarMoneda()
    {
        Console.WriteLine("Encontraste una moneda de oro brillante.");
    }

    static void EncontrarTrampa()
    {
        Console.WriteLine("¡Cuidado! Pisaste una trampa y pierdes 10 de vida.");
    }

    static void EncontrarPocion()
    {
        Console.WriteLine("Encontraste una poción de curación.");
    }

    static void EjecutarEventoAleatorio(Evento[] eventos)
    {
        Random rnd = new Random();
        int indice = rnd.Next(eventos.Length);
        eventos[indice]();
    }

    public static void Main()
    {
        Evento[] posibles = { EncontrarMoneda, EncontrarTrampa, EncontrarPocion };

        Console.WriteLine("Entras al bosque...");
        EjecutarEventoAleatorio(posibles);
    }
}
```

Cada vez que corran este programa, `EjecutarEventoAleatorio` va a llamar a una función distinta — a veces la moneda, a veces la trampa, a veces la poción — sin que `Main` ni la función que elige el evento tengan que saber de antemano cuál será.

---

## 📝 Ejercicio

1. Agreguen **al menos dos eventos nuevos** (funciones nuevas) al array `posibles` — por ejemplo `EncontrarNada()`, `EncontrarEnemigo()`, `EncontrarCofre()`.
2. Llamen a `EjecutarEventoAleatorio` **tres veces seguidas** en `Main` y corran el programa varias veces. Observen que no siempre sale lo mismo.
3. **Reto:** ¿Qué pasaría si en vez de un array de 3 eventos "igual de probables", quisieran que `EncontrarTrampa` sea más rara que las demás (por ejemplo, que aparezca solo el 10% de las veces)? No hace falta que lo resuelvan todavía — piensen qué le tendrían que cambiar a `EjecutarEventoAleatorio` para lograrlo. Lo vamos a resolver juntos en la próxima sesión.

---

## Por qué esto les sirve para su proyecto final

Esta técnica implementa directamente la mecánica **1.8 Azar y eventos aleatorios** de su lista, pero de una forma muy reutilizable: `EjecutarEventoAleatorio` no está "pegada" a un evento específico — sirve para el bosque, para un cofre, para cualquier situación donde quieran que ocurra "una cosa al azar entre varias posibles". Solo necesitan armar un array distinto de funciones para cada situación.

Es también la puerta de entrada a la mecánica **1.4 Condiciones y estados**: el mismo concepto de "pasar funciones como argumento" se puede usar para escribir algo como `EjecutarSegunCondicion(bool condicion, Evento siVerdadero, Evento siFalso)`, que en vez de elegir al azar, elige qué función ejecutar según si una condición es `true` o `false`. Eso lo veremos en una próxima sesión.

Claro. El ejercicio debe plantear **una decisión de diseño**: revisar el código anterior, reconocer qué decisiones se benefician de `switch` y cuáles deben permanecer con `if`, y después actualizar el programa.

# `switch`, `case`, `break` y `default` en C#

Hasta ahora hemos utilizado `if`, `else if` y `else` para que nuestro programa pueda tomar decisiones.

Por ejemplo, podemos tener varias posibilidades:

```csharp
if (herramienta == "espada")
{
    // ...
}
else if (herramienta == "arco")
{
    // ...
}
else if (herramienta == "antorcha")
{
    // ...
}
else
{
    // ...
}
```

Esta estructura funciona muy bien cuando las condiciones son diferentes o necesitan comparaciones.

Pero ¿qué ocurre cuando queremos comparar **una misma variable con diferentes valores posibles**?

Para estos casos existe otra estructura:

```csharp
switch
```

---

# 1. ¿Qué es `switch`?

`switch` permite que un programa tome diferentes caminos dependiendo del valor de una variable.

Podemos imaginarlo como una especie de **selector de opciones**.

Por ejemplo, tenemos una variable:

```csharp
string herramienta = "espada";
```

Podemos preguntarle al programa:

```text
¿Qué herramienta tiene el jugador?

espada   → hacer una cosa
arco     → hacer otra
antorcha → hacer otra
```

En lugar de escribir muchos `if` y `else if`, podemos utilizar `switch`.

---

# 2. La estructura básica

La estructura de un `switch` es:

```csharp
switch (variable)
{
    case valor:
        // instrucciones
        break;

    case otroValor:
        // instrucciones
        break;

    default:
        // instrucciones
        break;
}
```

Podemos identificar cuatro elementos principales:

* `switch`
* `case`
* `break`
* `default`

---

# 3. `switch`

Después de `switch` colocamos entre paréntesis la variable cuyo valor queremos revisar.

Por ejemplo:

```csharp
string herramienta = "espada";

switch (herramienta)
{
    // casos
}
```

El programa va a revisar el contenido de:

```text
herramienta
```

y buscará un `case` que corresponda con ese valor.

---

# 4. `case`

`case` significa aproximadamente:

> **En caso de que el valor sea este...**

Por ejemplo:

```csharp
string herramienta = "espada";

switch (herramienta)
{
    case "espada":
        Console.WriteLine("Has elegido una espada.");
        break;
}
```

El programa compara:

```text
herramienta
     ↓
"espada"
     ↓
case "espada"
```

Como los valores coinciden, ejecuta las instrucciones de ese `case`.

El resultado será:

```text
Has elegido una espada.
```

---

# 5. Varios `case`

Podemos tener diferentes `case` para diferentes valores.

```csharp
string herramienta = "arco";

switch (herramienta)
{
    case "espada":
        Console.WriteLine("Has elegido una espada.");
        break;

    case "arco":
        Console.WriteLine("Has elegido un arco.");
        break;

    case "antorcha":
        Console.WriteLine("Has elegido una antorcha.");
        break;
}
```

El programa revisa el valor de `herramienta`.

Si contiene:

```text
"espada"
```

entra en el primer `case`.

Si contiene:

```text
"arco"
```

entra en el segundo.

Si contiene:

```text
"antorcha"
```

entra en el tercero.

---

# 6. `break`

La palabra `break` indica que hemos terminado de ejecutar ese `case`.

Por ejemplo:

```csharp
case "arco":
    Console.WriteLine("Has elegido un arco.");
    break;
```

Podemos imaginar el `break` como una señal que dice:

> **Ya encontramos la opción correspondiente. Sal de este `switch`.**

Esto es importante porque después de ejecutar un `case`, queremos continuar con el programa y no seguir ejecutando los otros casos.

Por ejemplo:

```text
switch
  │
  ├── case "espada"
  │
  ├── case "arco" ← coincide
  │       │
  │      break
  │       │
  │       ▼
  │    salir del switch
  │
  └── case "antorcha"
```

Si el usuario eligió `"arco"`, se ejecuta ese `case` y `break` termina el `switch`.

---

# 7. ¿Qué ocurre si no utilizamos `break`?

En C#, un `case` normalmente debe terminar de forma explícita, por ejemplo con `break`, `return`, `throw` u otra instrucción que impida continuar dentro del `switch`.

Para nuestros ejercicios utilizaremos `break` después de cada `case`.

Por ejemplo:

```csharp
switch (herramienta)
{
    case "espada":
        Console.WriteLine("Espada");
        break;

    case "arco":
        Console.WriteLine("Arco");
        break;
}
```

De esta manera cada opción tiene claramente:

```text
case
 ↓
acciones
 ↓
break
 ↓
salir
```

---

# 8. `default`

¿Pero qué pasa si el valor de la variable no coincide con ninguno de los `case`?

Podemos utilizar:

```csharp
default
```

`default` significa:

> **Si ninguna de las opciones anteriores coincide, haz esto.**

Por ejemplo:

```csharp
string herramienta = "poción";

switch (herramienta)
{
    case "espada":
        Console.WriteLine("Has elegido una espada.");
        break;

    case "arco":
        Console.WriteLine("Has elegido un arco.");
        break;

    case "antorcha":
        Console.WriteLine("Has elegido una antorcha.");
        break;

    default:
        Console.WriteLine("No reconocemos esa herramienta.");
        break;
}
```

Si `herramienta` contiene `"poción"`, ninguno de los `case` coincide.

Entonces se ejecuta:

```text
No reconocemos esa herramienta.
```

`default` funciona de manera similar al `else` que ya conocemos:

```text
if / else

si ocurre una condición
        ↓
       if

si no ocurre
        ↓
      else
```

En `switch`:

```text
case

si coincide una opción
        ↓
      case

si ninguna coincide
        ↓
     default
```

### `default` no es obligatorio

Un `switch` puede funcionar sin `default`.

Por ejemplo:

```csharp
switch (herramienta)
{
    case "espada":
        Console.WriteLine("Has elegido una espada.");
        break;

    case "arco":
        Console.WriteLine("Has elegido un arco.");
        break;
}
```

Si la variable no coincide con ninguno de los `case`, simplemente no se ejecutará ningún bloque del `switch` y el programa continuará después de él.

Sin embargo, `default` resulta útil cuando queremos establecer qué debe ocurrir cuando ninguna opción coincide.

---

# 9. `switch` con entradas del usuario

Podemos combinar `switch` con `Console.ReadLine()`.

Por ejemplo:

```csharp
Console.WriteLine("Elige una herramienta:");
Console.WriteLine("1. Espada");
Console.WriteLine("2. Arco");
Console.WriteLine("3. Antorcha");

string herramienta = Console.ReadLine();

switch (herramienta)
{
    case "1":
        Console.WriteLine("Has elegido una espada.");
        break;

    case "2":
        Console.WriteLine("Has elegido un arco.");
        break;

    case "3":
        Console.WriteLine("Has elegido una antorcha.");
        break;

    default:
        Console.WriteLine("Opción no válida.");
        break;
}
```

Aquí el usuario toma una decisión.

El programa recibe esa decisión y `switch` determina qué camino seguir.

Podemos representarlo así:

```text
             elección del usuario
                     │
                     ▼
                  switch
                     │
        ┌────────────┼────────────┐
        ▼            ▼            ▼
      case 1       case 2       case 3
        │            │            │
        ▼            ▼            ▼
      espada        arco       antorcha
```

Si ninguna opción coincide:

```text
                     switch
                        │
                        ▼
               ninguna coincidencia
                        │
                        ▼
                     default
```

---

# 10. `switch` y `if`

`switch` y `if` pueden utilizarse para tomar decisiones, pero no funcionan exactamente de la misma manera.

Con `if` podemos realizar comparaciones:

```csharp
if (puntos > 30)
{
    Console.WriteLine("Puedes pasar de nivel.");
}
```

Aquí estamos preguntando si:

```text
puntos > 30
```

Con `switch`, normalmente estamos buscando coincidencias entre un valor y diferentes opciones:

```csharp
switch (herramienta)
{
    case "espada":
        // ...
        break;

    case "arco":
        // ...
        break;
}
```

Estamos preguntando:

```text
¿herramienta es "espada"?

¿herramienta es "arco"?
```

Por eso `switch` resulta especialmente útil cuando tenemos **una variable con diferentes opciones posibles**.

---

# 11. `switch` con números

`switch` no solamente funciona con textos.

También podemos utilizar números.

Por ejemplo:

```csharp
int nivel = 2;

switch (nivel)
{
    case 1:
        Console.WriteLine("Nivel inicial.");
        break;

    case 2:
        Console.WriteLine("Nivel intermedio.");
        break;

    case 3:
        Console.WriteLine("Nivel avanzado.");
        break;

    default:
        Console.WriteLine("Nivel no válido.");
        break;
}
```

El programa revisa el valor de `nivel` y busca el `case` correspondiente.

Si:

```text
nivel = 2
```

se ejecuta:

```text
Nivel intermedio.
```

---

# 12. `switch` no reemplaza todos los `if`

Es importante entender que `switch` no significa que ya no necesitemos `if`.

Cada estructura tiene situaciones en las que resulta más conveniente.

Por ejemplo, si queremos preguntar:

```csharp
if (puntos > 30)
```

`if` resulta apropiado porque estamos haciendo una comparación.

Pero si queremos saber cuál de varias opciones eligió el usuario:

```text
espada
arco
antorcha
poción
```

`switch` puede hacer que el código sea más claro.

También podemos utilizar `if` y `switch` dentro del mismo programa.

---

# Ejercicio: actualizar el programa de creación de personajes

En el ejercicio anterior creamos un programa en el que el usuario:

* introduce su nombre;
* elige una herramienta;
* elige su color preferido;
* indica si le gusta el té;
* recibe un rol;
* recibe características de acuerdo con ese rol;
* puede ver las características de su personaje.

Ahora vamos a **revisar ese mismo programa para decidir dónde resulta conveniente utilizar `switch` y dónde es mejor mantener `if`**.

## Objetivo

Analizar las decisiones que ya existen en el programa y determinar **qué estructura resulta más apropiada para cada una**.

No todas las decisiones deben convertirse en `switch`.

La pregunta principal es:

> **¿Esta decisión consiste en comparar una variable con diferentes opciones concretas?**

Si la respuesta es sí, `switch` puede ser una buena opción.

Si necesitamos realizar comparaciones como:

```text
puntos > 30
puntos >= 50
!estaCansado
tieneAntorcha && tieneLlave
```

`if` continúa siendo una estructura apropiada.

---

## Revisar el código anterior

Toma el programa creado en el ejercicio anterior y revisa cada una de sus decisiones.

Por ejemplo:

```text
¿La herramienta tiene diferentes opciones?
        ↓
¿El color tiene diferentes opciones?
        ↓
¿Le gusta el té?
        ↓
¿Los puntos cumplen una condición?
        ↓
¿Tiene determinadas características?
```

Para cada decisión, determina si resulta más conveniente utilizar:

```text
if
```

o:

```text
switch
```

---

## Identificar los casos apropiados para `switch`

Busca dentro de tu programa las situaciones en las que una misma variable puede tener diferentes valores concretos.

Por ejemplo:

```text
herramienta
    ├── espada
    ├── arco
    └── antorcha
```

o:

```text
color
    ├── rojo
    ├── azul
    └── verde
```

Estas son situaciones en las que puedes considerar utilizar:

```text
switch
case
break
default
```

---

## Mantener los `if` cuando sean necesarios

No debes eliminar los `if` solamente porque ahora conoces `switch`.

Si una condición necesita realizar una comparación, puedes mantener el `if`.

Por ejemplo:

```text
puntos > 30
```

o:

```text
tieneAntorcha && tieneLlave
```

siguen siendo condiciones apropiadas para `if`.

El objetivo es **elegir la estructura adecuada para cada decisión**.

---

## Actualizar el programa

Después de identificar las situaciones apropiadas:

1. Actualiza el código.
2. Utiliza `switch` donde resulte más claro.
3. Mantén `if` donde sea necesario.
4. Utiliza `case` para las diferentes opciones.
5. Utiliza `break` después de cada `case`.
6. Utiliza `default` cuando quieras establecer qué ocurre si ninguna opción coincide.

El programa debe seguir funcionando de la misma manera para el usuario.

---

## Resultado

Al finalizar, el programa debe continuar mostrando:

```text
Nombre del jugador
Rol
Velocidad
Fuerza
Inteligencia
Resistencia
```

El resultado debe depender de las decisiones tomadas por el usuario.

La diferencia estará en **cómo está organizado el código para tomar esas decisiones**.

---

## Pregunta final

Compara el programa original con el programa actualizado.

Pregúntate:

* ¿Qué decisiones funcionan mejor con `if`?
* ¿Qué decisiones funcionan mejor con `switch`?
* ¿Por qué?
* ¿Qué función cumple `case`?
* ¿Qué función cumple `break`?
* ¿Qué ocurre cuando ninguna opción coincide?
* ¿Para qué sirve `default`?
* ¿Por qué no sería conveniente utilizar `switch` para absolutamente todas las decisiones?

El objetivo no es reemplazar `if` por `switch`, sino aprender a **reconocer cuándo cada estructura resulta más adecuada**.


# `switch`, `case` y `break` en C#

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

espada  → hacer una cosa
arco    → hacer otra
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

Podemos identificar tres elementos principales:

* `switch`
* `case`
* `break`

También existe `default`, que veremos más adelante.

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

```csharp
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

# Ejercicio: transformar el programa de creación de personajes

En el ejercicio anterior creamos un programa en el que el usuario:

* introduce su nombre;
* elige una herramienta;
* elige su color preferido;
* indica si le gusta el té;
* recibe un rol;
* recibe características de acuerdo con ese rol;
* puede ver las características de su personaje.

Ahora vamos a **transformar ese mismo programa** utilizando `switch`.

## Objetivo

Tomar el código realizado anteriormente y modificar la forma en que se toman las decisiones.

El resultado final debe ser equivalente al programa anterior, pero utilizando `switch`, `case`, `break` y `default` en las decisiones donde resulte apropiado.

---

## Mantener el funcionamiento anterior

El programa debe seguir permitiendo que el usuario:

1. Introduzca su nombre.
2. Seleccione una herramienta de las opciones disponibles.
3. Seleccione su color preferido.
4. Indique si le gusta el té.
5. Reciba un rol.
6. Consulte las características de ese rol.

Los roles y características pueden mantenerse iguales a los del ejercicio anterior.

---

## Transformar las decisiones

Revisa las decisiones que realizaste anteriormente con:

```text
if
else if
else
```

y determina cuáles pueden expresarse mejor utilizando:

```text
switch
case
break
default
```

Por ejemplo, si una decisión depende de que una variable pueda tener diferentes opciones concretas:

```text
espada
arco
antorcha
```

puede ser una buena candidata para utilizar `switch`.

---

## Utilizar `default`

El programa debe contemplar qué ocurre cuando el usuario introduce una opción que no corresponde con las opciones disponibles.

Para estos casos utiliza:

```text
default
```

---

## Mantener las decisiones del usuario

El usuario debe seguir siendo quien tome las decisiones.

El programa no debe tener todas las respuestas determinadas desde el principio.

Las decisiones deben realizarse mediante las entradas del usuario.

---

## Resultado

Al finalizar, el programa debe mostrar nuevamente información como:

```text
Nombre del jugador
Rol
Velocidad
Fuerza
Inteligencia
Resistencia
```

El resultado debe depender de las decisiones tomadas por el usuario.

---

## Pregunta final

Compara tu programa anterior con esta nueva versión.

Pregúntate:

* ¿Qué decisiones eran más fáciles de expresar con `if`?
* ¿Cuáles resultan más claras con `switch`?
* ¿Qué función cumple `case`?
* ¿Qué función cumple `break`?
* ¿Qué ocurre cuando ninguna opción coincide?
* ¿Para qué sirve `default`?

El objetivo no es solamente conseguir que el programa funcione, sino reconocer **cuándo una estructura `switch` puede hacer que las decisiones del programa sean más claras de leer**.

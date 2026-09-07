# Condicionales en C#: `if`, `else` y `else if`

Los condicionales permiten que un programa **tome decisiones**.

Hasta ahora hemos trabajado con variables, tipos de datos, operadores, arrays y entradas del usuario. Ahora podemos hacer que el programa **reaccione de diferentes maneras dependiendo de los datos que recibe**.

La estructura más importante para esto es `if`.

---

# 1. ¿Qué es un `if`?

`if` significa **"si"**.

Podemos imaginarlo como una pregunta que el programa se hace:

> **Si ocurre esto, haz esto.**

Por ejemplo:

```csharp
if (tieneAntorcha)
{
    Console.WriteLine("Puedes entrar a la cueva.");
}
```

El programa pregunta:

> ¿`tieneAntorcha` es verdadero?

Si la respuesta es `true`, ejecuta lo que está dentro de las llaves `{ }`.

Si la respuesta es `false`, no ejecuta esas instrucciones.

---

# 2. `if` utilizando una entrada del usuario

También podemos utilizar las decisiones que toma el usuario.

Por ejemplo:

```csharp
Console.WriteLine("¿Quieres entrar a la cueva?");
string respuesta = Console.ReadLine();

if (respuesta == "si")
{
    Console.WriteLine("Entras a la cueva.");
}
```

Aquí ocurre lo siguiente:

1. El programa pregunta algo.
2. El usuario escribe una respuesta.
3. La respuesta se guarda en una variable.
4. `if` compara esa respuesta.
5. Si la condición es verdadera, se ejecuta el código dentro de `{ }`.

La condición es:

```csharp
respuesta == "si"
```

Estamos preguntando:

> ¿La variable `respuesta` contiene exactamente `"si"`?

---

# 3. Los operadores de comparación

Los condicionales utilizan operadores de comparación para tomar decisiones.

| Operador | Significado       |
| -------- | ----------------- |
| `>`      | mayor que         |
| `<`      | menor que         |
| `>=`     | mayor o igual que |
| `<=`     | menor o igual que |
| `==`     | igual a           |
| `!=`     | diferente de      |

Por ejemplo:

```csharp
if (puntos > 30)
{
    Console.WriteLine("Puedes pasar de nivel.");
}
```

Aquí la condición pregunta:

> ¿Los puntos son mayores que 30?

Si `puntos` vale `35`, la condición es verdadera.

Si `puntos` vale `20`, la condición es falsa.

---

# 4. `=` no es lo mismo que `==`

Es importante diferenciar estos dos operadores.

### `=`

Se utiliza para **asignar un valor** a una variable.

```csharp
int puntos = 50;
```

Estamos diciendo:

> Guarda el valor `50` dentro de `puntos`.

### `==`

Se utiliza para **comparar**.

```csharp
if (puntos == 50)
{
    Console.WriteLine("Tienes exactamente 50 puntos.");
}
```

Estamos preguntando:

> ¿`puntos` es igual a `50`?

Una forma sencilla de recordarlo:

```text
=   → guardar / asignar

==  → comparar
```

---

# 5. Las variables también pueden ser condiciones

Una variable `bool` puede utilizarse directamente en un `if`.

Por ejemplo:

```csharp
bool tieneAntorcha = true;

if (tieneAntorcha)
{
    Console.WriteLine("Puedes entrar a la cueva.");
}
```

No necesitamos escribir:

```csharp
if (tieneAntorcha == true)
```

aunque también funcionaría.

Podemos simplemente escribir:

```csharp
if (tieneAntorcha)
```

Porque la variable ya contiene un valor `true` o `false`.

---

# 6. Utilizar números como condiciones

También podemos utilizar variables numéricas.

```csharp
int puntos = 45;

if (puntos > 30)
{
    Console.WriteLine("Puedes pasar de nivel.");
}
```

El programa comprueba la condición:

```text
45 > 30
```

Como es verdadera, ejecuta el código dentro del `if`.

Podemos hacer lo mismo con otras comparaciones:

```csharp
if (puntos >= 100)
{
    Console.WriteLine("Has alcanzado el nivel máximo.");
}
```

---

# 7. Combinar condiciones con `&&`

El operador `&&` significa **"y"**.

Las dos condiciones deben ser verdaderas.

Por ejemplo:

```csharp
if (tieneAntorcha && tieneLlave)
{
    Console.WriteLine("Puedes entrar a la cámara secreta.");
}
```

Para entrar necesitamos:

```text
tener antorcha
     Y
tener llave
```

Si falta cualquiera de las dos, la condición será falsa.

Podemos imaginarlo así:

```text
tieneAntorcha → TRUE
tieneLlave    → TRUE

TRUE && TRUE → TRUE
```

Pero:

```text
tieneAntorcha → TRUE
tieneLlave    → FALSE

TRUE && FALSE → FALSE
```

---

# 8. Combinar condiciones con `||`

El operador `||` significa **"o"**.

En este caso, basta con que una de las condiciones sea verdadera.

Por ejemplo:

```csharp
if (tieneAntorcha || tieneLinterna)
{
    Console.WriteLine("Puedes entrar a la cueva.");
}
```

El personaje puede entrar si tiene:

* una antorcha
* una linterna
* o ambas

Podemos imaginarlo así:

```text
tieneAntorcha → TRUE
tieneLinterna → FALSE

TRUE || FALSE → TRUE
```

---

# 9. El operador `!`

El operador `!` significa **"no"** o **"lo contrario de"**.

Por ejemplo:

```csharp
bool estaCansado = false;

if (!estaCansado)
{
    Console.WriteLine("Puedes continuar caminando.");
}
```

La condición:

```csharp
!estaCansado
```

significa:

> No está cansado.

Si:

```csharp
estaCansado = false;
```

entonces:

```csharp
!estaCansado
```

es `true`.

---

# 10. Combinar diferentes operadores

Podemos utilizar varios operadores al mismo tiempo.

Por ejemplo:

```csharp
if (puntos > 30 && tieneAntorcha)
{
    Console.WriteLine("Puedes entrar al siguiente nivel.");
}
```

Aquí necesitamos cumplir **dos condiciones**:

```text
puntos > 30
     Y
tieneAntorcha
```

También podemos utilizar `||`:

```csharp
if (puntos > 30 || tieneAntorcha)
{
    Console.WriteLine("Puedes continuar.");
}
```

Ahora basta con cumplir una de las dos condiciones.

También podemos combinar `!`:

```csharp
if (puntos > 30 && !estaCansado)
{
    Console.WriteLine("Puedes continuar.");
}
```

La condición significa:

> Tienes más de 30 puntos **y además** no estás cansado.

---

# 11. `else`

Hasta ahora hemos visto qué ocurre cuando una condición es verdadera.

Pero ¿qué pasa cuando es falsa?

Para eso podemos utilizar `else`.

`else` significa:

> **Si no ocurre lo anterior, haz esto.**

Por ejemplo:

```csharp
if (tieneAntorcha)
{
    Console.WriteLine("Puedes entrar a la cueva.");
}
else
{
    Console.WriteLine("No puedes entrar a la cueva.");
}
```

Tenemos dos posibilidades:

```text
          ¿Tiene antorcha?
             /       \
           SÍ         NO
           |           |
        entra        no entra
```

Si `tieneAntorcha` es `true`, se ejecuta el primer bloque.

Si es `false`, se ejecuta el bloque de `else`.

---

# 12. `else if`

A veces no tenemos solamente dos posibilidades.

Podemos tener varias.

Para eso utilizamos `else if`.

Por ejemplo:

```csharp
if (puntos >= 100)
{
    Console.WriteLine("Nivel 3");
}
else if (puntos >= 50)
{
    Console.WriteLine("Nivel 2");
}
else
{
    Console.WriteLine("Nivel 1");
}
```

Aquí tenemos tres posibilidades:

```text
100 o más puntos → Nivel 3

50 a 99 puntos   → Nivel 2

menos de 50      → Nivel 1
```

El programa revisa las condiciones **de arriba hacia abajo**.

Cuando encuentra una condición verdadera, ejecuta ese bloque y continúa después de toda la estructura.

Por ejemplo, si:

```csharp
puntos = 75;
```

El programa pregunta:

```text
¿puntos >= 100?
NO

¿puntos >= 50?
SÍ
```

Entonces muestra:

```text
Nivel 2
```

No continúa comprobando las siguientes condiciones de esa cadena.

---

# Ejercicio: creación de un personaje a partir de decisiones

## Objetivo

Continuar el programa creado en el ejercicio anterior utilizando **entradas del usuario y condicionales** para construir un personaje dentro de un juego ficticio.

El programa debe hacer preguntas al usuario y, de acuerdo con sus respuestas, determinar qué **rol** tendrá su personaje y cuáles serán sus características.

---

## Historia

Imagina que estás creando un personaje para un videojuego.

Al comenzar la partida, el jugador debe tomar algunas decisiones. No existe una única respuesta correcta: sus elecciones determinarán el tipo de personaje que recibirá.

El programa puede preguntar:

* El **nombre** del jugador.
* Qué **herramienta** quiere llevar.
* Cuál es su **color preferido**.
* Si le gusta o no el **té**.

Las opciones deben ser presentadas por el programa para que el usuario pueda elegir entre ellas.

Por ejemplo, el programa puede ofrecer diferentes herramientas, colores y respuestas posibles, es a tu eleccion.

---

## Creación del rol

A partir de las decisiones del jugador, el programa debe asignarle un **rol** dentro de un juego inventado.

Puedes crear tus propios roles.

Por ejemplo:

* Explorador
* Guerrero
* Mago
* Ingeniero
* Curandero

Las decisiones del jugador deben determinar cuál de estos roles recibe.

No todos los roles tienen que depender de una sola decisión. Puedes combinar varias respuestas para determinar el resultado.

Por ejemplo, una combinación de decisiones podría hacer que el personaje sea un Explorador, mientras que otra combinación podría convertirlo en un Ingeniero.

---

## Características del personaje

Cada rol debe tener diferentes características.

Puedes utilizar características como:

* Velocidad
* Fuerza
* Inteligencia
* Resistencia
* Puntos
* Vida

Cada rol debe tener valores diferentes.

Por ejemplo:

| Rol        | Velocidad | Fuerza | Inteligencia | Resistencia |
| ---------- | --------: | -----: | -----------: | ----------: |
| Explorador |        90 |     50 |           70 |          60 |
| Guerrero   |        50 |     90 |           40 |          90 |
| Mago       |        40 |     30 |          100 |          50 |
| Ingeniero  |        60 |     50 |           95 |          70 |

Los valores de la tabla son solamente un ejemplo. Puedes crear tus propios roles y características.

---

## Condiciones

El programa debe utilizar las decisiones del usuario para determinar el rol.

Las condiciones deben utilizar diferentes operadores que ya conocemos:

* `==`
* `!=`
* `>`
* `<`
* `>=`
* `<=`
* `&&`
* `||`
* `!`

También debes utilizar:

* `if`
* `else if`
* `else`
* al menos un **`if` dentro de otro `if`**

---



## Resultado

Al finalizar las decisiones, el programa debe mostrar:

```text
Nombre del jugador
Rol
Velocidad
Fuerza
Inteligencia
Resistencia
```

El usuario debe poder introducir su nombre al inicio y, después de tomar sus decisiones, descubrir qué personaje obtuvo.

---

## Condición importante

**No debe existir un único camino obligatorio.**

El resultado debe cambiar dependiendo de las respuestas introducidas por el usuario.

La idea es que el mismo programa pueda producir diferentes personajes.

Por ejemplo:

```text
Jugador 1 → Explorador
Jugador 2 → Guerrero
Jugador 3 → Mago
Jugador 4 → Ingeniero
```

Cada jugador debe poder obtener características diferentes a partir de sus decisiones.

---

## Pregunta final

Una vez terminado el programa, prueba diferentes combinaciones de respuestas.

Pregúntate:

**¿Qué ocurre si cambio solamente una de las decisiones del jugador?**

¿El rol cambia?

¿Cambian sus características?

¿Hay decisiones que, combinadas con otras, producen un resultado diferente?

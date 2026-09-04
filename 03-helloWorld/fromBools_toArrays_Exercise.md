# Variables booleanas y operaciones

## 1. Variables booleanas

En C# existe un tipo de variable llamado `bool`.

Una variable `bool` solo puede tener uno de dos valores:

```csharp
true
false
```

Por ejemplo:

```csharp
bool tieneVida = true;
bool juegoTerminado = false;
```

Podemos utilizar las variables booleanas para representar situaciones que pueden ser **verdaderas o falsas**.

En un videojuego podrían representar:

```csharp
bool estaVivo = true;
bool tieneLlave = false;
bool puedeSaltar = true;
bool juegoTerminado = false;
```

---

## 2. Operaciones con booleanos

Podemos comparar valores para obtener un resultado `true` o `false`.

Por ejemplo:

```csharp
int vidas = 3;

bool estaVivo = vidas > 0;
```

La expresión:

```csharp
vidas > 0
```

pregunta:

> ¿`vidas` es mayor que `0`?

Como `vidas` vale `3`, el resultado es:

```text
true
```

También podemos utilizar:

```csharp
>   mayor que
<   menor que
>=  mayor o igual que
<=  menor o igual que
==  igual a
!=  diferente de
```

Ejemplos:

```csharp
int puntos = 100;

bool tienePuntos = puntos > 0;
bool gano = puntos >= 100;
bool sinPuntos = puntos == 0;
```

---

## 3. Operadores lógicos

También podemos combinar condiciones.

### AND `&&`

Las dos condiciones deben ser verdaderas.

```csharp
bool tieneLlave = true;
bool estaEnPuerta = true;

bool puedeAbrir = tieneLlave && estaEnPuerta;
```

### OR `||`

Al menos una condición debe ser verdadera.

```csharp
bool tieneLlave = false;
bool tieneLlaveMaestra = true;

bool puedeAbrir = tieneLlave || tieneLlaveMaestra;
```

### NOT `!`

Invierte el valor.

```csharp
bool estaVivo = true;

bool estaMuerto = !estaVivo;
```

---

# 4. Ejercicio: estado del personaje

Crea un programa que represente el estado de un personaje de videojuego.

El personaje debe tener las siguientes variables:

```text
nombre
vidas
puntos
velocidad
tieneLlave
estaEnLaPuerta
```

Utiliza los tipos de variables apropiados.

Después crea variables booleanas que permitan determinar:

1. Si el personaje está vivo.
2. Si el personaje puede abrir la puerta.
3. Si el personaje puede avanzar de nivel.

### Condiciones

El personaje está vivo si tiene más de 0 vidas.

El personaje puede abrir la puerta si:

* tiene una llave **Y**
* está en la puerta.

El personaje puede avanzar de nivel si:

* tiene al menos 100 puntos **Y**
* está vivo.

Finalmente, utiliza `Console.WriteLine()` para mostrar los resultados.

### Código inicial

```csharp
using System;

class Program
{
    static void Main()
    {
        // Variables del personaje


        
        // Variables booleanas


        
        // Mostrar resultados


    }
}
```

### Preguntas

**¿Qué variables son necesarias para representar la información del personaje?**

**¿Cuáles son `bool` y por qué?**

**¿Qué operaciones utilizaste para obtener los valores booleanos?**

**¿Qué ocurre si cambias el número de vidas a `0`?**

**¿Qué ocurre si `tieneLlave` cambia de `false` a `true`?**

**¿Qué ocurre si el personaje tiene 150 puntos pero `estaVivo` es `false`?**

# Arrays y organización de información

## 1. ¿Qué es un array?

Un **array** permite guardar varios valores dentro de una misma variable.

Por ejemplo:

```csharp
string[] nombres = { "Ana", "Bruno", "Carla", "Diego" };
```

Este array guarda cuatro nombres:

```text
Índice:    0        1        2        3
           ↓        ↓        ↓        ↓
Valor:    Ana    Bruno    Carla    Diego
```

Un array comienza siempre en el **índice 0**.

Podemos acceder a un elemento utilizando su índice:

```csharp
Console.WriteLine(nombres[0]);
```

Resultado:

```text
Ana
```

También:

```csharp
Console.WriteLine(nombres[2]);
```

Resultado:

```text
Carla
```

---

## 2. Un array organiza información

Un array puede guardar información del mismo tipo.

Por ejemplo:

```csharp
int[] edades = { 20, 25, 19, 22 };
```

Aquí todos los elementos son números enteros.

También podemos tener:

```csharp
string[] nombres = { "Ana", "Bruno", "Carla", "Diego" };
```

Aquí todos los elementos son `string`.


---

## 3. Relacionar información mediante índices

Podemos tener diferentes arrays que utilizan los **mismos índices** para relacionar información.

Por ejemplo:

```csharp
string[] nombres = { "Ana", "Bruno", "Carla", "Diego" };

int[] edades = { 20, 25, 19, 22 };
```

Podemos organizar la información así:

| Índice | `nombres` | `edades` |
| -----: | --------- | -------: |
|      0 | Ana       |       20 |
|      1 | Bruno     |       25 |
|      2 | Carla     |       19 |
|      3 | Diego     |       22 |

El índice `0` relaciona:

```text
Ana → 20
```

El índice `1` relaciona:

```text
Bruno → 25
```

El índice `2` relaciona:

```text
Carla → 19
```


---

# 4. Ejercicio

Base de datos de jugadores

Crea una base de datos con al menos 5 jugadores ficticios.

Cada jugador debe tener las siguientes características:

Nombre
Vidas
Puntos
Velocidad
Tiene llave
Está en la puerta

La información de cada jugador debe estar relacionada correctamente, de manera que puedas identificar todas las características de un mismo jugador.

Además:

Debe existir una sola variable que permita seleccionar qué jugador visualizar.
Al cambiar únicamente el valor de esa variable, deben mostrarse las características completas de otro jugador.
Utiliza Console.WriteLine() para visualizar la información del jugador seleccionado.

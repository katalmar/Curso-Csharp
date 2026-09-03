
# Introducción a variables en C#

## 1. Ejecuta el código

Ingresa a **.NET Fiddle**:

https://dotnetfiddle.net/

Selecciona **C# → Console**, copia el siguiente código y presiona **Run**.

```csharp
using System;

class Program
{
    static void Main()
    {
        string nombre = "Luna";
        int vidas = 3;
        float velocidad = 5.5f;

        Console.WriteLine("Nombre: " + nombre);
        Console.WriteLine("Vidas: " + vidas);
        Console.WriteLine("Velocidad: " + velocidad);

        vidas = vidas - 1;
        velocidad = velocidad + 2.0f;

        Console.WriteLine("Después de jugar:");
        Console.WriteLine("Vidas: " + vidas);
        Console.WriteLine("Velocidad: " + velocidad);
    }
}
```

Observa el resultado y luego responde las siguientes preguntas.

## 2. Variables
Una **variable** es un espacio de memoria identificado por un nombre que permite almacenar un valor que puede ser utilizado y modificado durante la ejecución del programa.
Observa:

```csharp
string nombre = "Luna";
int vidas = 3;
float velocidad = 5.5f;
```

**¿Cuántas variables se están declarando en el código?**

**¿Cuáles son sus nombres?**

**¿Cuántos tipos de variables diferentes encuentras?**

**¿Que otro tipos de variables crees que existan?**


---

## 3. Operaciones con variables

Observa:

```csharp
vidas = vidas - 1;
velocidad = velocidad + 2.0f;
```

**¿Qué ocurre con las variables `vidas` y `velocidad`?**

**¿Se pueden realizar operaciones utilizando variables?**

**¿Se pueden modificar los valores de las variables?**

**¿Se pueden utilizar dos o más variables dentro de una misma operación?**

---

## 4. `Console.WriteLine()`

Observa:

```csharp
Console.WriteLine("Nombre: " + nombre);
```

**¿Qué hace `Console.WriteLine()`?**

**¿Qué información aparece en la consola?**

**¿Qué crees que significa `"Nombre: "`?**

**¿Qué crees que significa `nombre`?**

Prueba cambiar:

```csharp
Console.WriteLine("Nombre: " + nombre);
```

por:

```csharp
Console.WriteLine("Hola");
```

¿Qué ocurre?

---

## 5. El punto y coma `;`

Observa las instrucciones del código.

**¿Qué símbolo aparece al final de muchas de ellas?**

```csharp
int vidas = 3;
vidas = vidas - 1;
Console.WriteLine(vidas);
```

Elimina uno de los `;` y vuelve a ejecutar.

**¿Qué sucede?**

**¿Para qué crees que sirve el `;`?**

En C#, el `;` indica normalmente el **final de una instrucción**.

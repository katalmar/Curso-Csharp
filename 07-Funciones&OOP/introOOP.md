# Programación Orientada a Objetos (POO): clases, objetos y member variables

## De variables sueltas a algo que las agrupe

Hasta ahora, cuando queríamos representar a un personaje, usábamos variables sueltas o un array:

```csharp
string nombre = "Ana";
string rol = "Explorador";
int velocidad = 90;
int fuerza = 50;
int inteligencia = 70;
int resistencia = 60;
```

O, como en el ejercicio anterior, guardábamos las características numéricas en un array:

```csharp
int[] caracteristicas = { 90, 50, 70, 60 }; // velocidad, fuerza, inteligencia, resistencia
```

Esto funciona, pero tiene un problema: nada en el código te dice "estas 6 variables (o estas 4 posiciones del array) pertenecen juntas, representan a un solo personaje". Si tuvieran que manejar dos jugadores a la vez, terminarían con `nombre1`, `nombre2`, `caracteristicas1`, `caracteristicas2`... o arrays de arrays, cada vez más confuso.

La **Programación Orientada a Objetos (POO)** resuelve exactamente este problema: nos deja crear **un nuevo tipo propio**, hecho a la medida, que agrupa todos los datos que pertenecen juntos bajo un solo nombre.

---

## Clase: el molde

Una **clase** es la definición de un nuevo tipo de dato — un molde que describe **qué información** va a tener algo. Se parece a la idea del `delegate` que vimos hace poco (que describía la "forma" de una función); una clase describe la "forma" de un objeto.

```csharp
class Personaje
{
    public string nombre;
    public int vida;
}
```

Aquí `Personaje` es un tipo nuevo, tan válido como `int` o `string`, que nosotros mismos acabamos de inventar. Dice: *"todo lo que sea de tipo `Personaje` va a tener un `nombre` (string) y una `vida` (int)"*.

### Member variables (campos)

`nombre` y `vida`, dentro de la clase, se llaman **member variables** (o **campos**): son las variables que le pertenecen a cada objeto de ese tipo. La palabra `public` significa que, por ahora, van a poder acceder y modificar esos campos libremente desde fuera de la clase (más adelante verán por qué a veces conviene restringir esto — por ahora, `public` para todo).

> 🔑 Por ahora nos quedamos **solo** en esta parte: declarar member variables dentro de una clase. Los métodos (funciones dentro de una clase) y los constructores los veremos en otra sesión.

---

## Objeto: una instancia del molde

La clase es solo el **molde** — el plano. Para tener algo real que usar, hay que crear un **objeto**, también llamado una **instancia** de esa clase, usando `new`:

```csharp
Personaje heroe = new Personaje();
```

`heroe` ahora es una variable de tipo `Personaje`, con sus propios `nombre` y `vida`, listos para usarse (aunque todavía vacíos/en cero).

### Accediendo y asignando los campos: el `.`

Para leer o modificar los campos de un objeto, se usa un punto `.` entre el nombre del objeto y el nombre del campo:

```csharp
heroe.nombre = "Ana";
heroe.vida = 100;

Console.WriteLine(heroe.nombre); // Ana
Console.WriteLine(heroe.vida);   // 100
```

### La clave: se pueden crear muchas instancias del mismo molde

```csharp
Personaje heroe = new Personaje();
heroe.nombre = "Ana";
heroe.vida = 100;

Personaje villano = new Personaje();
villano.nombre = "Draven";
villano.vida = 150;

Console.WriteLine(heroe.nombre);   // Ana
Console.WriteLine(villano.nombre); // Draven
```

`heroe` y `villano` son dos objetos completamente independientes, ambos hechos con el mismo molde (`Personaje`), cada uno con sus propios valores. Esto es justo lo que antes nos costaba trabajo lograr con variables sueltas o arrays — ahora cada personaje es **una sola cosa**, con nombre propio, en vez de un montón de variables o posiciones de array dispersas que había que recordar que iban juntas.

---

## `private`: campos que solo la propia clase puede tocar

Hasta ahora todos nuestros campos son `public`: cualquier código de afuera puede leerlos y modificarlos libremente (`heroe.vida = -500;` funcionaría, aunque no tenga sentido que una vida sea negativa). `private` restringe eso: un campo `private` **solo puede ser leído o modificado desde dentro de la misma clase**, nunca directamente desde afuera.

```csharp
class Personaje
{
    private int vida;
}
```

```csharp
Personaje heroe = new Personaje();
heroe.vida = 100; // ❌ Error: 'vida' es privado, no se puede acceder desde afuera
```

¿Y entonces cómo le damos o le leemos el valor? Ahí es donde entran los **métodos**.

---

## Métodos: funciones que viven dentro de una clase

Un **método** es simplemente una función, igual a las que ya conocen, pero declarada **dentro** de una clase. La diferencia es que un método tiene acceso directo a los campos de esa clase (incluyendo los `private`), sin que se los tengan que pasar como parámetro.

```csharp
class Personaje
{
    private int vida;

    public void RecibirDaño(int cantidad)
    {
        vida = vida - cantidad; // accede directamente al campo "vida" de este objeto
        Console.WriteLine($"Vida restante: {vida}");
    }
}
```

```csharp
Personaje heroe = new Personaje();
heroe.RecibirDaño(30); // Vida restante: -30 (bueno, faltaría inicializar vida en 100, ¡pero la idea es esa!)
```

Fíjense en algo importante: `RecibirDaño` es `public` (se puede llamar desde afuera, con `heroe.RecibirDaño(...)`), pero el campo `vida` que modifica por dentro es `private` (nadie de afuera puede tocarlo directamente). Este es el patrón típico en POO: **los campos se esconden como `private`, y los métodos `public` son la única forma permitida de interactuar con ellos.** Así la clase controla exactamente cómo se le puede cambiar el estado — nadie desde afuera puede, por accidente, dejar la vida en un valor absurdo.

### Lo más importante para nuestro ejercicio: una clase puede calcular sus propios valores

Hasta ahora, en el ejercicio del `Jugador`, la lógica de "qué rol le toca y qué características tiene" vivía en `Main`, y desde afuera le íbamos asignando campo por campo (`jugador1.rol = "Explorador"; jugador1.velocidad = 90;` ...). Con métodos, podemos mover **toda esa lógica adentro de la clase**: le pasamos el nombre y las decisiones del usuario como argumentos a un método, y es la propia clase la que decide su rol y calcula sus características.

```csharp
class Jugador
{
    public string nombre;
    private string rol;
    private int velocidad;
    private int fuerza;
    private int inteligencia;
    private int resistencia;

    public void AsignarPersonaje(string nombreElegido, string herramienta, bool leGustaElTe)
    {
        nombre = nombreElegido;

        if (herramienta == "mapa")
        {
            rol = "Explorador";
            velocidad = 90;
            fuerza = 50;
            inteligencia = 70;
            resistencia = 60;
        }
        else if (herramienta == "espada")
        {
            if (leGustaElTe)
            {
                rol = "Guerrero";
                velocidad = 50;
                fuerza = 90;
                inteligencia = 40;
                resistencia = 90;
            }
            else
            {
                rol = "Mago";
                velocidad = 40;
                fuerza = 30;
                inteligencia = 100;
                resistencia = 50;
            }
        }
    }

    public void MostrarPersonaje()
    {
        Console.WriteLine($"Nombre: {nombre}");
        Console.WriteLine($"Rol: {rol}");
        Console.WriteLine($"Velocidad: {velocidad}");
        Console.WriteLine($"Fuerza: {fuerza}");
        Console.WriteLine($"Inteligencia: {inteligencia}");
        Console.WriteLine($"Resistencia: {resistencia}");
    }
}
```

Y desde `Main`, todo lo que hacemos es recolectar las decisiones del usuario y pasárselas al objeto:

```csharp
Jugador jugador1 = new Jugador();
jugador1.AsignarPersonaje("Ana", "espada", true); // la clase decide: será Guerrero
jugador1.MostrarPersonaje();
```

`Main` ya no sabe (ni le importa) **cómo** se decide el rol — solo le entrega las decisiones crudas del usuario, y confía en que `AsignarPersonaje` se encargue de toda la lógica. Esa lógica quedó encapsulada (guardada, protegida) dentro de la clase `Jugador`, junto con los datos que le pertenecen.

---

## 📝 Ejercicio

Retomen el ejercicio que ya hicieron con `if` — el de las decisiones que determinaban el rol y las características del personaje — y modifíquenlo para que, en vez de guardar los resultados en variables sueltas o en un array, creen una clase `Jugador` que se encargue de todo: el nombre y las decisiones del usuario deben pasarse a un método de esa clase, y es la propia clase la que debe calcular y asignar internamente el rol y las características correspondientes.

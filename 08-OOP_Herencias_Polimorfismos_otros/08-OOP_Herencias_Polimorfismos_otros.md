# POO: Constructores, Herencia, Polimorfismo, `virtual` y `override`

## ¿Por qué el jugador no debería elegir su propio rol?

En el ejercicio anterior, la clase `Jugador` tenía un método `AsignarPersonaje` que hacía preguntas del estilo "¿qué herramienta elegiste?", y con eso decidía el rol y las características. Vale la pena detenerse a pensar si eso realmente le corresponde a la clase `Jugador`.

`Jugador` es un **concepto de las acciones del personaje dentro del juego**: mostrar sus datos, atacar, usar una habilidad especial. Pero **el jugador no está decidiendo conscientemente su propio rol** — el rol es el *resultado* de interpretar unas decisiones que alguien más tomó (el usuario, respondiendo preguntas). Esa interpretación — "dado que eligió espada y le gusta el té, ¿qué rol le corresponde?" — es lógica de **asignación y procesamiento**, no es algo que el personaje "hace" dentro del juego.

Por eso, esa lógica no debería vivir dentro de `Jugador`. Le corresponde al **exterior**: al código que está afuera de la clase, que recoge la información del usuario, decide qué rol le corresponde, y **luego** se lo entrega ya resuelto a `Jugador`.

---

## Sacando la decisión del rol a una función externa

En vez de un método `AsignarPersonaje` dentro de la clase, escribimos una función **fuera** de `Jugador` (junto a `Main`, no dentro de la clase) que recibe las decisiones del usuario y devuelve el nombre del rol que le corresponde:

```csharp
static string DeterminarRol(string herramienta, bool leGustaElTe)
{
    if (herramienta == "mapa")
    {
        return "Explorador";
    }
    else if (herramienta == "espada" && leGustaElTe)
    {
        return "Guerrero";
    }
    else
    {
        return "Mago";
    }
}
```

Esta función no sabe nada de la clase `Jugador` — solo recibe datos, y devuelve un `string` con el resultado. `Jugador`, por su parte, no va a necesitar saber **cómo** se decidió el rol, solo va a recibirlo ya resuelto.

---

## El constructor: pasando argumentos al crear un objeto

Hasta ahora, para llenar los datos de un objeto, primero lo creábamos vacío y después le íbamos asignando campo por campo:

```csharp
Jugador jugador1 = new Jugador();
jugador1.nombre = "Ana";
```

Un **constructor** nos permite hacer esto en un solo paso: es un método especial, con el mismo nombre de la clase, sin tipo de retorno, que se ejecuta automáticamente cuando usamos `new` — y que puede recibir argumentos, igual que cualquier otra función.

```csharp
class Jugador
{
    public string nombre;

    public Jugador(string nombreElegido)
    {
        nombre = nombreElegido;
    }
}
```

```csharp
Jugador jugador1 = new Jugador("Ana"); // nombre queda asignado de una vez, al crear el objeto
```

Ahora, con esto, ya podemos entregarle a `Jugador` el nombre **y** el rol ya resuelto, ambos como argumentos del constructor:

```csharp
public Jugador(string nombreElegido, string rolElegido)
{
    nombre = nombreElegido;
    rol = rolElegido;
    // ... (seguimos completando esto abajo)
}
```

---

## Dos tipos de valores dentro de una clase

Al construir un `Jugador`, no todos sus datos se comportan igual. Hay dos categorías:

1. **Valores que vienen del constructor** — se los tienen que entregar desde afuera al crear el objeto, porque son distintos para cada instancia. `nombre` y `rol` son así: no hay forma de que la clase "adivine" el nombre o el rol de un jugador, tienen que dárselo.

2. **Valores que ya vienen definidos por defecto en la clase** — son iguales para *cualquier* jugador, sin importar quién sea ni qué rol tenga, así que no hace falta pedirlos como argumento. `vidas` y `salud` son así: todo jugador arranca con las mismas vidas y la misma salud, sin importar si es Explorador, Guerrero o Mago.

```csharp
class Jugador
{
    public string nombre;
    public string rol;
    public int velocidad;
    public int fuerza;
    public int inteligencia;
    public int resistencia;
    public int vidas;
    public int salud;

    public Jugador(string nombreElegido, string rolElegido)
    {
        nombre = nombreElegido;
        rol = rolElegido;

        vidas = 3;      // valor por defecto: igual para todos, no viene del constructor
        salud = 100;    // valor por defecto: igual para todos, no viene del constructor

        AsignarCaracteristicasSegunRol(rol);
    }
}
```

> 🔑 Fíjense en la diferencia: `nombreElegido` y `rolElegido` son **parámetros** del constructor — el valor lo decide quien llama `new Jugador(...)`. `vidas = 3` y `salud = 100`, en cambio, están escritos directamente en el cuerpo del constructor, como un valor fijo — nadie de afuera los elige, la clase misma los define.

---

## Un método interno que asigna las características según el rol

Como `velocidad`, `fuerza`, `inteligencia` y `resistencia` sí dependen del rol (pero el rol ya nos llega resuelto, como un `string`), usamos un método `private` — solo lo usa la propia clase — para traducir ese `string` en números concretos:

```csharp
private void AsignarCaracteristicasSegunRol(string rolAsignado)
{
    if (rolAsignado == "Explorador")
    {
        velocidad = 90;
        fuerza = 50;
        inteligencia = 70;
        resistencia = 60;
    }
    else if (rolAsignado == "Guerrero")
    {
        velocidad = 50;
        fuerza = 90;
        inteligencia = 40;
        resistencia = 90;
    }
    else if (rolAsignado == "Mago")
    {
        velocidad = 40;
        fuerza = 30;
        inteligencia = 100;
        resistencia = 50;
    }
}
```

El constructor la llama internamente (`AsignarCaracteristicasSegunRol(rol);`), así que quien crea un `Jugador` nunca tiene que llamarla a mano — sucede automáticamente al hacer `new`.

---

## El código completo, probado desde `Main`

```csharp
using System;

public class Program
{
    static string DeterminarRol(string herramienta, bool leGustaElTe)
    {
        if (herramienta == "mapa")
        {
            return "Explorador";
        }
        else if (herramienta == "espada" && leGustaElTe)
        {
            return "Guerrero";
        }
        else
        {
            return "Mago";
        }
    }

    public static void Main()
    {
        Console.WriteLine("¿Qué herramienta eliges? (mapa/espada)");
        string herramienta = Console.ReadLine();

        Console.WriteLine("¿Te gusta el té? (si/no)");
        bool leGustaElTe = Console.ReadLine() == "si";

        string rol = DeterminarRol(herramienta, leGustaElTe);

        Jugador jugador1 = new Jugador("Ana", rol);
        jugador1.MostrarPersonaje();
    }
}

class Jugador
{
    public string nombre;
    public string rol;
    public int velocidad;
    public int fuerza;
    public int inteligencia;
    public int resistencia;
    public int vidas;
    public int salud;

    public Jugador(string nombreElegido, string rolElegido)
    {
        nombre = nombreElegido;
        rol = rolElegido;

        vidas = 3;
        salud = 100;

        AsignarCaracteristicasSegunRol(rol);
    }

    private void AsignarCaracteristicasSegunRol(string rolAsignado)
    {
        if (rolAsignado == "Explorador")
        {
            velocidad = 90; fuerza = 50; inteligencia = 70; resistencia = 60;
        }
        else if (rolAsignado == "Guerrero")
        {
            velocidad = 50; fuerza = 90; inteligencia = 40; resistencia = 90;
        }
        else if (rolAsignado == "Mago")
        {
            velocidad = 40; fuerza = 30; inteligencia = 100; resistencia = 50;
        }
    }

    public void MostrarPersonaje()
    {
        Console.WriteLine($"Nombre: {nombre} | Rol: {rol}");
        Console.WriteLine($"Velocidad: {velocidad}, Fuerza: {fuerza}, Inteligencia: {inteligencia}, Resistencia: {resistencia}");
        Console.WriteLine($"Vidas: {vidas}, Salud: {salud}");
    }
}
```

> 🔑 Fíjense que `Jugador` quedó como clase independiente, al mismo nivel que `Program`, no metida dentro de ella — es un concepto central del juego, no un detalle interno de `Program`.

Pruébenlo: `Main` recoge las decisiones, se las pasa a `DeterminarRol` (que vive afuera de `Jugador`), y el resultado se lo entrega al constructor de `Jugador`, que ya se encarga de todo lo demás por su cuenta.

---

## El problema: esto tampoco es sostenible

Funciona, pero fíjense qué pasó: la lógica de "conocer todos los roles posibles" no desapareció — simplemente se movió de un método `public` (`AsignarPersonaje`) a uno `private` (`AsignarCaracteristicasSegunRol`), pero sigue estando **toda dentro de una sola clase**. `Jugador` sigue siendo la única que sabe que existen `"Explorador"`, `"Guerrero"` y `"Mago"`, y sigue teniendo que revisar, con `if`, cuál es cuál.

Esto se vuelve un problema serio en cuanto cada rol necesite **comportarse** distinto, no solo tener números distintos — por ejemplo, si cada rol tuviera su propia habilidad especial. Tendríamos que seguir agregando `if` dentro de `Jugador` cada vez que se comporten distinto, y la clase terminaría sabiendo demasiado sobre roles que, conceptualmente, son cosas distintas entre sí.

La solución es la misma idea que motivó todo este documento, aplicada un nivel más arriba: **si un rol es un concepto distinto, debería ser una clase distinta** — no un `string` más que `Jugador` tiene que interpretar.

---

## Herencia: una clase por rol

En vez de un solo `Jugador` que reconoce todos los roles por dentro, vamos a tener una clase base `Jugador` con lo que **todos los roles comparten sin importar cuál sea**, y una clase distinta **por cada rol**, que hereda de `Jugador`.

### Qué se queda en la clase base

Que algo viva en la clase base no depende de si su *valor* es igual para todos — depende de si el **concepto** le pertenece a todos los roles, aunque la *implementación* (el valor concreto, o el comportamiento) cambie de uno a otro:

| Elemento | ¿El concepto es compartido? | ¿La implementación es igual para todos? | ¿Dónde vive? |
|---|---|---|---|
| `nombre` | Sí, todo jugador tiene nombre | Sí, es un dato simple, sin lógica distinta por rol | Clase base, campo normal |
| `vidas`, `salud` | Sí, todo jugador tiene vidas y salud | Sí, mismo valor por defecto para cualquier rol | Clase base, campo normal |
| `velocidad`, `fuerza`, `inteligencia`, `resistencia` | Sí, todo jugador tiene estas cuatro características | **No** — el número concreto depende del rol | Clase base, pero el *valor* lo asigna cada clase hija |
| `MostrarPersonaje()` | Sí, todo jugador se puede mostrar | Sí, exactamente el mismo formato para cualquier rol | Clase base, método normal (heredado sin cambios) |
| Habilidad especial | Sí, todo jugador debería tener una | **No** — cada rol la implementa distinto | Clase base, pero como método `virtual` (para que cada clase hija decida su propia versión) |

La columna que realmente importa es la última: cuando el concepto es compartido **y** la implementación también es idéntica, el elemento va en la base como algo normal, heredado tal cual. Cuando el concepto es compartido pero la implementación **varía** por rol, también va en la base — pero como algo que las clases hijas puedan sobreescribir (`virtual`) o completar ellas mismas (como los valores de `velocidad`, `fuerza`, etc., que cada clase hija asigna en su propio constructor).

Como las clases hijas van a necesitar asignar `velocidad`, `fuerza`, etc., esos campos deben ser `protected` (no `public`, para seguir protegiéndolos de cambios desde afuera de la jerarquía de clases, pero tampoco `private`, porque `private` bloquearía también a las clases hijas).

```csharp
class Jugador
{
    public string nombre;
    protected int velocidad;
    protected int fuerza;
    protected int inteligencia;
    protected int resistencia;
    protected int vidas;
    protected int salud;

    public Jugador(string nombreElegido)
    {
        nombre = nombreElegido;
        vidas = 3;
        salud = 100;
    }

    public void MostrarPersonaje()
    {
        Console.WriteLine($"Nombre: {nombre}");
        Console.WriteLine($"Velocidad: {velocidad}, Fuerza: {fuerza}, Inteligencia: {inteligencia}, Resistencia: {resistencia}");
        Console.WriteLine($"Vidas: {vidas}, Salud: {salud}");
    }

    public virtual void HabilidadEspecial()
    {
        Console.WriteLine($"{nombre} no tiene ninguna habilidad especial todavía.");
    }
}
```

Fíjense que ya no existe `rol` como campo, ni `AsignarCaracteristicasSegunRol`. `Jugador` ya no necesita saber que existen Exploradores, Guerreros o Magos — eso es justo lo que veníamos buscando.

### Cada rol, como su propia clase

Cada clase hija llama al constructor de `Jugador` (con `base(...)`) para heredar `nombre`, `vidas` y `salud`, y directamente asigna sus propios valores de `velocidad`, `fuerza`, `inteligencia` y `resistencia` — sin ningún `if` que revise "qué rol soy", porque la clase misma ya es la respuesta a esa pregunta.

```csharp
class Explorador : Jugador
{
    public Explorador(string nombreElegido) : base(nombreElegido)
    {
        velocidad = 90;
        fuerza = 50;
        inteligencia = 70;
        resistencia = 60;
    }

    public override void HabilidadEspecial()
    {
        base.HabilidadEspecial();
        Console.WriteLine($"{nombre} encuentra un atajo secreto y avanza más rápido.");
    }

    public void EncontrarAtajo()
    {
        Console.WriteLine($"{nombre} revisa el mapa y descubre un camino más corto.");
    }
}
```

```csharp
class Guerrero : Jugador
{
    public Guerrero(string nombreElegido) : base(nombreElegido)
    {
        velocidad = 50;
        fuerza = 90;
        inteligencia = 40;
        resistencia = 90;
    }

    public override void HabilidadEspecial()
    {
        Console.WriteLine($"{nombre} lanza un golpe crítico devastador."); // reemplaza por completo, no usa base.
    }

    public void GolpeCritico()
    {
        Console.WriteLine($"{nombre} concentra toda su fuerza en un solo golpe.");
    }
}
```

```csharp
class Mago : Jugador
{
    public Mago(string nombreElegido) : base(nombreElegido)
    {
        velocidad = 40;
        fuerza = 30;
        inteligencia = 100;
        resistencia = 50;
    }

    // sin override: Mago hereda HabilidadEspecial() de Jugador, tal cual

    public void LanzarHechizo()
    {
        Console.WriteLine($"{nombre} lanza una bola de fuego.");
    }
}
```

Con esto, `Explorador` **expande** `HabilidadEspecial()` (usa `base.HabilidadEspecial()` y le agrega algo), `Guerrero` la **reemplaza** por completo, y `Mago` la **hereda sin tocarla** — cada rol decide su propia relación con el comportamiento heredado, sin que `Jugador` tenga que saber nada de eso.

---

## `Main`, con la función externa decidiendo qué clase crear

`DeterminarRol` se queda exactamente igual que antes — no necesitó ningún cambio. Lo único que cambia es qué hacemos con su resultado: en vez de pasárselo a `Jugador` para que lo interprete, lo usamos para decidir **cuál clase instanciar**.

```csharp
public static void Main()
{
    Console.WriteLine("¿Qué herramienta eliges? (mapa/espada)");
    string herramienta = Console.ReadLine();

    Console.WriteLine("¿Te gusta el té? (si/no)");
    bool leGustaElTe = Console.ReadLine() == "si";

    string rol = DeterminarRol(herramienta, leGustaElTe);

    Jugador jugador1;

    if (rol == "Explorador")
    {
        jugador1 = new Explorador("Ana");
    }
    else if (rol == "Guerrero")
    {
        jugador1 = new Guerrero("Ana");
    }
    else
    {
        jugador1 = new Mago("Ana");
    }

    jugador1.MostrarPersonaje();
    jugador1.HabilidadEspecial();
}
```

`jugador1` está declarado como `Jugador`, pero contiene un objeto de la clase específica que corresponda — así que `jugador1.HabilidadEspecial()` ejecuta automáticamente la versión correcta (expandida, reemplazada, o heredada) según cuál clase se haya creado. Esto es **polimorfismo**: el mismo código (`jugador1.HabilidadEspecial();`) produce un resultado distinto según el tipo real del objeto que `jugador1` esté guardando en ese momento.

Y si más adelante quisieran manejar varios jugadores a la vez, el mismo principio se extiende a un array:

```csharp
Jugador[] equipo = { new Explorador("Ana"), new Guerrero("Luis"), new Mago("Sofía") };

foreach (Jugador j in equipo)
{
    j.HabilidadEspecial(); // cada uno ejecuta la suya, sin ningún if
}
```

> ⚠️ Como `jugador1` (o cada elemento del `equipo`) está guardado como tipo `Jugador`, solo se pueden llamar desde ahí los métodos que `Jugador` conoce (`MostrarPersonaje`, `HabilidadEspecial`) — no `EncontrarAtajo()`, `GolpeCritico()` ni `LanzarHechizo()`, aunque el objeto real sí los tenga. Para usar un método exclusivo de un rol, hace falta una variable declarada específicamente como ese rol.

---

## 📝 Ejercicio

El ejercicio final es sobre la clase que ya escribieron para su **proyecto personal**, no sobre `Jugador`:

1. Tomen esa clase y créenle una clase nueva que **herede** de ella.
2. En esa nueva clase, **expandan** al menos un método heredado (usando `base.NombreDelMetodo()` y agregándole algo propio) y **sobreescriban** por completo al menos otro — según lo que tenga sentido para las necesidades de su propio proyecto.

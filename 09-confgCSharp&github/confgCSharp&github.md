# Tutorial: GitHub + VS Code + C# — trabajando en pareja sobre un solo repositorio

Este tutorial asume que ya tienen **.NET SDK**, **VS Code** y la extensión de C# instalados y funcionando. Vamos a: crear **un solo repositorio compartido entre los dos**, hacer que ambos lo clonen, organizar las clases y funciones que ya tienen en varios archivos, y ver el flujo de trabajo para no pisarse el trabajo entre los dos.

---

## 1. Crear el repositorio en GitHub (lo hace uno de los dos)

Solo **uno** de los dos integrantes del equipo crea el repositorio — el otro se va a unir después como colaborador.

1. Entren a [github.com](https://github.com) y hagan clic en **New** (o el botón `+` de arriba a la derecha → **New repository**).
2. Pónganle un nombre (por ejemplo, `mi-juego-csharp`).
3. Elijan **Public** o **Private**, según prefieran.
4. Marquen la casilla **Add a README file**.
5. En **Add .gitignore**, elijan la plantilla **Visual Studio** de la lista — esto evita que suban al repositorio archivos que .NET genera automáticamente (las carpetas `bin/` y `obj/`), que no deberían guardarse en Git.
6. Hagan clic en **Create repository**.

## 2. Agregar a su compañero como colaborador

Para que los dos puedan subir cambios al **mismo** repositorio (en vez de tener cada uno su propia copia separada en GitHub):

1. Dentro del repositorio recién creado, vayan a **Settings** (pestaña de arriba).
2. En el menú de la izquierda, hagan clic en **Collaborators**.
3. Hagan clic en **Add people**.
4. Busquen el nombre de usuario de GitHub de su compañero, y envíenle la invitación.

Su compañero va a recibir una notificación (por correo o en GitHub) para aceptar la invitación — debe aceptarla antes de poder clonar o subir cambios al repositorio.

> 🔑 Con esto, **ambos** tienen permiso de subir (`push`) cambios directamente al mismo repositorio — no es necesario que cada uno tenga su propia copia (*fork*) por separado, como sí sería necesario en un proyecto más grande con muchos colaboradores externos.

---

## 3. Clonar el repositorio (lo hacen los dos)

Cada integrante clona el repositorio en su propio computador — **ambos van a tener una copia local del mismo repositorio**.

1. En GitHub, botón verde **Code** → pestaña **HTTPS** → copien la URL.
2. En VS Code: `Ctrl+Shift+P` → **Git: Clone** → pegar la URL → elegir carpeta.
3. Cuando termine, abran la carpeta clonada.

O desde la terminal:

```bash
git clone https://github.com/su-usuario/mi-juego-csharp.git
cd mi-juego-csharp
code .
```

---

## 4. Crear el proyecto de consola (lo hace solo uno de los dos)

Solo **uno** de los dos crea el proyecto inicial, para evitar que ambos generen estructuras distintas al mismo tiempo:

```bash
dotnet new console -n MiJuego
```

Esto crea `MiJuego/MiJuego.csproj` y `MiJuego/Program.cs`. Después de crearlo, esa persona debe subirlo a GitHub (ver la sección 6) **antes** de que el otro integrante empiece a trabajar, para que el segundo lo descargue con `git pull` en vez de crear su propio proyecto por separado.

> ⚠️ Las plantillas recientes de `dotnet new console` generan un `Program.cs` con **top-level statements** (código suelto, sin clase `Program` ni `Main` explícito). Si prefieren la estructura clásica que hemos usado en clase (`public class Program { public static void Main() { ... } }`), simplemente reescriban `Program.cs` con esa estructura a mano — funciona igual.

---

## 5. Organizando varias clases y funciones para que `Main` las use

Ya tienen varias clases (`Jugador`, `Explorador`, `Guerrero`, `Mago`, etc.) y funciones sueltas escritas durante el curso. En C#, lo normal es **un archivo por clase**, no todo en uno solo:

```
MiJuego/
├── MiJuego.csproj
├── Program.cs
├── Jugador.cs
├── Explorador.cs
├── Guerrero.cs
└── Mago.cs
```

```csharp
// Jugador.cs
class Jugador
{
    public string nombre;
    // ...
}
```

```csharp
// Explorador.cs
class Explorador : Jugador
{
    // ...
}
```

### ¿Por qué `Main` las puede usar sin nada extra?

En un proyecto de consola, **todos los archivos `.cs` que estén dentro de la carpeta del proyecto se compilan juntos automáticamente** — no hace falta "importarlos" a mano. Si no usan `namespace` (o usan el mismo en todos los archivos), `Program.cs` puede usar cualquier clase directamente:

```csharp
// Program.cs
public class Program
{
    public static void Main()
    {
        Jugador jugador1 = new Explorador("Ana"); // no hace falta ningún "using" especial
        jugador1.MostrarPersonaje();
    }
}
```

> 🔑 Separar las clases en archivos distintos no cambia cómo se comportan ni cómo se llaman entre sí — solo mejora la organización. Esto también hace que trabajar en pareja sea mucho más fácil: si cada uno está trabajando en una clase distinta (por ejemplo, uno en `Guerrero.cs` y el otro en `Mago.cs`), es mucho menos probable que sus cambios choquen entre sí.

### Funciones sueltas (como `DeterminarRol`)

Las funciones que no pertenecen a ninguna clase en particular normalmente viven junto a `Main`, dentro de `Program.cs`:

```csharp
public class Program
{
    static string DeterminarRol(string herramienta, bool leGustaElTe)
    {
        // ...
    }

    public static void Main()
    {
        string rol = DeterminarRol("espada", true);
        // ...
    }
}
```

---

## 6. Flujo de trabajo cuando son dos personas en el mismo repositorio

Esta es la parte que cambia respecto a trabajar solos: como los dos van a subir cambios al mismo repositorio, hay que seguir un orden para no pisarse el trabajo.

### La regla de oro: `pull` antes de empezar, `push` cuando terminen

1. **Antes de ponerse a programar**, siempre traigan los cambios más recientes de su compañero:

```bash
git pull
```

2. Trabajen en su parte (idealmente, cada uno en archivos `.cs` distintos, para minimizar choques).
3. **Al terminar** (o cada vez que completen algo que funcione), guarden y suban:

```bash
git add .
git commit -m "Agrego clase Guerrero con HabilidadEspecial"
git push
```

O, desde VS Code: pestaña de **Control de código fuente** (`Ctrl+Shift+G`) → escribir el mensaje → **Commit** → **Sync Changes**.

### ¿Qué pasa si los dos editaron el mismo archivo?

Si intentan hacer `push` y GitHub tiene cambios que ustedes todavía no tienen (porque su compañero subió algo mientras ustedes trabajaban), Git se los va a rechazar y les va a pedir que hagan `pull` primero:

```bash
git pull
```

- Si editaron **archivos distintos**, Git casi siempre los combina automáticamente, sin pedirles nada.
- Si editaron **las mismas líneas del mismo archivo**, Git va a marcar un **conflicto**: el archivo va a mostrar ambas versiones, separadas por símbolos como `<<<<<<<`, `=======` y `>>>>>>>`. Tienen que abrir el archivo, decidir juntos qué versión (o combinación) dejar, borrar esos símbolos, y hacer un nuevo `commit` para cerrar el conflicto. VS Code muestra estos conflictos resaltados y con botones para elegir "Accept Current", "Accept Incoming" o "Accept Both" — es la forma más fácil de resolverlos.

> 💡 La mejor forma de evitar conflictos casi por completo: avísense qué archivo va a tocar cada uno antes de empezar, y hagan `pull`/`push` seguido (no esperen hasta el final de la sesión para subir todo junto).

---

## Resumen del flujo completo

| Paso | Quién | Comando / acción |
|---|---|---|
| Crear el repositorio | Uno de los dos | GitHub → New repository |
| Agregar colaborador | Quien creó el repo | Settings → Collaborators → Add people |
| Clonar el repositorio | Ambos | `git clone <url>` |
| Crear el proyecto | Uno de los dos, luego el otro hace `pull` | `dotnet new console -n MiJuego` |
| Antes de programar | Ambos, cada vez | `git pull` |
| Correr el programa | Ambos | `dotnet run` (dentro de la carpeta del proyecto) |
| Guardar cambios | Ambos, seguido | `git add .` → `git commit -m "..."` → `git push` |
| Si hay conflicto | Quien lo encuentre | Resolver en VS Code, luego `commit` de nuevo |

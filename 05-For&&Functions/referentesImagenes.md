# ASCII Art — Contexto y Referentes

## ¿Qué es el ASCII art?

El **ASCII art** es una técnica para "dibujar" imágenes usando solo los caracteres disponibles en el teclado: letras, números, puntos, guiones y símbolos (`.`, `_`, `x`, `o`, `O`, `#`, `*`, espacios, etc.). Nace de una limitación técnica: antes de que existieran gráficos a color o texturas, las pantallas de las primeras computadoras solo podían mostrar **texto**. Los programadores convirtieron esa limitación en un estilo propio — y ese estilo sigue vivo hoy, incluso cuando ya no es necesario.

En videojuegos, este estilo se volvió icónico dentro de un género completo: los **roguelikes**.

## Referentes que puedes explorar

### 🎮 Rogue (1980)
El juego que le dio nombre al género "roguelike". Todo el mapa se construye con símbolos: `@` es el jugador, `#` son pasillos, `.` es piso, y las letras representan monstruos distintos (`K` un kestrel, `D` un dragón, etc.).
- Artículo introductorio: https://www.asciiart.eu/ascii-games/articles/rogue-the-dawn-of-roguelikes


### 🎮 Roguelikes modernos con ASCII art
El estilo no murió — sigue usándose por elección estética, no por limitación técnica.
- Lista de roguelikes modernos con ASCII art (Cogmind, Brogue, Caves of Qud): https://gamerant.com/best-roguelikes-ascii-art/

### 🔬 El Juego de la Vida de Conway (Conway's Game of Life)
No es un videojuego tradicional, sino un experimento matemático de 1970 que se representa clásicamente como una cuadrícula de texto: `O` (o `*`) para una célula viva, `.` o espacio para una célula muerta. Es **el ejemplo clásico por excelencia** para aprender matrices/arrays 2D en programación, porque el patrón cambia solo, generación tras generación, según reglas simples.
- Artículo en Wikipedia: https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life
- Implementación en C/C++ con ASCII (para referencia técnica): https://kennycason.com/posts/2011-07-20-john-conways-game-of-life-windowsc-ascii.html

### 🖥️ Galería general de ASCII art en videojuegos
- https://www.asciiart.eu/ascii-games — sitio dedicado con artículos, historia y ejemplos jugables.

---

## Ejemplo simple: un mapa con solo `Console.WriteLine`

Por ahora, sin arrays todavía — solo usando lo que ya conocemos: `string`, `char` y `Console.WriteLine()`. La idea es "dibujar" un mini-mapa línea por línea, tal como se veía en los primeros roguelikes.

```csharp
Console.WriteLine("########################");
Console.WriteLine("#......................#");
Console.WriteLine("#...@..................#");
Console.WriteLine("#......................#");
Console.WriteLine("#..........O...........#");
Console.WriteLine("#......................#");
Console.WriteLine("#.............#####....#");
Console.WriteLine("#.............#...#....#");
Console.WriteLine("#.............#.$.#....#");
Console.WriteLine("#.............#####....#");
Console.WriteLine("#......................#");
Console.WriteLine("########################");
```

Con este código estamos "dibujando" un pequeño dungeon:

- `#` → paredes
- `.` → piso
- `@` → el jugador
- `O` → un enemigo
- `$` → un tesoro

Cada `Console.WriteLine()` imprime **una fila completa** del mapa, y al ejecutarlas en orden, una debajo de otra, la consola termina formando la imagen completa — exactamente la misma lógica que usaban Rogue y NetHack, solo que aquí lo estamos haciendo "a mano", línea por línea, en vez de generarlo automáticamente.



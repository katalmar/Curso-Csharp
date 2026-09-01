# 🎮 Programar para hacer videojuegos: el vocabulario que necesitas

*Una guía introductoria para quienes nunca han programado, pero van a diseñar mundos jugables.*

---

## 1. ¿Qué significa "programar"?

Ustedes ya conocen, aunque sea intuitivamente, el concepto de **mecánica de juego**: una regla o sistema pequeño que, combinado con otras mecánicas, le da forma a la experiencia completa (saltar, esquivar, recolectar, subir de nivel, perder vida al caer). Ninguna mecánica existe sola — siempre es el resultado de **varios procesos simples trabajando juntos**.

Programar es, en esencia, **construir esos sistemas descomponiéndolos en procesos lo suficientemente simples como para que una computadora pueda ejecutarlos sin ambigüedad, uno por uno**.

Tomemos la mecánica de "saltar". Para un jugador, es una sola acción intuitiva. Pero un motor como Unity no "entiende" saltar — solo entiende procesos diminutos y exactos. Diseñar esa mecánica en código significa partirla en piezas como:

1. Detectar si se presionó la tecla espacio.
2. Verificar si el personaje está tocando el suelo en ese instante.
3. Si ambas condiciones se cumplen, aplicar una fuerza hacia arriba al personaje.
4. Mientras el personaje está en el aire, impedir que vuelva a saltar.
5. Al tocar el suelo de nuevo, permitir que el ciclo se repita.

Cada uno de esos pasos es un proceso sencillo. Ninguno por sí solo "es" la mecánica de saltar — es la **combinación ordenada** de todos ellos lo que produce el comportamiento que el jugador percibe como "saltar". Así funciona prácticamente cualquier sistema de un videojuego: una barra de vida, un inventario, la IA de un enemigo, un sistema de crafteo — todos son mecánicas que, al mirarlas de cerca, están hechas de procesos pequeños encadenados.

---

## 2. El lenguaje real de las computadoras: binario, bits y bytes

Antes de hablar de "niveles" de lenguaje, hay que entender con qué está trabajando la computadora en el fondo, siempre, sin excepción: **electricidad que está encendida o apagada**. Un transistor solo puede estar en dos estados: sí pasa corriente, o no pasa. A eso lo representamos con dos símbolos: **1** (encendido) y **0** (apagado). Ese es el **sistema binario**, y es el único idioma que el hardware entiende de verdad — no importa si programas en C#, Python o Assembly, todo termina convertido a una cadena de unos y ceros antes de ejecutarse.

Cada uno de esos 1 o 0 es un **bit**. Un bit solo, por sí mismo, no dice mucho — apenas puede representar dos estados (encendido/apagado, verdadero/falso). Pero si agrupamos **8 bits**, obtenemos un **byte**, y ahí la cosa cambia: con 8 bits podemos combinar ceros y unos de 256 formas distintas (2⁸ = 256), lo que nos da un rango de valores que va de **0 a 255**.

### ¿Por qué justo 8, y no 6 o 10?

No es una ley matemática obligatoria, sino una **convención** que terminó imponiéndose por conveniencia: 8 es una potencia de 2 (encaja perfecto con cómo funciona el hardware binario), alcanza justo para cubrir todo el alfabeto y símbolos básicos del código ASCII. Cuando fabricantes influyentes como IBM adoptaron el byte de 8 bits como estándar en los años 60, el resto de la industria se alineó, y desde entonces quedó fijado como **la unidad básica de almacenamiento** en prácticamente todo el hardware que existe.

### El problema: 256 valores no siempre alcanzan

Ese número — 256 — no es una casualidad técnica sin importancia: es la unidad básica con la que la computadora **captura, procesa y representa** casi cualquier tipo de información. Pero el estándar de 8 bits fue pensado originalmente para cosas simples como letras y números pequeños — cuando se necesita más **detalle** o **matiz** en la información (un color más preciso, un sonido más limpio), 256 escalones se quedan cortos. La solución no es inventar un nuevo sistema: es simplemente **juntar varios bytes seguidos**, formando paquetes más grandes, para tener más escalones disponibles.

> 🎨 Lo que llamamos **"resolución"** o **"profundidad"** (de color, de audio, de imagen) no es más que **cuánta capacidad tiene el sistema para representar información dentro de este esquema binario**. No es una propiedad mágica de la imagen o el sonido: es, literalmente, cuántos bits (agrupados en uno o varios bytes) se están usando para describir cada pedacito de esa información.

### El caso del audio: cuando 8 bits no alcanzan y se escucha

En audio digital, cada instante de la onda de sonido se convierte en un número que representa el volumen exacto en ese momento. Si ese número se guarda usando **solo 8 bits (1 byte)**, apenas hay 256 "escalones" posibles entre el silencio total y el volumen máximo. Cuando el volumen real de la onda cae *entre* dos escalones, la computadora tiene que redondear al más cercano — a ese redondeo se le llama **cuantización**, y el error que introduce se escucha literalmente como un ruido de fondo, un "grano" áspero y comprimido en el sonido.

Ese "grano" característico es precisamente la textura sonora que reconoces en la música **chiptune** de consolas como la NES — no es un efecto estético inventado, es el sonido real de un hardware limitado a procesar información de a 8 bits a la vez. te recomiendo este vido si te interesa saber mas sobre **chiptune** y videojuegos https://www.youtube.com/watch?v=C7HFa5HkmYg&t=168s

Por eso, cuando se necesita mayor resolución sonora (para que ese "grano" desaparezca y el sonido se escuche limpio), la industria simplemente **agrupa más bytes por cada muestra de sonido**: el audio de calidad CD usa 16 bits (2 bytes) por muestra, dando 65.536 escalones en vez de 256, y el audio profesional de estudio usa 24 bits (3 bytes), con más de 16 millones de escalones — suficiente margen para que el oído humano ya no perciba ningún salto ni ruido de cuantización.

Ejemplos concretos que ya conocen como diseñadores de juegos:
- Un color en **8 bits por canal** (el estándar RGB de toda la vida) puede tener 256 valores posibles de rojo, 256 de verde y 256 de azul — de ahí que combinándolos se hable de "millones de colores".
- El estilo visual **"8-bit"** de los videojuegos retro (NES, primeras consolas) no es solo una estética nostálgica: refleja literalmente el límite real de esas máquinas, que solo podían representar paletas de hasta 256 colores o menos, porque su hardware trabajaba con bytes de 8 bits.
- El audio digital también se mide en bits (16-bit, 24-bit): más bits = más "escalones" posibles entre el silencio y el volumen máximo = un sonido más fiel al original, sin el "grano" de cuantización.

Más bits disponibles = más posibilidades de representar matices de información. Esa es la idea central detrás de "resolución", ya sea visual, sonora, o de cualquier otro tipo de dato dentro de una computadora.

---

## 3. Entonces, ¿qué hace que un lenguaje sea de bajo, medio o alto nivel?

Aquí está la clave: **todo código, sin importar en qué lenguaje lo escribas, termina convertido en esa cadena de binario** que vimos arriba. Lo que cambia entre los "niveles" de un lenguaje es **qué tan cerca o lejos escribes tú de ese binario**, y **cuánto trabajo de traducción se hace por ti automáticamente**.

### 🔧 Bajo nivel — casi binario puro
Escribes instrucciones que corresponden casi directamente a operaciones del procesador: mover un valor de un lugar de la memoria a otro, sumar dos bytes, comparar bits. Hay muy poca (o ninguna) traducción intermedia entre lo que escribes y lo que la máquina ejecuta.
- **Ejemplo:** lenguaje ensamblador (Assembly), donde literalmente trabajas con direcciones de memoria y registros del procesador.

### ⚙️ Medio nivel — el puente entre lo humano y lo binario
Un lenguaje se cataloga como de **nivel medio** cuando te da estructuras legibles para humanos (funciones, variables, ciclos, condicionales) **pero sigue permitiéndote manipular directamente la memoria** — es decir, sigue dejándote "tocar" cómo se organizan esos bytes que vimos arriba (a través de punteros, gestión manual de memoria, acceso a direcciones específicas). Es un lugar intermedio: traduce tus órdenes humanas al sistema binario, pero exige que tú entiendas parte de esa organización de bajo nivel para escribir código correcto y eficiente.
- **Ejemplos:** C, C++, Rust.
- **Uso en videojuegos:** el corazón de motores gráficos (Unreal Engine está hecho en C++) donde el rendimiento y el control exacto sobre la memoria son críticos — por ejemplo, para que un juego corra a 60 cuadros por segundo sin desperdiciar recursos.

### 🧩 Alto nivel — abstracción casi total del binario
Un lenguaje se cataloga como de **nivel alto** cuando **te aísla casi por completo de la organización binaria y de memoria**: no necesitas saber cuántos bytes ocupa una variable, ni gestionar manualmente dónde vive esa información en la memoria — el propio lenguaje (o el motor que lo ejecuta) se encarga de traducir tu lógica a binario y de administrar la memoria automáticamente (esto se llama *recolección de basura* o *garbage collection*). Tu atención se queda casi enteramente en la lógica del problema, no en la máquina.
- **Ejemplos:** C#, Python, JavaScript, Java.
- **Uso en videojuegos:** **C# es el lenguaje de Unity**, precisamente porque les permite a diseñadores y programadores enfocarse en la lógica del juego (comportamientos, reglas, POO) sin preocuparse de cómo se organiza la memoria del procesador por debajo — de eso ya se encarga el motor.

**En resumen, la clasificación se basa en tres preguntas:**
1. ¿Qué tan cerca escribo del binario/hardware real?
2. ¿Tengo que gestionar yo mismo la memoria (bajo/medio nivel), o lo hace el lenguaje automáticamente por mí (alto nivel)?
3. ¿Cuánta "traducción" adicional hace el compilador o intérprete entre lo que yo escribo y lo que la máquina finalmente ejecuta como unos y ceros?

Mientras más preguntas de esas resuelva el lenguaje *por ti*, más "alto" es su nivel.

---


## 4. Palabras, conceptos y herramientas que vas a escuchar todo el tiempo

### Lenguaje de programación vs. IDE vs. plataforma: no es lo mismo

Esta es una confusión súper común al empezar, así que vamos a separarla con una analogía de cocina 👩‍🍳:

| Concepto | Qué es | Analogía |
|---|---|---|
| **Lenguaje de programación** | El idioma en el que escribes las instrucciones (reglas de gramática y vocabulario) | El **idioma** en el que está escrita una receta (español, francés) |
| **IDE** (Entorno de Desarrollo Integrado) | El programa donde escribes, revisas y ejecutas tu código, con ayudas como autocompletado y detección de errores | La **cocina equipada**: mesón, cuchillos, horno — herramientas para ejecutar la receta |
| **Editor de código** | Una versión más ligera de un IDE, a veces solo para escribir texto con resaltado de sintaxis | Una **libreta** donde anotas la receta, sin electrodomésticos |

**Ejemplos concretos:**
- **C#** → es el *lenguaje*.
- **Visual Studio Code**, **Visual Studio**, **JetBrains Rider** → son *IDEs/editores* donde escribes ese C#.
- **Unity** → no es un lenguaje ni un simple editor: es un **motor de videojuegos** que usa C# como su lenguaje de scripting, y trae su propio ecosistema (física, gráficos, assets, escenas).

Un mismo lenguaje puede escribirse en distintos IDEs, igual que una receta en español se puede escribir en una libreta, en un procesador de texto o dictada a alguien más.

### Glosario de supervivencia: terminal, compilar, debug, build, run, dev

Términos que aparecerán constantemente en clase, en tutoriales y en la documentación de Unity:

- **Terminal (o consola):** una ventana donde escribes comandos de texto directamente al sistema, en vez de hacer clic en botones. Es el "modo directo" de hablarle a la computadora.

- **Compilar:** es el proceso de **traducir** el código que escribiste (legible para humanos) a un formato que la computadora puede ejecutar directamente. Si tu código tiene errores de sintaxis, la compilación falla y te avisa dónde está el problema — antes incluso de ejecutar nada.

- **Debug (depurar):** el proceso de **encontrar y corregir errores** en tu código. "Hacer debug" es literalmente ir paso a paso revisando qué está pasando en tu programa para descubrir por qué no se comporta como esperabas. Unity y los IDEs traen herramientas de debug que te permiten pausar el juego y revisar el valor de las variables en tiempo real.

- **Build:** es la versión **final y ejecutable** de tu proyecto — el archivo que puedes compartir con alguien para que lo juegue sin necesitar Unity instalado (un `.exe` en Windows, una app en Android, etc.). "Hacer un build" es empaquetar todo tu juego para distribuirlo.

- **Run:** simplemente **ejecutar** el programa — darle play. En Unity, presionar el botón de "Play" corre tu juego dentro del editor, sin necesidad de hacer un build completo.

- **Dev (development / desarrollo):** se refiere al estado de trabajo en progreso, antes de que algo esté terminado o publicado. Un "build de dev" o "entorno de dev" es una versión interna, usada para probar, que aún no está lista para el público.

---

## 🧭 Para cerrar

No necesitas memorizar todo esto de una vez. La idea de este texto es que, cuando en clase escuches "vamos a compilar y hacer debug de este script antes del build", **no te sientas perdida** — sepas de qué se está hablando, aunque todavía no domines cómo hacerlo tú misma.

A medida que avancemos en POO con C#, vas a ir usando estas palabras en la práctica, hasta que dejen de sonar como una lista y se conviertan en parte natural de tu vocabulario como desarrolladora.

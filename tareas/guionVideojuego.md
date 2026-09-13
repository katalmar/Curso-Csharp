# Ejercicio: Diseñar un videojuego de texto

## Objetivo

Diseñar el **guion y las reglas de un videojuego de texto** que pueda ser desarrollado posteriormente en C#.

El juego debe utilizar **al menos 4 de las mecánicas** estudiadas en clase. No es necesario programar el juego todavía: en esta etapa nos interesa definir **qué puede hacer el jugador, qué reglas tiene el mundo y cómo esas reglas afectan la experiencia**.

El objetivo no es solamente escribir una historia, sino diseñar un sistema en el que las **acciones del jugador, las reglas y los estados del juego produzcan diferentes situaciones y consecuencias**.

---

# 1. Mecánicas disponibles

Para este ejercicio puedes utilizar las siguientes mecánicas.

No es necesario utilizar todas. **Debes escoger al menos 4.**

---

## 1.1. Reconocimiento de la intención del jugador — Player Input / Command Parsing

El juego debe ser capaz de **reconocer qué quiere hacer el jugador** a partir de una entrada.

Por ejemplo, el jugador puede escribir:

```text
> tomar llave
```

El sistema debe identificar que la intención del jugador es **tomar** un objeto llamado **llave**.

Otro ejemplo:

```text
> abrir puerta
```

El juego puede identificar:

```text
acción: abrir
objeto: puerta
```

y posteriormente comprobar si esa acción es posible.

Esta mecánica puede implementarse de diferentes maneras. No necesariamente tiene que utilizar un *parser* complejo. También puede utilizar comandos sencillos, palabras clave u opciones predeterminadas.

Por ejemplo:

```text
¿Qué quieres hacer?

1. Examinar
2. Tomar
3. Abrir
4. Salir
```

En este caso, el juego también está reconociendo la intención del jugador, aunque la entrada esté limitada a opciones.

**Nombres utilizados:** `Player Input`, `Command Parsing`, `Input Recognition`, `Intent Recognition`.

---

## 1.2. Inventario y objetos — Inventory / Item System

El jugador puede **recolectar, transportar y utilizar objetos**.

Los objetos pueden tener diferentes funciones dentro del juego:

* abrir una puerta;
* activar un mecanismo;
* resolver un acertijo;
* entregar a otro personaje;
* desbloquear una nueva opción;
* permitir acceder a un lugar;
* modificar alguna característica del personaje.

Por ejemplo:

> El jugador encuentra una llave oxidada.
> Más adelante encuentra una puerta cerrada.
> Al utilizar la llave sobre la puerta, puede acceder a una nueva habitación.

Los objetos también pueden combinarse con otras mecánicas.

Por ejemplo:

> El jugador necesita una antorcha para atravesar una zona oscura.

**Nombres utilizados:** `Inventory System`, `Item System`, `Item Interaction`.

---

## 1.3. Decisiones y rutas narrativas — Player Choices / Narrative Paths

El jugador puede tomar **decisiones explícitas** que modifican temporalmente el recorrido de la historia.

La decisión se presenta directamente al jugador y este escoge entre diferentes posibilidades.

La pregunta principal de esta mecánica es:

> **¿Qué decisión quiere tomar el jugador en este momento?**

Por ejemplo:

```text
Encuentras una persona herida.

¿Qué quieres hacer?

1. Ayudarla
2. Ignorarla
3. Robarle
```

La elección puede producir diferentes acontecimientos:

```text
                    HISTORIA PRINCIPAL
                           |
                    Persona herida
                    /      |      \
                ayudar   ignorar   robar
                   |        |         |
               evento A  evento B  evento C
                   \        |        /
                    \       |       /
                     HISTORIA PRINCIPAL
```

Una decisión no tiene que crear un nuevo recorrido completo del juego. Una ruta puede **desviarse temporalmente y después volver a integrarse con la historia principal**.

Por ejemplo:

> El jugador decide ayudar al personaje.

> Esto produce una escena diferente y permite obtener información.

> Después de esa escena, el jugador vuelve al objetivo principal de la historia.

Por esta razón, no es necesario pensar el juego como un árbol en el que **cada decisión genera permanentemente nuevas decisiones**. Un videojuego puede tener una **historia principal con diferentes rutas, situaciones y variaciones**, algunas de las cuales posteriormente vuelven a converger.

Las decisiones pueden modificar:

* los acontecimientos;
* los personajes que aparecen;
* la información que recibe el jugador;
* los objetos que obtiene;
* las relaciones con otros personajes;
* las condiciones del mundo;
* las posibilidades futuras;
* el final que finalmente alcanza.

**Nombres utilizados:** `Player Choice`, `Narrative Path`, `Narrative Branch`, `Branching Narrative`, `Decision Point`, `Choice Point`.

---

## 1.4. Condiciones y estados — Conditional Logic / Game State

En esta mecánica, el juego utiliza **información acumulada durante la partida y estados actuales del mundo** para determinar qué puede ocurrir.

A diferencia de las decisiones explícitas, **el juego no necesariamente le muestra al jugador cuáles son las condiciones que están determinando el resultado**.

La pregunta principal de esta mecánica es:

> **¿Qué puede ocurrir en este momento según el estado actual del juego?**

Por ejemplo, durante la partida pueden cambiar diferentes variables:

```text
¿Ayudaste al guardia?
¿Encontraste la llave?
¿Cuántas vidas tienes?
¿Es de noche?
¿Hablaste con determinado personaje?
```

El programa conserva esta información mediante variables o estados:

```text
ayudoAlGuardia = true
tieneLlave = false
vidas = 2
esDeNoche = true
```

Posteriormente, el juego puede utilizar estas variables para determinar qué ocurre:

```text
Si es de noche
    → aparece un enemigo

Si vidas <= 0
    → el personaje muere

Si ayudoAlGuardia == true
    → el guardia permite pasar

Si tieneLlave == true
    → la puerta puede abrirse
```

El jugador puede **no saber exactamente qué condición produjo el resultado**.

Por ejemplo:

> El jugador entra en una habitación y encuentra que la puerta del fondo está abierta.

El juego podría estar comprobando internamente:

```text
Si habloConGuardia == true
    → puerta abierta
```

Pero el jugador no necesariamente recibe una explicación como:

> "La puerta está abierta porque ayudaste al guardia anteriormente."

La relación entre las acciones anteriores, los estados del juego y las consecuencias puede permanecer **implícita**.

Esto permite crear experiencias en las que el jugador descubre progresivamente que sus acciones anteriores tienen consecuencias, incluso cuando no conoce todas las reglas del sistema.

### Diferencia entre decisiones y condiciones

Estas dos mecánicas pueden estar relacionadas, pero no son lo mismo.

**Decisión explícita:**

> El juego pregunta: **"¿Qué quieres hacer?"**

El jugador recibe un conjunto de opciones y escoge una.

**Condición o estado:**

> El programa comprueba: **"¿Qué puede ocurrir dadas las condiciones actuales?"**

El programa revisa las variables y estados de la partida para determinar qué mostrar, qué permitir o qué evento producir.

Las dos mecánicas pueden trabajar juntas:

```text
DECISIÓN DEL JUGADOR

"¿Quieres ayudar al guardia?"

       Sí ──────────→ ayudoAlGuardia = true
       No ──────────→ ayudoAlGuardia = false
                         |
                         v
                  ESTADO DEL JUEGO
                         |
                         v
                REGLA DEL SISTEMA

Más adelante:

Si ayudoAlGuardia == true
    → el guardia te deja pasar

Si ayudoAlGuardia == false
    → el guardia bloquea el camino
```

En este ejemplo:

* **Ayudar al guardia** es una decisión explícita del jugador.
* **Guardar esa decisión como un estado** permite recordarla.
* **La condición posterior** utiliza ese estado para determinar qué sucede.

**Nombres utilizados:** `Game State`, `Conditional Logic`, `State`, `Condition`, `Flag`.

---

## 1.5. Finales múltiples — Multiple Endings

El juego puede tener **más de un final posible**.

Los finales no tienen que ser infinitos ni cada decisión tiene que producir un final diferente. El juego puede tener un **número finito de finales**, y diferentes combinaciones de decisiones, objetos, estados o recursos pueden conducir a uno de ellos.

Por ejemplo:

```text
                  HISTORIA PRINCIPAL
                         |
                    decisiones
                         |
              diferentes situaciones
                         |
                         v
                  estado final
                 /      |      \
                /       |       \
          Final A    Final B    Final C
```

Un final puede depender de una sola variable:

```text
Si vidas <= 0
    → Final: muerte
```

O de una combinación de variables:

```text
Si tieneLlave == true
y ayudoAlGuardia == true
y esDeNoche == false

    → Final A
```

Mientras que:

```text
Si tieneLlave == false
y ayudoAlGuardia == true

    → Final B
```

El juego también puede utilizar diferentes tipos de finales:

* victoria;
* derrota;
* muerte;
* escape;
* fracaso;
* final secreto;
* final verdadero;
* diferentes versiones de la misma resolución.

Lo importante es que **exista un conjunto finito de posibles resultados finales**, y que las acciones y estados acumulados durante la partida determinen cuál de ellos alcanza el jugador.

### Las decisiones no tienen que producir un nuevo final inmediatamente

Una decisión puede modificar el estado del juego y después la historia puede continuar:

```text
Historia principal
       |
       v
Decisión del jugador
       |
    /     \
   A       B
   |       |
 evento   evento
   \       /
    \     /
     \   /
Historia principal
       |
       v
Más decisiones y acontecimientos
       |
       v
Estado final
       |
   /   |   \
  A    B    C
```

De esta manera, un juego puede tener **muchas combinaciones posibles de acciones y estados**, pero finalmente todas esas combinaciones conducen a un número limitado de finales.

**Nombres utilizados:** `Multiple Endings`, `Alternative Endings`, `Ending States`, `Final States`.

---

## 1.6. Roles y habilidades del personaje — Character Abilities / Role-Based Mechanics

El jugador puede elegir o recibir un **rol** que determine sus posibilidades dentro del juego.

Por ejemplo:

### Mago

* puede utilizar hechizos;
* puede leer símbolos mágicos;
* puede detectar pasajes ocultos.

### Guerrero

* puede enfrentarse a determinados enemigos;
* puede abrir objetos mediante la fuerza;
* puede utilizar determinadas armas.

### Explorador

* puede encontrar caminos ocultos;
* puede desplazarse por determinados terrenos;
* puede detectar pistas.

El rol puede modificar las acciones disponibles y generar **diferentes formas de resolver una misma situación**.

Por ejemplo:

> Una puerta bloquea el camino.

> El guerrero puede derribarla.
> El mago puede abrirla mediante un hechizo.
> El explorador puede encontrar un pasaje alternativo.

El rol también puede combinarse con otras mecánicas como inventario, navegación, decisiones y condiciones.

**Nombres utilizados:** `Character Abilities`, `Role-Based Mechanics`, `Character Class`, `Class-Based Abilities`.

---

## 1.7. Navegación y espacio — Spatial Navigation / World Map

El juego puede representar un espacio que el jugador debe recorrer.

Una posibilidad es construir un mundo compuesto por diferentes lugares conectados entre sí:

```text
              Bosque
                |
Cueva —— Entrada —— Río
                |
             Aldea
```

El jugador puede desplazarse mediante comandos como:

```text
ir norte
ir sur
ir este
ir oeste
```

También puede utilizarse una representación basada en pasos:

```text
camina 20 pasos al norte
camina 10 pasos al oeste
```

La navegación puede combinarse con condiciones:

> El jugador intenta ir al norte, pero el camino está bloqueado.

> El jugador puede atravesar el río solamente si consiguió la cuerda.

El espacio también puede representarse mediante texto o ASCII.

**Nombres utilizados:** `Spatial Navigation`, `World Map`, `Room System`, `World Model`.

---

## 1.8. Azar y eventos aleatorios — Random Events

Algunos acontecimientos pueden depender del azar.

Por ejemplo:

> Cada vez que el jugador entra en el bosque existe un 30 % de probabilidad de encontrar un animal.

O:

> Al abrir el cofre puede ocurrir aleatoriamente una de tres cosas:

* encontrar dinero;
* encontrar una poción;
* activar una trampa.

El azar también puede determinar características iniciales del juego:

* rol del personaje;
* objeto inicial;
* posición inicial;
* enemigo encontrado;
* cantidad de dinero;
* evento que ocurre.

Los eventos aleatorios pueden combinarse con decisiones y condiciones para producir partidas diferentes.

**Nombres utilizados:** `Random Events`, `Random Outcomes`, `Randomization`.

---

## 1.9. Representación mediante ASCII — ASCII Art / Text-Based Visual Feedback

El texto también puede utilizarse para producir **representaciones visuales**.

Una posibilidad es representar espacialmente el mundo:

```text
+---+---+---+
|   | P |   |
+---+---+---+
|   |   | X |
+---+---+---+
```

También puede utilizarse ASCII para entregar información al jugador:

```text
========================
          SALUD
========================
████████░░  80%
========================
```

El ASCII puede utilizarse tanto para representar el espacio como para proporcionar **feedback visual** al jugador.

Por ejemplo, después de conseguir puntos:

```text
************************
*     +100 PUNTOS      *
************************
```

**Nombres utilizados:** `ASCII Art`, `Text-Based Interface`, `Visual Feedback`.

---

## 1.10. Progresión, puntos y recursos — Progression / Resource System

El jugador puede obtener y perder recursos durante el juego.

Por ejemplo:

* puntos;
* dinero;
* experiencia;
* energía;
* reputación;
* objetos;
* recursos.

Estos recursos pueden utilizarse posteriormente para desbloquear acciones.

Ejemplo:

> El jugador necesita 100 monedas para comprar el mapa.

O:

> Al completar una misión obtiene experiencia y sube de nivel.

El recurso debe tener una función dentro del sistema del juego y no ser solamente un número que aumenta.

**Nombres utilizados:** `Progression System`, `Resource System`, `Currency`, `Score`, `Experience Points`.

---

## 1.11. Salud, daño y vidas — Health / Damage System

El personaje puede tener un estado de salud que cambia durante el juego.

Por ejemplo:

```text
Salud: 80 / 100
```

Algunos acontecimientos pueden producir daño:

> El jugador entra en una zona venenosa → pierde 20 puntos de salud.

También puede existir recuperación:

> Utilizar una poción → recupera 30 puntos.

Si la salud llega a cero:

> El personaje muere.

El juego puede permitir que el jugador vuelva a un punto anterior de la historia, pierda una vida o termine la partida.

**Nombres utilizados:** `Health System`, `Damage System`, `Lives`, `Respawn`, `Checkpoint`.

---

## 1.12. Estados y eventos ambientales — Environmental States / Hazards

El entorno puede cambiar durante el juego y esos cambios pueden modificar las posibilidades del jugador.

Por ejemplo:

* comienza la noche;
* aparece una niebla;
* aumenta el nivel del río;
* comienza una tormenta;
* se incendia un lugar;
* desaparece un camino;
* aparece un personaje;
* se bloquea una entrada.

Estos cambios pueden ser **eventos** que ocurren durante la partida o **estados persistentes** que modifican el mundo.

Ejemplo:

> Durante el día existe un camino que atraviesa el bosque.

> Cuando llega la noche, aparece una niebla que impide utilizar ese camino.

> El jugador debe encontrar otra ruta.

**Nombres utilizados:** `Environmental State`, `Environmental Hazard`, `Dynamic Environment`, `World State`, `Environmental Event`.

---

# 2. El ejercicio

Diseña un videojuego de texto utilizando **al menos 4 de las mecánicas anteriores**.

El objetivo no es escribir todavía el código, sino construir las reglas y la estructura del juego.

Tu propuesta debe contener:

### 1. Título

Nombre del videojuego.

### 2. Premisa

Explica brevemente:

* ¿Dónde ocurre?
* ¿Quién es el jugador?
* ¿Qué está intentando conseguir?
* ¿Cuál es el conflicto o problema principal?

### 3. Objetivo del jugador

Explica qué debe conseguir el jugador para ganar.

Puede ser, por ejemplo:

* escapar de un lugar;
* resolver un misterio;
* encontrar un objeto;
* llegar a determinado lugar;
* rescatar a un personaje;
* sobrevivir determinado tiempo;
* completar una misión.

### 4. Mecánicas utilizadas

Selecciona **al menos 4 mecánicas** de la lista anterior.

Para cada una explica:

* qué mecánica utilizarás;
* cómo funciona en tu juego;
* qué puede hacer el jugador;
* cómo afecta la experiencia;
* qué relación tiene con las demás mecánicas, si aplica.

### 5. Guion y estructura del juego

Escribe el recorrido posible del juego.

No es necesario escribir todos los diálogos. Lo importante es mostrar:

* cuál es la historia principal;
* qué decisiones puede tomar el jugador;
* qué situaciones pueden desviarse temporalmente;
* cómo algunas rutas vuelven a la historia principal;
* qué estados se van modificando;
* cómo esos estados pueden afectar acontecimientos posteriores;
* cuáles son los posibles finales.

Puedes utilizar un esquema como:

```text
                    HISTORIA PRINCIPAL
                           |
                           v
                    Situación inicial
                           |
                           v
                   Decisión del jugador
                     /             \
                    /               \
               Evento A           Evento B
                    |               |
                    |               |
                    +-------+-------+
                            |
                            v
                    HISTORIA PRINCIPAL
                            |
                            v
                     Nuevos eventos
                            |
                            v
                       Estado final
                      /      |      \
                     /       |       \
                 Final A  Final B  Final C
```

El objetivo no es construir un árbol infinito de decisiones. **El juego debe tener una estructura finita**, aunque pueda contener muchas combinaciones posibles de decisiones y estados.

### 6. Estado del juego

Indica qué información necesita recordar el programa durante la partida.

Por ejemplo:

```text
salud
dinero
tieneLlave
esDeNoche
rol
puertaAbierta
ayudoAlGuardia
vidas
```

No necesitas escribir código. Solo debes explicar **qué variables o estados serían necesarios y para qué sirven**.

### 7. Finales posibles

Define los diferentes finales que puede tener el juego.

Por ejemplo:

```text
Final A — Escapas
Final B — Te capturan
Final C — Descubres la verdad
Final D — Mueres
```

Para cada final explica brevemente **qué condiciones llevan a él**.

Por ejemplo:

```text
Final A:
tieneLlave == true
y
ayudoAlGuardia == true

Final B:
tieneLlave == false
y
vidas > 0

Final C:
descubrioSecreto == true
```

No es necesario que cada decisión tenga un final diferente. **Varias rutas y combinaciones de decisiones pueden conducir al mismo final.**

### 8. Ejemplo de una partida

Escribe un pequeño ejemplo de cómo sería jugar tu videojuego.

Por ejemplo:

```text
Te encuentras frente a una puerta de metal.

¿Qué quieres hacer?

> examinar puerta

La puerta está cerrada. Tiene una pequeña cerradura.

> inventario

Tienes:
- llave oxidada
- linterna

> usar llave

La llave entra en la cerradura.

La puerta se abre.

¿Quieres entrar?

1. Sí
2. No

> 1

Entras en una habitación completamente oscura...
```

El ejemplo debe mostrar **cómo funcionan las mecánicas que escogiste**.

---

# 3. Condiciones del ejercicio

Tu videojuego debe:

* utilizar **mínimo 4 mecánicas** de la lista;
* tener un objetivo claro;
* permitir que el jugador realice acciones o tome decisiones;
* estar diseñado de manera que pueda ser posteriormente programado en C#.

**No es necesario programar todavía el videojuego.**

En esta etapa nos interesa principalmente diseñar las **reglas del juego**, sus posibilidades y su estructura narrativa.

---

# 4. Entrega

Entrega un archivo `.md` que contenga:

1. **Título del juego**
2. **Premisa**
3. **Objetivo**
4. **Mecánicas utilizadas**
5. **Descripción de cada mecánica**
6. **Guion y estructura del juego**
7. **Estados o variables necesarias**
8. **Finales posibles**
9. **Ejemplo de una partida**

La propuesta debe ser suficientemente clara para que otra persona pueda entender **cómo se juega sin necesidad de ver el código**.

---

## Importante

No se trata solamente de escribir una historia.

Una historia dice:

> "El personaje entra al bosque y encuentra un monstruo."

Un diseño de videojuego debe definir qué puede hacer el jugador y qué reglas determinan el resultado:

> "El jugador entra al bosque. Tiene un 30 % de probabilidad de encontrar al monstruo. Si su personaje es guerrero puede enfrentarlo. Si tiene una antorcha puede evitarlo. Si no tiene ninguna de las dos cosas, debe escapar hacia el río."

También es importante distinguir entre **las decisiones que toma explícitamente el jugador** y **las decisiones que toma el sistema a partir del estado del juego**.

Por ejemplo:

> El jugador decide explícitamente si ayuda o no a un personaje.

Esa decisión puede modificar una variable:

```text
ayudoAlPersonaje = true
```

Más adelante, el programa puede utilizar esa variable junto con otras condiciones:

```text
Si ayudoAlPersonaje == true
y tieneLaLlave == true
y esDeNoche == false

→ Final A
```

El jugador no necesariamente sabe que esa combinación de variables determina el resultado.

Finalmente, una aventura puede tener **muchas combinaciones posibles de decisiones, objetos, estados y acontecimientos**, pero todas ellas forman parte de un sistema finito. Las diferentes rutas pueden desviarse de la historia principal, volver a ella y finalmente conducir a **uno de un número limitado de finales posibles**.

En este ejercicio, **las reglas que relacionan las acciones del jugador, los estados del juego y las consecuencias son tan importantes como la historia que se está contando**.

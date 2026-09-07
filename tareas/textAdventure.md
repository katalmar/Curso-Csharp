Claro. Hice una última comprobación de los referentes y mantengo solo los que tienen página jugable en navegador. Por ejemplo, *Las Minas de Socartes* y *Rúnari* aparecen como juegos HTML5 con opción de jugar en navegador, y *El Horror de Chambertown* confirma que es ficción interactiva en español y jugable en HTML5. ([itch.io][1])

# Tarea: referentes de Text Adventure y mecánicas

## Objetivo

Investigar referentes de los **juegos de aventura de texto (Text Adventure)** e identificar las mecánicas que utilizan para construir sus experiencias interactivas.

La tarea busca reconocer **qué reglas y sistemas utiliza un juego** y qué características de esas mecánicas pueden ser importantes al momento de programarlas.

---

# 1. Referentes para conocer el género

Los siguientes son algunos referentes de **ficción interactiva y aventuras de texto en español**.

Puedes utilizar estos juegos para realizar la tarea o buscar otros juegos en internet.

Se recomienda **jugar al menos una parte del juego** antes de analizar sus mecánicas.

---

## Las Minas de Socartes

**Año:** 2019
**Autor:** Billy Y. Fernández / Textagames

Aventura de texto basada en la novela *Marianela* de Benito Pérez Galdós. El jugador controla a Teodoro Golfín y puede interactuar con el mundo mediante diferentes acciones como **mirar, examinar, ir, hablar, coger, dar, usar e inventario**.

Es un buen referente para observar cómo una historia puede convertirse en un sistema de acciones, objetos, exploración y condiciones. ([itch.io][1])

**Jugar:** [Las Minas de Socartes](https://textagames.itch.io/socartes?utm_source=chatgpt.com)

---

## Rúnari

**Año:** 2020
**Autor:** Textagames

Aventura interactiva sobre los últimos hijos del Sol. El jugador puede tomar decisiones, recoger objetos y consultar el estado de salud de su personaje. El juego plantea diferentes consecuencias y varios posibles finales. ([itch.io][2])

Es un buen referente para analizar **decisiones, objetos, estados y consecuencias**.

**Jugar:** [Rúnari](https://textagames.itch.io/runari?utm_source=chatgpt.com)

---

## La Habitación

**Año:** 2020
**Autor:** archtron

Ficción interactiva en la que el jugador debe resolver diferentes rompecabezas relacionados con sus propios recuerdos para conseguir salir de una habitación.

Es un buen referente para observar cómo se pueden utilizar **información, condiciones, objetos y resolución de problemas**. La página del autor confirma que cuenta con versión para jugar en navegador. ([itch.io][3])

**Jugar:** [La Habitación](https://archtron.itch.io/la-habitacion?utm_source=chatgpt.com)

---

## Nueve y cinco

**Año:** 1987
**Autor:** Adam Cadre

Versión en español para navegador del juego *9:05*. El jugador comienza en una situación cotidiana: despierta tarde, recibe una llamada y debe prepararse para llegar al trabajo. Las acciones aparentemente sencillas permiten descubrir progresivamente información sobre la situación. ([itch.io][4])

Es especialmente interesante para analizar cómo las **acciones, información y consecuencias** pueden modificar la experiencia del jugador.

**Jugar:** [Nueve y cinco](https://archtron.itch.io/nueve-y-cinco?utm_source=chatgpt.com)

---

## El Horror de Chambertown

**Año:** 2022
**Autora:** Florencia C. Wagemann

Narrativa hipertextual interactiva inspirada en H. P. Lovecraft, el horror cósmico y el cine de terror de los años 80. Utiliza decisiones y diferentes recorridos narrativos, y cuenta con múltiples finales. Fue realizada con Twine y puede jugarse en navegador. ([itch.io][5])

Es un buen referente para observar **decisiones, ramificaciones, ambiente y diferentes finales**.

**Jugar:** [El Horror de Chambertown](https://florenciaw.itch.io/el-horror-de-chambertown?utm_source=chatgpt.com)

---

# 2. Buscar referentes

Selecciona **al menos 2 juegos de Text Adventure o Interactive Fiction** para analizar.

Puedes escoger cualquiera de los cinco referentes anteriores o buscar otros juegos en internet.

De cada juego solamente debes registrar:

* **Nombre**
* **Año**
* **Autor**

juega los referentes que seleccionaste para poder continuar

---

# 3. Identificar las mecánicas

Después de jugar y conocer los juegos seleccionados, identifica **al menos 3 mecánicas** que utilicen.

Puedes encontrar, entre otras, las siguientes:

1. **Decisiones y ramificaciones**
   Una decisión del jugador puede llevar a diferentes situaciones, lugares o resultados.

2. **Objetos e inventario**
   El jugador puede encontrar, recoger, conservar o utilizar objetos.

3. **Objetos y condiciones**
   Una acción puede depender de que el jugador tenga determinado objeto o haya realizado previamente determinada acción.

4. **Exploración**
   El jugador puede desplazarse entre diferentes lugares y descubrir nuevas situaciones.

5. **Ambiente**
   El contexto del mundo puede cambiar independientemente de las decisiones del jugador. Por ejemplo, puede ser de día o de noche, y ese cambio puede modificar lo que ocurre aunque el jugador haya tomado exactamente las mismas decisiones.

6. **Estados del jugador**
   El jugador puede tener características que cambian durante el juego, como energía, salud, tiempo disponible o algún otro estado.

7. **Comandos o acciones**
   El jugador puede realizar diferentes acciones para interactuar con el mundo, y el juego responde dependiendo de la acción realizada.

8. **Consecuencias**
   Una acción puede modificar situaciones posteriores, haciendo que una decisión tomada anteriormente tenga efectos más adelante.

---

# 4. Describir las mecánicas

De las mecánicas que identificaste, selecciona **al menos 3 y descríbelas de manera concreta**.

No basta con nombrarlas.

Por ejemplo, no es suficiente escribir:

> "El juego tiene objetos."

Debes explicar **cómo funciona esa mecánica dentro del juego**.

Para cada una de las tres mecánicas explica:

### ¿Qué puede hacer el jugador?

Describe la acción o interacción que puede realizar.

### ¿Qué condiciones intervienen?

¿Qué determina si la acción puede realizarse o qué resultado produce?

### ¿Qué ocurre como consecuencia?

Explica qué sucede después de la acción.

### ¿De qué depende la mecánica?

Identifica si depende de:

* una decisión del jugador;
* una condición previa;
* un objeto;
* una característica del jugador;
* una variable independiente del jugador;
* o una combinación de varios elementos.

Esta última parte es importante porque las características de una mecánica pueden orientar **qué estrategia de programación podría utilizarse para implementarla**.

---

# 5. Ejemplos

## Ejemplo 1: mecánica de ambiente

Imagina que en un juego el ambiente puede ser **de día o de noche**.

Durante la aventura aparece un mensaje:

```text
Está anocheciendo.
```

A partir de ese momento, algunas situaciones cambian.

Lo importante es que el cambio de ambiente **no depende de la decisión del jugador**.

Aunque el jugador hubiera elegido diferentes caminos, el ambiente habría cambiado igualmente.

Podemos representarlo conceptualmente como:

```text
ambiente = día
      ↓
   pasa el tiempo
      ↓
ambiente = noche
```

La característica importante de esta mecánica es que `ambiente` funciona como una **variable independiente de las decisiones del jugador**.

Posteriormente, diferentes partes del juego pueden consultar esta variable:

```text
misma decisión
      ↓
 ┌────┴────┐
día      noche
 ↓          ↓
resultado A resultado B
```

---

## Ejemplo 2: objeto y condición

Un jugador encuentra una puerta cerrada.

Para abrirla necesita una llave.

La posibilidad de abrir la puerta depende de dos cosas:

* si el jugador tiene la llave;
* la decisión de intentar abrir la puerta.

Conceptualmente:

```text
¿Tiene la llave?
      ↓
     sí
      ↓
¿Quiere abrir la puerta?
      ↓
     sí
      ↓
La puerta se abre
```

Aquí la mecánica depende tanto del **estado anterior del jugador** como de una **decisión que toma el usuario**.

Esto puede llevar a una estrategia de programación diferente a la utilizada para una variable de ambiente independiente.

---

# 6. Entrega

Tu entrega debe contener:

### Referentes

Al menos **2 juegos**:

* Nombre
* Año
* Autor

### Mecánicas

Identifica **al menos 3 mecánicas** presentes en los juegos investigados.

### Descripción

Describe detalladamente esas **3 mecánicas**.

Para cada una explica:

* qué puede hacer el jugador;
* qué condiciones intervienen;
* qué ocurre como consecuencia;
* de qué elementos depende la mecánica.

El objetivo es entender las mecánicas lo suficientemente bien como para comenzar a pensar **qué estrategias de programación podrían utilizarse para implementarlas**.

[1]: https://textagames.itch.io/socartes?utm_source=chatgpt.com "Las Minas De Socartes by Textagames"
[2]: https://textagames.itch.io/runari?utm_source=chatgpt.com "Rúnari by Textagames"
[3]: https://archtron.itch.io/?utm_source=chatgpt.com "archtron - itch.io"
[4]: https://archtron.itch.io/nueve-y-cinco?utm_source=chatgpt.com "Nueve y cinco (port a web del juego 9:05) by archtron"
[5]: https://florenciaw.itch.io/el-horror-de-chambertown?utm_source=chatgpt.com "El Horror de Chambertown by Florencia C. Wagemann"

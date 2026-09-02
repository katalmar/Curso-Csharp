# Tutorial: conectar VS Code con GitHub en Windows

Este tutorial explica cómo conectar un proyecto de **Visual Studio Code (VS Code)** con una cuenta personal de **GitHub**, utilizando Git.
---

# 3. Comprobar si Git está instalado

Git es el programa que permite controlar las versiones de nuestro proyecto y conectarlo con GitHub.

## 3.1 Abrir la terminal de VS Code

Abre VS Code.

En el menú superior selecciona:

**Terminal → New Terminal**

También puedes utilizar:

```text
Ctrl + `
```

Se abrirá una terminal en la parte inferior de VS Code.

---

## 3.2 Comprobar Git

En la terminal escribe:

```bash
git --version
```

y presiona:

**Enter**

### Si Git está instalado

Aparecerá algo parecido a:

```text
git version 2.50.1.windows.1
```

En ese caso, puedes continuar directamente con el **paso 5**.

### Si Git no está instalado

Puede aparecer un mensaje parecido a:

```text
git : The term 'git' is not recognized...
```

No hay problema. Puedes instalar Git y continuar con el tutorial.

---

# 4. Instalar Git si no está instalado

VS Code puede detectar que Git no está disponible y permitirte instalarlo mediante las opciones de integración de control de código fuente.

## 4.1 Abrir Source Control

En la barra lateral izquierda de VS Code busca el icono:

**Source Control**

Su icono tiene aproximadamente esta forma:

```text
    o
   /
  o──o
```

Haz clic sobre él.

Si Git no está instalado, VS Code puede mostrar un mensaje indicando que Git no está disponible y ofrecer opciones para instalarlo o abrir la documentación correspondiente.

> **Importante:** la disponibilidad exacta del botón de instalación puede variar según la versión de VS Code. Si VS Code no muestra directamente un instalador, puedes instalar Git desde su instalador oficial de Windows y después reiniciar VS Code.

---

## 4.2 Instalar Git para Windows

Si VS Code no ofrece directamente la instalación, utiliza **Git for Windows**.

Descarga e instala Git siguiendo el instalador.

Durante la instalación, si no sabes qué opciones elegir, puedes mantener las opciones predeterminadas.

Una vez terminada la instalación:

1. Cierra VS Code.
2. Vuelve a abrir VS Code.
3. Abre una nueva terminal.
4. Ejecuta:

```bash
git --version
```

Deberías obtener algo parecido a:

```text
git version 2.50.1.windows.1
```

Ahora Git está instalado.

---

# 5. Configurar Git por primera vez

Antes de comenzar a utilizar Git, es recomendable configurar el nombre y el correo electrónico que Git utilizará para identificar tus commits.

En la terminal de VS Code escribe:

```bash
git config --global user.name "Tu Nombre"
```

Por ejemplo:

```bash
git config --global user.name "Katherine Romero"
```

Después configura tu correo:

```bash
git config --global user.email "tu-correo@example.com"
```

Utiliza el correo que tengas asociado a tu cuenta de GitHub o el correo que hayas configurado para tus commits.

---

## 5.1 Comprobar la configuración

Puedes comprobar la configuración utilizando:

```bash
git config --global user.name
```

y:

```bash
git config --global user.email
```

Git debería mostrar los datos configurados.

---

# 6. Iniciar sesión en GitHub desde VS Code

Ahora vamos a conectar VS Code con tu cuenta personal de GitHub.

## 6.1 Abrir la paleta de comandos

En VS Code presiona:

```text
Ctrl + Shift + P
```

Aparecerá una barra en la parte superior.

Escribe:

```text
GitHub
```

Busca las opciones relacionadas con iniciar sesión en GitHub.

VS Code puede abrir tu navegador para realizar la autenticación.

---

## 6.2 Autorizar VS Code

En el navegador:

1. Inicia sesión en tu cuenta personal de GitHub.
2. Autoriza a VS Code cuando se solicite.
3. Regresa a VS Code.

Ahora VS Code podrá utilizar tu cuenta de GitHub para publicar y sincronizar repositorios.

---

# 7. Abrir el proyecto en VS Code

Ahora debemos abrir el proyecto que queremos conectar con GitHub.

En VS Code selecciona:

**File → Open Folder...**

Busca la carpeta donde está tu proyecto.

Por ejemplo:

```text
C:\Users\TuUsuario\Documents\MiProyecto
```

La estructura podría ser:

```text
MiProyecto
│
├── Program.cs
├── README.md
└── ...
```

Selecciona la carpeta:

```text
MiProyecto
```

y presiona:

**Select Folder**

---

# 8. Crear un repositorio Git local

Ahora debemos indicarle a Git que esta carpeta es un repositorio.

En VS Code abre:

**Source Control**

Si la carpeta todavía no tiene Git, aparecerá una opción como:

**Initialize Repository**

Haz clic sobre ella.

VS Code ejecutará internamente:

```bash
git init
```

Esto crea un repositorio Git local.

---

## 8.1 ¿Qué significa "repositorio local"?

Significa que Git comienza a controlar los cambios de los archivos que están en tu computador.

Tenemos ahora:

```text
COMPUTADOR
│
└── MiProyecto
       │
       └── Git
```

Pero todavía **no hemos conectado el proyecto con GitHub**.

---

# 9. Preparar los archivos para el primer commit

Después de inicializar Git, abre:

**Source Control**

VS Code mostrará los archivos que Git ha detectado.

Por ejemplo:

```text
CHANGES

U  Program.cs
U  README.md
```

La `U` significa:

**Untracked**

Es decir, Git ha encontrado el archivo, pero todavía no lo está siguiendo.

---

## 9.1 Agregar los archivos al Stage

En Source Control encontrarás un botón `+` junto a los archivos.

Haz clic en `+`.

También puedes utilizar la opción para agregar todos los cambios.

Los archivos pasarán de:

```text
CHANGES
```

a:

```text
STAGED CHANGES
```

El proceso es:

```text
Archivo
   ↓
Stage
```

El **Stage** es una zona donde seleccionamos los cambios que queremos incluir en el próximo commit.

---

# 10. Crear el primer commit

Ahora debemos crear nuestro primer commit.

En Source Control aparecerá un campo para escribir el mensaje del commit.

Escribe:

```text
Primer commit
```

Después presiona:

**Commit**

---

## 10.1 ¿Qué es un commit?

Un commit es una especie de punto de guardado de nuestro proyecto.

Por ejemplo:

```text
Commit 1
Primer commit
```

Más adelante podríamos tener:

```text
Commit 1
Primer commit
      ↓
Commit 2
Agrega menú principal
      ↓
Commit 3
Agrega sistema de puntuación
```

Git conserva este historial.

Esto permite saber qué cambios se hicieron y cuándo.

---

# 11. Publicar el proyecto en GitHub

Hasta este momento tenemos:

```text
COMPUTADOR
│
└── MiProyecto
       │
       └── Git
```

Ahora queremos:

```text
COMPUTADOR
│
└── MiProyecto
       │
       └── Git
             │
             ↓
          GitHub
```

---

## 11.1 Utilizar "Publish to GitHub"

Después del primer commit, VS Code debería mostrar una opción como:

**Publish to GitHub**

Haz clic sobre ella.

VS Code utilizará la cuenta de GitHub con la que acabamos de iniciar sesión.

---

## 11.2 Elegir la cuenta

Si tienes varias cuentas de GitHub configuradas, VS Code puede preguntarte cuál quieres utilizar.

Selecciona tu:

**Cuenta personal de GitHub**

---

## 11.3 Elegir la visibilidad

VS Code te preguntará si quieres crear el repositorio como:

### Public

El repositorio puede ser visto por cualquier persona.

```text
GitHub
└── MiProyecto
    └── Public
```

### Private

El repositorio solamente puede ser visto por ti y por las personas a las que autorices.

```text
GitHub
└── MiProyecto
    └── Private
```

Si estás trabajando en un proyecto personal que todavía no quieres hacer público, selecciona:

**Private**

---

## 11.4 Publicar

Después de seleccionar la visibilidad, VS Code creará el repositorio en GitHub y subirá el proyecto.

El proceso completo será:

```text
MiProyecto
    ↓
Git
    ↓
Commit
    ↓
Publish
    ↓
GitHub
```

---

# 12. Comprobar el repositorio en GitHub

Abre GitHub en tu navegador e ingresa a tu cuenta.

Deberías encontrar el nuevo repositorio.

Por ejemplo:

```text
Tu cuenta de GitHub
│
└── MiProyecto
      │
      ├── Program.cs
      ├── README.md
      └── ...
```

Si aparecen tus archivos, significa que el proyecto ya está conectado con GitHub.

---

# 13. Trabajar normalmente con el proyecto

A partir de ahora comienza el flujo normal de trabajo.

Supongamos que modificas:

```text
Program.cs
```

VS Code detectará automáticamente el cambio.

En Source Control aparecerá algo parecido a:

```text
CHANGES

M  Program.cs
```

La `M` significa:

**Modified**

Es decir:

> El archivo fue modificado después del último commit.

---

# 14. Hacer un nuevo commit

El proceso será nuevamente:

```text
Modificar
   ↓
Stage
   ↓
Commit
```

Por ejemplo:

### 1. Modificar

Cambias `Program.cs`.

### 2. Stage

Presionas `+`.

### 3. Commit

Escribes:

```text
Agrega cálculo de promedio
```

y presionas:

**Commit**

Ahora tienes:

```text
Commit 1
Primer commit
      ↓
Commit 2
Agrega cálculo de promedio
```

Pero hay una diferencia importante:

**El segundo commit todavía puede estar solamente en tu computador.**

Para enviarlo a GitHub necesitas hacer un **Push**.

---

# 15. Push: enviar cambios a GitHub

**Push** significa enviar tus commits locales al repositorio de GitHub.

El flujo es:

```text
COMPUTADOR
    │
    │ PUSH
    ↓
 GITHUB
```

En VS Code puedes utilizar:

**Sync Changes**

o la opción de:

**Push**

Después de hacer Push, el nuevo commit aparecerá en GitHub.

---

# 16. Pull: traer cambios desde GitHub

**Pull** hace el proceso contrario.

Sirve para traer cambios que están en GitHub hacia tu computador.

```text
GITHUB
   │
   │ PULL
   ↓
COMPUTADOR
```

Por ejemplo:

```text
GitHub
   │
   │
   ↓
Nuevo cambio
   │
   │ Pull
   ↓
Tu computador
```

Esto es especialmente importante cuando trabajas con el mismo proyecto desde diferentes computadores o cuando otras personas también modifican el repositorio.

---

# 17. Sync Changes

VS Code también tiene una opción llamada:

**Sync Changes**

La sincronización permite mantener el repositorio local y el repositorio de GitHub coordinados.

Conceptualmente:

```text
       VS CODE
          ↕
        SYNC
          ↕
       GITHUB
```

En términos simples:

* **Push** → enviar cambios a GitHub.
* **Pull** → traer cambios desde GitHub.
* **Sync** → sincronizar ambos lados.

---

# 18. El flujo normal de trabajo

Una vez que el proyecto está conectado, el flujo más común será:

```text
1. Abrir el proyecto
        ↓
2. Trabajar en VS Code
        ↓
3. Modificar archivos
        ↓
4. Revisar los cambios
        ↓
5. Stage (+)
        ↓
6. Escribir mensaje
        ↓
7. Commit
        ↓
8. Push / Sync Changes
        ↓
9. Cambios aparecen en GitHub
```

---

# 19. El archivo `.gitignore`

No todos los archivos del proyecto deberían subirse a GitHub.

Para indicar a Git qué archivos debe ignorar se utiliza:

```text
.gitignore
```

Por ejemplo:

```gitignore
.env
node_modules/
.DS_Store
```

Esto puede evitar que archivos innecesarios o información privada sean incluidos en el repositorio.

---

## 19.1 Información que nunca deberías subir

No debes subir accidentalmente:

* Contraseñas.
* Tokens.
* Claves API.
* Credenciales.
* Información privada.
* Archivos `.env` que contengan secretos.

Antes de hacer un commit, revisa siempre los archivos que aparecen en **Source Control**.

---

# 20. Git y GitHub no son lo mismo

Es importante entender esta diferencia.

## Git

Git es el sistema de control de versiones que funciona en tu computador.

```text
TU COMPUTADOR
      ↓
     GIT
```

## GitHub

GitHub es un servicio donde puedes almacenar repositorios Git de manera remota.

```text
TU COMPUTADOR
      ↓
     GIT
      ↓
    GITHUB
```

Por eso:

```text
Git ≠ GitHub
```

Git controla las versiones.

GitHub permite almacenar y compartir esos repositorios de manera remota.

---

# 21. Resumen de los conceptos principales

| Concepto         | ¿Qué significa?                                         |
| ---------------- | ------------------------------------------------------- |
| **Git**          | Sistema de control de versiones                         |
| **GitHub**       | Servicio donde almacenamos repositorios Git remotamente |
| **Repository**   | Carpeta/proyecto controlado por Git                     |
| **Stage**        | Seleccionar cambios para el próximo commit              |
| **Commit**       | Guardar una versión del proyecto en el historial        |
| **Push**         | Enviar commits a GitHub                                 |
| **Pull**         | Traer cambios desde GitHub                              |
| **Sync**         | Sincronizar el repositorio local y GitHub               |
| **`.gitignore`** | Indica qué archivos Git debe ignorar                    |

---

# 22. El flujo que debes recordar

La primera vez:

```text
VS CODE
   ↓
Comprobar Git
   ↓
Instalar Git si es necesario
   ↓
Configurar Git
   ↓
Iniciar sesión en GitHub
   ↓
Abrir proyecto
   ↓
Initialize Repository
   ↓
Stage
   ↓
Commit
   ↓
Publish to GitHub
   ↓
GITHUB
```

Después de que el proyecto ya está conectado:

```text
Modificar archivos
       ↓
     Stage
       ↓
     Commit
       ↓
   Push / Sync
       ↓
     GitHub
```

Y para traer cambios desde GitHub:

```text
GitHub
   ↓
 Pull
   ↓
VS Code
```

**Con este flujo puedes trabajar con GitHub desde VS Code sin tener que utilizar constantemente la terminal.**

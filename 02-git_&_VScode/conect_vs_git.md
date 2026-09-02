# Tutorial: conectar VS Code con GitHub

Este tutorial explica cómo conectar un proyecto que tienes en tu computador, abierto en **Visual Studio Code (VS Code)**, con tu cuenta personal de **GitHub**.

La idea general es:

```text
Proyecto en tu computador
          ↓
         Git
          ↓
       GitHub
```

---

## 1. ¿Qué necesitas?

Antes de comenzar necesitas:

* Una cuenta personal de GitHub.
* Visual Studio Code instalado.
* Git instalado en tu computador.
* Una carpeta con tu proyecto.

VS Code tiene integración con Git y GitHub, por lo que puedes realizar muchas operaciones directamente desde su interfaz.

---

# 2. Comprobar que Git está instalado

Abre VS Code.

Después abre la terminal:

**Terminal → New Terminal**

También puedes utilizar el atajo correspondiente a tu sistema.

En la terminal escribe:

```bash
git --version
```

Si aparece algo parecido a:

```text
git version 2.50.1
```

significa que Git está instalado correctamente.

Si aparece un mensaje indicando que `git` no existe o no se encuentra, primero debes instalar Git.

---

# 3. Iniciar sesión en GitHub desde VS Code

Abre la paleta de comandos de VS Code:

**View → Command Palette**

También puedes utilizar:

```text
Mac: ⇧ + ⌘ + P
```

Escribe:

```text
GitHub
```

Busca las opciones relacionadas con iniciar sesión en GitHub.

VS Code puede abrir una ventana del navegador para que autorices la conexión con tu cuenta de GitHub.

Una vez autorizada la cuenta, regresa a VS Code.

---

# 4. Abrir tu proyecto en VS Code

En VS Code selecciona:

**File → Open Folder...**

Selecciona la carpeta que contiene tu proyecto.

Por ejemplo:

```text
Documentos/
└── MiProyecto/
    ├── Program.cs
    ├── README.md
    └── ...
```

Es importante abrir la **carpeta principal del proyecto**, no solamente uno de los archivos.

---

# 5. Inicializar Git en el proyecto

En la barra lateral izquierda de VS Code busca:

**Source Control**

El icono normalmente parece una ramificación:

```text
    o
   /
  o──o
```

Haz clic sobre él.

Si el proyecto todavía no tiene Git, VS Code debería mostrar una opción similar a:

**Initialize Repository**

Haz clic en ella.

Esto crea un repositorio Git local dentro de tu proyecto.

Es equivalente a ejecutar:

```bash
git init
```

Pero en este caso VS Code realiza la operación por ti.

---

# 6. ¿Qué acaba de ocurrir?

Ahora tu proyecto tiene un repositorio Git local:

```text
MiProyecto
     ↓
    Git
```

Git comenzará a registrar los cambios que hagas en los archivos.

Sin embargo, todavía **no está conectado con GitHub**.

En este momento Git existe solamente en tu computador.

---

# 7. Preparar los archivos para el primer commit

Vuelve a:

**Source Control**

Es posible que aparezcan tus archivos bajo:

```text
CHANGES
```

Por ejemplo:

```text
U  Program.cs
U  README.md
```

La letra `U` significa:

```text
Untracked
```

Es decir, Git todavía no está siguiendo esos archivos.

Para prepararlos, pulsa el botón `+` que aparece junto a cada archivo o utiliza la opción para preparar todos los cambios.

Los archivos pasarán a:

```text
STAGED CHANGES
```

---

# 8. Crear el primer commit

En Source Control encontrarás un espacio para escribir el mensaje del commit.

Escribe algo como:

```text
Primer commit
```

Después selecciona:

**Commit**

Un commit representa una versión guardada de tu proyecto.

El proceso es:

```text
Archivos
   ↓
Stage
   ↓
Commit
```

Pero todavía hay algo importante:

El commit está solamente en tu computador.

Todavía no está en GitHub.

---

# 9. Publicar el proyecto en GitHub

Ahora VS Code puede mostrar una opción como:

**Publish to GitHub**

Haz clic sobre ella.

VS Code te preguntará qué cuenta de GitHub quieres utilizar.

Selecciona tu **cuenta personal**.

---

# 10. Elegir si el repositorio será público o privado

VS Code puede preguntarte si quieres crear el repositorio como:

### Public

Cualquier persona puede ver el repositorio.

```text
GitHub
└── MiProyecto
    └── Público
```

### Private

Solamente tú y las personas que autorices podrán acceder al repositorio.

```text
GitHub
└── MiProyecto
    └── Privado
```

Si estás aprendiendo o trabajando en un proyecto que todavía no quieres hacer público, puedes seleccionar:

**Private**

---

# 11. VS Code conecta el proyecto con GitHub

Al publicar el proyecto, VS Code realizará automáticamente varias operaciones.

Conceptualmente ocurre esto:

```text
TU COMPUTADOR

MiProyecto
     │
     ↓
    Git
     │
     ↓
   Commit
     │
     │ Push
     ↓
   GitHub
     │
     ↓
tu-cuenta/MiProyecto
```

Tu repositorio local queda conectado con el repositorio remoto de GitHub.

---

# 12. Comprobar que el proyecto está en GitHub

Entra a GitHub desde tu navegador y abre tu perfil.

Deberías encontrar el repositorio que acabas de crear.

Por ejemplo:

```text
Tu cuenta
│
└── MiProyecto
    ├── Program.cs
    ├── README.md
    └── ...
```

Si aparecen tus archivos, la conexión funcionó correctamente.

---

# 13. ¿Qué hago cuando modifico un archivo?

A partir de ahora trabajarás normalmente en VS Code.

Por ejemplo, modificas:

```text
Program.cs
```

VS Code detectará el cambio.

En Source Control puede aparecer:

```text
CHANGES

M  Program.cs
```

La `M` significa:

```text
Modified
```

Es decir, el archivo fue modificado.

---

# 14. El ciclo normal de trabajo

Cada vez que hagas cambios importantes en tu proyecto, puedes seguir este proceso:

```text
MODIFICAR ARCHIVOS
        ↓
       STAGE
        ↓
      COMMIT
        ↓
       PUSH
        ↓
      GITHUB
```

## Paso 1: modificar

Trabajas normalmente en VS Code.

Por ejemplo:

```text
Program.cs
```

---

## Paso 2: Stage

En Source Control presiona `+` para preparar los archivos modificados.

```text
CHANGES

M  Program.cs
       ↓
       +
       ↓
STAGED CHANGES
```

---

## Paso 3: Commit

Escribe un mensaje que explique qué cambiaste.

Por ejemplo:

```text
Agrega cálculo de promedio
```

Después presiona:

**Commit**

---

## Paso 4: Push

Después debes enviar el commit a GitHub.

Puedes utilizar:

**Sync Changes**

o la opción equivalente de **Push**.

El resultado será:

```text
COMPUTADOR
    │
    │ Push
    ↓
 GITHUB
```

Ahora el cambio también estará almacenado en GitHub.

---

# 15. ¿Qué significa Commit?

Un **commit** es una versión guardada del proyecto.

Por ejemplo:

```text
Commit 1
Primer programa
```

Después haces cambios:

```text
Commit 2
Agrega menú
```

Después:

```text
Commit 3
Agrega cálculo
```

Git mantiene un historial:

```text
Commit 1
   ↓
Commit 2
   ↓
Commit 3
```

Esto permite saber qué cambios se hicieron a lo largo del tiempo.

---

# 16. ¿Qué significa Push?

**Push** significa enviar tus commits desde tu computador hacia GitHub.

```text
COMPUTADOR
    │
    │ PUSH
    ↓
  GITHUB
```

Por ejemplo:

```text
Tu computador:

Commit 1
Commit 2
Commit 3

       ↓ PUSH

GitHub:

Commit 1
Commit 2
Commit 3
```

---

# 17. ¿Qué significa Pull?

**Pull** hace lo contrario.

Sirve para traer desde GitHub cambios que todavía no tienes en tu computador.

```text
COMPUTADOR
    ↑
    │ PULL
    │
  GITHUB
```

Por ejemplo, si modificaste el proyecto desde otro computador y subiste esos cambios a GitHub, puedes utilizar `Pull` para traerlos a tu computador.

---

# 18. ¿Qué significa Sync Changes?

**Sync Changes** sirve para sincronizar tu repositorio local con GitHub.

En términos sencillos:

```text
TU COMPUTADOR
      ↕
    SYNC
      ↕
    GITHUB
```

Puede enviar tus cambios y traer cambios remotos.

---

# 19. Una advertencia importante: `.gitignore`

No todos los archivos de un proyecto deberían subirse a GitHub.

Por ejemplo, no debes subir:

* Contraseñas.
* Claves API.
* Tokens.
* Información privada.
* Archivos `.env` que contengan secretos.
* Archivos generados automáticamente que no sean necesarios.

Para evitar subir determinados archivos se utiliza:

```text
.gitignore
```

Por ejemplo:

```gitignore
.env
node_modules/
.DS_Store
```

El archivo `.gitignore` le indica a Git qué archivos o carpetas debe ignorar.

---

# 20. Resumen del proceso completo

La primera vez:

```text
1. Instalar Git
       ↓
2. Iniciar sesión en GitHub desde VS Code
       ↓
3. Abrir la carpeta del proyecto
       ↓
4. Initialize Repository
       ↓
5. Stage
       ↓
6. Commit
       ↓
7. Publish to GitHub
       ↓
8. Elegir Public o Private
       ↓
9. Proyecto publicado en GitHub
```

Después, cada vez que trabajes:

```text
Modificar archivos
       ↓
     Stage
       ↓
     Commit
       ↓
      Push
       ↓
     GitHub
```

---

# 21. La idea fundamental

Hay que distinguir entre **Git** y **GitHub**.

### Git

Es el sistema que controla las versiones de tu proyecto en tu computador.

```text
TU COMPUTADOR
     ↓
    GIT
```

### GitHub

Es el servicio donde puedes almacenar el repositorio Git de manera remota.

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

Git es la herramienta de control de versiones.

GitHub es un servicio que permite almacenar y trabajar con repositorios Git en línea.

---

# 22. Flujo que debes recordar

Si solamente quieres recordar una cosa de este tutorial, recuerda:

```text
        VS CODE
           │
           │
      modificas archivos
           │
           ↓
         STAGE
           │
           ↓
         COMMIT
           │
           ↓
          PUSH
           │
           ↓
        GITHUB
```

Y cuando necesites traer cambios desde GitHub:

```text
GITHUB
   │
   │ PULL
   ↓
VS CODE
```

Ese es el flujo básico para trabajar con VS Code + Git + GitHub.


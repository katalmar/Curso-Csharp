# Guía: preparar el entorno para programar en C#

En esta guía instalarás las herramientas necesarias para comenzar a programar en **C#**.

Al finalizar tendrás:

* El **SDK de .NET** instalado.
* **Visual Studio Code** instalado.
* La extensión **C# Dev Kit** configurada.

---

## 1. Instala el SDK de .NET


El **SDK de .NET** es la herramienta más importante. Contiene el **compilador de C#** y todo lo necesario para crear y ejecutar programas.

### Primero, verifica si ya está instalado

Antes de descargarlo, comprueba si tu computadora ya tiene instalado el SDK.

#### Windows

Abre **PowerShell** o el **Símbolo del sistema (CMD)** y ejecuta:


dotnet --list-sdks


Si aparece una o más versiones, por ejemplo:


8.0.414 [C:\Program Files\dotnet\sdk]
9.0.305 [C:\Program Files\dotnet\sdk]


significa que el **SDK de .NET está instalado**.

También puedes comprobar directamente la carpeta de instalación:


Get-ChildItem "C:\Program Files\dotnet\sdk"


Si aparecen carpetas con números de versión, el SDK está instalado.

> **Nota:** que `dotnet --version` no funcione no necesariamente significa que el SDK no esté instalado. El problema puede ser que la ubicación de `dotnet` no esté incluida en el **PATH** del sistema.

#### macOS

Abre la aplicación **Terminal** y ejecuta:


ls -d /usr/local/share/dotnet/sdk/*

Si aparecen carpetas con números de versión, por ejemplo:


/usr/local/share/dotnet/sdk/8.0.414


significa que el SDK está instalado en esa ubicación.

> **Nota:** en macOS, la ubicación puede variar dependiendo de cómo se haya instalado .NET. Por esta razón, que `dotnet --version` no funcione no demuestra por sí solo que el SDK no esté instalado.

---

### Si el SDK no está instalado

Descarga el SDK desde:

https://dotnet.microsoft.com/download

Selecciona la **versión LTS más reciente**.

> **Importante:** asegúrate de descargar el **SDK**, no solamente el *Runtime*. Para programar en C# necesitas el SDK.

Instala el SDK siguiendo las instrucciones correspondientes a tu sistema operativo.

---

### Después de instalar: verifica nuevamente

Cuando termine la instalación, **cierra y vuelve a abrir la terminal**.

#### Windows


dotnet --list-sdks


Deberías ver la versión del SDK que acabas de instalar.

Después ejecuta:

dotnet --version


Este comando muestra la versión del SDK que se utilizará por defecto.

#### macOS

Primero comprueba directamente la carpeta del SDK:


ls -d /usr/local/share/dotnet/sdk/*

Después prueba:


dotnet --list-sdks


y:


dotnet --version


> **Importante:** la primera comprobación confirma que el SDK está instalado. Los comandos `dotnet --list-sdks` y `dotnet --version` además permiten comprobar que el sistema puede encontrar y utilizar el comando `dotnet`.

> ✅ **Resultado esperado:** debe existir al menos una versión del SDK y, preferiblemente, `dotnet --version` debe mostrar una versión sin producir errores.



## 2. Instala Visual Studio Code

Si todavía no tienes **Visual Studio Code**, descárgalo desde:

https://code.visualstudio.com

VS Code es un editor de código **gratuito y liviano** que utilizaremos para escribir nuestros programas de C#.

Instálalo utilizando las opciones recomendadas.

---

## 3. Instala C# Dev Kit

Abre **Visual Studio Code**.

Ve a la pestaña **Extensions**, ubicada en la barra lateral, o utiliza el atajo:

Ctrl + Shift + X


Busca:
C# Dev Kit


Instala la extensión desarrollada por **Microsoft**.

C# Dev Kit proporciona herramientas para trabajar con C#, incluyendo:

* Autocompletado de código.
* Detección de errores.
* Depuración (*debugging*).
* Administración de proyectos .NET.
* Navegación por el código.

> **Nota:** al instalar C# Dev Kit, VS Code puede instalar automáticamente otras extensiones necesarias, como la extensión base de C#.

---

## 4. Verifica la instalación

Abre una terminal en Visual Studio Code, View → Terminal.

Luego escribe:
dotnet --version


Si todo está correctamente instalado, aparecerá un número de versión, por ejemplo:

8.0.XXX
o
9.0.XXX

La versión exacta dependerá del SDK que hayas instalado.

> ✅ **Si aparece un número de versión, el SDK de .NET está correctamente instalado.**

---

## 5. Crea tu primer proyecto de C#

Ahora vamos a crear nuestro primer programa de C#.

### 1. Observa la ubicación actual

Cuando abres una terminal, aparece una línea similar a esta: 
user@MacBook-Pro ~ % 
o en Windows  
C:\Users\TuNombre>


Esta información nos indica **en qué ubicación del computador estamos trabajando**.

En macOS y Linux, puedes comprobar la ubicación exacta escribiendo: pwd
`pwd` significa **Print Working Directory** y muestra la ruta de la carpeta actual.

Por ejemplo:/Users/miguelazuero

En Windows puedes utilizar: pwd o cd
para conocer la ubicación actual.

> **Importante:** cuando creamos un proyecto utilizando `dotnet new`, el proyecto se crea dentro de la carpeta en la que nos encontramos actualmente.

---

### 2. Muévete a la carpeta donde quieres guardar tus proyectos

Para cambiar de carpeta utilizamos el comando: 'cd' + ' ' + 'direccion carpeta'
`cd` significa **Change Directory**.

---

### 3. Abre el proyecto en VS Code

Ahora vamos a abrir la carpeta del proyecto desde la interfaz de VS Code.

En la barra superior, selecciona:

File → Open Folder...

Se abrirá una ventana para seleccionar una carpeta.

Busca la carpeta que acabamos de crear:

MiPrimerPrograma

Selecciónala y haz clic en Open.

En la barra lateral izquierda de VS Code aparecerán los archivos del proyecto, entre ellos:

MiPrimerPrograma
├── Program.cs
└── MiPrimerPrograma.csproj

Haz clic en Program.cs para abrir el archivo y ver el código de nuestro primer programa.

Importante: debes seleccionar la carpeta MiPrimerPrograma, no solamente el archivo Program.cs. De esta manera VS Code reconoce y carga el proyecto completo de .NET.

---
### 4. Ejecuta el programa

Finalmente, ejecuta: dotnet run

El proyecto recién creado contiene un programa básico que mostrará:
Hello, World!


🎉 **¡Acabas de crear y ejecutar tu primer programa de C#!**


# Resumen

Para trabajar con C# utilizaremos principalmente estas tres herramientas:

| Herramienta            | Función                                  |
| ---------------------- | ---------------------------------------- |
| **.NET SDK**           | Compila y ejecuta nuestros programas     |
| **Visual Studio Code** | Editor donde escribiremos el código      |
| **C# Dev Kit**         | Agrega herramientas para trabajar con C# |

El flujo básico será:

Visual Studio Code
        ↓
    Escribimos C#
        ↓
      .NET SDK
        ↓
   Compila y ejecuta
        ↓
      Programa


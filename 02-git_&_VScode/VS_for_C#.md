Aquí está solo esa parte:

---

## Instala el SDK de .NET desde Visual Studio Code (con C# Dev Kit)

### 1. Instala Visual Studio Code

Descárgalo desde:

https://code.visualstudio.com

Instálalo con las opciones recomendadas.

### 2. Instala la extensión C# Dev Kit

Abre VS Code y ve a la pestaña **Extensions** (o `Ctrl+Shift+X`).

Busca:

C# Dev Kit


Instala la extensión publicada por **Microsoft**.

> **Nota:** VS Code puede instalar automáticamente otras extensiones necesarias, como la extensión base de C#.

### 3. Instala el SDK desde el panel de bienvenida

Al terminar de instalar C# Dev Kit, se abre automáticamente un panel de bienvenida ("Get Started with C# Dev Kit"). Ahí aparece una opción para **instalar el SDK de .NET** si VS Code no lo detecta en tu equipo. Solo haz clic y sigue el asistente.

> **Si el panel no aparece o lo cerraste:** abre la paleta de comandos con `Ctrl+Shift+P` (o `Cmd+Shift+P` en macOS) y busca **".NET: Get Started"**.

> **Importante:** esta vía instala la versión que Microsoft recomienda en ese momento, que puede no coincidir con una LTS específica que necesites para un curso o proyecto. Si requieres una versión exacta, es más seguro descargar el SDK manualmente desde https://dotnet.microsoft.com/download.

### 4. Verifica la instalación

Abre una terminal en VS Code (View → Terminal) y ejecuta:

dotnet --version


Si aparece un número de versión (por ejemplo, `9.0.305`), el SDK quedó instalado correctamente.

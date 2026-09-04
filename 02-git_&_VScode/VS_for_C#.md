# Instalar el entorno de C# en Windows (VS Code + C# Dev Kit + SDK)

Esta es la ruta de instalación que funcionó, sin salir de Visual Studio Code.

---

## 1. Instala Visual Studio Code

Descárgalo desde:

https://code.visualstudio.com

Instálalo con las opciones recomendadas.

---

## 2. Instala la extensión C# Dev Kit

1. Abre VS Code.
2. Ve a la pestaña **Extensions** (o presiona `Ctrl+Shift+X`).
3. Busca:

   C# Dev Kit

4. Instala la extensión publicada por **Microsoft**.

Al instalarla, VS Code instala automáticamente dos dependencias necesarias:

- **C# extension** (el motor de lenguaje: IntelliSense, sintaxis, etc.)
- **.NET Install Tool** (la herramienta que se encarga de descargar e instalar el SDK/runtime de .NET)

> **Nota:** estas dos extensiones no son el SDK, son las herramientas que te van a permitir instalarlo en el siguiente paso.

---

## 3. Instala el SDK de .NET desde la paleta de comandos

1. Abre la paleta de comandos: `Ctrl+Shift+P`.
2. Escribe y selecciona:

   .NET Install Tool: Install the .NET SDK System-Wide

3. Si aparece un cuadro de **UAC** (permisos de administrador), acéptalo. La instalación "System-Wide" necesita escribir en carpetas del sistema (`C:\Program Files\dotnet`).
4. Espera a que termine la descarga e instalación.

> **Por qué esta opción y no otra:** "System-Wide" deja el SDK disponible en cualquier terminal del sistema (no solo dentro de VS Code) y lo agrega automáticamente al **PATH**.

---

## 4. Verifica que el SDK quedó instalado

1. **Cierra y vuelve a abrir** la terminal integrada de VS Code (`View → Terminal`), para que reconozca el PATH actualizado.
2. Ejecuta:

   dotnet --list-sdks

   Deberías ver una línea con la versión instalada, por ejemplo:

   9.0.305 [C:\Program Files\dotnet\sdk]

3. Ejecuta también:

   dotnet --version

   Debe mostrar el número de versión sin errores, por ejemplo:

   9.0.305

> ✅ **Si ambos comandos muestran una versión, el SDK de .NET quedó correctamente instalado.**

---

## Resumen de la ruta

| Paso | Acción |
|------|--------|
| 1 | Instalar Visual Studio Code |
| 2 | Instalar la extensión **C# Dev Kit** (instala C# extension y .NET Install Tool como dependencias) |
| 3 | Desde la paleta de comandos (`Ctrl+Shift+P`), ejecutar **".NET Install Tool: Install the .NET SDK System-Wide"** |
| 4 | Verificar con `dotnet --list-sdks` y `dotnet --version` en la terminal integrada |

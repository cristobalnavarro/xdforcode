# XDForCode — Manual de usuario

> IDE estilo VS Code con integración de agentes de IA para Windows.  
> Desarrollado con FiveWin / Harbour por XDEVFORYOU SOLUTIONS.

---

## Tabla de contenidos

1. [¿Qué es XDForCode?](#1-qué-es-xdforcode)
2. [La interfaz de un vistazo](#2-la-interfaz-de-un-vistazo)
3. [Primeros pasos](#3-primeros-pasos)
4. [Editores — Scintilla y Monaco](#4-editores--scintilla-y-monaco)
5. [Agentes de IA — instalación recomendada](#5-agentes-de-ia--instalación-recomendada)
6. [Activar un agente en la aplicación](#6-activar-un-agente-en-la-aplicación)
7. [Configurar proveedor y modelo](#7-configurar-proveedor-y-modelo)
8. [Usar el panel de chat (sidebar derecho)](#8-usar-el-panel-de-chat-sidebar-derecho)
9. [Skills — fragmentos y plantillas de contexto](#9-skills--fragmentos-y-plantillas-de-contexto)
10. [Sistema Kanban — múltiples agentes en paralelo](#10-sistema-kanban--múltiples-agentes-en-paralelo)
11. [Acceso remoto desde el navegador](#11-acceso-remoto-desde-el-navegador)
12. [Explorador de archivos](#12-explorador-de-archivos)
13. [Terminales integradas](#13-terminales-integradas)
14. [Preguntas frecuentes](#14-preguntas-frecuentes)

---

## 1. ¿Qué es XDForCode?

XDForCode es un entorno de desarrollo integrado (IDE) para Windows con apariencia y funcionamiento similar a VS Code. Está diseñado especialmente para desarrolladores **Harbour / FiveWin**, aunque puede editar cualquier tipo de fichero.

Su característica principal es la **integración nativa con agentes de IA**: puedes conversar directamente con Claude, Gemini, OpenCode, Ollama y otros desde dentro del propio IDE, sin salir de la aplicación, con acceso al código que estás editando.

**Características principales:**

- Editor de código Monaco (el mismo que usa VS Code) con soporte Harbour/FiveWin
- Panel de chat con agentes de IA en el sidebar derecho
- Múltiples terminales integradas (Git, SSH, consola del sistema)
- Kanban para lanzar y coordinar varios agentes IA en paralelo
- Servidor web embebido para acceso remoto desde el navegador
- Sistema de Skills: fragmentos de contexto o instrucciones reutilizables
- Explorador de archivos con árbol de directorios
- Compatible con herramientas MCP (Model Context Protocol)

---

## 2. La interfaz de un vistazo

```
┌──────────┬──────────────┬────────────────────────────┬────────────────────────┐
│  Barra   │  Explorador  │                            │   Panel de agente IA   │
│  lateral │  de archivos │      Editor de código      │                        │
│  de      │              │      (Monaco Editor)       │  ┌──────────────────┐  │
│  iconos  │              │                            │  │  Respuesta del   │  │
│          │              ├────────────────────────────┤  │    agente        │  │
│          │              │  Consolas / Terminales     │  ├──────────────────┤  │
│          │              │  (Git, SSH, IA, Build...)  │  │  Tu mensaje      │  │
└──────────┴──────────────┴────────────────────────────┴──┴──────────────────┘──┘
```

| Zona | Función |
|---|---|
| **Barra lateral de iconos** | Acceso a explorador, servidor web, Kanban y configuración |
| **Explorador de archivos** | Árbol de directorios; clic en un fichero lo abre en el editor |
| **Editor Monaco** | Edición de código con resaltado de sintaxis |
| **Consolas inferiores** | Pestañas Results, GIT, SSH, Sistema, Terminal IA |
| **Panel derecho** | Chat con el agente IA activo |

---

## 3. Primeros pasos

Al iniciar XDForCode verás el editor vacío. Los pasos básicos para empezar:

1. **Abrir una carpeta de trabajo**: desde el menú o haciendo clic en el icono de explorador en la barra lateral. La carpeta seleccionada se muestra en el árbol de archivos.
2. **Abrir un fichero**: haz clic sobre él en el árbol. Se abre en el editor Monaco.
3. **Seleccionar un agente de IA**: en el panel derecho elige el agente que quieres usar (Claude, Gemini, Ollama, etc.) y escribe tu consulta.
4. **Activar el servidor web** (opcional): si quieres acceder desde el navegador o usar acceso remoto, pulsa el icono del servidor en la barra lateral.

---

## 4. Editores — Scintilla y Monaco

XDForCode dispone de dos motores de edición que se usan según el tipo de fichero:

### Monaco Editor

El mismo motor que utiliza VS Code internamente. Se usa para la mayoría de los ficheros de código y texto. Ofrece resaltado de sintaxis moderno, autocompletado inteligente y vista previa de ficheros web (HTML, CSS, JS).

Tipos de fichero habituales en Monaco: `.prg`, `.ch`, `.prw`, `.js`, `.html`, `.css`, `.json`, `.md`, `.ini`, `.txt`, ...

### Scintilla

Editor nativo de Windows, más ligero. Se usa para ficheros específicos que se abren en sus propias pestañas dentro del IDE, con resaltado optimizado para Harbour y FiveWin.

### Comportamiento al abrir un fichero

- **Ficheros de texto y código** → se abren en el editor (Monaco o Scintilla según configuración y tipo).
- **Ficheros binarios** (`.exe`, `.dll`, imágenes...) → se abren con la aplicación asociada de Windows.
- **Ficheros HTML** → puedes elegir abrirlos en el editor de código o en el panel de vista previa del sidebar izquierdo.

Cada fichero abierto ocupa su propia **pestaña** en la zona de edición. Puedes tener varios ficheros abiertos a la vez y navegar entre ellos.

---

## 5. Agentes de IA — instalación recomendada

XDForCode funciona con agentes externos que se instalan en tu sistema. La aplicación los detecta y los invoca automáticamente.

### Agentes recomendados

#### Claude Code
El agente de Anthropic. Muy potente para razonamiento y edición de código.

```
npm install -g @anthropic-ai/claude-code
```

Después inicia sesión:
```
claude
```

---

#### OpenClaude
Fork de Claude Code con funcionalidades ampliadas.

```
npm install -g openclaude
```

---

#### OpenCode
Agente de código abierto compatible con múltiples proveedores (Anthropic, OpenAI, Gemini, etc.).

```
npm install -g opencode
```

Configuración inicial:
```
opencode auth
```

---

#### MIMO
Fork de OpenCode. Se usa exactamente igual que OpenCode.

```
npm install -g mimo
```

---

#### Gemini CLI
El agente de Google. Soporta modelos Gemini y tiene contexto muy grande (1M tokens).

```
npm install -g @google/gemini-cli
```

Autenticación:
```
gemini auth
```

---

#### Ollama
Agente para modelos **locales** (sin conexión a internet, sin coste). Ejecuta los modelos en tu propio ordenador.

Descarga desde: **https://ollama.com**

Instalar un modelo (ejemplos):
```
ollama pull llama3.2
ollama pull qwen2.5-coder
ollama pull deepseek-r1
```

> Ollama es la única opción que **no requiere cuenta ni API key** y funciona completamente sin internet.

---

### ¿Cuál elegir?

| Agente | Requiere internet | Coste | Ideal para |
|---|---|---|---|
| Claude Code | Sí | Según plan Anthropic | Razonamiento, código complejo |
| OpenClaude | Sí | Según plan Anthropic | Igual que Claude Code |
| OpenCode | Sí | Según proveedor | Flexibilidad de proveedor |
| MIMO | Sí | Según proveedor | Igual que OpenCode |
| Gemini CLI | Sí | Según plan Google | Contexto grande, código |
| Ollama | **No** | **Gratuito** | Privacidad, uso sin internet |

---

## 5. Activar un agente en la aplicación

Una vez instalados los agentes, actívalos dentro de XDForCode:

1. Haz clic en el icono de **configuración del agente** en la barra lateral derecha, o usa el menú desplegable en la parte superior del panel de chat.
2. Selecciona el agente de la lista (OpenCode, MIMO, Claude CLI, OpenClaude, Gemini CLI, Ollama...).
3. La pestaña del panel de chat cambia al agente seleccionado y queda listo para recibir mensajes.

Puedes tener **varios agentes activos simultáneamente** usando el sistema Kanban (ver sección 9).

---

## 6. Configurar proveedor y modelo

Cada agente permite seleccionar el proveedor (empresa que ofrece el modelo) y el modelo concreto a usar.

### OpenCode / MIMO

Dentro de XDForCode, en el panel del agente:

- **Proveedor**: Anthropic, OpenAI, Google, Mistral, etc.
- **Modelo**: `claude-sonnet-4-5`, `gpt-4o`, `gemini-2.0-flash`, etc.

También puedes configurarlo globalmente con:
```
opencode auth       # iniciar sesión con el proveedor
```

### Claude Code / OpenClaude

El modelo se selecciona desde el panel de chat de XDForCode. La aplicación pasa `--model <nombre>` al invocar el agente. Ejemplos de modelos:

- `claude-opus-4-5` (más potente)
- `claude-sonnet-4-5` (equilibrado, recomendado)
- `claude-haiku-4-5` (más rápido y económico)

### Gemini CLI

Modelos disponibles:
- `gemini-2.0-flash` (rápido, recomendado)
- `gemini-2.5-pro` (más potente)

### Ollama

El modelo se elige en el selector de XDForCode. Solo aparecen los modelos que **ya tienes descargados** en tu sistema. Para ver los instalados:
```
ollama list
```

> Si cambias el modelo, el cambio se aplica en la siguiente consulta.

---

## 7. Usar el panel de chat (sidebar derecho)

El panel de chat es el corazón de la integración con IA.

### Enviar un mensaje

Escribe tu pregunta o instrucción en el cuadro inferior y pulsa **Enviar** (o `Ctrl+Enter`).

### Contexto automático

El agente recibe automáticamente el **contenido del fichero que estás editando** como contexto. No necesitas copiar y pegar el código.

### Comandos de barra (`/`)

Escribe `/` en el cuadro de chat y aparecerá automáticamente la lista de todos los comandos disponibles. **El primer comando que debes probar cuando empieces es `/help`**: te mostrará una explicación de todos los comandos y opciones del chat.

Algunos de los comandos más habituales:

| Comando | Acción |
|---|---|
| `/help` | Muestra la ayuda completa del chat y los comandos disponibles |
| `/mode` | Cambiar el agente o modo activo |
| `/ollama` | Listar y cambiar modelos de Ollama |
| `/clear` | Limpiar el historial del chat |
| `/skill` | Insertar una skill en el mensaje |

### Cancelar una respuesta en curso

Mientras el agente responde aparece el botón **Cancelar**. Púlsalo para interrumpir.

### Historial

El historial de la conversación se mantiene durante la sesión. Cada mensaje nuevo se envía junto con el contexto de los mensajes anteriores.

### Preguntar sobre el código abierto en el editor

El agente tiene acceso al contenido del **fichero activo** (el que está en primer plano en el editor). Puedes preguntarle directamente sobre él sin copiar nada:

> _"Explícame qué hace esta función"_
> _"¿Hay algún posible error en este código?"_
> _"Resume qué hace este fichero"_

Si tienes varias pestañas abiertas y quieres preguntar sobre una concreta, menciona el nombre del fichero explícitamente para evitar ambigüedades:

> _"Explícame qué hace el código del fichero `fev_server.prg` abierto en el editor"_
> _"¿Qué función gestiona el login en `chat_login.prg`?"_

Para preguntar sobre un fichero que **no está abierto en el editor**, indícalo igualmente de forma explícita con su nombre o ruta:

> _"Analiza el fichero `fevscode.prg` y dime cómo está estructurado"_
> _"¿Qué hace la función `AdjustLayout` en `fev_layout.prg`?"_

### Pedir modificaciones de código

El agente puede modificar el fichero activo directamente. Algunos ejemplos habituales:

> _"Añade validación de que el campo usuario no esté vacío antes de hacer el login"_
> _"Refactoriza la función `XDServerStart` para separar la lógica de login en una función propia"_
> _"Añade al final del fichero una nueva función `GetUserCount` que devuelva el número de usuarios en `xdusers.json`"_
> _"Corrige el bug en la función `remotePoll` para que reintente si la respuesta está vacía"_

---

## 8. Skills — fragmentos y plantillas de contexto

Las **Skills** son fragmentos de texto predefinidos (instrucciones, plantillas, fragmentos de código frecuentes) que puedes insertar en tus mensajes con un solo clic.

### Para qué sirven

- Instrucciones de sistema ("responde siempre en español", "actúa como experto en FiveWin...")
- Plantillas de código que usas con frecuencia
- Contexto del proyecto que quieres enviar al agente sin reescribirlo cada vez

### Cómo usarlas

1. En el cuadro de mensaje escribe `/skill` o usa el botón de Skills en el panel.
2. Aparece la lista de skills disponibles.
3. Selecciona la que quieras: su contenido se inserta en el mensaje.

### Gestionar Skills

Las Skills se guardan en el fichero `xdskills.json` junto a la aplicación. Puedes editarlo directamente con el editor de XDForCode para añadir, modificar o eliminar skills.

---

## 9. Sistema Kanban — múltiples agentes en paralelo

El **Kanban** permite lanzar y coordinar múltiples agentes de IA simultáneamente, cada uno con su propia tarea.

### Abrir el Kanban

Pulsa el icono de **Kanban** en la barra lateral de iconos. Se abre el tablero en el panel central.

### Cómo funciona

1. Crea una **tarea** en el tablero: asígnale un nombre, una descripción y un agente.
2. El agente arranca en su propia pestaña de terminal.
3. El tablero muestra el estado de cada tarea: pendiente, en curso, completada.
4. Puedes ver la conversación de cada agente en su pestaña individual.

### Casos de uso típicos

- Lanzar un agente que refactoriza el código mientras otro escribe los tests.
- Pedir a tres agentes distintos (Claude, Gemini, Ollama) que respondan a la misma pregunta y comparar resultados.
- Dejar tareas largas corriendo en segundo plano mientras trabajas en otra cosa.

---

## 10. Acceso remoto desde el navegador

XDForCode incluye un **servidor web** que permite acceder al chat con el agente desde cualquier navegador de tu red local (o internet, si lo expones).

### Arrancar el servidor web

Pulsa el icono del servidor en la barra lateral de iconos. Cuando está activo, la barra de estado inferior muestra el puerto: `Server :8003`.

### Acceder desde el navegador

Abre en tu navegador:
```
http://localhost:8003
```

Verás la interfaz de chat, idéntica al panel de XDForCode. Las respuestas del agente llegan en tiempo real al navegador.

### Acceso multiusuario con contraseña

Si quieres proteger el acceso (por ejemplo, para compartir con tu equipo), crea el fichero `xdusers.json` junto al ejecutable con este formato:

```json
[
  { "user": "cristobal", "pass": "<SHA-256 de la contraseña>" }
]
```

Para calcular el hash SHA-256 de una contraseña puedes usar cualquier herramienta online de confianza o la propia terminal.

Con `xdusers.json` presente, al acceder desde el navegador aparece una pantalla de inicio de sesión.

> Sin `xdusers.json`, el acceso es libre (modo local, sin contraseña).

---

## 11. Menú de la aplicación — opciones de configuración

El menú principal de XDForCode cubre la **gran mayoría de opciones de configuración** de la aplicación. Se recomienda revisarlo detenidamente antes de empezar a trabajar, ya que contiene ajustes que no siempre son evidentes desde la interfaz visual.

Entre las opciones que encontrarás en el menú:

- **Configuración del agente IA**: selección del agente activo, modo de ejecución, proveedor y modelo.
- **Configuración del servidor web**: puerto, carpeta de documentos y acceso remoto.
- **Rutas de compilación**: ruta de Harbour, FiveWin y compilador C para el sistema de build.
- **Apariencia y layout**: visibilidad de paneles laterales, consola y barra de estado.
- **Opciones del editor**: fuente, tamaño, tema de color y autoguardado.
- **Herramientas MCP**: gestión de las tools MCP disponibles para los agentes.
- **Terminal y aplicaciones externas**: configuración de las pestañas de terminal adicionales.

> Dedica unos minutos a explorar cada sección del menú: muchas funcionalidades de XDForCode solo son accesibles desde ahí.

---

## 12. Explorador de archivos

El explorador ocupa el panel izquierdo. Muestra el árbol de directorios de la carpeta de trabajo actual.

- **Clic simple**: abre el fichero en el editor.
- **Ficheros binarios** (imágenes, ejecutables): se abren con la aplicación por defecto de Windows.
- **Ficheros HTML**: puedes elegir abrirlos en el editor o en el panel de vista previa.

El explorador se **actualiza automáticamente** cuando se crean o modifican ficheros desde los agentes IA.

---

## 13. Terminales integradas

En la parte inferior encontrarás varias pestañas de terminal. Las pestañas disponibles por defecto son:

| Pestaña | Para qué sirve |
|---|---|
| **Results** | Salida de compilación y build |
| **GIT** | Terminal Git en la carpeta de trabajo |
| **SSH** | Conexión SSH a servidores remotos |
| **System Console** | Consola de Windows estándar |
| **Console CLI** | Terminal donde corre el agente IA (opencode serve, etc.) |

Todas son terminales interactivas completas con soporte de color.

> **Las pestañas de terminal y los agentes disponibles en el panel inferior son configurables desde el menú.** Puedes añadir, quitar o modificar tanto los terminales como los agentes que aparecen en ese panel según tus necesidades.

---

## 14. Preguntas frecuentes

**¿Necesito instalar todos los agentes?**  
No. Con instalar uno ya puedes trabajar. Si no tienes claro cuál elegir, empieza con **Ollama** (gratuito, sin internet) o **Claude Code**.

**¿El agente tiene acceso a mis ficheros?**  
El agente recibe como contexto el contenido del fichero que tienes abierto en el editor. No explora tus directorios automáticamente salvo que le des permiso explícito o uses herramientas MCP.

**¿Puedo usar varios agentes a la vez?**  
Sí, mediante el Kanban puedes tener varios agentes activos en paralelo, cada uno en su propia pestaña.

**¿El chat queda guardado?**  
El historial de la sesión actual se mantiene mientras la aplicación está abierta. Al cerrar la aplicación, el historial no se persiste por defecto.

**¿Puedo usar XDForCode sin conexión a internet?**  
Sí, siempre que uses **Ollama** como agente. El resto de agentes requieren conexión para conectarse a sus APIs en la nube.

**¿Qué ocurre si el agente tarda mucho?**  
Puedes cancelar la respuesta en cualquier momento con el botón **Cancelar** del panel de chat. El agente se detiene y puedes volver a escribir.

**¿Qué ocurre si el mode /inference no funciona?**  
Debes editar el ficheron **xdinference.json** y completar las apikeys de cada provider.

---

## 15. Descarga el repositorio y ejecuta xdforcode.exe, no es un instalador, es la propia aplicacion
**Al abrir el .exe, haz clic en 'Más información' → Ejecutar de todas formas**

*XDForCode — XDEVFORYOU SOLUTIONS · 2025–2026*

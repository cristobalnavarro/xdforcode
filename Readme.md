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
6. [Modos de ejecución: Run, ACP e Inference](#6-modos-de-ejecución-run-acp-e-inference)
   - [Auto-fallback de provider](#auto-fallback-de-provider)
7. [Activar y configurar un agente](#7-activar-y-configurar-un-agente)
8. [Usar el panel de chat (sidebar derecho)](#8-usar-el-panel-de-chat-sidebar-derecho)
9. [Skills — tipos y uso avanzado](#9-skills--tipos-y-uso-avanzado)
10. [Preview HTML en vivo](#10-preview-html-en-vivo)
11. [Sistema Kanban — múltiples agentes en paralelo](#11-sistema-kanban--múltiples-agentes-en-paralelo)
12. [Sistema de Build y Toolchains](#12-sistema-de-build-y-toolchains)
13. [Proyectos (.xdprj)](#13-proyectos-xdprj)
14. [Acceso remoto desde el navegador](#14-acceso-remoto-desde-el-navegador)
15. [Gestión de usuarios del chat remoto](#15-gestión-de-usuarios-del-chat-remoto)
16. [Explorador de archivos](#16-explorador-de-archivos)
17. [Terminales y pestañas configurables](#17-terminales-y-pestanas-configurables)
18. [Integración con WhatsApp](#18-integración-con-whatsapp)
19. [Menú de la aplicación](#19-menú-de-la-aplicación)
20. [Preguntas frecuentes](#20-preguntas-frecuentes)
21. [Indexación de Código y Documentos (CodeGraph)](#21-indexación-de-código-y-documentos-codegraph)
22. [Motor de Reportes — show_report](#22-motor-de-reportes--show_report)
23. [Curso de IA para Harbour/FiveWin](#23-curso-de-ia-para-harbourfivewin) *(próximamente)*
24. [Herramientas MCP para MySQL/MariaDB](#24-herramientas-mcp-para-mysqlmariadb)
25. [Interfaces GUI de configuración](#25-interfaces-gui-de-configuración)
26. [Dashboard — Panel de Estado en Tiempo Real](#26-dashboard--panel-de-estado-en-tiempo-real)
27. [API REST Local Integrada](#27-api-rest-local-integrada)

---

## 1. ¿Qué es XDForCode?

XDForCode es un entorno de desarrollo integrado (IDE) para Windows con apariencia y funcionamiento similar a VS Code. Está diseñado especialmente para desarrolladores **Harbour / FiveWin**, aunque puede editar cualquier tipo de fichero.

Su característica principal es la **integración nativa con agentes de IA**: puedes conversar directamente con Claude, Gemini, OpenCode, Ollama y otros desde dentro del propio IDE, sin salir de la aplicación, con acceso al código que estás editando.

**Características principales:**

- Editor de código Monaco (el mismo que usa VS Code) con soporte Harbour/FiveWin
- **Dashboard** — panel de estado en tiempo real: agentes activos, Kanban, servidor, MCP tools, skills, proveedores
- **Sistema de perfiles** (`.xdprofile`) — guarda y carga configuración de agente + carpeta de trabajo en un clic
- Panel de chat con agentes de IA en el sidebar derecho
- Adjuntar ficheros e imágenes al prompt del chat (soporte de visión en Claude 3+, Gemini 1.5+)
- **`/loop`** — bucle autónomo: el agente itera sobre un objetivo hasta que lo resuelve
- **Motor de reportes** — los agentes pueden mostrar tablas, diagramas Mermaid, diffs de código y botones de acción interactivos usando la tool MCP `show_report`
- Múltiples terminales integradas (Git, SSH, consola del sistema)
- Kanban para lanzar y coordinar varios agentes IA en paralelo
- **Kanban auto-gestionado**: los propios agentes pueden crear y encolar tareas via tools MCP
- Sistema de build completo con toolchains y gestión de proyectos
- Servidor web embebido para acceso remoto desde el navegador
- Skills reutilizables con múltiples tipos (acciones, contexto, plantillas, reglas)
- Preview HTML en vivo en el sidebar izquierdo
- CodeGraph indexa código, documentos, PDF, ficheros Office e imágenes via OCR
- Integración con WhatsApp Web
- Compatible con herramientas MCP (Model Context Protocol)

---

## 2. La interfaz de un vistazo

```
┌──────────┬──────────────┬────────────────────────────┬────────────────────────┐
│  Barra   │  Explorador  │                            │   Panel de agente IA   │
│  lateral │  de archivos │      Editor de código      │                        │
│  de      │              │      (Monaco / Scintilla)  │  ┌──────────────────┐  │
│  iconos  │              │                            │  │  Respuesta del   │  │
│          │              ├────────────────────────────┤  │    agente        │  │
│          │              │  Consolas / Terminales     │  ├──────────────────┤  │
│          │              │  (Git, SSH, IA, Build...)  │  │  Tu mensaje      │  │
└──────────┴──────────────┴────────────────────────────┴──┴──────────────────┘──┘
```

| Zona | Función |
|---|---|
| **Barra lateral de iconos** | Acceso a explorador, servidor web, Kanban, preview HTML y configuración |
| **Explorador de archivos** | Árbol de directorios; clic en un fichero lo abre en el editor |
| **Editor de código** | Edición con Monaco o Scintilla según el tipo de fichero |
| **Consolas inferiores** | Pestañas Results, GIT, SSH, Sistema, Terminal IA, WhatsApp |
| **Panel derecho** | Chat con el agente IA activo |

---

## 3. Primeros pasos

Al iniciar XDForCode verás el editor vacío. Los pasos básicos para empezar:

1. **Abrir una carpeta de trabajo**: desde el menú o haciendo clic en el icono de explorador en la barra lateral. La carpeta seleccionada se muestra en el árbol de archivos.
2. **Abrir un fichero**: haz clic sobre él en el árbol. Se abre en el editor Monaco o Scintilla.
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

### Pantalla de inicio — botones de acción

Al abrir XDForCode sin fichero activo se muestra la pantalla de bienvenida (XDEdit.html). Cuatro botones en la esquina superior derecha del editor permiten acceder a las funciones principales sin usar el menú:

| Botón | Acción |
|---|---|
| **DASHBOARD** | Abre el panel de estado del IDE (ver §24) |
| **TASK MANAGER** | Abre el tablero Kanban directamente |
| **LOAD PROFILE** | Carga un perfil de configuración (`.xdprofile`) |
| **SAVE PROFILE** | Guarda el perfil actual en `profiles\` |

El triángulo **▲** en la barra de estado inferior recarga la configuración desde `XDForCodeUI.ini` sin necesidad de reiniciar la aplicación.

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

#### Pi (Coding Agent)
Agente de coding con protocolo RPC propio sobre stdin/stdout. Soporta herramientas interactivas (confirm, select) y puede escribir directamente en el editor del IDE (`set_editor_text`). El modelo y configuración se definen en el fichero `AGENTS.md` de tu proyecto.

```
npm install -g @earendil/pi
```

Comando de activación en XDForCode: `/pi`  
Ejecutable: `pi` (ruta o nombre en PATH)  
Protocolo: JSONL (`pi --mode rpc`)

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
| Pi | Depende del modelo | Según proveedor | Coding agent con RPC, herramientas interactivas |
| Ollama | **No** | **Gratuito** | Privacidad, uso sin internet |

---

## 6. Modos de ejecución: Run, ACP e Inference

Además de los agentes CLI tradicionales, XDForCode dispone de tres modos de ejecución que determinan cómo se comunica la aplicación con el agente de IA.

### Modo Run

Ejecuta el agente como proceso de línea de comandos en una pestaña de terminal. El agente recibe el prompt como texto y devuelve la respuesta por stdout. Es el modo más sencillo.

**Agentes que usan este modo:** OpenCode (`opencode_run`), MIMO (`mimo_run`).

### Modo ACP (Agent Communication Protocol)

Establece una comunicación bidireccional vía pipes o HTTP entre XDForCode y el agente. Permite recibir respuestas progresivas (streaming), usar herramientas MCP y mantener memoria de la conversación.

**Agentes que usan este modo:** OpenCode (`opencode_acp`), MIMO (`mimo_acp`), Gemini (`gemini_acp`), OpenClaude (`openclaude_acp`).

**Submodos de sesión ACP:**
- **Modo 1 (Memoria)**: mantiene una sesión persistente con memoria de la conversación.
- **Modo 2 (Per-request)**: cada mensaje crea una nueva petición con el modelo seleccionado.
- **Modo 3 (Modelo por defecto)**: usa el modelo por defecto configurado en opencode.

> **Compatibilidad de sesiones entre agentes:** cada agente ACP (opencode, mimo, gemini) usa su propio formato interno de sesión. Si cambias de agente mientras hay una sesión activa, el nuevo agente puede rechazar la sesión anterior (`session/load` falla). XDForCode detecta este error automáticamente, descarta la sesión antigua y crea una nueva sin mostrar ningún aviso al usuario. La conversación continúa con normalidad.

### Modo Pi RPC

Protocolo JSONL bidireccional sobre stdin/stdout propio de Pi. XDForCode lanza `pi --mode rpc` como proceso y se comunica con él enviando y recibiendo objetos JSON (un objeto por línea).

**Agentes que usan este modo:** Pi (`pi_rpc`).

**Características exclusivas del modo Pi RPC:**
- **Streaming nativo**: los tokens llegan en tiempo real sin polling.
- **confirm / select**: Pi puede solicitar confirmación o selección al usuario; XDForCode muestra un diálogo y Pi bloquea hasta recibir la respuesta.
- **input / editor**: Pi puede pedir texto al usuario; XDForCode muestra un formulario inline en el chat (campo de una línea para `input`, multiline para `editor`) y espera la respuesta antes de continuar.
- **set_editor_text**: Pi escribe texto directamente en el editor activo del IDE (Scintilla o Monaco).
- **Sin gestión de modelo en XDForCode**: el modelo se configura en el fichero `AGENTS.md` del proyecto o globalmente en la instalación de Pi.

**Activación:**
```
/pi
/exe <ruta-a-pi>    (si pi no está en el PATH)
```

**Comandos exclusivos del modo Pi:**

| Comando | Acción |
|---|---|
| `/steer <texto>` | Inyecta una instrucción en mitad de una respuesta sin interrumpirla |
| Botón cancelar | Envía `abort` al proceso Pi (cancela el turno sin matar el proceso) |

---

### Modo Inference

Conecta directamente con APIs OpenAI-compatible (NVIDIA, GROQ, OpenRouter, Together, HuggingFace, Ollama) sin necesidad de instalar agentes externos. Usa hbcurl nativo de Harbour con streaming SSE.

**Configuración:** Edita el fichero `xdinference.json` junto al ejecutable para añadir providers y modelos. Cada provider necesita su endpoint y API key.

**Providers preconfigurados:**
- **NVIDIA NIM** — Nemotron, Llama, DeepSeek, Qwen, Gemma, MiniMax, GLM
- **GROQ** — Llama, DeepSeek, Gemma, Mixtral (latencia muy baja)
- **OpenRouter** — acceso a Claude, GPT-4o, Gemini y cientos de modelos
- **Together AI** — Llama, DeepSeek, Qwen, Mistral
- **HuggingFace** — amplia variedad de modelos open source (3 API keys configuradas)
- **OLLAMA** — modelos locales + modelos cloud (requiere `ollama signin`)
- **Cloudflare AI** / **Cloudflare Gateway** — Workers AI y gateway proxy

**Autodiscovery de modelos:** los providers con `"autodiscover": true` en el JSON consultan automáticamente `/v1/models` del provider al ejecutar `/models`, mostrando la lista real de modelos disponibles en tu cuenta en ese momento. Los modelos que no soportan tool calling (embed, rerank, OCR, TTS) se filtran automáticamente.

**Modelos Ollama `:cloud`:** los modelos con sufijo `:cloud` (ej. `gemma4:31b:cloud`) se ejecutan en los servidores de Ollama. Requieren haber hecho `ollama signin` previamente. XDForCode muestra un aviso la primera vez que seleccionas uno en la sesión.

**Herramientas MCP sin agente externo:** el modo Inference incluye un bucle de tool calling nativo. Cuando el toggle **Agente externo (ACP) [ OFF ]** está desactivado en el menú TOOLS, XDForCode envía las herramientas MCP directamente al LLM y ejecuta el ciclo tool_use → resultado → siguiente vuelta internamente, sin necesidad de tener opencode o mimo instalados. Cualquier provider inference que soporte tool calling (GROQ, OpenRouter, NVIDIA, ollama con modelos compatibles) puede ejecutar herramientas MCP en modo completamente autónomo.

> El modo Inference es ideal para usar modelos potentes sin instalar agentes CLI, solo necesitas una API key.

---

### Modo Puter

Conecta con la plataforma **Puter.com** — más de 549 modelos de IA (Claude, Gemini, GPT-4o, Llama, Mistral y cientos más) disponibles gratuitamente sin API key propia, usando solo tu cuenta Puter.

**Características:**
- **Autenticación JWT** automática: XDForCode solicita el token al servidor Puter y lo renueva en cada sesión sin intervención manual.
- **Streaming NDJSON**: los tokens llegan en tiempo real igual que en otros modos de streaming.
- **Autodiscovery de modelos**: al ejecutar `/models` se consulta `/drivers/list` de Puter y se filtra la lista de modelos del driver `puter-chat-completion`.
- **Tools MCP via inyección de contexto**: el driver de Puter no admite function calling nativo. XDForCode pre-ejecuta las tools MCP relevantes (fecha/hora, IP pública, temperatura, versión de Harbour) antes de cada mensaje e inyecta los resultados reales en el system message, evitando que el modelo los invente.

**Configuración:** Crea una cuenta gratuita en **puter.com** e inicia sesión una vez desde el diálogo **TOOLS → Configurar Puter...**. XDForCode guarda el token JWT en `XDForCodeUI.ini [PUTER] token` y lo renueva automáticamente.

**Activación:**
```
/puter
```

> El modo Puter es ideal para acceder a modelos premium sin coste adicional si ya tienes cuenta Puter. La limitación principal es que no soporta function calling nativo; las tools MCP se inyectan como contexto real antes del mensaje.

---

### Auto-fallback de provider

Cuando un provider devuelve un error de cuota o límite de tasa (429, `rate_limit`, `quota_exceeded`, `insufficient_credits`…), XDForCode cambia automáticamente al siguiente provider de la cadena y reintenta la misma consulta sin que tengas que hacer nada.

**Cadena de degradación por familia de modo:**

```
opencode* / mimo* / gemini* / claude*  →  inference  →  puter  →  ollama (local)
inference (cualquier provider)         →  puter  →  ollama
puter                                  →  inference  →  ollama
ollama                                 →  (último recurso, sin fallback)
```

**Comportamiento:**
- El error original aparece en el chat (el usuario queda informado).
- Inmediatamente después aparece `⚡ Límite alcanzado — cambiando a **X**...` y la respuesta del nuevo provider.
- El cambio de provider **persiste** para el siguiente mensaje (sin restaurar el original).
- Para modos HTTP directos (`inference`, `puter`) el reintento es inmediato en el mismo hilo. Para modos de proceso (`opencode_*`, `mimo_*`, `gemini_*`, `claude_*`) el nuevo provider se activa antes de relanzar el proceso.
- Máximo 1 reintento por turno (configurable en `xdfallback.json` → `max_retries`).

**Configuración** (`xdfallback.json` junto al ejecutable):
- `enabled` — activa o desactiva globalmente el fallback.
- `triggers.http` — lista de palabras clave que identifican errores de cuota en la respuesta.
- `rules[]` — cadena de fallbacks por `(mode, provider)`: cada regla tiene un `match` y un array `fallbacks` con entradas `{ mode, provider, model, label }`.
- Regla catch-all con `"provider": "*"` que se aplica a cualquier mode/provider no cubierto explícitamente.

**Comandos:**

```
/fallback          → muestra estado actual y cadena de degradación
/fallback on       → activa el fallback automático (por defecto)
/fallback off      → desactiva; los errores de cuota se muestran sin reintento
```

El estado actual aparece siempre en la tabla de `/mode` en la fila `fallback`.

---

## 7. Activar y configurar un agente

### Seleccionar el agente activo

1. Haz clic en el **selector de agente** en la parte superior del panel de chat (sidebar derecho).
2. Selecciona el agente de la lista (OpenCode, MIMO, Claude CLI, OpenClaude, Gemini CLI, Ollama, Inference...).
3. El panel de chat cambia al agente seleccionado y queda listo para recibir mensajes.

Puedes tener **varios agentes activos simultáneamente** usando el sistema Kanban (ver sección 11).

### Configurar proveedor y modelo

Cada agente permite seleccionar el proveedor (empresa que ofrece el modelo) y el modelo concreto a usar. El cambio se aplica en la siguiente consulta.

#### OpenCode / MIMO

Dentro de XDForCode, en el panel del agente:

- **Proveedor**: Anthropic, OpenAI, Google, Mistral, etc.
- **Modelo**: `claude-sonnet-4-5`, `gpt-4o`, `gemini-2.0-flash`, etc.

#### Claude Code / OpenClaude

El modelo se selecciona desde el panel de chat. La aplicación pasa `--model <nombre>` al invocar el agente.

- `claude-opus-4-5` (más potente)
- `claude-sonnet-4-5` (equilibrado, recomendado)
- `claude-haiku-4-5` (más rápido y económico)

#### Gemini CLI

- `gemini-2.0-flash` (rápido, recomendado)
- `gemini-2.5-pro` (más potente)

#### Ollama

El modelo se elige en el selector. Solo aparecen los modelos que **ya tienes descargados** en tu sistema. Para ver los instalados:
```
ollama list
```

#### Modo Inference

Selecciona el provider (NVIDIA, GROQ, OpenRouter, Together, HuggingFace) y el modelo de la lista. Los modelos marcados con **[tools]** soportan llamadas a herramientas MCP.

### Sistema de perfiles (`.xdprofile`)

Un perfil guarda toda la configuración del agente activo y la carpeta de trabajo en un único fichero JSON, de forma que puedes cambiar de proyecto o de agente en un solo clic.

**Qué se guarda en un perfil:**

| Campo | Contenido |
|---|---|
| `ai.mode` | Modo de ejecución (`opencode_acp`, `claude_cli`, `ollama`, `inference`…) |
| `ai.model` | Modelo activo |
| `ai.exe` | Ruta al ejecutable del agente |
| `ai.provider` | Proveedor (Anthropic, NVIDIA, GROQ…) |
| `ai.stream` | Streaming activado/desactivado |
| `work_folder` | Carpeta de trabajo del proyecto |

**Guardar un perfil:** botón **SAVE PROFILE** en la pantalla de inicio. El fichero se guarda en `profiles\<modo>_<fecha>.xdprofile`.

**Cargar un perfil:** botón **LOAD PROFILE** → selecciona el fichero `.xdprofile`. Al cargar un perfil con `mode = "inference"` los providers de inference se recargan automáticamente.

### Parámetros avanzados del agente

| Parámetro | Descripción |
|---|---|
| **AcpMode** | Modo de sesión ACP (1=memoria, 2=per-request, 3=por defecto) |
| **Stream** | Streaming incremental de respuestas (activado por defecto) |
| **Tools Filter** | Filtrado de herramientas MCP (blacklist/whitelist) |
| **Auto-approve** | Aprobación automática de comandos peligrosos (solo ACP) |

---

## 8. Usar el panel de chat (sidebar derecho)

El panel de chat es el corazón de la integración con IA.

### Enviar un mensaje

Escribe tu pregunta o instrucción en el cuadro inferior y pulsa **Enviar** (o `Ctrl+Enter`).

### Contexto automático

El agente recibe automáticamente el **contenido del fichero que estás editando** como contexto. No necesitas copiar y pegar el código.

### Comandos de barra (`/`)

Escribe `/` en el cuadro de chat y aparecerá automáticamente la lista de todos los comandos disponibles. **El primer comando que debes probar cuando empieces es `/help`**: te mostrará una explicación de todos los comandos y opciones del chat.

#### Estado y configuración general

| Comando | Argumentos | Acción |
|---|---|---|
| `/` | — | Mostrar configuración actual (modo, modelo, endpoint, tools…) |
| `/help` | — | Mostrar ayuda completa del chat |
| `/mode` | — | Mostrar modo y agente activo |
| `/savemode` | — | Guardar la configuración de modo actual |
| `/restoremode` | — | Restaurar la configuración guardada (guarda la actual antes) |

#### Selección de agente / modo

| Comando | Argumentos | Acción |
|---|---|---|
| `/opencode-acp` | — | Modo OpenCode ACP (streaming + herramientas) |
| `/mimo-acp` | — | Modo MIMO ACP (streaming + herramientas) |
| `/gemini-acp` | — | Modo Gemini ACP |
| `/openclaude-acp` | — | Modo OpenClaude ACP |
| `/opencode` | — | Modo OpenCode headless (run, una sola respuesta) |
| `/mimo` | — | Modo MIMO headless |
| `/claude` | — | Modo Claude Code headless (`-p`) |
| `/openclaude` | — | Modo OpenClaude headless |
| `/gemini` | — | Modo Gemini CLI headless |
| `/pi` | — | Modo Pi RPC (agente coding, JSONL stdin/stdout) |
| `/ollama` | — | Modo Ollama (modelos locales) |
| `/openai` | — | Modo OpenAI compatible (REST directo) |
| `/inference` | — | Modo Inference HTTP directo |
| `/puter` | — | Modo Puter (549+ modelos, sin API key propia) |
| `/fallback` | `on\|off` | Activar/desactivar auto-fallback de provider |

#### Modelo, proveedor y endpoint

| Comando | Argumentos | Acción |
|---|---|---|
| `/model` | `<nombre>` | Cambiar el modelo activo |
| `/models` | — | Elegir modelo desde un desplegable |
| `/provider` | `<nombre>` | Establecer proveedor activo (inference) |
| `/providers` | — | Elegir proveedor desde un desplegable |
| `/endpoint` | `<url>` | Cambiar la URL del endpoint |
| `/key` | `<key>` | Establecer API key |
| `/exe` | `<nombre>` | Nombre o ruta del ejecutable CLI del agente |
| `/acpmode` | `1\|2\|3` | Sesión ACP: 1=memoria compartida, 2=tu modelo, 3=default |
| `/stream` | `on\|off` | Activar/desactivar streaming en agentes headless |

#### Contexto del editor

| Comando | Argumentos | Acción |
|---|---|---|
| `/file` | — | Adjuntar el fichero activo del editor al prompt |
| `/sel` | — | Adjuntar la selección actual del editor al prompt |
| `/nocontext` | — | No adjuntar contexto del editor en este prompt |
| `/attach` | — | Adjuntar fichero externo (imagen o texto, máx. 4) |
| `/detach` | — | Quitar todos los ficheros adjuntos |

#### Skills y herramientas MCP

| Comando | Argumentos | Acción |
|---|---|---|
| `/skills` | `[off <nombre>\|clear]` | Gestionar skills activos (prompt templates persistentes) |
| `/reloadskills` | — | Recargar `xdskills.json` sin reiniciar |
| `/context` | `[clear]` | Ver o limpiar caché de skills de contexto (docs/URLs) |
| `/tools` | — | Gestionar filtro de tools MCP (picker visual) |
| `/mcplist` | — | Listar todas las tools MCP disponibles |
| `/reloadmcp` | — | Recargar la lista de tools MCP sin reiniciar |
| `/showmcpused` | `0\|1` | Mostrar u ocultar las tools MCP usadas en cada respuesta |
| `/showtools` | `0\|1` | Mostrar u ocultar el nombre del tool ejecutado en el chat (`› nombre_tool`) |

#### Bucle autónomo (`/loop`)

| Comando | Argumentos | Acción |
|---|---|---|
| `/loop` | `<objetivo>` | Iniciar bucle autónomo: el agente itera hasta escribir `[LISTO]` |
| `/loop stop` | — | Detener el bucle en curso |
| `/loop max` | `<n>` | Establecer número máximo de iteraciones (por defecto: 20) |
| `/loop status` | — | Mostrar estado del bucle actual |

#### Planes multi-agente

| Comando | Argumentos | Acción |
|---|---|---|
| `/plan` | `<descripción>` | Generar un plan Kanban multi-agente desde lenguaje natural |

#### ACP HTTP (chat remoto desde navegador)

| Comando | Argumentos | Acción |
|---|---|---|
| `/http` | `1\|0` | Activar o desactivar el servidor ACP HTTP (puerto 8003) |
| `/httpport` | `<puerto>` | Cambiar el puerto del servidor ACP HTTP |
| `/httphost` | `<host>` | Cambiar el host del servidor ACP HTTP |
| `/httpstatus` | — | Mostrar la configuración ACP HTTP actual |

#### Historial y sesión

| Comando | Argumentos | Acción |
|---|---|---|
| `/savechat` | — | Guardar historial del chat en fichero con fecha y hora |
| `/restorechat` | — | Restaurar o elegir una sesión anterior del chat |
| `/search` | `<texto>` | Buscar texto en el historial de todas las sesiones guardadas |
| `/diffreview` | `on\|off` | Activar revisión de diff antes de que la IA aplique cambios (solo ACP) |
| `/autoapprove` | `on\|off` | Auto-aprobar comandos del agente sin pedir confirmación |
| `/clear` | — | Limpiar la pantalla (el agente **sigue recordando** el historial) |
| `/reset` / `/new` | — | Nueva sesión: limpia pantalla e historial, olvida memoria ACP |
| `/reload` | — | Recargar la página del chat |
| `/refresh` | — | Recargar la página conservando el historial de prompts |

#### Específicos de agente Pi

| Comando | Argumentos | Acción |
|---|---|---|
| `/steer` | `<texto>` | Pi: inyectar una instrucción en mitad de una respuesta en curso |
| `/cmd` | `<comando>` | Ejecutar un comando de shell desde el chat |

### Información de uso al terminar cada respuesta

Al terminar una respuesta en modo ACP aparece un pie de texto con los datos del turno:

```
opencode_acp · qwen3:32b · tokens: 130↑ 23↓ · total 17710 · cache 17536 · razonamiento 21 · 4.7 t/s
```

- **↑ / ↓** — tokens de entrada y salida del turno
- **total** — tokens acumulados de la sesión
- **cache** — tokens servidos desde caché (no se refacturan)
- **razonamiento** — tokens de *thinking* interno (qwen3, deepseek-r1…); usa `/no_think` al inicio del prompt para suprimirlos
- **t/s** — velocidad de generación (tokens de salida por segundo)

La etiqueta **modo · modelo** de la barra superior se actualiza automáticamente cada vez que cambias de agente o modelo con un comando `/`.

### Cancelar una respuesta en curso

Mientras el agente responde aparece el botón **Cancelar**. Púlsalo para interrumpir.

### Historial y límite de contexto

El historial de la conversación se mantiene durante la sesión. Cada mensaje nuevo se envía junto con el contexto de los mensajes anteriores.

Para evitar que sesiones muy largas superen el límite de tokens del modelo, XDForCode aplica automáticamente un **límite de historial**: solo se envían los últimos N pares de mensajes (por defecto 30). Los mensajes más antiguos se descartan del contexto enviado al modelo, pero siguen visibles en pantalla y persisten en la base de datos.

El límite se configura en `XDForCodeUI.ini`:
```
[AI]
maxhistory = 30    ; 0 = sin límite (envía todo el historial)
```

### Preguntar sobre el código abierto en el editor

El agente tiene acceso al contenido del **fichero activo** (el que está en primer plano en el editor). Puedes preguntarle directamente sobre él sin copiar nada:

> _"Explícame qué hace esta función"_
> _"¿Hay algún posible error en este código?"_
> _"Resume qué hace este fichero"_

Si tienes varias pestañas abiertas y quieres preguntar sobre una concreta, menciona el nombre del fichero explícitamente:

> _"Explícame qué hace el código del fichero `fev_server.prg` abierto en el editor"_
> _"¿Qué función gestiona el login en `chat_login.prg`?"_

### Pedir modificaciones de código

El agente puede modificar el fichero activo directamente:

> _"Añade validación de que el campo usuario no esté vacío antes de hacer el login"_
> _"Refactoriza la función `XDServerStart` para separar la lógica de login en una función propia"_
> _"Añade al final del fichero una nueva función `GetUserCount` que devuelva el número de usuarios en `xdusers.json`"_

### Adjuntar ficheros e imágenes al prompt

Puedes incluir hasta **4 ficheros o imágenes** como adjunto en cualquier mensaje del chat.

#### Botón 📎 (adjuntar fichero)

Al pulsarlo se abre el selector de ficheros. Puedes adjuntar:
- **Ficheros de texto** (`.prg`, `.json`, `.md`, …): su contenido se añade automáticamente al mensaje como bloque de código.
- **Imágenes** (`.png`, `.jpg`, `.gif`, `.webp`): se envían al agente para que las describa, extraiga texto o responda preguntas sobre lo que muestran.

#### Botón Paste (pegar desde portapapeles)

Detecta automáticamente el contenido del portapapeles:
- Si hay una **imagen** (captura de pantalla, imagen copiada): la adjunta como imagen al mensaje.
- Si hay **texto**: lo pega directamente en el cuadro de mensaje.

#### Barra de adjuntos

Los adjuntos aparecen como chips bajo el cuadro de mensaje con el nombre del fichero y un botón **×** para eliminarlos. Se pueden combinar texto e imágenes libremente.

> **Soporte de visión:** Claude 3+, Gemini 1.5+ y los modelos GPT-4V procesan imágenes nativamente. En modos ACP (`opencode_acp`, `mimo_acp`, `gemini_acp`) las imágenes se envían en formato base64 dentro del protocolo de sesión.

### /loop — Bucle autónomo

El comando `/loop` pone al agente en modo autónomo: itera sobre un objetivo hasta que lo considera resuelto o hasta que le indicas que pare.

```
/loop <objetivo>
```

**Cómo funciona:**

1. Envías `/loop Implementa el sistema de login completo con validación y tests`.
2. El agente trabaja, responde y en cada turno evalúa si el objetivo está cumplido.
3. Si no lo está, XDForCode lanza automáticamente la siguiente iteración.
4. El agente escribe `[LISTO]`, `[DONE]`, `[FIN]` o `[TERMINADO]` al final de su respuesta para indicar que ha terminado.

**Comandos del bucle:**

| Comando | Acción |
|---|---|
| `/loop <objetivo>` | Inicia el bucle con el objetivo dado |
| `/loop stop` | Para el bucle en cuanto termine el turno actual |
| `/loop max <n>` | Limita a *n* iteraciones máximas |
| `/loop status` | Muestra el estado actual (activo/inactivo, iteración) |

**Integración con el Build:**  
Si el loop activa una compilación, XDForCode inyecta automáticamente la salida de la compilación (errores, warnings) en el siguiente turno del agente, de forma que puede corregir los errores detectados sin intervención manual.

**Integración con el Kanban:**  
El loop es compatible con las tareas Kanban: si hay una tarea en marcha, el loop no interfiere con la captura de resultados del Kanban.

> **Tip:** Combina `/loop` con una skill `rule` para que el agente siga las convenciones de tu proyecto en cada iteración.

### Diff review — revisar cambios de la IA antes de aplicarlos

Cuando el diff review está activo, **cada vez que un agente ACP quiere escribir un fichero**, XDForCode interrumpe la escritura y muestra el diff en el panel de chat antes de aplicarlo:

- Las líneas **eliminadas** se muestran en rojo.
- Las líneas **añadidas** se muestran en verde.
- Dos botones: **✓ Aplicar** (el fichero se escribe) y **✗ Rechazar** (la escritura se cancela, el fichero no cambia).

El agente queda en espera hasta que el usuario responde. Si rechaza el cambio, el agente recibe un resultado vacío y puede proponer una alternativa o detenerse.

**Activar / desactivar:**
```
/diffreview on     → activa la revisión de diff
/diffreview off    → desactiva (los cambios se aplican directamente, como siempre)
```

El estado persiste en `XDForCodeUI.ini [AI] diffreview`.

> **Limitación:** el diff review solo cubre el path ACP (`fs/write_text_file`), que es la escritura que usan opencode, mimo, gemini y similares. Las escrituras directas via MCP HTTP (tool `ide_write_file`) no pasan por este filtro. Con `/autoapprove on` o en planes Kanban con modo silencioso, el diff review se salta automáticamente para no interrumpir el flujo autónomo.

---

### Guardar y restaurar el modo de configuración

Si trabajas con varios proyectos o cambias frecuentemente entre agentes, estos comandos te permiten guardar y recuperar la configuración completa del chat en un solo paso:

| Comando | Acción |
|---|---|
| `/savemode` | Guarda un snapshot de la configuración actual (modo, exe, modelo, provider, ACP, http, stream) |
| `/restoremode` | Restaura el snapshot guardado (la config actual pasa a ser el nuevo snapshot; un segundo `/restoremode` deshace el cambio) |
| `/savechat` | Copia el historial de chat actual a `xdchat_YYYYMMDD_HH-MM-SS.json` |
| `/restorechat` | Lista los chats guardados y permite restaurar cualquiera de ellos |
| `/refresh` | Recarga la página del chat |

### Buscar en el historial de conversaciones anteriores

El historial de todas las sesiones queda persistido en `data/xdchat.db` (SQLite). Hay dos formas de buscarlo:

#### Desde el chat con `/search`

El comando `/search` busca directamente en todos los mensajes guardados (de todas las sesiones) y muestra los resultados en el chat. Cada resultado incluye la fecha de la sesión, el rol (usuario/asistente) y un fragmento del mensaje. Al hacer clic en un resultado, se carga esa sesión completa.

```
/search CodeGraph          → busca "CodeGraph" en todos los mensajes de usuario guardados
/search función AdjustLayout
/search error OrdIsUnique
```

> La búsqueda cubre los mensajes no comprimidos (todos los mensajes de usuario y los de asistente cortos). Los mensajes muy largos del asistente que se almacenan comprimidos no se incluyen en la búsqueda.

#### Desde el agente con la tool MCP `chat_search`

Los agentes de IA también pueden buscar en el historial directamente mediante la tool MCP `chat_search`.

| Parámetro | Descripción |
|---|---|
| `query` | Texto a buscar (requerido) |
| `session_id` | Limitar la búsqueda a una sesión concreta |
| `role` | Filtrar por `"user"` (tus preguntas) o `"assistant"` (respuestas del agente) |
| `limit` | Máximo de resultados (defecto 20) |
| `context` | Mensajes antes/después de cada match como contexto (defecto 1) |

**Ejemplos:**

```
Busca en el historial qué dijimos sobre CodeGraph
→ chat_search({"query": "CodeGraph"})

Busca solo en mis preguntas sobre el Kanban
→ chat_search({"query": "kanban", "role": "user"})

Busca la solución al error OrdIsUnique que el agente explicó antes
→ chat_search({"query": "OrdIsUnique", "role": "assistant"})

Busca en la sesión de ayer con más contexto alrededor de cada match
→ chat_search({"query": "harbour", "session_id": "ses_0995", "context": 3})
```

El `session_id` de cada sesión se puede ver con el comando `/restorechat`.

---

## 9. Skills — tipos y uso avanzado

Las **Skills** son fragmentos de texto predefinidos que se activan en el panel de chat para dar instrucciones permanentes, contexto o plantillas al agente.

> **Estado inicial:** ningún skill está activo al arrancar. El estado tampoco persiste entre sesiones: si recargas el panel o reinicias el IDE, vuelve a cero. Debes activarlos de nuevo cada vez que los necesites.

### Tipos de skills y dónde va su contenido

La diferencia clave entre tipos es **dónde llega el texto del skill al modelo**:

| Tipo | Dónde llega | Uso típico |
|---|---|---|
| **system** | System prompt | Instrucciones globales de comportamiento que el modelo debe seguir siempre |
| **context** | System prompt (como bloque de conocimiento) + el campo `prompt` también al system | Cargar ficheros o URLs como base de conocimiento; el modelo los recibe como contexto |
| **template** | Reemplaza por completo el mensaje del usuario (usa `{message}` como placeholder) | Flujos guiados donde el mensaje del usuario se inserta dentro de una plantilla mayor |
| **action** | Antepuesto al mensaje del usuario | Tarea concreta sobre el código; soporta `{code}` y `{selection}` como placeholders |
| **modifier** | Antepuesto al mensaje del usuario | Instrucciones de estilo o tono (respuesta corta, formal, telegráfica…) |
| **rule** | Antepuesto al mensaje del usuario | Reglas de codificación que el agente debe aplicar en su respuesta |

> **Nota sobre modifier y rule:** sus instrucciones llegan como prefijo del turno del usuario, no como system prompt. Si necesitas que una regla sea más autoritativa (que el modelo la priorice frente a sus instrucciones base), cambia el tipo a `system`.

### Skills disponibles

| Skill | Tipo | Descripción |
|---|---|---|
| `explain` | action | Explica el código activo paso a paso |
| `findbugs` | action | Busca bugs y problemas en el código |
| `refactor` | action | Propone refactorización sin cambiar funcionalidad |
| `test` | action | Genera tests unitarios para el código activo |
| `docstring` | action | Genera documentación para la selección |
| `formal` | modifier | Responde en tono técnico y formal |
| `concise` | modifier | Responde de forma concisa y directa |
| `caveman` | modifier | **Modo telegráfico:** sin preámbulos, sin resúmenes, sin cortesías. Ahorra 40-65% de tokens de salida. Ideal cuando ya sabes lo que quieres y solo necesitas el código |
| `harbour` | context | Contexto del proyecto Harbour + FiveWin |
| `harbour-locals` | rule | Obliga a declarar LOCAL al inicio de función y STATIC antes de cualquier función |
| `kanban-orquestador` | rule | Distribuye automáticamente tareas multi-módulo entre agentes PTY disponibles |
| `yagni` | rule | **YAGNI estricto:** solo implementa lo que se pide; sin manejo de errores imposibles, sin abstracciones prematuras, sin comentarios que expliquen qué hace el código |
| `harbexpert` | system | Consulta el repositorio oficial de Harbour antes de responder |
| `fivexpert` | system | Consulta la instalación de FiveWin (C:\fwh) antes de responder |
| `XDForCode` | context | Carga el doc de referencia de XDForCode y el README como base de conocimiento |

### Cómo usarlas

1. Escribe `/skills` en el cuadro de mensaje — aparece un panel con todos los skills disponibles.
2. Haz clic en el skill para activarlo (aparece con ✓ y se muestra en la barra superior).
3. El skill permanece activo en todos los mensajes hasta que lo desactives.
4. Para desactivar uno concreto: `/skills off <nombre>`. Para desactivar todos: `/skills clear`.

### Recargar skills sin reiniciar

Si editas `xdskills.json` directamente o añades skills nuevas, usa:
```
/reloadskills
```
Recarga el fichero en caliente sin necesidad de reiniciar el IDE ni recompilar nada.

### Gestionar Skills (diálogo CRUD)

Desde el menú puedes abrir el diálogo de gestión de Skills para añadir, modificar o eliminar skills de forma visual. Las skills se guardan en `xdskills.json` junto al ejecutable.

### Skills tipo context: conocimiento externo

Las skills de tipo `context` pueden cargar contenido desde:

- **Ficheros locales**: rutas absolutas o relativas al directorio de la aplicación.
- **URLs remotas**: contenido descargado vía HTTP (se eliminan los tags HTML automáticamente).

El contenido se inyecta automáticamente en el system prompt como bloques `### CONOCIMIENTO: nombre — fuente ###` mientras el skill está activo. Para forzar la recarga del disco usa `/context clear`.

El skill `XDForCode` incluido carga dos fuentes en cada mensaje:
- `docs/xdforcode.md` — arquitectura completa y referencia técnica del proyecto
- `Readme.md` — descripción de funcionalidades y guía de usuario

Ejemplo de skill con múltiples fuentes:
```json
{
  "name": "mi-proyecto",
  "type": "context",
  "sources": ["docs/arquitectura.md", "CLAUDE.md"],
  "prompt": "Conoce la arquitectura del proyecto desde las fuentes."
}
```

---

## 10. Preview HTML en vivo

XDForCode incluye un **panel de vista previa HTML** en el sidebar izquierdo que muestra en tiempo real el resultado de los ficheros HTML que estás editando.

### Cómo usarlo

1. Abre un fichero `.html` en el editor.
2. Pulsa el botón de **Preview HTML** en la barra lateral de iconos (el icono de ojo/preview).
3. El sidebar izquierdo cambia para mostrar la vista previa del HTML.
4. Cada vez que guardas el fichero, la vista previa se actualiza automáticamente.

### Comportamiento

- El botón de Preview solo se activa cuando el tab activo es un fichero HTML.
- Si el sidebar derecho o la consola estaban visibles, se ocultan temporalmente para dar más espacio al preview.
- Al cerrar el preview, se restauran los paneles que estaban visibles antes.

---

## 11. Sistema Kanban — múltiples agentes en paralelo

El **Kanban** permite lanzar y coordinar múltiples agentes de IA simultáneamente, cada uno con su propia tarea.

### Abrir el Kanban

Pulsa el icono de **Kanban** en la barra lateral de iconos. Se abre el tablero en el panel central.

### Cómo funciona

1. Crea una **tarea** en el tablero: asígnale un nombre, una descripción y un agente.
2. El agente arranca en su propia pestaña de terminal o en el agente IA activo.
3. El tablero muestra el estado de cada tarea: pendiente, en curso, completada.
4. Puedes ver la conversación de cada agente en su pestaña individual.

### Dependencias entre tareas

El Kanban soporta **dependencias**: puedes indicar que una tarea no se ejecute hasta que otra haya terminado. El prompt de una tarea puede referenciar el resultado de una anterior — basta con usar el botón `{ }` al editar el prompt y seleccionar la tarea cuyo resultado quieres insertar.

También puedes reutilizar el prompt completo de otra tarea (útil cuando varias tareas deben hacer exactamente lo mismo pero con datos distintos).

### Orden de ejecución de las tareas

Las tareas **no se ejecutan necesariamente en el orden visual** del tablero. El sistema sigue este criterio:

- Las tareas se ordenan internamente por su número de secuencia (`nOrder`).
- Una tarea se lanza en cuanto su agente está libre **y** todas sus condiciones de dependencia están satisfechas.
- Si el prompt de una tarea contiene `{{task.X.result}}`, el sistema espera automáticamente a que la tarea X haya terminado antes de lanzarla — aunque no hayas definido `depends_on`.
- Las tareas asignadas a agentes distintos sin dependencias entre sí pueden ejecutarse **en paralelo**.

Esto significa que en un plan con XDAGENT, MIMO y OPENCODE, si la tarea de OPENCODE usa el resultado de la de MIMO, el sistema lo detecta y respeta el orden. Si no tienen relación, las tres pueden correr simultáneamente.

### Reordenar tareas

Desde el diálogo **VER PLAN** puedes cambiar el orden de ejecución de cualquier tarea pendiente. Si alguna otra tarea referenciaba a la que has movido, su referencia se actualiza automáticamente para seguir apuntando a la misma tarea en su nueva posición. El resto de tareas que también hayan cambiado de posición se actualizan de la misma manera.

### Modo silencioso y auto-aprobación

Las tareas pueden ejecutarse en **modo silencioso**: trabajan en segundo plano sin mostrar los mensajes en el panel de chat. En este modo, si el agente solicita confirmación para realizar alguna acción, el sistema la aprueba automáticamente para no interrumpir el flujo.

### Editar el prompt de una tarea

Cada tarjeta tiene un botón **✏** que abre un editor directamente sobre la tarjeta. Puedes modificar el prompt antes de que la tarea empiece, sin necesidad de abrir ningún diálogo aparte.

### Eliminar tareas y planes

- Botón **✕** en la tarjeta: elimina una tarea individual que todavía no ha empezado.
- Botón **Eliminar plan** en la barra del tablero: elimina el plan completo.

### Cancelar tareas y watchdog

Puedes cancelar tareas en ejecución desde el tablero. Si una tarea lleva demasiado tiempo sin terminar, el sistema la marca automáticamente como fallida para evitar que quede bloqueada.

### Herramientas utilizadas por cada tarea

Al terminar, cada tarjeta muestra las herramientas que el agente usó durante su ejecución. Útil para auditar qué hizo el agente y detectar patrones de uso.

### Guardar y cargar planes

Desde el diálogo **VER PLAN** puedes guardar el conjunto de tareas actual como una plantilla reutilizable:

1. Pulsa **💾 Guardar plan** e introduce un nombre.
2. El plan se guarda en `tools/plans/<nombre>.json` junto al ejecutable.
3. Para cargarlo más adelante, pulsa **📂 Planes guardados**, selecciona el plan y pulsa **Cargar**.

El plan guarda por cada tarea: el agente al que pertenece, el prompt y el `idtask` (identificador interno). Esto permite que al cargarlo el sistema pueda reparar automáticamente las referencias entre tareas si los IDs han cambiado.

#### Validación de agentes al cargar un plan

Al cargar un plan, XDForCode comprueba que **todos los agentes que el plan necesita están activos** antes de añadir ninguna tarea al tablero. Si falta alguno:

- Se muestra un aviso con la lista de agentes ausentes.
- Se ofrece activarlos en `XDTermApps.ini` (equivale al botón "Añadir a Inicio").
- Se informa de que la aplicación debe reiniciarse para que la activación surta efecto.
- **El plan no se carga** hasta que todos los agentes estén disponibles.

Si el agente faltante no tiene entrada en `[APPS]` (solo en `[AGENTS]`), habrá que añadirla manualmente al INI.

#### Remapeo automático de tokens al cargar

Si los IDs internos de los agentes han cambiado desde que se guardó el plan (por ejemplo porque se desactivó un agente que estaba antes en la lista), los tokens `{{task.X-Y.result}}` de los prompts quedarían apuntando a IDs incorrectos. XDForCode detecta estos cambios y **repara automáticamente los tokens** en todos los prompts al cargar el plan.

#### Compatibilidad con planes guardados antes de esta versión

Los planes guardados con versiones anteriores (sin campo `idtask` por tarea) **cargan sin ningún problema**: simplemente no se benefician del remapeo automático de tokens (porque no se guardó el ID original). Para convertir un plan antiguo al nuevo formato basta con:

1. Cargarlo (los agentes deben estar activos).
2. Abrir **VER PLAN** y pulsar **💾 Guardar plan** con el mismo nombre.

A partir de ese momento el plan quedará en el nuevo formato con `idtask` por tarea.

### Planes de ejemplo incluidos

La carpeta `tools/plans/` incluye 8 planes listos para cargar que cubren todas las capacidades del motor:

| Fichero | Qué demuestra |
|---|---|
| `demo_paralelo_fanin.json` | Mimo y OpenCode trabajan **en paralelo**; XD Agent hace fan-in con ambos resultados via `{{task}}` |
| `demo_pipeline_secuencial.json` | OpenCode genera código → Mimo escribe tests → OpenCode refactoriza; **mismo agente dos veces** (`3-1` y `3-2`) |
| `demo_mismo_agente_dos_veces.json` | Patrón **A→B→A**: Mimo busca → OpenCode documenta → Mimo aplica en los ficheros |
| `demo_todas_capacidades.json` | Combinación completa: paralelo + fan-in + cadena + token `{{repeat:}}` + múltiples tareas por agente |
| `demo_mcp_git_workflow.json` | XD Agent revisa el estado del repositorio → Mimo redacta el mensaje de commit → XD Agent registra los cambios |
| `demo_mcp_entorno_changelog.json` | XD Agent obtiene fecha, versión de Harbour y commits recientes → OpenCode redacta entrada de CHANGELOG → Mimo la inserta |
| `demo_mcp_leer_parchear.json` | XD Agent lee fev_layout.prg y analiza expresiones repetidas (dos tareas propias); OpenCode aplica el refactor |
| `demo_cruzado.json` | OpenCode y XD Agent analizan el proyecto **en paralelo** (fan-in real con dos fuentes); Mimo sintetiza y OpenCode evalúa viabilidad |

Los tres planes `demo_mcp_*` ilustran el patrón más potente de XD Agent: **recopilar datos reales del entorno** (estado git, fecha/hora, versión de Harbour, contenido de ficheros) y pasarlos a los agentes de código mediante tokens `{{task.X-Y.result}}`. El agente decide qué herramienta usar según el objetivo de cada tarea.

### Generar un plan con IA (`/plan`)

En lugar de crear las tareas manualmente, puedes describir el objetivo en lenguaje natural y dejar que el agente IA genere el plan por ti.

**Uso:**

```
/plan Analiza el fichero fev_layout.prg, lista todas sus funciones y genera un índice Markdown
```

**Cómo funciona:**

1. El agente recibe la descripción y genera un plan en JSON con las tareas, agentes y dependencias necesarias.
2. El resultado se muestra en el chat como siempre (puedes ver el JSON generado).
3. Aparece una barra verde con el botón **📋 Cargar en Kanban** y el nombre y número de tareas del plan.
4. Al pulsar el botón, el plan se guarda en `tools/plans/` con el nombre que la IA le asignó y se abre automáticamente en el tablero listo para ejecutar.

El plan generado queda guardado en disco y puede reutilizarse y editarse como cualquier otro plan guardado manualmente.

> **Planes consecutivos:** Al cargar un nuevo plan con el botón **📋 Cargar en Kanban**, el tablero se limpia automáticamente (las tareas sin ejecutar del plan anterior desaparecen). No es necesario pulsar "Limpiar" manualmente antes de generar un segundo `/plan`.

**Otro ejemplo con paralelismo:**

```
/plan Revisa fev_agent.prg y fev_kanban.prg por separado y combina los resultados en un documento comparativo de sus funciones públicas
```

El agente generará tres tareas: dos en paralelo (una por fichero, en agentes distintos) y una tercera que hace fan-in usando los resultados de ambas.

### El agente como orquestador — auto-generación de tareas

XDForCode incluye dos herramientas MCP especiales que permiten a los propios agentes de IA crear y programar tareas en el Kanban **sin intervención manual**:

| Tool MCP | Para qué sirve |
|---|---|
| `ide_kanban_agents` | Devuelve la lista de agentes disponibles con sus IDs actuales |
| `ide_kanban_add_task` | Añade una tarea al Kanban (staged o en cola, con dependencias opcionales) |

Con estas tools, un agente (por ejemplo el XDAGENT principal) puede analizar el objetivo, dividirlo en subtareas y asignar cada una al agente más adecuado — todo de forma automática.

**Ejemplo de flujo:**

```
Tú → XDAGENT: "Refactoriza todos los módulos del proyecto separando la lógica de UI"

XDAGENT (usando ide_kanban_agents):
  → descubre que hay MIMO y OPENCODE disponibles

XDAGENT (usando ide_kanban_add_task):
  → añade tarea a MIMO: "Refactoriza fev_layout.prg"
  → añade tarea a OPENCODE: "Refactoriza fev_agent.prg"
  → añade tarea a MIMO: "Revisa y unifica los cambios" (depends_on: las dos anteriores)
```

El Kanban ejecuta el plan automáticamente en cuanto XDAGENT termina de encolarlo.

> **Nota:** Para que este flujo funcione, los agentes MIMO y OPENCODE deben estar activos (pestañas abiertas en el panel de consola).

### Casos de uso típicos

- Lanzar un agente que refactoriza el código mientras otro escribe los tests.
- Pedir a tres agentes distintos (Claude, Gemini, Ollama) que respondan a la misma pregunta y comparar resultados.
- Dejar tareas largas corriendo en segundo plano mientras trabajas en otra cosa.
- Crear flujos de trabajo encadenados donde cada paso usa el resultado del anterior.
- Repetir el mismo prompt en varias tareas para aplicar una instrucción a múltiples ficheros.
- **Delegar la planificación al propio agente**: pídele que diseñe y encole el plan Kanban completo.

---

## 12. Sistema de Build y Toolchains

XDForCode incluye un **sistema de build completo** para compilar proyectos Harbour/FiveWin directamente desde el IDE.

### ¿Qué es una toolchain?

Una **toolchain** es un perfil de compilación que define las rutas y opciones de todas las herramientas necesarias para compilar tu proyecto: Harbour, compilador C, linker, recursos y librerías.

### Configurar una toolchain

Desde el menú, abre el **editor de toolchains** (fichero `XDToolchains.json`). Puedes configurar:

- **Harbour**: ruta de instalación, flags de compilación, includes adicionales.
- **Compilador C**: ruta del compilador (cl.exe), flags, includes.
- **Linker**: ejecutable del linker y flags.
- **Recursos**: ruta de rc.exe para compilar ficheros `.rc`.
- **Librerías**: lista de `.lib` del sistema, Harbour y FiveWin.
- **Batch de entorno**: opcional, un `.bat` que configura las variables de entorno antes de compilar.

### Compilar el fichero activo

Pulsa la tecla de build o usa el menú para compilar el `.prg` que estás editando. El resultado aparece en la pestaña **Results** del panel inferior.

Si la compilación termina sin errores y la opción "ejecutar tras build" está activada, el `.exe` resultante se ejecuta automáticamente.

### Importar desde FivEdit

Si ya tienes un proyecto en el IDE de FiveWin, puedes importarlo:

- **Importar toolchain** (`.fiv`): lee las preferencias de FivEdit y las convierte en una toolchain compatible.
- **Importar proyecto** (`.prj`): lee las fuentes, recursos y librerías del proyecto de FivEdit y genera un `.xdprj`.

---

## 13. Proyectos (.xdprj)

Un **proyecto** en XDForCode es un fichero `.xdprj` (formato JSON) que agrupa las fuentes, recursos, librerías y configuración de compilación de tu aplicación.

### Editor visual de proyectos

Desde el menú puedes abrir el **editor visual de proyectos** que muestra una interfaz web con:

- Lista de fuentes (`.prg`, `.prw`, `.c`, `.cpp`) con opción de activar/desactivar cada una.
- Lista de recursos (`.rc`, `.res`).
- Librerías adicionales del proyecto.
- Toolchain asociada y ejecutable de salida.

### Crear un proyecto nuevo

1. Abre el menú y selecciona **Nuevo Proyecto**.
2. Se crea un `.xdprj` vacío que puedes rellenar desde el editor visual.
3. Asocia una toolchain existente o crea una nueva.

### Compilar un proyecto

Selecciona el proyecto activo y ejecuta el build. El sistema genera un script de compilación que:

1. Compila cada fuente `.prg` → `.c` → `.obj` con Harbour y el compilador C.
2. Compila cada fuente `.c` → `.obj`.
3. Compila los recursos `.rc` → `.res` si los hay.
4. Linka todos los `.obj`, librerías y recursos para generar el `.exe` final.

---

## 14. Acceso remoto desde el navegador

XDForCode incluye un **servidor web** que permite acceder al chat con el agente desde cualquier navegador de tu red local (o internet, si lo expones).

### Arrancar el servidor web

Pulsa el icono del servidor en la barra lateral de iconos. Cuando está activo, la barra de estado inferior muestra el puerto: `Server :8003`.

### Acceder desde el navegador

Abre en tu navegador:
```
http://localhost:8003
```

Verás la interfaz de chat, idéntica al panel de XDForCode. Las respuestas del agente llegan en tiempo real al navegador.

### Configuración del servidor

Desde el menú puedes configurar:

- **Puerto** del servidor (por defecto 8003).
- **Carpeta de documentos** (docroot) para los ficheros estáticos.
- **Monitor remoto**: opción para mostrar en el IDE las consultas que llegan del navegador.

---

## 15. Gestión de usuarios del chat remoto

Si quieres proteger el acceso al chat remoto con autenticación, puedes gestionar los usuarios desde un **diálogo CRUD** accesible desde el menú.

### Añadir un usuario

1. Abre el diálogo de **Gestión de Usuarios** desde el menú.
2. Pulsa **Añadir**.
3. Introduce el nombre de usuario y la contraseña (se guarda como hash SHA-256).
4. Configura opcionalmente el modo IA, provider, modelo y ejecutable que usará ese usuario.
5. Pulsa **Aceptar**.

### Configuración por usuario

Cada usuario remoto puede tener configurado:

| Campo | Descripción |
|---|---|
| **Usuario** | Nombre de login |
| **Modo** | Modo de ejecución IA (opencode_acp, ollama, etc.) |
| **Provider** | Proveedor del modelo (Anthropic, NVIDIA, etc.) |
| **Modelo** | Modelo concreto a usar |
| **Exe** | Ruta del ejecutable del agente |

Esto permite que cada usuario remoto use un agente y modelo diferente sin afectar a otros.

### Fichero de usuarios

Los usuarios se almacenan en `xdusers.json` junto al ejecutable. El acceso es libre mientras este fichero no exista o esté vacío.

---

## 16. Explorador de archivos

El explorador ocupa el panel izquierdo. Muestra el árbol de directorios de la carpeta de trabajo actual.

- **Clic simple**: abre el fichero en el editor.
- **Ficheros binarios** (imágenes, ejecutables): se abren con la aplicación por defecto de Windows.
- **Ficheros HTML**: puedes elegir abrirlos en el editor o en el panel de vista previa.
- **Drag & drop**: puedes arrastrar ficheros desde el explorador.

El explorador se **actualiza automáticamente** cuando se crean o modifican ficheros desde los agentes IA.

---

## 17. Terminales y pestañas configurables

En la parte inferior encontrarás varias pestañas de terminal. Las pestañas disponibles por defecto son:

| Pestaña | Para qué sirve |
|---|---|
| **Results** | Salida de compilación y build |
| **GIT** | Terminal Git en la carpeta de trabajo |
| **SSH** | Conexión SSH a servidores remotos |
| **System Console** | Consola de Windows estándar |
| **Console CLI** | Terminal interactiva; dropdown AGENTS para lanzar agentes |
| **WhatsApp** | WhatsApp Web embebido (si está habilitado) |

La pestaña **Console CLI** incluye dos botones flotantes que aparecen al iniciar un proceso:
- **Home** — vuelve a la pantalla inicial manteniendo el proceso activo en segundo plano
- **Repintar** — fuerza un redibujado del terminal

El dropdown **AGENTS** de Console CLI se abre automáticamente hacia arriba o hacia abajo según el espacio disponible, y tiene scroll si hay muchos agentes.

### Pestañas personalizadas

El fichero `XDTermApps.ini` permite crear pestañas personalizadas de terminal y agentes:

Cada entrada sigue el formato `Nombre = comando, flag`:

| Flag | Comportamiento |
|---|---|
| `1` | Crea la pestaña y arranca automáticamente al iniciar |
| `0` | No crea pestaña (equivale a comentar la línea con `;`) |
| `shell` | App Harbour/FiveWin, botón "Abrir" (ShellExecute) |
| `http://...` | Lanza servidor + abre URL en WebView (manual) |
| `http://..., 1` | Igual pero arranca automáticamente |

El flag `0` es útil para tener entradas preconfiguradas pero inactivas, sin necesidad de borrarlas o comentarlas.

**Sección `[APPS]`** — Pestañas de terminal (también elegibles como agentes en el Kanban):
```ini
[APPS]
Mimo     = cmd.exe /k mimo --never-ask, 1   ; pestaña activa
OpenCode = cmd.exe /k opencode --auto, 1    ; pestaña activa
OpenWiki = cmd.exe /k openwiki, 0           ; desactivada (sin pestaña)
```

**Sección `[AGENTS]`** — Agentes disponibles en el dropdown de Console CLI (sin pestaña fija propia):
```ini
[AGENTS]
OpenWiki   = cmd.exe /k openwiki, 1
OpenCode   = cmd.exe /k opencode, 1
Claude     = cmd.exe /k claude, 1
Ollama     = cmd.exe /k ollama run qwen3.5:9b, 1
```

Todas son terminales interactivas completas con soporte de color ANSI.

### OpenWiki

[OpenWiki](https://github.com/langchain-ai/openwiki) es una herramienta LangChain que combina búsqueda en Wikipedia con resumen mediante LLM. Permite preguntar en lenguaje natural sobre cualquier tema y obtener respuestas fundamentadas en artículos de Wikipedia.

**Instalación:**
```
pip install openwiki
```

**Integración en XDForCode:**

- En `[AGENTS]` con flag `1`: disponible en el dropdown de Console CLI. Se lanza bajo demanda desde la consola interactiva.
- En `[APPS]` con flag `1`: crea una pestaña permanente en el panel inferior; queda disponible también como agente Kanban.
- En `[APPS]` con flag `0` (por defecto): desactivado sin borrar la entrada — cámbialo a `1` si lo usas frecuentemente.

> **Combinación recomendada:** `0` en `[APPS]` y `1` en `[AGENTS]` — accesible desde el dropdown sin ocupar pestaña fija.

#### Ejemplo Kanban con OpenWiki

OpenWiki resulta especialmente útil como primer eslabón en un plan Kanban: busca y resume información de Wikipedia y pasa el resultado a otro agente que lo procesa.

```
┌───────────────────────────┐        ┌──────────────────────────────┐
│  Tarea 1 — OpenWiki       │───────▶│  Tarea 2 — OpenCode          │
│                           │        │                              │
│  "Busca en Wikipedia      │        │  "Usando {{task.1.result}},  │
│   información sobre el    │        │   crea documentación técnica │
│   protocolo WebSocket y   │        │   en README.md para nuestro  │
│   devuelve un resumen"    │        │   proyecto Harbour"          │
│                           │        │                              │
│  Agente: OpenWiki         │        │  Agente: OpenCode            │
│  Estado: done ✓           │        │  depends_on: [tarea-1]       │
└───────────────────────────┘        └──────────────────────────────┘
```

El marcador `{{task.1.result}}` se sustituye automáticamente por la salida de la tarea 1 antes de enviar el prompt a OpenCode. Las tareas con dependencias implícitas (usan `{{task.N.result}}`) esperan automáticamente aunque no se declare `depends_on` de forma explícita.

### Diálogo de gestión de agentes ("Añadir a Inicio")

Desde la consola CLI hay un botón que abre el listado de agentes definidos en `[AGENTS]`. Al seleccionar uno y pulsar **Añadir a Inicio**, XDForCode modifica `XDTermApps.ini` con estas reglas:

| Situación | Acción |
|---|---|
| El agente **no existe** en `[APPS]` | Se añade al **final** de la sección con flag `1` |
| El agente existe con flag **`0`** (desactivado) | Se reactiva cambiando el flag a `1` |
| El agente existe con flag **`1`** (ya activo) | Pregunta si se desea **desactivar** (cambia a `0`) |

El cambio requiere reiniciar la aplicación para que tenga efecto.

---

## 18. Integración con WhatsApp

XDForCode incluye una pestaña de **WhatsApp Web** embebida en el panel inferior que permite enviar y recibir mensajes de WhatsApp desde el IDE.

### Activar la pestaña

La pestaña WhatsApp se muestra si está habilitada en la configuración (fichero `XDForCodeUI.ini`). Puedes activarla o desactivarla desde el menú.

### Cómo funciona

1. Al abrir la pestaña, se carga WhatsApp Web en un WebView embebido.
2. Inicia sesión con tu cuenta de WhatsApp escaneando el código QR.
3. Puedes enviar mensajes programáticamente desde el chat de IA o mediante tools MCP.

### Envío de mensajes

El agente IA puede enviar mensajes de WhatsApp mediante la tool MCP `mcp_whatsapp_send`. Esto permite crear automatizaciones como:

- Enviar notificaciones cuando termine una tarea del Kanban.
- Alertar por WhatsApp si un build falla.
- Enviar resúmenes de conversaciones del chat.

---

## 19. Menú de la aplicación — opciones de configuración

El menú principal de XDForCode cubre la **gran mayoría de opciones de configuración** de la aplicación. Se recomienda revisarlo detenidamente antes de empezar a trabajar.

Entre las opciones que encontrarás en el menú:

- **Configuración del agente IA**: selección del agente activo, modo de ejecución, proveedor y modelo.
- **Configuración del servidor web**: puerto, carpeta de documentos y acceso remoto.
- **Build y Compilación**: ruta de Harbour, FiveWin y compilador C para el sistema de build.
- **Toolchains**: editor visual de perfiles de compilación.
- **Importar**: importar toolchains y proyectos desde FivEdit (`.fiv`, `.prj`).
- **Proyectos**: crear y gestionar proyectos `.xdprj`.
- **Skills**: diálogo CRUD para gestionar las skills del agente.
- **Usuarios**: gestión de usuarios del chat remoto.
- **Apariencia y layout**: visibilidad de paneles laterales, consola y barra de estado.
- **Opciones del editor**: fuente, tamaño, tema de color y autoguardado.
- **Herramientas MCP**: gestión de las tools MCP disponibles para los agentes.
- **Terminal y aplicaciones externas**: configuración de las pestañas de terminal adicionales.
- **Diagnóstico ACP** (`Log ACP`): toggle que activa el registro detallado del protocolo ACP en el fichero `xdacp.log` (en el directorio del exe). Útil para depurar problemas de comunicación con el agente.
- **Agente externo (ACP) `[ ON / OFF ]`**: toggle que controla si el modo Inference requiere un agente externo (opencode, mimo) para ejecutar herramientas MCP. Con `[ OFF ]`, XDForCode ejecuta el bucle de tool calling internamente — cualquier provider inference (GROQ, NVIDIA, OLLAMA, OpenRouter...) puede usar herramientas MCP sin tener instalado ningún agente ACP. Con `[ ON ]` (valor por defecto), las herramientas en inference solo se activan si el modelo está marcado como `"tools": true` en `xdinference.json`.

> Dedica unos minutos a explorar cada sección del menú: muchas funcionalidades de XDForCode solo son accesibles desde ahí.

---

## 20. Preguntas frecuentes

**¿Necesito instalar todos los agentes?**  
No. Con instalar uno ya puedes trabajar. Si no tienes claro cuál elegir, empieza con **Ollama** (gratuito, sin internet) o **Claude Code**.

**¿El agente tiene acceso a mis ficheros?**  
El agente recibe como contexto el contenido del fichero que tienes abierto en el editor. No explora tus directorios automáticamente salvo que le des permiso explícito o uses herramientas MCP.

**¿Puedo usar varios agentes a la vez?**  
Sí, mediante el Kanban puedes tener varios agentes activos en paralelo, cada uno en su propia pestaña.

**¿El chat queda guardado?**  
Sí. Todas las sesiones se guardan automáticamente en `data/xdchat.db` (SQLite). Puedes restaurar cualquier sesión anterior con `/restorechat`, y los agentes pueden buscar en el historial completo con la tool MCP `chat_search`.

**¿Puedo usar XDForCode sin conexión a internet?**  
Sí, siempre que uses **Ollama** como agente o el modo **Inference** con un provider que no requiera autenticación. El resto de agentes requieren conexión para conectarse a sus APIs en la nube.

**¿Qué ocurre si el agente tarda mucho?**  
XDForCode tiene un sistema de watchdog automático: si el agente lleva **45 segundos** sin responder, aparece un aviso en el chat informando de que la espera se alargará 45 segundos más. Si tras esos segundos adicionales sigue sin responder (90s en total), el proceso se cancela automáticamente y el chat queda disponible para seguir escribiendo. También puedes cancelar en cualquier momento con el botón **Cancelar** del panel de chat. Si el agente cancela repetidamente por límite de cuota del modelo, cambia a otro modelo o proveedor con `/model`.

**¿Qué es el modo Inference?**  
Es un modo de conexión directa a APIs OpenAI-compatible (NVIDIA, GROQ, OpenRouter, etc.) sin necesidad de instalar agentes externos. Solo necesitas configurar una API key en `xdinference.json`.

**¿Los datos que el agente busca en mis ficheros locales (CodeGraph, DBF) salen del equipo?**  
Depende del modelo que uses. El agente MCP busca en la base de datos local (SQLite de CodeGraph) y obtiene los resultados — eso no sale del equipo. Sin embargo, esos resultados se envían al modelo como parte del contexto de la conversación. Si usas un **modelo en la nube** (Claude, OpenAI, GROQ, NVIDIA, HuggingFace…), los datos de la búsqueda viajan a los servidores del proveedor. Si usas un **modelo local** (Ollama, vLLM/LM Studio en `localhost`), los datos nunca salen del equipo.

**¿Puede el agente buscar en mis ficheros DBF y encontrar datos de mis clientes o proveedores?**  
Sí, siempre que esos ficheros estén indexados en CodeGraph (**TOOLS → CodeGraph Index → Index DATABASES**). Una vez indexados, el agente puede buscar datos de empresa, CIFs, importes o cualquier texto libre usando la tool MCP `project_search`. Si no encuentra nada en el índice, puede hacer una búsqueda en tiempo real con `db_open_dbf(mode="smart_search")`.

**¿Cómo configuro las rutas de compilación?**  
Desde el menú, abre la sección de **Build / Compilación** y configura las rutas de Harbour, FiveWin y el compilador C. También puedes importar perfiles desde FivEdit.

**¿Puedo compilar mi proyecto directamente desde el IDE?**  
Sí. Configura una toolchain, asocia un proyecto `.xdprj` y ejecuta el build desde el menú o la tecla de compilación. Los resultados aparecen en la pestaña Results.

---

## 21. Indexación de Código y Documentos (CodeGraph)

XDForCode incluye un potente motor interno de indexación llamado **CodeGraph**. Este motor permite a los agentes de IA entender todo tu proyecto al instante, realizando búsquedas ultrarrápidas tanto sobre tu código fuente como sobre tu documentación, sin necesidad de que el agente tenga que leer todos los ficheros del disco en cada mensaje.

Al usar CodeGraph, la IA adquiere una memoria instantánea y global de cómo están estructuradas tus clases, qué funciones llaman a otras funciones, y dónde encontrar respuestas exactas en tus manuales.

### 21.1 ¿Cómo configurarlo? (`codegraph.json`)

Para que el sistema sepa qué partes de tu disco duro debe leer, necesita un archivo de configuración llamado `codegraph.json` en la raíz de tu proyecto. 

Si el archivo no existe, puedes crearlo con la siguiente estructura básica. Este archivo te permite tener un control total (mediante la propiedad `"enabled"`) de qué quieres indexar.

```json
{
  "db": ".codegraph\\codegraph.db",
  "sources": [
    {
      "path": "E:\\ruta\\a\\tu\\proyecto",
      "label": "Proyecto principal",
      "enabled": true,
      "extensions": ["*.prg", "*.ch"]
    }
  ],
  "documents": [
    {
      "path": "E:\\ruta\\a\\tu\\proyecto\\docs",
      "label": "Documentacion",
      "enabled": true,
      "extensions": ["*.txt", "*.md"]
    }
  ],
  "databases": [
    {
      "path": "E:\\ruta\\a\\tu\\proyecto\\data",
      "label": "Datos DBF",
      "enabled": true,
      "extensions": ["*.dbf", "*.db"]
    }
  ],
  "options": {
    "max_doc_size_kb": 15,
    "skip_dirs": [
      ".git",
      "node_modules",
      "build",
      "build64",
      "obj"
    ]
  }
}
```

**Explicación de las secciones:**
- **`db`**: Dónde se guardará la base de datos de SQLite. Por defecto se recomienda ponerlo dentro de una carpeta oculta `.codegraph`.
- **`sources`**: Rutas de carpetas donde guardas código fuente. Puedes configurar qué extensiones buscar en `extensions` (por defecto `*.prg` y `*.ch`).
- **`documents`**: Rutas de carpetas donde guardas archivos de texto o Markdown (`*.txt`, `*.md`). Es ideal para que la IA se empape de las reglas de negocio o manuales de tu aplicación.
- **`databases`**: Novedad. Rutas a tus tablas `.dbf` o bases `.sqlite`. CodeGraph extraerá de forma inteligente su estructura (campos) y todo el contenido útil de sus registros, **separando automáticamente los campos largos (Memos)** para evitar límites de tamaño, permitiendo a la IA contestar preguntas precisas sobre tu modelo de datos y clientes sin esfuerzo.
- **`options`**: 
  - `max_doc_size_kb`: El tamaño máximo en KB que leerá de cada documento (para evitar colapsar la base de datos con logs inmensos).
  - `skip_dirs`: Nombres de carpetas que el indexador debe ignorar completamente al buscar archivos recursivamente.

### 21.2 ¿Cómo iniciar la indexación?

Una vez tienes tu archivo `codegraph.json` listo, abre tu proyecto en XDForCode.

Desde el menú superior del IDE:
👉 **TOOLS → CodeGraph Index**

Aquí encontrarás varias opciones que te permitirán tener control total sobre qué indexar sin perder tiempo:
- **Index ALL**: Escanea y actualiza absolutamente todo (Fuentes, Documentos y Bases de datos).
- **Index SOURCES**: Escanea únicamente los ficheros de código fuente, ignorando lo demás.
- **Index DOCUMENTS**: Útil cuando solo has añadido o modificado un manual `.md` o `.txt` y quieres que la IA lo sepa rápido.
- **Index DATABASES**: Exclusivo para re-escanear tablas y sus registros.

Al hacer clic, el proceso comienza inmediatamente de forma local. Verás un mensaje en pantalla indicándote qué parte del proyecto se está procesando en ese instante.

**El proceso es 100% automático y transparente:**
- **Sin dependencias**: No necesitas Node.js, Python ni conexiones a internet. Todo ocurre dentro del núcleo Harbour de XDForCode de manera silenciosa.
- **Creación de la BD**: Se crea automáticamente el archivo `codegraph.db` y todas sus tablas e índices si es la primera vez.
- **Auto-limpieza Inteligente (Categorizada)**: Si borras un archivo o modificas algo, el sistema de limpieza borrará automáticamente los restos antiguos de la base de datos (nodos huérfanos) para que la IA no se confunda. **Y lo mejor:** si eliges indexar solo Documentos, el sistema sabe que solo debe limpiar Documentos, preservando a la perfección tu código fuente y tus bases de datos intactas sin necesidad de reescanearlo todo.
- **Reset de la Base de Datos**: Si en algún momento necesitas empezar de cero o hay un cambio estructural en las tablas, desde el menú **TOOLS** puedes seleccionar **Reset CodeGraph DB** para eliminar la base de datos completa y regenerar su estructura limpia instantáneamente.

### 21.3 Auto-Indexación en Tiempo Real (Incremental)

El indexador global a través del menú solo necesitas usarlo la primera vez o cuando configuras el proyecto inicialmente. A partir de entonces, el IDE se encarga de todo:

**¡Indexación Mágica al Guardar!**  
Cada vez que modificas un archivo de código (`.prg`, `.ch`) o un documento web/markdown y lo guardas (`Ctrl+S`), XDForCode intercepta el evento silenciosamente. En tan solo 1 milisegundo:
1. Elimina los registros antiguos de ese fichero de la base de datos local.
2. Analiza los nuevos cambios y los inyecta en la BD (incluyendo su AST o su estructura de capítulos).
3. Todo ocurre en segundo plano, sin bloqueos ni barras de carga. Los agentes de IA siempre dispondrán de la información actualizada al segundo, incluso si son ellos mismos los que te escriben un nuevo fichero.

### 21.4 Indexar PDF, ficheros Office e imágenes (OCR)

CodeGraph puede extraer texto de formatos binarios mediante scripts Python embebidos. Esto permite indexar manuales en PDF, hojas de cálculo Excel y capturas de pantalla junto con el código fuente.

**Instalar una sola vez:**

```
pip install markitdown[all] Pillow pytesseract
```

También necesitas **Tesseract OCR** para las imágenes: descárgalo desde [UB-Mannheim/tesseract](https://github.com/UB-Mannheim/tesseract/wiki).

| Formato | Motor |
|---|---|
| PDF (texto nativo) | `pdfminer.six` (incluido en `markitdown[all]`) |
| PDF (escaneado) | Tesseract OCR via `pytesseract` |
| Excel / Word / PowerPoint | `markitdown` |
| Imágenes (PNG, JPG…) | Tesseract OCR |

Tras la instalación, añade las rutas a tu `codegraph.json` con la extensión correspondiente y ejecuta **TOOLS → CodeGraph Index → Index DOCUMENTS**.

### 21.5 `project_search` — búsqueda de código y datos en CodeGraph

La tool MCP `project_search` es la herramienta de búsqueda universal del proyecto. Busca simultáneamente en **dos fuentes**:

| Fuente | Qué contiene | Ejemplos |
|---|---|---|
| `nodes_fts` | Código fuente Harbour: funciones, clases, métodos, variables | `AdjustLayout`, `CreateWebView`, `KanbanScheduler` |
| `documents_fts` | Registros de ficheros DBF indexados, documentos Markdown, PDFs, imágenes | Empresas, CIFs, importes, nombres de cliente, contenido de manuales |

**Uso desde el agente:**
```
Busca qué tenemos sobre "Hermanos Puertas" en el proyecto
→ project_search({"query": "Hermanos Puertas"})

¿Cuánto le vendimos a Cobra Instal.?
→ project_search({"query": "Cobra Instal"})

¿Dónde está definida la función AdjustLayout?
→ project_search({"query": "AdjustLayout"})
```

> **Importante**: para que encuentre datos de DBF, esos ficheros deben estar indexados en CodeGraph (**TOOLS → CodeGraph Index → Index DATABASES**). La búsqueda FTS5 usa coincidencias de prefijo (`"Cobra"` encuentra `"COBRA INSTAL."`).

> **`codegraph_explore`** solo busca en código fuente (`nodes_fts`). No puede encontrar datos de DBF aunque estén indexados. Para datos de negocio, usa siempre `project_search`.

### 21.6 `harbour_search` — búsqueda de símbolos Harbour/FiveWin

La tool MCP `harbour_search` permite a los agentes buscar clases, métodos y funciones del runtime de Harbour y FiveWin directamente, sin necesidad de leer los ficheros fuente. Está implementada en Python (`tools/mcp/src/mcp_harbour_search.py`) y accede a la misma base de datos SQLite de CodeGraph.

**Uso desde el agente:**
```
Usa harbour_search para buscar la clase TBrowse y ver sus métodos
```

> Los resultados incluyen firma, fichero y número de línea del símbolo en la instalación de FiveWin/Harbour.

### 21.6 ¿Cómo utilizan la IA el proyecto indexado?

Una vez que el proyecto y los documentos están indexados, los agentes integran herramientas (*tools*) que se conectan en tiempo real a esta base de datos local.

- **Para tu código**: Si le pides a la IA "Busca dónde se usa la función Facturar()", la IA no intentará leer tus 500 archivos `.prg`. Consultará la base de datos y sabrá en milisegundos la línea exacta, quién la llama y a quién llama.
- **Clasificación por Importancia (PageRank interno)**: Al buscar en el código, el sistema utiliza un algoritmo de *In-Degree Centrality*. Esto significa que cuando el agente busca código, los resultados se ordenan devolviendo primero aquellos ficheros y funciones que son más llamados por el resto del proyecto. ¡El código más crítico siempre aparece primero!
### 21.7 Exploración Visual del Grafo

Puedes explorar tu código visualmente e interrogar a la base de datos de CodeGraph de dos formas:
- A través del menú principal: **TOOLS -> Native CodeGraph**
- (Próximamente) Haciendo clic derecho sobre cualquier palabra o función en el editor de código para abrir el menú contextual.

Dispones de las siguientes opciones:

1. **Find Definition (Ir a la definición)**
   - **Qué hace:** Busca exactamente el archivo `.prg` y la línea donde está escrita la definición original de la clase o función (`CLASS TPanel`, `Function TTimer()`, etc.).
   - **Cuándo usarlo:** Úsalo cuando necesites ver cómo está programada por dentro una función o qué propiedades tiene una clase en su código original.

2. **Find Callers (Quién me llama)**
   - **Qué hace:** Busca en todo tu proyecto y en FiveWin todos los lugares donde se invoca o utiliza la función o clase sobre la que has hecho clic.
   - **Cuándo usarlo:** Úsalo cuando quieras ver ejemplos de cómo se usa una función (buscando dónde la has usado antes) o cuando vayas a modificar los parámetros de una función y necesites saber a quién tienes que ir a corregir para que no dé error al compilar.

3. **Find Callees (A quién llamo yo)**
   - **Qué hace:** Es exactamente lo contrario a Callers. Busca dentro de la función que has seleccionado y te hace un resumen de qué otras funciones o métodos invoca internamente.
   - **Cuándo usarlo:** Úsalo cuando estés leyendo una función muy larga o compleja que hizo otro programador (o tú mismo hace tiempo) y quieras un resumen rápido de qué dependencias tiene o en qué otras subrutinas se apoya, sin tener que leerte el código línea por línea.

4. **Blast Radius / Impact Analysis (Radio de Impacto en cadena)**
   - **Qué hace:** Es una versión "extrema" y recursiva de Callers. No solo te dice quién te llama a ti directamente, sino quién llama al que te llama, y quién llama al que llama al que te llama...
   - **Cuándo usarlo:** Úsalo exclusivamente cuando vayas a modificar una función "Core" o crítica (por ejemplo, una función de conexión a BD o de login). El radio de impacto te dirá absolutamente todas las partes del programa que podrían "romperse" en cadena por culpa de ese cambio, para que sepas qué pantallas tienes que testear antes de darlo por bueno.

---

---

## 22. Motor de Reportes — `show_report`

XDForCode incluye un motor de reportes HTML que los agentes de IA pueden usar para mostrar resultados de forma visual y estructurada directamente en el IDE, sin necesidad de abrir ningún fichero externo.

### Cómo lo usa el agente

Los agentes acceden al motor a través de la tool MCP `show_report`. Cuando el agente llama a esta tool, XDForCode abre un diálogo emergente con el reporte renderizado. El agente puede invocarla así:

```
Usa show_report para mostrar los resultados del análisis con una tabla de errores y un diagrama de dependencias
```

### Tipos de sección disponibles

| Tipo | Para qué sirve |
|---|---|
| `table` | Tabla con cabecera y filas de datos |
| `markdown` | Texto formateado con Markdown |
| `code` | Bloque de código con resaltado de sintaxis |
| `mermaid` | Diagrama Mermaid (flowchart, sequence, gantt, etc.) |
| `diff` | Visor de diferencias lado a lado (formato unified diff) |
| `alert` | Mensaje de alerta con nivel de severidad (info, warning, error, success) |
| `accordion` | Sección colapsable para contenido extenso |
| `chart` | Gráfico de barras o líneas |
| `buttons` | Botones de acción que interactúan con el IDE |

### Botones de acción interactivos

Las secciones de tipo `buttons` permiten al agente crear botones que hacen cosas reales en el IDE cuando el usuario los pulsa:

| Acción del botón | Efecto |
|---|---|
| `open_file` | Abre el fichero indicado en el editor, opcionalmente en una línea concreta |
| `run_cmd` | Envía un comando al terminal Console CLI |
| `copy` | Copia texto al portapapeles (sin pasar por el bridge) |

**Estilos de botón:** `primary` (azul), `secondary` (gris), `danger` (rojo), `success` (verde).

### Visor de diferencias (Diff View)

La sección de tipo `diff` renderiza un diff en formato unified lado a lado, con colores para líneas añadidas, eliminadas y de contexto. Útil para que el agente muestre los cambios propuestos antes de aplicarlos:

```
Agente: "Aquí están los cambios propuestos en fev_layout.prg — pulsa 'Aplicar' cuando estés listo"
→ show_report con sección diff + botón run_cmd para aplicar el parche
```

---

## 24. Herramientas MCP para MySQL/MariaDB

XDForCode incluye un conjunto completo de herramientas MCP para acceder a bases de datos MySQL y MariaDB directamente desde los agentes de IA. Hay dos familias de tools, cada una con su propia implementación interna, pero ambas comparten el mismo fichero de configuración de conexiones.

### Familias de tools

| Familia | Prefijo | Motor interno | N.º de tools |
|---|---|---|---|
| TDolphin | `mysql_*` | `TDolphinSrv` (FiveWin) | 13 |
| FWMaria | `fwmaria_*` | `FWMariaConnection` (FiveWin) | 15 |

**¿Cuál usar?** Ambas hacen CRUD básico. Usa `fwmaria_*` si necesitas stored procedures, vistas, triggers, importar/exportar DBF, o pivotes de datos.

### Configurar conexiones (`mysql_shared.ini`)

Crea el fichero `mysql_shared.ini` en la carpeta del ejecutable (o en `tools/mcp/`). Cada sección `[nombre]` define una conexión:

```ini
[local1]
host=127.0.0.1
user=root
password=mi_contraseña
database=mi_base
port=3306

[produccion]
host=192.168.1.100
user=app_user
password=app_pass
database=prod_db
port=3306
```

Al llamar a cualquier tool puedes indicar qué conexión usar con el parámetro `"connection"` (por defecto `"local1"`).

### Tools `mysql_*` — referencia rápida

| Tool | Para qué sirve |
|---|---|
| `mysql_list_tables` | Lista todas las tablas de la BD |
| `mysql_table_info` | Estructura de columnas de una tabla |
| `mysql_query` | Ejecuta un SELECT y devuelve filas |
| `mysql_exec` | INSERT, UPDATE, DELETE, CREATE TABLE... |
| `mysql_insert` | Inserta una fila (`values`) o varias (`rows`) |
| `mysql_update` | Actualiza filas (requiere `where`) |
| `mysql_delete` | Elimina filas (requiere `where` o `confirm_all`) |
| `mysql_transaction` | Ejecuta varios SQL como una transacción |
| `mysql_create_table` | Crea una tabla a partir de una struct Harbour |
| `mysql_table_ops` | Acciones sobre tablas: listar, count, drop, truncate, rename... |
| `mysql_databases` | Listar, crear o eliminar bases de datos |
| `mysql_server_info` | Información del servidor: versión, charset, ping |
| `mysql_backup` | Exporta tablas a un fichero SQL de volcado |

### Tools `fwmaria_*` — referencia rápida

| Tool | Para qué sirve |
|---|---|
| `fwmaria_query` | SELECT con LIMIT automático |
| `fwmaria_exec` | DML/DDL arbitrario |
| `fwmaria_insert` | INSERT simple o batch; con opción upsert |
| `fwmaria_update` | UPDATE (requiere `where`) |
| `fwmaria_delete` | DELETE (requiere `where` o `confirm_all`) |
| `fwmaria_transaction` | Transacción multi-SQL con COMMIT/ROLLBACK automático |
| `fwmaria_server_info` | Versión, IsMariaDB, ping, charset |
| `fwmaria_databases` | Listar/crear/eliminar/seleccionar BD |
| `fwmaria_table_ops` | Acciones sobre tablas: listar, count, drop, truncate, rename... |
| `fwmaria_create_table` | Crear tabla desde struct Harbour |
| `fwmaria_backup` | Volcado SQL de tablas seleccionadas |
| `fwmaria_schema` | Columnas, índices, vistas y triggers de una tabla |
| `fwmaria_procedures` | Listar y llamar stored procedures y funciones SQL |
| `fwmaria_dbf` | Importar/exportar .dbf, copiar tablas, pivotes de datos |
| `fwmaria_alter` | Añadir, modificar, renombrar y eliminar columnas e índices |

### Ejemplos de uso desde el agente

```
Usa mysql_query para listar los 10 últimos pedidos de la tabla 'orders' en la conexion 'produccion'

Con fwmaria_insert inserta un cliente nuevo en la tabla 'clientes': nombre='Acme S.A.', ciudad='Madrid'

Usa fwmaria_schema action=columns table=facturas para ver la estructura de la tabla de facturas

Con fwmaria_procedures action=call name=sp_calcula_totales llama al procedimiento almacenado
```

### Cómo activar/desactivar estas tools

Desde el chat escribe `/tools` para abrir el selector de herramientas. Todas las tools de base de datos están en la categoría **GENERAL**. Puedes activarlas o desactivarlas individualmente sin necesidad de reiniciar.

---

## 25. Interfaces GUI de configuración

XDForCode incluye diálogos CRUD para gestionar visualmente todos los ficheros de configuración relevantes, sin necesidad de editar ficheros a mano. Todos están accesibles desde el menú **TOOLS**.

| Entrada en TOOLS | Fichero que gestiona | Función |
|---|---|---|
| Agente IA... | `XDForCodeUI.ini` | `AgentConfigDialog()` |
| API Keys... | (variables de entorno) | `ApiKeysDialog()` |
| Configure ACP... | (conexión ACP) | `ACPConfigDialog()` |
| Log ACP (diagnóstico) | `xdacp.log` | toggle `lAcpDebug` — registra todo el tráfico ACP |
| MCP Tools... | `mcp_tools.db` / `mcp_tools.json` | `MCPToolsDialog()` (requiere Modo Admin) |
| Skills... | `xdskills.json` | `SkillsDialog()` |
| MySQL Connections... | `mysql_shared.ini` | `MySQLConnectionsDialog()` |
| Inference Providers... | `xdinference.json` | `InferenceDialog()` |
| Folder Project Config... | `codegraph.json` | `CodeGraphConfigDialog()` |
| Terminal Apps & Agents... | `XDTermApps.ini` | `TermAppsDialog()` |
| Contraseña BD... | (cifrado SQLite) | `SQLCipherDialog()` |
| Configurar Puter... | `XDForCodeUI.ini [PUTER]` | `PuterConfigDialog()` |

### Agente IA (`XDForCodeUI.ini`)

Diálogo de configuración rápida del agente activo: modo de ejecución, ejecutable, proveedor, modelo, API key y opciones de ACP/HTTP. Equivale a configurar el agente desde el panel del chat, pero en un formulario GUI dedicado. Útil para cambiar la configuración antes de abrir el chat.

### API Keys

Gestiona las claves de API de los 16 proveedores soportados (Anthropic, OpenAI, Google, NVIDIA, GROQ, OpenRouter, Together, HuggingFace, Mistral, etc.). Cada clave se almacena en la variable de entorno correspondiente del proceso. Las claves se muestran enmascaradas; el botón **Mostrar** las revela temporalmente. Desde el chat también puedes establecer la clave activa con el comando `/key <clave>`.

### MySQL Connections (`mysql_shared.ini`)

Lista, añade, modifica y elimina conexiones MySQL/MariaDB compartidas por las tools MCP `mysql_*` y `fwmaria_*`.

- Columnas: Nombre · Host · Puerto · Base de datos · Usuario
- **Probar >** — menú desplegable con dos opciones: *Probar con FWMariaConnection* o *Probar con TDolphin*; muestra versión del servidor si la conexión es exitosa.

### Inference Providers (`xdinference.json`)

Gestiona los proveedores de IA en modo inferencia directa (NVIDIA, GROQ, OpenRouter, Together, HuggingFace, OLLAMA...) y sus modelos.

- **Panel superior** — proveedores: Nombre · Endpoint · Default · API Key (enmascarada)
- **Panel inferior** — modelos del proveedor seleccionado: Nombre · Tools · Default (`*`) · **Temp**; se actualiza al cambiar de proveedor
- **Set Default** — establece el modelo activo; al añadir el primer modelo a un proveedor nuevo queda automáticamente como default
- **Editar modelo** — diálogo expandido con campos de parámetros: Temperature · Top-P · Max tokens (nivel payload) + Num ctx · Top-K · Repeat penalty (sección `options`, específica de OLLAMA)

Cada modelo puede tener un bloque `params` opcional en `xdinference.json` con sus parámetros de inferencia:

```json
{
  "name": "qwen3:14b",
  "tools": true,
  "params": {
    "temperature": 0.6,
    "top_p": 0.9,
    "max_tokens": 8192,
    "options": { "num_ctx": 32768, "top_k": 40, "repeat_penalty": 1.1 }
  }
}
```

Los parámetros top-level se mezclan directamente en el payload; `options` se fusiona en `payload.options` (solo OLLAMA los usa).

### MCP Tools (`mcp_tools.db` / `mcp_tools.json`)

El CRUD completo de tools MCP está disponible en **TOOLS → MCP Tools...** (requiere **Modo Admin** activo, ver abajo). Permite editar nombre, descripción, categoría, parámetros, tags y código fuente de cada tool, además de exportar a JSON.

La fuente activa se controla desde **TOOLS → Fuente MCP tools**: `[ JSON ]` usa `mcp_tools.json`; `[ SQLite ]` usa `mcp_tools.db` (BD con FTS5 y bytecodes precompilados).

### Folder Project Config (`codegraph.json`)

Configura las carpetas que CodeGraph indexa: código fuente, documentos, bases de datos e imágenes.

- Combobox selector de sección: **Sources · Documents · Databases · Images**
- Columnas: Ruta · Etiqueta · Habilitado
- **Habilitar/Des.** — activa o desactiva un ítem sin eliminarlo (útil para excluir temporalmente una carpeta del índice)
- **Opciones...** — sub-diálogo para la ruta de la BD SQLite, `max_doc_size_kb` y `skip_dirs`
- Sub-diálogo de ítem: botón `...` para explorar carpeta, campo Extensions (una extensión por línea, p.ej. `*.prg`), campo Excludes (rutas o ficheros a omitir)

### Terminal Apps & Agents (`XDTermApps.ini`)

Gestiona las pestañas PTY dinámicas del panel de consola.

- Combobox selector de sección: **APPS · AGENTS · MCPSERVERS**
- Columnas: Nombre · Comando · Modo
- Campo **Modo**: `1`=auto al inicio · `0`=desactivado · `shell`=ShellExecute · `http://url[,1]`=WebView servidor

Las tres secciones del fichero `XDTermApps.ini` tienen propósitos distintos:

| Sección | Qué contiene |
|---|---|
| **APPS** | Aplicaciones PTY de propósito general (shells, herramientas, scripts) que se abren en el panel de consola. Ejemplos: PowerShell, Node REPL, un linter. |
| **AGENTS** | Agentes IA que se lanzan en una terminal PTY propia (opencode, mimo, etc.). El Kanban puede enviarles tareas directamente por teclado. Pueden escribir ficheros `.done` en `kanban_done/` para señalizar al orquestador que han terminado. |
| **MCPSERVERS** | Servidores MCP en modo stdio que XDForCode arranca automáticamente al inicio de la sesión y registra en la lista `mcpServers` de las sesiones ACP. Cada entrada es un proceso independiente que el agente puede usar como fuente de tools MCP. |

> **Nota:** Este diálogo gestiona las pestañas dinámicas de `XDTermApps.ini`. Las pestañas fijas del panel de consola (GIT, SSH, Console CLI, System Console, WhatsApp) se configuran desde **VIEW → Console Folder Tabs**.

### Modo Administrador

**TOOLS → "Modo Admin [ OFF ]"** — toggle sin persistencia que habilita funciones de administración:

| Estado | Efecto |
|---|---|
| **OFF** (defecto) | MCP Tools... deshabilitado en el menú |
| **ON** | Acceso completo a CRUD de tools MCP y otras funciones admin |

Al reiniciar la aplicación vuelve a OFF. No requiere contraseña (aún).

### Cifrado de bases de datos — SQLCipher AES-256

**TOOLS → Contraseña BD** — gestiona el cifrado AES-256 de todas las bases de datos SQLite del IDE mediante SQLCipher, sin depender de OpenSSL (usa la API BCrypt de Windows).

Bases de datos protegidas:
- `data/xdchat.db` — historial de chat
- `.codegraph/codegraph.db` — índice CodeGraph
- `mcp_tools.db` — herramientas MCP

| Opción | Acción |
|---|---|
| **Establecer contraseña** | Cifra todas las BDs con AES-256; pide confirmación |
| **Cambiar contraseña** | Recifra con la nueva contraseña sin perder datos |
| **Quitar contraseña** | Descifra todas las BDs (vuelven a ser SQLite estándar) |

Al establecer una contraseña, XDForCode la pedirá cada vez que arranque. Si la contraseña es incorrecta, el IDE inicia pero sin acceso al historial ni al índice CodeGraph.

---

## 26. Dashboard — Panel de Estado en Tiempo Real

El Dashboard (`TOOLS → Dashboard` o botón **DASHBOARD** en la pantalla de inicio) muestra en tiempo real el estado completo del IDE en un panel de tarjetas. Se renderiza en el mismo panel del editor Monaco, sin abrir ventanas adicionales.

### Tarjetas disponibles

| Tarjeta | Qué muestra |
|---|---|
| **Web Server** | Estado del servidor (activo/inactivo) y puerto |
| **AI Mode** | Modo activo, modelo, ejecutable y proveedor configurado |
| **MCP Tools** | Número de tools disponibles y cuáles están activas |
| **Skills** | Skills cargadas y cuáles están activadas en la sesión |
| **Inference Providers** | Lista de proveedores con sus modelos y API key configurada |
| **Remote Users** | Usuarios del chat remoto con su configuración individual |
| **Agents** | Agentes activos (pestañas abiertas), estado y tarea actual |
| **Kanban Plan** | Resumen del plan activo: tareas por estado |
| **Terminal Apps** | Apps/agentes definidos en `XDTermApps.ini` y su estado |
| **PTY** | Terminales activos y sus procesos |
| **Project** | Carpeta de trabajo, fichero activo y nombre del proyecto |

El Dashboard actualiza los datos cada vez que se abre (no hace polling continuo). Es especialmente útil para hacer un diagnóstico rápido del estado del sistema antes de lanzar un plan Kanban.

---

## 27. API REST Local Integrada

XDForCode incorpora de forma nativa un servidor HTTP embebido (basado en CivetWeb) que, además de servir el chat remoto, provee una API REST completa en la ruta `/xd/v12/` para permitir controlar el motor de IA desde fuera del IDE (por ejemplo, desde otras aplicaciones, scripts de automatización o llamadas `curl`).

### Autenticación
Todos los endpoints requieren un **Token de Seguridad (Bearer)**. 
- Enviar por cabecera: `Authorization: Bearer <token>`
- En pruebas iniciales, usa el token configurado en tu IDE o base de datos.
- A nivel del wrapper en C, CivetWeb protege adicionalmente las conexiones WebSocket exigiendo el token, y rechaza los frames de datos que no lo incluyan, ofreciendo un escudo frente a ataques masivos.

### Endpoints Disponibles

Todos los endpoints base están en `http://127.0.0.1:8008/xd/v12/` (el puerto puede variar según tu configuración):

| Endpoint | Método | Acción | Parámetros (JSON Body) |
|---|---|---|---|
| `/help` | GET | Lista de rutas disponibles en el API | - |
| `/status` | GET | Estado actual del motor (mode, provider, model) | - |
| `/mode` | GET | Obtiene el modo activo actualmente | - |
| `/mode/inference` | POST | Cambia el motor de IA al modo Inference | - |
| `/mode/ollama` | POST | Cambia el motor de IA al modo Ollama | - |
| `/mode/opencode_acp` | POST | Cambia el motor de IA al modo OpenCode ACP | - |
| `/providers` | GET | Devuelve la lista de proveedores disponibles | - |
| `/provider` | POST | Establece el proveedor activo para Inference | `{"provider": "NVIDIA"}` |
| `/models` | GET | Devuelve la lista de modelos del proveedor activo | - |
| `/model` | POST | Establece el modelo activo a usar | `{"model": "gemma4"}` |
| `/prompt` | POST | Envía un mensaje a la IA y espera la respuesta | `{"prompt": "Escribe un hola mundo"}` |

### Aislamiento de Estado

Cuando haces una petición a cualquier endpoint que altera el estado (como `/model` o `/provider`), **la API realiza una copia de seguridad** del estado de tu IDE. Modifica la configuración en memoria de Harbour exclusivamente para procesar tu petición, y al finalizar la restaura (a través de las funciones `XD_ApiSaveMode()` y `XD_ApiRestoreMode()`). 

De esta forma, puedes automatizar llamadas por detrás sin que afecte en absoluto a la conversación o modelo que tengas activo en el panel de chat del IDE.

### Herramienta de Testing Integrada

Puedes probar todos estos endpoints directamente desde dentro de XDForCode sin necesidad de usar herramientas externas como Postman:
1. Ve al menú **TESTS** de la barra superior.
2. Selecciona **Test API REST local**.
3. Se abrirá un diálogo con estilo visual integrado donde podrás seleccionar el endpoint desde un desplegable (se autorellena interrogando a CivetWeb), meter tu token, especificar un JSON en el Body y ver la respuesta.
4. Internamente este diálogo utiliza la librería `libcurl` nativa de Harbour para realizar las llamadas (GET/POST automáticos) en lugar de depender de ejecutables externos de Windows.

*XDForCode — XDEVFORYOU SOLUTIONS · 2026*

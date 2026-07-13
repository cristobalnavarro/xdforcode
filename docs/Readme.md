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

---

## 1. ¿Qué es XDForCode?

XDForCode es un entorno de desarrollo integrado (IDE) para Windows con apariencia y funcionamiento similar a VS Code. Está diseñado especialmente para desarrolladores **Harbour / FiveWin**, aunque puede editar cualquier tipo de fichero.

Su característica principal es la **integración nativa con agentes de IA**: puedes conversar directamente con Claude, Gemini, OpenCode, Ollama y otros desde dentro del propio IDE, sin salir de la aplicación, con acceso al código que estás editando.

**Características principales:**

- Editor de código Monaco (el mismo que usa VS Code) con soporte Harbour/FiveWin
- Panel de chat con agentes de IA en el sidebar derecho
- Múltiples terminales integradas (Git, SSH, consola del sistema)
- Kanban para lanzar y coordinar varios agentes IA en paralelo
- Sistema de build completo con toolchains y gestión de proyectos
- Servidor web embebido para acceso remoto desde el navegador
- Skills reutilizables con múltiples tipos (acciones, contexto, plantillas, reglas)
- Preview HTML en vivo en el sidebar izquierdo
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

Conecta directamente con APIs OpenAI-compatible (NVIDIA, GROQ, OpenRouter, Together, HuggingFace) sin necesidad de instalar agentes externos. Usa hbcurl nativo de Harbour con streaming SSE.

**Configuración:** Edita el fichero `xdinference.json` junto al ejecutable para añadir providers y modelos. Cada provider necesita su endpoint y API key.

**Providers preconfigurados:**
- **NVIDIA** — modelos Nemotron, Llama, DeepSeek, Qwen
- **GROQ** — modelos Llama, DeepSeek, Gemma, Mixtral
- **OpenRouter** — acceso a Claude, GPT-4o, Gemini y otros
- **Together** — Llama, DeepSeek, Qwen, Mistral
- **HuggingFace** — amplia variedad de modelos open source

> El modo Inference es ideal para usar modelos potentes sin instalar agentes CLI, solo necesitas una API key.

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

Algunos de los comandos más habituales:

| Comando | Acción |
|---|---|
| `/help` | Muestra la ayuda completa del chat y los comandos disponibles |
| `/mode` | Cambiar el agente o modo activo |
| `/ollama` | Listar y cambiar modelos de Ollama |
| `/clear` | Limpiar el historial del chat |
| `/skill` | Insertar una skill en el mensaje |
| `/provider` | Cambiar el provider de inference |
| `/model` | Cambiar el modelo activo |

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

### Historial

El historial de la conversación se mantiene durante la sesión. Cada mensaje nuevo se envía junto con el contexto de los mensajes anteriores.

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

---

## 9. Skills — tipos y uso avanzado

Las **Skills** son fragmentos de texto predefinidos que puedes insertar en tus mensajes para dar contexto, instrucciones o plantillas al agente.

### Tipos de skills

| Tipo | Comportamiento |
|---|---|
| **action** | Se inserta como prefijo del prompt con una tarea concreta |
| **system** | Se envía como system prompt permanente para toda la conversación |
| **context** | Carga conocimiento desde ficheros locales o URLs y lo inyecta como contexto |
| **template** | Sustituye `{message}` con el texto del usuario. Útil para flujos guiados |
| **modifier** | Modifica el estilo de la respuesta (tono, idioma, formato) |
| **rule** | Regla obligatoria de codificación que el agente debe seguir |

### Skills predefinidas

| Skill | Tipo | Descripción |
|---|---|---|
| `explain` | action | Explica el código activo paso a paso |
| `findbugs` | action | Busca bugs y problemas en el código |
| `refactor` | action | Propone refactorización del código |
| `test` | action | Genera tests unitarios |
| `docstring` | action | Genera documentación para la selección |
| `formal` | modifier | Responde en tono técnico y formal |
| `concise` | modifier | Responde de forma concisa y directa |
| `harbour` | context | Contexto del proyecto Harbour + FiveWin |
| `harbour-locals` | rule | Reglas de declaración de variables en Harbour |
| `harbexpert` | system | Consulta el repositorio oficial de Harbour antes de responder |
| `fivexpert` | system | Consulta la instalación de FiveWin (C:\fwh) antes de responder |
| `XDForCode` | context | Carga el doc de referencia de XDForCode y el README como base de conocimiento |

### Cómo usarlas

1. Escribe `/skills` en el cuadro de mensaje o usa el botón de Skills en el panel.
2. Aparece la lista de skills disponibles.
3. Activa las que quieras: permanecen activas en todos los mensajes hasta que las desactives.

### Gestionar Skills (diálogo CRUD)

Desde el menú puedes abrir el diálogo de gestión de Skills para añadir, modificar o eliminar skills de forma visual. Las skills se guardan en el fichero `xdskills.json`.

### Skills tipo context: conocimiento externo

Las skills de tipo `context` pueden cargar contenido desde:

- **Ficheros locales**: rutas absolutas o relativas al directorio de la aplicación.
- **URLs remotas**: contenido descargado vía HTTP (se eliminan los tags HTML automáticamente).

El contenido se inyecta automáticamente en el **system prompt** de cada mensaje mientras el skill está activo, sin necesidad de adjuntar nada manualmente. Para forzar la recarga del contenido del disco usa `/context clear`.

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

### Casos de uso típicos

- Lanzar un agente que refactoriza el código mientras otro escribe los tests.
- Pedir a tres agentes distintos (Claude, Gemini, Ollama) que respondan a la misma pregunta y comparar resultados.
- Dejar tareas largas corriendo en segundo plano mientras trabajas en otra cosa.
- Crear flujos de trabajo encadenados donde cada paso usa el resultado del anterior.
- Repetir el mismo prompt en varias tareas para aplicar una instrucción a múltiples ficheros.

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
El historial de la sesión actual se mantiene mientras la aplicación está abierta. Al cerrar la aplicación, el historial no se persiste por defecto.

**¿Puedo usar XDForCode sin conexión a internet?**  
Sí, siempre que uses **Ollama** como agente o el modo **Inference** con un provider que no requiera autenticación. El resto de agentes requieren conexión para conectarse a sus APIs en la nube.

**¿Qué ocurre si el agente tarda mucho?**  
Puedes cancelar la respuesta en cualquier momento con el botón **Cancelar** del panel de chat. El agente se detiene y puedes volver a escribir.

**¿Qué es el modo Inference?**  
Es un modo de conexión directa a APIs OpenAI-compatible (NVIDIA, GROQ, OpenRouter, etc.) sin necesidad de instalar agentes externos. Solo necesitas configurar una API key en `xdinference.json`.

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

### 21.4 ¿Cómo utilizan la IA el proyecto indexado?

Una vez que el proyecto y los documentos están indexados, los agentes integran herramientas (*tools*) que se conectan en tiempo real a esta base de datos local.

- **Para tu código**: Si le pides a la IA "Busca dónde se usa la función Facturar()", la IA no intentará leer tus 500 archivos `.prg`. Consultará la base de datos y sabrá en milisegundos la línea exacta, quién la llama y a quién llama.
- **Clasificación por Importancia (PageRank interno)**: Al buscar en el código, el sistema utiliza un algoritmo de *In-Degree Centrality*. Esto significa que cuando el agente busca código, los resultados se ordenan devolviendo primero aquellos ficheros y funciones que son más llamados por el resto del proyecto. ¡El código más crítico siempre aparece primero!
### 21.5 Exploración Visual del Grafo

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

*XDForCode — XDEVFORYOU SOLUTIONS · 2025–2026*

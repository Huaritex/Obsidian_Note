# 🪝 Hook and the SDK

> [!important] Los hooks permiten ejecutar comandos antes o después de que Claude intente ejecutar una herramienta. Son increíblemente útiles para implementar flujos de trabajo automatizados, como ejecutar formateadores de código después de editar archivos, ejecutar pruebas cuando se modifican archivos o bloquear el acceso a archivos específicos.

![[Pasted image 20260313143249.png]]

---

## ⚙️ How Hooks Work

> [!info] Para entender los hooks, primero revisemos el flujo normal al interactuar con Claude Code. Cuando le haces una pregunta a Claude, tu consulta se envía al modelo de Claude junto con las definiciones de las herramientas. Claude puede decidir usar una herramienta proporcionando una respuesta formateada, y luego Claude Code ejecuta esa herramienta y devuelve el resultado.

- 🔹 Los hooks se insertan en este proceso, lo que te permite ejecutar código justo antes o justo después de que se ejecute la herramienta.

```mermaid
sequenceDiagram
    participant U as Usuario
    participant C as Claude Code
    participant Pre as PreToolUse Hook
    participant T as Herramienta
    participant Post as PostToolUse Hook

    U->>C: Petición
    C->>Pre: Decisión de usar herramienta
    Pre-->>C: Permite o Bloquea
    C->>T: Ejecuta Herramienta (si se permite)
    T-->>C: Resultado de Herramienta
    C->>Post: Se ejecuta post-herramienta
    Post-->>C: Fin de ejecución post-herramienta
    C->>U: Respuesta Final
```

![[Pasted image 20260313142356.png]]

- Existen dos tipos de ganchos:

1. **Ganchos PreToolUse:** Se ejecutan *antes* de que se llame a una herramienta.
2. **Ganchos PostToolUse:** Se ejecutan *después* de que se llame a una herramienta.

---

## 🔧 Hook Configuration

> [!note] Los hooks se definen en los archivos de configuración de Claude. Puedes agregarlos a:

- **Global:** `~/.claude/settings.json` (afecta a todos los proyectos)
- **Proyecto:** `.claude/settings.json` (compartido con el equipo)
- **Proyecto (no confirmado):** `.claude/settings.local.json` (configuración personal)

> [!tip] Puedes escribir los hooks manualmente en estos archivos o usar el comando `/hooks` dentro de Claude Code.

![[Pasted image 20260313142712.png]]

- 🔹 La estructura de configuración incluye dos secciones principales:

![[Pasted image 20260313142741.png]]

---

## 🛑 Ganchos PreToolUse

> [!abstract] Los ganchos PreToolUse se ejecutan antes de que se ejecute una herramienta. Incluyen un comparador que especifica a qué tipos de herramientas se debe aplicar:

```json
"PreToolUse": [
  {
    "matcher": "Read",
    "hooks": [
      {
        "type": "command",
        "command": "node /home/hooks/read_hook.ts"
      }
    ]
  }
]
```

> [!quote] Antes de ejecutar la herramienta «Leer», esta configuración ejecuta el comando especificado. Su comando recibe detalles sobre la llamada a la herramienta que Claude desea realizar, y usted puede:

- ✅ Permitir que la operación se ejecute con normalidad
- ❌ Bloquear la llamada a la herramienta y enviar un mensaje de error a Claude

---

## 🔄 Ganchos PostToolUse

> [!abstract] Los ganchos PostToolUse se ejecutan después de que se haya ejecutado una herramienta. Aquí hay un ejemplo que se activa después de operaciones de escritura, edición o edición múltiple:

```json
"PostToolUse": [
  {
    "matcher": "Write|Edit|MultiEdit",
    "hooks": [
      {
        "type": "command", 
        "command": "node /home/hooks/edit_hook.ts"
      }
    ]
  }
]
```

> [!quote] Dado que la llamada a la herramienta ya se ha producido, los ganchos PostToolUse no pueden bloquear la operación. Sin embargo, sí pueden:

- 🛠️ Ejecutar operaciones posteriores (como formatear un archivo que acaba de editarse)
- 📊 Proporcionar información adicional a Claude sobre el uso de la herramienta

![[Pasted image 20260313143018.png]]

---

## 💡 Aplicaciones Practicas

- 🔹 Aquí tienes algunas formas comunes de usar los hooks:

- **Formato de código:** Formatea automáticamente los archivos después de que Claude los edite.
- **Pruebas:** Ejecuta pruebas automáticamente cuando se modifican archivos.
- **Control de acceso:** Impide que Claude lea o edite archivos específicos.
- **Calidad del código:** Ejecuta analizadores de código o verificadores de tipos y proporciona retroalimentación a Claude.
- **Registro de eventos:** Registra los archivos a los que Claude accede o modifica.
- **Validación:** Comprueba las convenciones de nomenclatura o los estándares de codificación.

> [!summary] La clave está en que los hooks te permiten ampliar las capacidades de Claude Code integrando tus propias herramientas y procesos en el flujo de trabajo. Los hooks PreToolUse te dan control sobre lo que Claude puede hacer, mientras que los hooks PostToolUse te permiten mejorar lo que Claude ha hecho.

---

# 🪝 Definiendo Hooks

> [!info] Los hooks en Claude Code permiten interceptar y controlar las llamadas a las herramientas antes o después de su ejecución. Esto proporciona un control preciso sobre lo que Claude puede y no puede hacer en tu entorno de desarrollo.

---

## 🛠️ Construyendo el Hook

> [!tip] La creación de un gancho implica cuatro pasos principales:

![[Pasted image 20260313145915.png]]

```mermaid
flowchart TD
    A["1. Decidir Tipo de Hook"] --> B["2. Monitorizar Herramientas"]
    B --> C["3. Escribir Comando"]
    C --> D["4. Informar a Claude"]
```

1. **Decide si usarás un hook PreToolUse o PostToolUse:** los hooks PreToolUse impiden la ejecución de llamadas a herramientas, mientras que los PostToolUse se ejecutan después de que la herramienta ya se haya utilizado.
2. **Determina qué tipo de llamadas a herramientas quieres monitorizar:** debes especificar exactamente qué herramientas deben activar tu hook.
3. **Escribe un comando que reciba la llamada a la herramienta:** este comando obtiene datos JSON sobre la llamada propuesta a través de la entrada estándar.
4. **Si es necesario, el comando debe proporcionar información a Claude:** el código de salida del comando le indica a Claude si debe permitir o bloquear la operación.

---

## 🧰 Herramientas Disponibles

> [!note] Claude Code ofrece varias herramientas integradas que puedes monitorizar mediante hooks:

![[Pasted image 20260313150101.png]]

> [!quote] Para ver exactamente qué herramientas están disponibles en tu configuración actual, puedes solicitarle una lista directamente a Claude. Esto es especialmente útil, ya que las herramientas disponibles pueden cambiar al agregar servidores MCP personalizados.

---

## 📦 Estructura de Datos de la llamada de la Herramienta

> [!abstract] Cuando se ejecuta el comando de enlace, Claude envía datos JSON a través de la entrada estándar con detalles sobre la llamada a la herramienta propuesta:

![[Pasted image 20260313150204.png]]

```json
{
  "session_id": "2d6a1e4d-6...",
  "transcript_path": "/Users/sg/...",
  "hook_event_name": "PreToolUse",
  "tool_name": "Read",
  "tool_input": {
    "file_path": "/code/queries/.env"
  }
}
```

> [!info] Tu comando lee este JSON de la entrada estándar, lo analiza y luego decide si permite o bloquea la operación según el nombre de la herramienta y los parámetros de entrada.

---

## 🚦 Codigo de Salida y Flujo de Control

> [!abstract] Tu comando de enlace se comunica con Claude mediante códigos de salida:

![[Pasted image 20260313150321.png]]

```mermaid
flowchart LR
    A{"Código de Salida"}
    A -- Código 0 --> B["✅ Se permite continuar"]
    A -- Código 2 --> C["❌ Se bloquea la llamada"]
    
    style C stroke:#f66,stroke-width:2px,stroke-dasharray: 5 5
```

- 🟢 **Código de salida 0:** Todo está correcto, se permite que la llamada a la herramienta continúe.
- 🔴 **Código de salida 2:** Se bloquea la llamada a la herramienta (solo en hooks PreToolUse).

> [!warning] Al salir con el código 2 en un hook PreToolUse, cualquier mensaje de error que se escriba en la salida de error estándar se enviará a Claude como retroalimentación, explicando por qué se bloqueó la operación.

---

## 🎯 Ejemplo de Caso de Uso

> [!example] Un caso de uso común es impedir que Claude lea archivos confidenciales como los archivos `.env`. Dado que tanto la herramienta `Read` como la herramienta `Grep` pueden acceder al contenido de los archivos, conviene monitorizar ambas y comprobar si intentan acceder a rutas de archivo restringidas.

> [!summary] Este enfoque proporciona un control total sobre el acceso de Claude al sistema de archivos, a la vez que ofrece información clara sobre por qué se restringen ciertas operaciones.

---

# Defining Hooks

-> Downloads
queries: https://cc.sj-cdn.net/instructor/4hdejjwplbrm-anthropic/assets/1773097175/queries.zip?response-content-disposition=attachment&Expires=1774453770&Signature=fvZab4qg~VZiRm2-l7B22E6mSLz1GVt3ESlkzW~Qv1hh2FgUI1mLJDhnzsMTJBsdSA4floHVp~aAJ07HAHcbJ8W-2ZgXa2eBzWTAyTdpgk5oc1L2wfIcHU60Ibxp0PygviLhYWS2L5up7wX3vFCdboHCv9FYHlKdFrfy8VLhyc5i1Gxtxg7Hy57DdvfbLJk79r3e8H9NzHHwiOVbuyIKxWQbFOJYeoK6HoGVBuYAwxmT0az5UWgDs8zdcG4AP6Eq9JQ~r9WlaMNYITsCqSkJ7kSmrLTFwelr5QPI772MdSd-StixydW7Yr0r0aussTiOQZzacxD6YrhsASFNp7QCDw__&Key-Pair-Id=APKAI3B7HFD2VYJQK4MQ

queries_completed: https://cc.sj-cdn.net/instructor/4hdejjwplbrm-anthropic/assets/1773097185/queries_COMPLETED.zip?response-content-disposition=attachment&Expires=1774453770&Signature=fGNLgSoDpQ2jDwI5021QQM1AMFsEilYs~qAPStmc2Pbkf3NYhte4iYNxoCtHw6tQ6hP256TPoh5w~KduAYdOc9o4Bf3p~UFswzRFaeOKK~iCjDSwxPcf-nHTNvxx5msq1kpuOFAkc~ka~Bxhem-aIdRRCaQS7rWw0mU7sxZY~UufsHvj8I3kiRQMh-0E-gVZ48ATCVlBiVYGv1jRVwAmk0vLMQvhdk-O7Iy4YnR7yWekBcIjIj2156K1PdDlXbYVTUFQsv1TVX9Boi8STgJw4B-kotGEzP0ry5vcGtJ~WYfpsT9wW9s1nnHnDoo41fbNsFv4C1x~i6FnnYR1EleSVg__&Key-Pair-Id=APKAI3B7HFD2VYJQK4MQ



> Los hooks en Claude Code permiten interceptar y controlar las llamadas a las herramientas antes o después de su ejecución. Esto proporciona un control preciso sobre lo que Claude puede y no puede hacer en tu entorno de desarrollo.

## Building a Hook

La creación de un gancho implica cuatro pasos principales:

![[Pasted image 20260325105458.png]]

1. Decide si usarás un hook PreToolUse o PostToolUse: los hooks PreToolUse impiden la ejecución de llamadas a herramientas, mientras que los PostToolUse se ejecutan después de que la herramienta ya se haya utilizado.
2. Determina qué tipo de llamadas a herramientas quieres monitorizar: debes especificar exactamente qué herramientas deben activar tu hook.
3. Escribe un comando que reciba la llamada a la herramienta: este comando obtiene datos JSON sobre la llamada propuesta a través de la entrada estándar.
4. Si es necesario, el comando debe proporcionar información a Claude: el código de salida del comando le indica a Claude si debe permitir o bloquear la operación.

### Herramientas Disponibles

> Claude Code ofrece varias herramientas integradas que puedes monitorizar mediante hooks:

![[Pasted image 20260325105615.png]]

To see exactly which tools are available in your current setup, you can ask Claude directly for a list. This is especially useful since the available tools can change when you add custom MCP servers.

## Estructura de Datos de la llamada a la herramienta

> Cuando se ejecuta el comando de enlace, Claude envía datos JSON a través de la entrada estándar con detalles sobre la llamada a la herramienta propuesta:

![[Pasted image 20260325105749.png]]

```json
{
  "session_id": "2d6a1e4d-6...",
  "transcript_path": "/Users/sg/...",
  "hook_event_name": "PreToolUse",
  "tool_name": "Read",
  "tool_input": {
    "file_path": "/code/queries/.env"
  }
}
```

> Tu comando lee este JSON desde la entrada estándar, lo analiza y luego decide si permite o bloquea la operación en función del nombre de la herramienta y los parámetros de entrada.

## Codigo de Salida y flujo de Control

> Tu comando de enlace se comunica con Claude mediante códigos de salida:

![[Pasted image 20260325105936.png]]

- Código de salida 0: Todo está correcto, se permite que la llamada a la herramienta continúe.
- Código de salida 2: Se bloquea la llamada a la herramienta (solo para los hooks PreToolUse).

> Cuando finalizas con el código 2 en un gancho PreToolUse, cualquier mensaje de error que escribas en el error estándar se enviará a Claude como retroalimentación, explicando por qué se bloqueó la operación.

## Ejemplo de Caso de Uso

> Un caso de uso común es impedir que Claude lea archivos confidenciales como los archivos .env. Dado que tanto la herramienta Read como la herramienta Grep pueden acceder al contenido de los archivos, conviene monitorizar ambas y comprobar si intentan acceder a rutas de archivo restringidas. Este enfoque proporciona un control total sobre el acceso de Claude al sistema de archivos, a la vez que ofrece información clara sobre por qué se restringen ciertas operaciones.

---

# Implementando Hook

> Vamos a crear un hook personalizado para evitar que Claude lea archivos confidenciales como .env. Este es un ejemplo práctico de cómo los hooks pueden proteger tus variables de entorno y otros datos confidenciales durante las sesiones de desarrollo.


## Configuracion del Hook

> Primero, debemos configurar nuestro hook en el archivo de configuración. Abre el archivo .claude/settings.local.json y localiza la sección de hooks. Crearemos un hook llamado PreToolUse, ya que queremos interceptar las llamadas a las herramientas antes de que se ejecuten.

-> La configuracion requiere dos elementos clave:

- `Matcher`: especifica qué herramientas se deben monitorizar.
- `Command`: el script que se ejecuta cuando se llaman esas herramientas.

>[!note] Para el matcher, queremos capturar tanto las operaciones de lectura como las de `grep` que puedan acceder al archivo `.env`.

```json
"matcher": "Read|Grep"
```

> The pipe symbol (|) acts as an OR operator, so this will trigger on either tool. For the command, we'll point to a Node.js script:

```json
"command": "node ./hooks/read_hook.js"
```

## Compresion de los datos de las llamadas a herramientas

> Cuando Claude intenta usar una herramienta, su script de enlace recibe información detallada sobre esa llamada a través de la entrada estándar en formato JSON. Estos datos incluyen:

- ID de sesión y ruta de la transcripción
- Nombre del evento del script de enlace (PreToolUse en nuestro caso)
- Nombre de la herramienta (Read, Grep, etc.)
- Parámetros de entrada de la herramienta, incluida la ruta del archivo

Su script de enlace procesa estos datos y puede permitir que la operación continúe o bloquearla finalizando con un código específico.

## Implementacion del Scrip enlace

> El script de enlace debe leer los datos de la llamada a la herramienta desde la entrada estándar y comprobar si Claude está intentando acceder al archivo .env. Esta es la lógica principal:

```
async function main() {
  const chunks = [];
  for await (const chunk of process.stdin) {
    chunks.push(chunk);
  }
  
  const toolArgs = JSON.parse(Buffer.concat(chunks).toString());
  
  // Extract the file path Claude is trying to read
  const readPath = 
    toolArgs.tool_input?.file_path || toolArgs.tool_input?.path || "";
  
  // Check if Claude is trying to read the .env file
  if (readPath.includes('.env')) {
    console.error("You cannot read the .env file");
    process.exit(2);
  }
}
```

> El script comprueba si existe la extensión .env en la ruta del archivo y bloquea la operación si la encuentra. Al salir con el código 2, Claude recibe un mensaje de error y comprende que la operación fue bloqueada por un gancho.

## Probar Hooks

- Tras guardar la configuración y el script del hook, reinicia Claude Code para que los cambios surtan efecto. A continuación, pruébalo pidiéndole a Claude que lea tu archivo .env.

- Cuando Claude intente leer el archivo, tu hook lo interceptará y devolverá un mensaje de error. Claude reconocerá que la operación se ha bloqueado y te lo explicará, indicando a menudo que un hook de lectura ha impedido el acceso al archivo.

- Esta misma protección funciona con las operaciones de grep: si Claude intenta buscar dentro del archivo .env, el hook también lo bloqueará.

## Beneficios Clave 

-> Este enfoque ofrece varias ventajas:

- Protección proactiva: bloquea el acceso antes de que se lean datos confidenciales.
- Funcionamiento transparente: Claude comprende por qué falló la operación.
- Coincidencia flexible: funciona con múltiples herramientas (read, grep, etc.).
- Información clara: proporciona mensajes de error significativos.

Si bien este ejemplo se centra en los archivos .env, el mismo patrón puede proteger cualquier archivo o directorio confidencial de su proyecto. Puede ampliar la lógica para verificar patrones de múltiples archivos o implementar controles de acceso más sofisticados según sus requisitos de seguridad.


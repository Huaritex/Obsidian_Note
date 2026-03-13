# 🤖 Como son los asistentes de Flujo

> [!quote] Cuando le asignas una tarea a un asistente de programacion, como corregir un error basandome en un mensaje de fallo, este sigue el proceso similar al que seguria un desarrollador humano para abordar el problema:

![[Pasted image 20260305114451.png]]

---

## 🔧 Tool Use

> [!info] Instrucciones al Modelo
> A los modelos se les dan instrucciones en texto plano sobre como responder de cierta manera para utilizar la **herramienta**.

> [!note] Cuando el Modelo responde con una solicitud para usar la herramienta, el asistente de programacion hace lo que se supone que debe hacer una herramienta (Leer archivo, escribir un archivo, realizar una solicitud, etc).

> [!summary] Capacidad de Claude
> La serie de modelos Claude (Opus, Sonnet, Haiku) es particularmente sólida a la hora de comprender qué hacen las herramientas y utilizarlas para completar tareas.

```mermaid
flowchart LR
    User([👤 Usuario]) -->|Pide una tarea| Claude{🤖 Claude}
    Claude -->|Decide usar herramienta| Tool[⚙️ Herramienta ej. Leer archivo]
    Tool -->|Resultado| Claude
    Claude -->|Respuesta Final| User
```

![[Pasted image 20260305112648.png]]

---

## 🌟 El uso de Herramientas lo es todo

> [!tip] La fortaleza en el uso de herramientas permite obtener beneficios unicos (e inesperados)

### 📈 Claude Code puede abordar tareas mas dificiles

- 🔹 `Claude combinara con entusiasmo` diferentes herramientas para manejar trabajos mas complejos
- 🔹 `Claude utilizara con destreza` herramientas que no haya visto antes.

### 🧩 Claude Code es Extendible

- 🔹 `Puedes Agregar facilmente herramientas adicionales` (Capacidades) de Claude Code
- 🔹 `La adicion de Herramientas permite la personalizacion` para tu flujo de trabajo particular.
- 🔹 `Agregar herramientas permite que Claude Code se mantenga al dia` con los rapidos cambios en el desarrollo habilitado por IA.

### 🛡️ Seguridad Mejorada

- 🔹 `Gracias al solido uso de herramientas de Claude` , Claude Code puede navegar facilmente por las bases de codigo
- 🔹 `Claude Code no depende de la indexacion de tu base de codigo`, lo que a menudo requiere enviar toda tu base de codigo a servidores externos.

---

## 📝 Re-Cap (Resumen)

> [!check] Conceptos Clave
>
> - Los asistentes de programación utilizan modelos de lenguaje para completar diferentes tareas.
> - Los modelos de lenguaje necesitan utilizar herramientas para realizar la gran mayoría de las tareas.
> - No todos los modelos de lenguaje utilizan las herramientas con la misma destreza.
> - **El sólido uso de herramientas de Claude con Claude Code permite una mejor seguridad, personalización y longevidad**.

```mermaid
mindmap
  root((Claude Code))
    Seguridad Mejorada
      Navegacion Local
      Sin Indexacion Externa
    Capacidad Extendible
      Nuevas Herramientas
      Flujos Personalizados
    Tareas Complejas
      Combina Herramientas
      Uso de Herramientas Nuevas
```

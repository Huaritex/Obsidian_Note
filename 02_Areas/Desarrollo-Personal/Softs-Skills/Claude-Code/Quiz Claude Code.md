---
tags: ["quiz", "claude", area]
---

# 📝 Quiz: Autoevaluación de Claude Code

> [!important] Pon a prueba tu comprensión técnica sobre Claude Code. Cada pregunta está diseñada para reforzar conceptos de arquitectura y flujo de trabajo.

---

### ❓ Pregunta 1: Capacidades del Modelo
![[Pasted image 20260305112648.png]]
**¿Por qué los LLM necesitan herramientas externas?**
> [!success] Respuesta
> Los modelos de lenguaje solo pueden procesar texto de entrada/salida. Para interactuar con el mundo real (leer archivos, ejecutar tests), necesitan una interfaz que ejecute acciones en su nombre.

---

### ❓ Pregunta 2: Seguridad y Permisos MCP
![[Pasted image 20260305134132.png]]
**¿Cómo se gestionan los permisos para un servidor MCP en un pipeline de CI/CD (GitHub Actions)?**
> [!success] Respuesta
> A diferencia del modo local, en GitHub Actions **cada herramienta de cada servidor MCP debe listarse individualmente** en la configuración de permisos permitidos.

---

### ❓ Pregunta 3: Modos de Operación
![[Pasted image 20260305114451.png]]
**¿Cuál es la diferencia principal entre el modo "Plan" y el modo "Thinking"?**
> [!success] Respuesta
> El modo **Plan** gestiona la amplitud (tareas de múltiples pasos), mientras que el modo **Thinking** gestiona la profundidad (lógica compleja y razonamiento interno).

---

### ❓ Pregunta 4: Jerarquía de Configuración
![[Pasted image 20260305130705.png]]
**Ordena los niveles de configuración de Claude Code:**
> [!success] Respuesta
> 1. **Project level:** Compartido con el equipo, se sube al repo (`.claude/settings.json`).
> 2. **Local level:** Personal, no se sube (`.claude/settings.local.json`).
> 3. **Machine level:** Global para todos los proyectos del usuario.

---

### ❓ Pregunta 5: Comandos Personalizados
![[Pasted image 20260305132223.png]]
**¿Cómo se pasan argumentos variables a un comando personalizado?**
> [!success] Respuesta
> Incluyendo el marcador de posición `$ARGUMENTS` dentro del archivo Markdown que define el comando.

---

### ❓ Pregunta 6: Ciclo de Vida de Herramientas
![[Pasted image 20260305115011.png]]
**¿Qué tipo de Hook usarías para bloquear el acceso a un archivo sensible antes de que Claude lo lea?**
> [!success] Respuesta
> Un **PreToolUse hook**.

---

### ❓ Pregunta 7: Aplicación Práctica de Hooks
![[Pasted image 20260305115719.png]]
**Si queremos evitar que Claude lea variables de entorno, ¿qué herramientas debemos monitorizar?**
> [!success] Respuesta
> Se debe usar un **PreToolUse hook** que monitoree las herramientas `Read` y `Grep`.

---
**Volver a:** [[Claude-Code]]

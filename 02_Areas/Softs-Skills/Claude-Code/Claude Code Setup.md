---
tags: ["setup", "claude-code", "tutorial"]
fecha_creacion: 2026-03-06
relaciones: ["[[Claude-Code]]"]
---

# 🛠️ Configurar Claude Code

> [!info] Documentación Oficial
> Las instrucciones de configuración completas se pueden encontrar aquí: [Install Claude Code (Quickstart)](https://code.claude.com/docs/en/quickstart)

---

## 🚀 Instalación de Claude Code

Sigue el comando correspondiente a tu sistema operativo para instalar `Claude Code`:

### 🍏 Mac

```shell
brew install --cask claude-code
```

### 🐧 Linux y WSL

```shell
curl -fsSL https://claude.ai/install.sh | bash
```

### 🪟 Windows CMD

```shell
curl -fsSL https://claude.ai/install.cmd -o install.cmd && install.cmd && del install.cmd
```

> [!warning] Importante: Autenticación
> Después de la instalación, ejecute `claude` en su terminal. La primera vez que ejecute este comando, se le solicitará que se autentique.

---

## ⚙️ Configuración Adicional

> [!note] Proveedores en la Nube
> Si utiliza AWS Bedrock o Google Cloud Vertex, se requiere alguna configuración adicional:

- **AWS Bedrock:** [Instrucciones especiales para AWS Bedrock](https://code.claude.com/docs/en/amazon-bedrock)
- **Google Cloud Vertex:** [Instrucciones especiales para Google Cloud Vertex](https://code.claude.com/docs/es/google-vertex-ai)

---

## 💻 Proyect Setup

> [!abstract] Requisitos Previos
> Este proyecto requiere una pequeña cantidad de configuración inicial antes de probar la aplicación localmente.

1. **Instalar Node JS:** Asegúrate de tener Node JS instalado localmente. [Enlace a las instrucciones de instalación](https://nodejs.org).

2. **Descargar Archivos:** Descargue el archivo zip llamado `uigen.zip` adjunto a esta conferencia y extráigalo.
   - 📥 **Descarga Directa:** [Descargar uigen.zip](https://cc.sj-cdn.net/instructor/4hdejjwplbrm-anthropic/assets/1769622681/uigen.zip?response-content-disposition=attachment&Expires=1772826565&Signature=jH4p3RuA-aoPYOkA~ti-QJ4SlLdfAzePwx-pxM7UkMWdIqO9EKt9lGVgFhmPsLUC2DOcuMDLhb1uqi~ga2kmYc~spgBW6M7CbEey10XRjpPISzjIbi-PBZalIHXUhGLeRLJKhlxQ8G1~EyaCasFY1fKLHpTU2d3mw0nC5zC9AIIAcdX3IWclywic0NgKOx557a83n~iiXVEzHoJXgarikNzMAyawmArFpm14M4LO0iwN2kE7crxsr~aZ6X01y5VOvTTg96PWjREhv4b2Tc7Gz5iU7ed8HIJqizfPMdS1GPdIsidihfXWRMBX0qI-2QJaJq7mXOODCovoDFlQTGy-xA__&Key-Pair-Id=APKAI3B7HFD2VYJQK4MQ)

3. **Instalar Dependencias:** En el directorio del proyecto, ejecute el siguiente comando para instalar las dependencias y configurar una base de datos SQLite local:

   ```bash
   npm run setup
   ```

4. **Configurar API Key (Opcional):**
   Este proyecto utiliza Claude a través de la API de Anthropic para generar componentes de interfaz de usuario. Si desea probar la aplicación por completo, deberá proporcionar una clave de API para acceder a la API de Anthropic.
   - _Nota: Esto es opcional. Si no se proporciona ninguna clave de API, la aplicación seguirá generando código estático falso._
   - **Obtenga una clave API de Anthropic en:** [Console Anthropic](https://console.anthropic.com/)
   - **Coloque su clave API en el archivo:** `.env`

5. **Iniciar Proyecto:** Start the project by running:
   ```bash
   npm run dev
   ```

---

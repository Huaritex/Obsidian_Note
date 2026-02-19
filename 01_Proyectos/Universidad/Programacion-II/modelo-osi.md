---
tags: ['note']
fecha_creacion: 2026-02-14
relaciones: []
---
---

# Modelo [[modelo-osi]]

> [!abstract] **Concepto Clave**
> El modelo [[modelo-osi]] (Open Systems Interconnection) es el marco conceptual universal que describe cómo se comunican los sistemas de red. Es el lenguaje común que permite que una computadora con **Arch Linux** se entienda con un servidor en la nube o un iPhone, sin importar el hardware o software que tengan.

---

## Las 7 Capas del Modelo [[modelo-osi]]

### 1. Capa Física (Physical)
> [!info] **Unidad de datos:** Bits
> Es el medio de transmisión físico (cables, fibra óptica, ondas de radio). Se encarga de la transmisión y recepción de la secuencia de bits puros (0s y 1s).

### 2. Capa de Enlace de Datos (Data Link)
> [!info] **Unidad de datos:** Tramas (Frames)
> Proporciona la transferencia de datos nodo a nodo. Aquí es donde operan los **Switches** y se gestionan las direcciones **MAC**.
> * **Funciones:** Detección de errores físicos y control de flujo.

### 3. Capa de Red (Network)
> [!info] **Unidad de datos:** Paquetes (Packets)
> Se encarga del direccionamiento lógico y el enrutamiento. Es la capa donde vive el protocolo **IP**.
> * **Dispositivo clave:** Routers.
> * **Dato:** Aquí se determina la mejor ruta física para que tus datos lleguen a su destino.

### 4. Capa de Transporte (Transport)
> [!info] **Unidad de datos:** Segmentos (TCP) / Datagramas (UDP)
> Garantiza que los mensajes se entreguen sin errores y en secuencia.
> * **Protocolos:** [[TCP]] (Confiable, orientado a conexión) y [[UDP]] (Rápido, sin conexión).
> * **Cybersec Tip:** El filtrado de puertos ocurre en esta capa.

### 5. Capa de Sesión (Session)
> [!info] **Unidad de datos:** Datos
> Maneja el establecimiento, mantenimiento y finalización de las "sesiones" entre aplicaciones.
> * **Propósito:** Permite que dos sistemas inicien y detengan diálogos, gestionando la sincronización para que no se pierda el progreso si hay una caída breve.

### 6. Capa de Presentación (Presentation)
> [!important] **Unidad de datos:** Datos
> Se encarga de traducir el formato de los datos para que la capa de aplicación los entienda.
> * **Funciones clave:**
> 	* **Cifrado/Decifrado:** Vital para la seguridad de tus datos.
> 	* **Compresión:** Reduce el tamaño de los archivos para una transmisión más rápida.
> 	* **Formateo:** Traduce formatos de datos (ej. ASCII, EBCDIC).

### 7. Capa de Aplicación (Application)
> [!example] **Unidad de datos:** Datos
> Es la capa más cercana al usuario. Proporciona la interfaz que utilizas para interactuar con la red.
> * **Protocolos comunes:** HTTP/HTTPS (Web), SSH (Acceso remoto en Linux), DNS, FTP.

---

### Mnemotecnia para recordar las capas
Frase (de la capa 7 a la 1):
**A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing
*(**A**plicación, **P**resentación, **S**esión, **T**ransporte, **R**ed, **E**nlace, **F**ísica)*
---
tags: ['note', 'networking', 'osi']
fecha_creacion: 2026-02-14
relaciones: []
---

> [!info] El modelo [[modelo-osi]] (Open Systems Interconnection) es el marco conceptual universal que describe como se comunican los sistemas de red. Como lenguaje comun que permite que una computadora con Arch Linux se entienda con un servidor en la nube o un Iphone, sin importar el hardware o software que tengan.

## Las 7 Capas del Modelo [[modelo-osi]]

### 1. Capa Física (Physical)
> [!info]
> Es el medio de transmision físico (cables, fibra óptica, ondas de radio). Se encarga de bits puros (0s y 1s).
>
> **Ejemplos**: Cables Ethernet, Hubs, Repetidores.

### 2. Capa de Enlace de Datos (Data Link)
> [!info]
> Organiza los bits en tramas (frames) y gestiona la dirección física (MAC). Asegura la transferencia libre de errores entre dos nodos conectados directamente.
>
> **Ejemplos**: Switches, Puentes, Direcciones MAC.

### 3. Capa de Red (Network)
> [!info]
> Determina la mejor ruta para enviar los paquetes a través de la red (enrutamiento). Se encarga del direccionamiento lógico (IP).
>
> **Ejemplos**: Routers, Protocolo IP.

### 4. Capa de Transporte (Transport)
> [!info]
> Garantiza la entrega de datos de extremo a extremo, controlando el flujo y la corrección de errores. Divide los datos en segmentos.
>
> **Ejemplos**: TCP (fiable), UDP (rápido).

### 5. Capa de Sesión (Session)
> [!info]
> Establece, gestiona y finaliza las conexiones (sesiones) entre aplicaciones locales y remotas.

### 6. Capa de Presentación (Presentation)
> [!info]
> Traduce los datos a un formato que la aplicación pueda entender (cifrado, compresión, codificación). Es el "traductor" de la red.
>
> **Ejemplos**: SSL/TLS, JPEG, ASCII.

### 7. Capa de Aplicación (Application)
> [!info]
> La capa que interactúa directamente con el usuario final. Proporciona servicios de red a las aplicaciones.
>
> **Ejemplos**: HTTP, FTP, SMTP, DNS.

> [!summary]
> **Regla Mnemotécnica**: "All People Seem To Need Data Processing" (Application, Presentation, Session, Transport, Network, Data Link, Physical).

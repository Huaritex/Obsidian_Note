
## 1. El Viaje de Bajada: Encapsulamiento (Emisor)

> Cuando tu aplicación (digamos, el cliente Tauri en tu Arch Linux) decide sincronizar una nota con la nube, los datos bajan desde la capa superior a la inferior.

- **Capas de Aplicación, Presentación y Sesión (7, 6, 5):** Aquí los datos son simplemente eso, **Data**. Se define el formato (JSON para tu nota de Obsidian) y se cifra (TLS).
    
- **Capa de Transporte (4):** Los datos se dividen en trozos manejables. Si usas TCP, se le añade un encabezado con los puertos de origen y destino. Aquí la unidad se llama **Segmento**.
    
- **Capa de Red (3):** El segmento se mete dentro de un "sobre" que contiene las direcciones IP (origen y destino). Ahora tenemos un **Paquete**. Aquí es donde vive el enrutamiento.
    
- **Capa de Enlace de Datos (2):** El paquete se encapsula con las direcciones MAC física de tu tarjeta de red y el router. Se añade un código de error (FCS) al final. La unidad es la **Trama (Frame)**.
    
- **Capa Física (1):** La trama se convierte en señales eléctricas, pulsos de luz o microondas. Aquí ya no hay estructuras, solo **Bits** (0s y 1s).

------------------------------------------------------------------------

## 2. El Viaje de Subida: Desencapsulamiento (Receptor)

Cuando los bits llegan al servidor (o a otro dispositivo en tu red local), el proceso se invierte. Cada capa "abre" el sobre correspondiente, lee las instrucciones y pasa el contenido a la capa superior.

### Ejemplo de flujo en una arquitectura moderna:

Si estás auditando el tráfico con `wireshark` en tu sistema, verías exactamente este orden:

1. **L1:** El hardware recibe los voltajes.
    
2. **L2:** Se verifica que la **MAC** sea la correcta. Si es así, se descarta el encabezado de la trama.
    
3. **L3:** Se verifica la **IP**. Si el paquete es para este host, se "pela" la capa de red.
    
4. **L4:** Se mira el **Puerto** (ej. 443 para HTTPS). Se reensamblan los segmentos en el orden correcto.
    
5. **L5-L7:** El sistema operativo entrega los datos limpios a la aplicación, que ahora puede leer el JSON de la nota y procesarlo con la IA.

------------------------------------------------------------------------
## 3. Unidades de Datos (PDU) por Capa

Para que no se te olvide nunca (muy útil para certificaciones como el CCNA), esta es la jerarquía:

|**Capa OSI**|**Unidad de Datos (PDU)**|**Ejemplo de Protocolo**|
|---|---|---|
|**7, 6, 5**|Datos|HTTP, SSH, MQTT|
|**4. Transporte**|Segmento (TCP) / Datagrama (UDP)|TCP, UDP|
|**3. Red**|Paquete|IPv4, IPv6, ICMP|
|**2. Enlace**|Trama (Frame)|Ethernet, Wi-Fi (802.11)|
|**1. Física**|Bits|Señal eléctrica, Fibra óptica|

------------------------------------------------------------------------

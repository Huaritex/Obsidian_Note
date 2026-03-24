---
tags: ['note', 'programming', 'structured-programming']
fecha_creacion: 2026-02-14
relaciones: []
---

>[!note] Programación II
>- Carpeta/curso: [[Programacion-II|Programación II]]
>- Objetivo: entender los requisitos **no funcionales** (NFR) y diferenciarlos de los **funcionales** (FR).

>[!info] Requisitos No Funcionales (NFR)
>Los **requisitos no funcionales** describen **cómo** debe comportarse un sistema, además de **qué** debe hacer (eso corresponde a los requisitos funcionales). Se enfocan en *calidad*, *restricciones* y *condiciones* del sistema durante su operación.
>
>En otras palabras:
>- Los funcionales responden: “¿Qué hace el sistema?”
>- Los no funcionales responden: “¿Con qué calidad y bajo qué condiciones debe hacerlo?”


>[!info] ¿Qué son los requisitos no funcionales?
>Son enunciados que establecen **criterios medibles** sobre aspectos como:
>
>- Rendimiento (tiempos de respuesta, throughput)
>- Seguridad (autenticación, autorización, cifrado)
>- Disponibilidad y confiabilidad (uptime, tolerancia a fallos)
>- Usabilidad (facilidad de uso, accesibilidad)
>- Mantenibilidad (facilidad de mantenimiento y cambios)
>- Escalabilidad (crecer en usuarios/carga)
>- Compatibilidad e interoperabilidad (funcionar con plataformas/estándares)
>- Portabilidad (moverse a otros entornos con facilidad)
>- Cumplimiento legal/regulatorio (normativas)
>
>Un buen NFR suele incluir **métrica + objetivo + condiciones**.


>[!tip] ¿Para qué son sirven?
>Los NFR sirven para que el equipo pueda:
>
>1. **Definir expectativas de calidad**  
>   Evitan que “funcione” sea suficiente: también importa *qué tan bien* y *en qué condiciones*.
>2. **Tomar decisiones de diseño y arquitectura**  
>   Ej.: si necesitas baja latencia, cambia la arquitectura (cachés, colas, bases, etc.).
>3. **Evaluar y verificar el sistema**  
>   Permiten pruebas: pruebas de carga, auditorías de seguridad, pruebas de usabilidad, etc.
>4. **Gestionar riesgos**  
>   Si no se especifican NFR, suelen aparecer tarde fallos de desempeño, vulnerabilidades o costos de mantenimiento.


>[!example] ¿Cuáles son? (Categorías comunes de NFR)
>A continuación, una lista práctica de categorías que casi siempre aparecen en proyectos de software:
>
>### 1) Rendimiento y eficiencia
>
>- Tiempo de respuesta máximo
>- Consumo de recursos (CPU/memoria)
>- Capacidad de procesar carga (requests/segundo)
>
>### 2) Seguridad
>
>- Control de acceso (roles/permisos)
>- Cifrado en tránsito y en reposo
>- Auditoría y trazabilidad
>- Resistencia a ataques (p. ej., XSS/CSRF)
>
>### 3) Disponibilidad y confiabilidad
>
>- Porcentaje de uptime
>- Manejo de fallos (reintentos, degradación)
>- Recuperación ante desastres
>
>### 4) Usabilidad y accesibilidad
>
>- Facilidad de aprendizaje
>- Claridad de interfaces y flujos
>- Cumplimiento de accesibilidad (p. ej., WCAG)
>
>### 5) Mantenibilidad
>
>- Complejidad y legibilidad del código
>- Cobertura de pruebas
>- Facilidad para extender o corregir
>
>### 6) Escalabilidad
>
>- Crecimiento horizontal/vertical
>- Capacidad para manejar picos de demanda
>
>### 7) Compatibilidad e interoperabilidad
>
>- Soportar navegadores/dispositivos
>- Integrar con APIs/estándares
>
>### 8) Portabilidad
>
>- Ejecutarse en distintos sistemas/entornos
>
>### 9) Cumplimiento y legalidad
>
>- Normativas (privacidad, retención de datos, etc.)


>[!important] Ejemplos (bien formulados)
>Ejemplos de NFR con métrica (para que sean verificables):
>
>- **Rendimiento:** “El sistema debe responder a la búsqueda en **menos de 300 ms** para el 95% de las solicitudes.”
>- **Disponibilidad:** “La plataforma debe mantener un **99.9% de uptime** mensual.”
>- **Seguridad:** “Todas las contraseñas deben almacenarse con **hash bcrypt** con factor de costo >= 12.”
>- **Seguridad (tránsito):** “El 100% del tráfico debe ir cifrado mediante **TLS 1.2+**.”
>- **Usabilidad:** “El flujo de registro debe completarse en **menos de 2 minutos** para usuarios nuevos (medido en pruebas de usabilidad).”
>- **Mantenibilidad:** “Se debe mantener una cobertura de pruebas de **>= 80%** para el módulo de pagos.”
>- **Escalabilidad:** “Debe soportar picos de **10,000 usuarios concurrentes** sin degradación superior a un 20%.”
>- **Compatibilidad:** “El sistema debe funcionar en los navegadores **Chrome, Firefox y Safari** en sus versiones actuales.”


>[!warning] Diferencia con los requisitos funcionales
>### Idea clave
>
>- **Requisitos funcionales (FR):** describen *funciones/acciones* (“hacer X”).
>- **Requisitos no funcionales (NFR):** describen *condiciones de calidad* (“hacer X con Y calidad”).
>
>### Comparación rápida
>
>| Tipo | Responde a “¿qué...?” | Responde a “¿cómo...?” | Verificación típica |
>|---|---|---|---|
>| Funcional | qué hace el sistema (características) | menos foco | pruebas de casos de uso |
>| No funcional | qué tan bien opera | criterios de calidad | pruebas de carga, seguridad, usabilidad |
>
>### Ejemplo paralelo (mismo tema)
>
>- **Funcional:** “El usuario puede iniciar sesión con correo y contraseña.”
>- **No funcional:** “El inicio de sesión debe ser seguro y en **< 500 ms** para el 95% de solicitudes; además, debe bloquear intentos tras **N** fallos.”


>[!question] Gráficas Mermaid (para visualizarlo)
>### 1) Mapa: Funcionales vs No Funcionales
>
>```mermaid
>flowchart TB
>  A[Requisitos] --> B[Requisitos Funcionales]
>  A[Requisitos] --> C[Requisitos No Funcionales]
>  
>  B --> B1["¿Qué hace el sistema?"]
>  B1 --> B2["Casos de uso / funciones"]
>  
>  C --> C1["¿Cómo debe operar?"]
>  C1 --> C2["Calidad, restricciones y criterios medibles"]
>  
>  B2 --> D[Implementación]
>  C2 --> D[Implementación]
>```
>
>### 2) Categorías de NFR (atributos de calidad)
>
>```mermaid
>mindmap
>  root((NFR: Calidad del sistema))
>    Rendimiento
>      "Tiempo de respuesta"
>      "Throughput"
>      "Uso de recursos"
>    Seguridad
>      "Autenticación"
>      "Autorización"
>      "Cifrado"
>    Confiabilidad
>      "Uptime"
>      "Tolerancia a fallos"
>      "Recuperación"
>    Usabilidad
>      "Facilidad de uso"
>      "Accesibilidad"
>    Mantenibilidad
>      "Legibilidad"
>      "Pruebas"
>      "Facilidad de cambio"
>    Escalabilidad
>      "Picos de carga"
>      "Crecimiento"
>    Compatibilidad
>      "Navegadores / SO"
>      "APIs / Estándares"
>    Cumplimiento
>      "Privacidad"
>      "Regulaciones"
>```
>
>### 3) Dependencia entre NFR y decisiones de arquitectura
>
>```mermaid
>flowchart LR
>  NFR[Rendimiento/Seguridad/Disponibilidad] --> D1[Diseño de arquitectura]
>  D1 --> E1[Estrategias]
>  E1 --> C1[Caché, colas, balanceo]
>  E1 --> C2[Modelo de autorización, cifrado]
>  E1 --> C3[Monitoreo, reintentos, backups]
>  C1 --> O[Operación con métricas]
>  C2 --> O
>  C3 --> O
>```


>[!tip] Plantilla rápida para redactar un NFR (recomendado)
>Usa este formato para que sea medible y testeable:
>
>`[Sistema] debe [comportamiento] en [métrica] bajo [condiciones] durante [tiempo]`
>
>Ejemplo:
>
>`El sistema debe mantener 99.9% de uptime mensual durante mantenimiento planificado y monitoreado.`


>[!note] Resumen (en una frase)
>Los **requisitos no funcionales** garantizan que el sistema, además de cumplir funciones, tenga **calidad verificable**: rendimiento, seguridad, confiabilidad, usabilidad y más.

---

# Codigo de Ejemplo

> "El sistema debe registrar una alerta si el tiempo de respuesta de la función excede los 500ms".

```python
import time
import functools

# Este decorador representa la implementación de un RNF de Rendimiento
def monitor_performance(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        start_time = time.perf_counter()
        
        result = func(*args, **kwargs)  # Ejecución del Requisito Funcional
        
        end_time = time.perf_counter()
        duration = end_time - start_time
        
        # Lógica del RNF: Si tarda más de 0.5s, notificamos
        if duration > 0.5:
            print(f"⚠️ ALERTA RNF: La función '{func.__name__}' excedió el tiempo límite. Tardó {duration:.4f}s")
        else:
            print(f"✅ RNF OK: Tiempo de respuesta {duration:.4f}s")
            
        return result
    return wrapper

# Requisito Funcional: Procesar una orden de compra
@monitor_performance
def procesar_pago(monto):
    # Simulamos una operación que podría ser lenta (ej. llamada a API externa)
    time.sleep(0.6) 
    return f"Pago de ${monto} procesado."

# Ejecución
print(procesar_pago(100))
```


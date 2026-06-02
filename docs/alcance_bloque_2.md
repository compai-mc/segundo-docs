# 📄 Documento de Alcance del Proyecto  
## Sistema de Desacoplo basado en Arquitectura Event-Driven

---

## 1. Propósito
El presente documento define el alcance de la segunda fase del proyecto, centrada en la transformación de un sistema legacy altamente acoplado hacia una arquitectura desacoplada basada en eventos utilizando Apache Kafka.

---

## 2. Descripción del Proyecto
El proyecto consiste en la construcción de una capa de desacoplo (wrapper) que permita redirigir las llamadas directas entre componentes hacia un modelo basado en mensajería asíncrona.

El objetivo es eliminar dependencias punto a punto en el código y en el acceso a bases de datos, introduciendo un bus de eventos como mecanismo único de comunicación entre componentes.

---

## 3. Objetivos del Sistema

El sistema deberá ser capaz de:

- Eliminar llamadas directas entre módulos o servicios  
- Interceptar peticiones y transformarlas en eventos  
- Utilizar Apache Kafka como canal central de comunicación  
- Ejecutar lógica mediante consumidores desacoplados  
- Desacoplar el acceso a bases de datos de la lógica de negocio  
- Facilitar la evolución del sistema sin dependencias rígidas  

---

## 4. Alcance Funcional

### 4.1 Capacidades principales

El sistema incluirá:

- Interceptación de llamadas existentes  
- Transformación de operaciones en eventos estructurados  
- Publicación de eventos en Kafka  
- Consumo de eventos mediante servicios independientes  
- Ejecución de lógica en consumidores  
- Generación opcional de eventos derivados  

---

### 4.2 Modelo de comunicación

#### Modelo actual (AS-IS)
- Llamadas síncronas entre módulos  
- Acceso directo a bases de datos  
- Dependencias rígidas  

#### Modelo objetivo (TO-BE)
- Comunicación mediante eventos  
- Desacoplo entre emisores y consumidores  
- Procesamiento asíncrono  

---

### 4.3 Tipos de eventos

El sistema gestionará:

- Eventos de comando (acciones solicitadas)
- Eventos de estado (cambios producidos)
- Eventos derivados (procesos posteriores)

#### Ejemplo de evento

```json
{
  "event": "factura.crear",
  "timestamp": "2026-06-01T10:00:00Z",
  "payload": {
    "cliente_id": 123,
    "importe": 100.0
  }
}
```

---

### 4.4 Componentes del sistema

#### ✅ Wrapper / Gateway
- Intercepta llamadas del sistema legacy  
- Traduce operaciones a eventos Kafka  
- Actúa como punto de entrada  

#### ✅ Kafka (Event Bus)
- Canal central de comunicación  
- Gestión de topics  
- Garantías de entrega  

#### ✅ Consumers
- Procesan eventos  
- Ejecutan lógica de negocio  
- Acceden a bases de datos  

#### ✅ Servicios desacoplados
- Implementan lógica por dominio  
- Independientes entre sí  

---

## 5. Arquitectura de Alto Nivel

El flujo general será:

```
Sistema Legacy → Wrapper → Kafka → Consumers → Sistemas destino
```

---

## 6. Fuera de alcance

Queda fuera del proyecto:

- Reescritura completa del sistema legacy  
- Sustitución total de la lógica existente  
- Desarrollo de interfaces de usuario  
- Migración completa de bases de datos  
- Consistencia fuerte en todos los casos  
- Eliminación total del sistema legacy en esta fase  

---

## 7. Supuestos

Se asume que:

- El sistema legacy permite interceptar llamadas  
- Se dispone de infraestructura Kafka  
- El sistema puede evolucionar de forma progresiva  
- Los consumidores pueden adaptarse al modelo asíncrono  

---

## 8. Restricciones

- Compatibilidad con el sistema actual  
- Introducción progresiva del modelo  
- Complejidad de sistemas asíncronos  
- Consistencia eventual  
- Incremento de latencia frente a llamadas síncronas  

---

## 9. Consideraciones técnicas

El sistema deberá contemplar:

- Idempotencia en consumidores  
- Reintentos automáticos  
- Dead Letter Queues (DLQ)  
- Versionado de eventos  
- Observabilidad y trazabilidad  
- Gestión de contratos de eventos  

---

## 10. Control de Cambios

Las modificaciones del alcance deberán evaluarse considerando:

- Impacto en el sistema legacy  
- Compatibilidad entre eventos  
- Complejidad añadida  

---

## 11. Aceptación

- **Responsable del proyecto:** ___________________  
- **Stakeholder:** ___________________  
- **Fecha:** ___________________  

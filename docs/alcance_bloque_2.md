# 📄 Documento de Alcance del Bloque II
## Metodología de Desacople Progresivo basada en Arquitectura Event-Driven y CQRS

---

## 1. Propósito

El presente documento define el alcance funcional y técnico del proyecto, estableciendo la estrategia de evolución de un sistema **legacy** altamente acoplado hacia una arquitectura desacoplada basada en eventos, manteniendo la compatibilidad con el sistema existente durante todo el proceso de transición.

---

## 2. Descripción del Proyecto

El proyecto consiste en la definición de una **Arquitectura de Desacople por Eventos (ADE)**, una metodología para la evolución progresiva de sistemas legacy hacia arquitecturas distribuidas basadas en eventos.

ADE define un patrón arquitectónico que sustituye las dependencias directas entre componentes por un modelo de comunicación desacoplado basado en eventos. Mediante este patrón, las llamadas síncronas existentes son encapsuladas, transformadas en eventos y distribuidas a través de un **Event Bus**, permitiendo desacoplar progresivamente la lógica de negocio sin necesidad de reescribir el sistema existente.

En esta primera implementación, la arquitectura utilizará **Apache Kafka** como Event Bus y mantendrá el comportamiento funcional actual del sistema. El MVP no modificará la lógica de negocio ni el mapeo de las operaciones existentes; únicamente sustituirá el mecanismo de comunicación entre componentes.

> ### Principio fundamental de ADE
>
> Ningún componente conocerá directamente a otro componente del sistema. Toda comunicación deberá realizarse mediante eventos publicados en el Event Bus.

---

## 3. Objetivos

- Eliminar llamadas directas entre módulos o servicios.
- Interceptar peticiones y transformarlas en eventos.
- Utilizar Apache Kafka como canal central de comunicación.
- Ejecutar lógica mediante consumidores desacoplados.
- Desacoplar el acceso a bases de datos de la lógica de negocio.
- Facilitar la evolución progresiva del sistema.

---

## 4. Alcance Funcional

### 4.1 Capacidades principales

- Interceptación de llamadas existentes.
- Transformación de operaciones en eventos.
- Publicación de eventos en Kafka.
- Consumo mediante servicios independientes.
- Ejecución de lógica en consumidores.
- Generación opcional de eventos derivados.

### 4.2 Alcance del MVP

El MVP validará la arquitectura ADE sobre un subconjunto representativo del sistema legacy.

Incluye:

- Interceptación de llamadas existentes.
- Transformación de llamadas en eventos.
- Publicación en Apache Kafka.
- Procesamiento mediante consumidores desacoplados.
- Respuesta funcional equivalente al sistema actual.

El MVP no modificará la lógica de negocio existente, limitándose a validar el nuevo patrón de comunicación.

### 4.3 Arquitectura funcional

#### Principios de la arquitectura ADE

- Eliminación del acoplamiento punto a punto.
- Comunicación exclusivamente mediante eventos.
- Evolución progresiva sin reescritura.
- Separación entre productores y consumidores.
- Independencia tecnológica entre componentes.
- Compatibilidad con el sistema legacy durante la transición.

#### Componentes

##### Wrapper / Gateway

- Intercepta llamadas del sistema legacy.
- Traduce operaciones a eventos.
- Punto único de entrada.

##### Event Bus (Apache Kafka)

- Canal central de comunicación.
- Gestión de tópicos.
- Garantías de entrega.

##### Consumidores

- Procesan eventos.
- Ejecutan la lógica de negocio.
- Acceden a los recursos necesarios.

##### Servicios desacoplados

- Un tópico por servicio origen.
- Independientes entre sí.

### 4.4 Modelo de comunicación

#### AS-IS

- Llamadas síncronas.
- Acceso directo a bases de datos.
- Dependencias rígidas.

#### TO-BE

- Comunicación mediante eventos.
- Desacoplamiento entre productores y consumidores.
- Procesamiento interno asíncrono con respuesta funcional equivalente.

### 4.5 Tipos de eventos

El MVP gestionará eventos de comando.

Fuera del MVP:

- Eventos de estado.
- Eventos derivados.
- Integraciones con otros sistemas.


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

## 5. Arquitectura de Servicios

#### Wrapper / Gateway
- Intercepta llamadas del sistema legacy  
- Traduce operaciones a eventos Kafka  
- Actúa como punto de entrada  

#### Kafka (Event Bus)
- Canal central de comunicación  
- Gestión de topics  
- Garantías de entrega  

#### Consumers
- Procesan eventos  
- Ejecutan lógica de negocio  
- Acceden a bases de datos  

#### Servicios desacoplados
- Se implementa un tópico por cada servicio origen 
- Independientes entre sí  


## 5. Arquitectura de Alto Nivel

El flujo general será:

    Sistema Original → Wrapper → Kafka → Consumidores → Sistemas destino

---

## 6. Fuera de alcance

- Reescritura completa del sistema legacy.
- Sustitución de la lógica existente.
- Desarrollo de interfaces de usuario.
- Migración completa de bases de datos.
- El MVP no garantiza consistencia fuerte entre todos los componentes distribuidos.
- Eliminación definitiva del sistema legacy.

---

## 7. Supuestos

- El sistema permite interceptar llamadas.
- Existe infraestructura Kafka.
- La migración será progresiva.
- Los consumidores podrán adaptarse al nuevo modelo.

---

## 8. Riesgos

- Compatibilidad con el sistema existente.
- Complejidad de la transición.
- Gestión de la asincronía.
- Incremento de latencia.

---

## 9. Consideraciones técnicas (posteriores al MVP)

- Idempotencia.
- Reintentos automáticos.
- Dead Letter Queue (DLQ).
- Versionado de eventos.
- Observabilidad y trazabilidad.
- Gestión de contratos de eventos.

# 📄 Documento de Alcance del Bloque I

## 1. Propósito

Este documento define el alcance funcional y técnico del proyecto,
estableciendo las capacidades incluidas, los límites del sistema y los
objetivos que se pretenden alcanzar durante el desarrollo del MVP.

------------------------------------------------------------------------



## 2. Descripción del Proyecto

El proyecto consiste en el desarrollo de un sistema inteligente de análisis de código basado en **Razonamiento Deliberativo Crítico (RDC)**, una metodología para la construcción de sistemas de razonamiento distribuidos capaz de comprender sistemas software complejos y proporcionar análisis técnico avanzado.

Razonamiento Deliberativo Crítico (RDC) es una metodología para la construcción de sistemas de razonamiento distribuido que se materializa mediante un patrón arquitectónico basado en la generación, deliberación y verificación de hipótesis independientes. En dicho patrón, múltiples componentes de razonamiento generan hipótesis sobre un mismo problema, que posteriormente son sometidas a un proceso de deliberación, contraste y verificación crítica antes de obtener una conclusión fundamentada. En esta primera implementación, dichos componentes de razonamiento estarán constituidos por múltiples modelos de lenguaje (arquitectura multi-LLM), aunque la metodología RDC es independiente de la tecnología utilizada y permite incorporar otros mecanismos de razonamiento o verificación.

> ### Principio fundamental de RDC
>
> Toda conclusión generada por el sistema deberá ser el resultado de un proceso de **Razonamiento Deliberativo Crítico (RDC)**. Ninguna respuesta será producida a partir de una única hipótesis; todas las conclusiones deberán obtenerse mediante un proceso de deliberación, contraste y verificación entre múltiples hipótesis independientes.

El sistema está orientado al análisis de repositorios de código fuente, permitiendo interpretar, documentar, analizar y proponer mejoras arquitectónicas de forma automatizada.




------------------------------------------------------------------------

## 3. Objetivos

El sistema deberá ser capaz de:

-   Comprender código en múltiples lenguajes (según el alcance del MVP).
-   Analizar módulos individuales y sistemas completos.
-   Responder preguntas técnicas sobre el código.
-   Generar documentación técnica automáticamente.
-   Detectar problemas, riesgos y antipatrones.
-   Proponer optimizaciones y mejoras arquitectónicas.
-   Contrastar resultados mediante múltiples LLM especializados.

------------------------------------------------------------------------

## 4. Alcance Funcional

### 4.1 Capacidades principales

-   Análisis sintáctico y semántico.
-   Comprensión de dependencias.
-   Generación automática de documentación.
-   Evaluación de calidad del código.
-   Detección de errores y antipatrones.
-   Generación de propuestas de optimización.
-   Consultas técnicas sobre el sistema.

### 4.2 Alcance del MVP

La primera versión del sistema (MVP) estará orientada a validar la metodología RDC sobre una parte representativa del ecosistema software de la organización.

El alcance del MVP comprenderá:

- El análisis de aplicaciones desarrolladas en **.NET**.
- El análisis de código **PL/SQL** asociado a dichas aplicaciones.
- La construcción de los procesos de descubrimiento, indexación, análisis, síntesis y optimización definidos por la metodología RDC para este ámbito tecnológico.
- La validación de la arquitectura sobre repositorios reales de la organización.

El MVP tendrá como objetivo demostrar la viabilidad técnica de la metodología RDC y servir como base para una futura extensión del sistema a otros lenguajes, tecnologías y dominios funcionales.


### 4.3 Arquitectura funcional

#### Principios de la arquitectura RDC

La arquitectura RDC se fundamenta en los siguientes principios:

- Ninguna conclusión se obtiene a partir de una única hipótesis.
- Todo resultado debe ser sometido a deliberación crítica.
- Cada módulo aplica RDC de forma especializada según su responsabilidad.
- La verificación forma parte del proceso de razonamiento y no constituye una fase posterior.
- Toda conclusión debe ser trazable hasta las hipótesis y evidencias que la sustentan.



El sistema estará organizado en cinco módulos deliberativos principales (RDC):

#### RDC Descubrimiento

-   Parseo específico por lenguaje.
-   Comprensión de funciones y módulos.
-   Resúmenes multinivel del código.
-   Análisis de dependencias (grafo).
-   Detección de errores.

#### RDC Indexación

-   Integración de la información del sistema.
-   Grafo de dependencias (base de datos de grafos).
-   Índice semántico (base de datos vectorial).
-   Índice estructural (base de datos multimodelo/documental).
-   API de indexación.
-   API de búsqueda semántica.

#### RDC Análisis

-   Clasificación de consultas.
-   Análisis estructural y semántico.
-   Recuperación contextual.
-   Deliberación multi‑LLM.
-   Verificación crítica.
-   Validación de resultados.

#### RDC Síntesis


Este módulo transforma los resultados generados por RDC Análisis en conocimiento de alto nivel mediante la ejecución de procesos de Razonamiento Deliberativo Crítico orientados a diferentes criterios de análisis.

Cada criterio constituye una perspectiva independiente desde la que se analiza el sistema y puede ser configurado o ampliado sin modificar la arquitectura RDC.

##### Criterios de análisis 

- Arquitectura global
- Componentes y responsabilidades
- Dependencias entre módulos
- Flujos de ejecución
- Riesgos de arquitectura
- Antipatrones
- Hotspots (zonas críticas del sistema)
- Otros criterios configurables

##### Funcionalidades

- Gestión de un catálogo de criterios de análisis editable.
- Ejecución independiente de un proceso RDC para cada criterio.
- Correlación de los resultados obtenidos.
- Eliminación de inconsistencias y duplicidades.
- Generación de una visión unificada del sistema.
- Construcción del informe final de análisis.

#### RDC Optimización

-   Deliberación (RDC) sobre mejoras.
-   Propuestas arquitectónicas.
-   Persistencia de resultados en almacenamiento S3.

### 4.4 Modelo de razonamiento

El sistema podrá utilizar diferentes familias de modelos (GPT, Claude,
Gemini, Llama, etc.).


Cada modelo participante ejecutará un proceso de RDC desde una perspectiva especializada. Las hipótesis generadas serán sometidas a un proceso de deliberación y verificación crítica que permitirá detectar inconsistencias, reforzar evidencias y construir una respuesta consensuada.

### 4.5 Casos de uso

-   Análisis de código.
-   Documentación automática.
-   Consultas técnicas.
-   Detección de riesgos y antipatrones.
-   Optimización arquitectónica.

------------------------------------------------------------------------

## 5. Arquitectura de Servicios

-   **Módulo Orquestador**
-   **Módulo RDC de Descubrimiento**
-   **Módulo RDC de Indexación**
-   **Módulo RDC de Análisis**
-   **Módulo RDC de Síntesis**
-   **Módulo RDC de Optimización**

### Persistencia (preferible)

-   Base de datos documental (ArangoDB).
-   Base de datos grafos (ArangoDB).
-   Base de datos vectorial (Milvus).
-   Almacenamiento de objetos (MinIO / S3).

------------------------------------------------------------------------

## 6. Fuera de alcance

-   Interfaces de usuario avanzadas.
-   Integraciones no definidas.
-   Ejecución automática en producción.
-   Automatización completa de despliegues.
-   Sustitución de la revisión humana.
-   Garantía absoluta de ausencia de errores.
-   Lenguajes no contemplados en el MVP.

------------------------------------------------------------------------

## 7. Supuestos

-   El código fuente estará disponible.
-   Existirá acceso a los modelos de lenguaje.
-   Infraestructura Linux para la ejecución.
-   Recursos suficientes para bases de datos y almacenamiento.

------------------------------------------------------------------------

## 8. Restricciones

-   Dependencia de proveedores de LLM.
-   Coste computacional del razonamiento multi‑LLM.
-   Variabilidad inherente a los modelos.
-   Necesidad de validación humana en escenarios críticos.

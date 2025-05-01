# Informe de Diseño Arquitectónico
## Sistema de Gestión de Emergencias Médicas (SGEM)

## Caso de Estudio

### Descripción del Sistema
El Sistema de Gestión de Emergencias Médicas (SGEM) es una aplicación que permite coordinar la atención de emergencias médicas, gestionando recursos como ambulancias, personal médico y camas hospitalarias. El sistema debe permitir recibir solicitudes de emergencia, asignar recursos apropiados, monitorear el estado de las emergencias en tiempo real y generar reportes estadísticos para la toma de decisiones.

### Requerimientos Funcionales
1. **Gestión de Emergencias**: Recepción y clasificación de llamadas de emergencia, asignación de prioridad según gravedad.
2. **Gestión de Recursos**: Seguimiento de ambulancias, personal médico y camas disponibles en tiempo real.
3. **Asignación Inteligente**: Algoritmo para asignar el recurso más adecuado según la emergencia y la ubicación.
4. **Monitoreo en Tiempo Real**: Visualización de la ubicación de recursos y estado de las emergencias.
5. **Generación de Reportes**: Estadísticas sobre tiempos de respuesta, eficiencia en la asignación y otros indicadores clave.
6. **Comunicación**: Envío de notificaciones a los equipos médicos y hospitales.
7. **Registro Médico**: Capacidad de acceder y actualizar información médica básica de los pacientes.

### Requerimientos No Funcionales
1. **Alta Disponibilidad**: El sistema debe funcionar 24/7 con un tiempo de actividad mínimo del 99.9%.
2. **Escalabilidad**: Capacidad para manejar hasta 500 emergencias simultáneas.
3. **Rendimiento**: Tiempo de respuesta inferior a 1 segundo para operaciones críticas.
4. **Seguridad**: Protección de datos sensibles de pacientes según normativas de salud.
5. **Usabilidad**: Interfaz intuitiva para operadores que trabajan bajo presión.
6. **Integración**: Capacidad para integrarse con sistemas externos (hospitales, servicios de emergencia).
7. **Operación Offline**: Funcionamiento parcial sin conexión a internet en caso de desastres.

### Stakeholders
1. **Operadores del Centro de Control**: Reciben llamadas y gestionan la asignación de recursos.
2. **Personal Médico**: Reciben notificaciones y actualizan el estado de las emergencias.
3. **Hospitales**: Reciben información sobre pacientes entrantes y actualizan disponibilidad.
4. **Administradores del Sistema**: Supervisan el funcionamiento y analizan rendimiento.
5. **Pacientes**: Beneficiarios finales del servicio.
6. **Autoridades de Salud**: Requieren estadísticas y cumplimiento normativo.

## 3.1 Análisis del Caso de Estudio

### Revisión Inicial
Tras analizar los requerimientos, identificamos que el SGEM es un sistema crítico que requiere alta disponibilidad, tiempo de respuesta rápido y seguridad en el manejo de datos. El sistema debe ser robusto para funcionar en situaciones de emergencia donde la conectividad puede ser limitada.

### Identificación de Stakeholders y sus Preocupaciones

| Stakeholder | Preocupaciones Principales |
|-------------|----------------------------|
| Operadores del Centro de Control | - Rapidez en la recepción y procesamiento de llamadas<br>- Interfaz intuitiva que minimice errores<br>- Visualización clara de recursos disponibles |
| Personal Médico | - Notificaciones claras y prioritizadas<br>- Acceso rápido a información relevante del paciente<br>- Actualización simple del estado de emergencias |
| Hospitales | - Información precisa sobre pacientes entrantes<br>- Integración con sistemas hospitalarios existentes<br>- Actualización fácil de disponibilidad de recursos |
| Administradores del Sistema | - Monitoreo del rendimiento del sistema<br>- Generación de reportes estadísticos<br>- Seguridad y cumplimiento normativo |
| Pacientes | - Tiempo de respuesta rápido<br>- Privacidad de información médica<br>- Atención adecuada según gravedad |
| Autoridades de Salud | - Cumplimiento de normativas de salud<br>- Estadísticas de rendimiento del sistema<br>- Transparencia en la gestión de emergencias |

## 3.2 Toma de Decisiones en el Diseño Arquitectónico

### Registro de Decisiones Arquitectónicas

| Decisión | Opciones Consideradas | Elección | Justificación |
|----------|------------------------|----------|---------------|
| Estilo arquitectónico principal | Monolítico vs. Microservicios vs. Híbrido | **Híbrido con núcleo monolítico y servicios satélite** | El núcleo crítico del sistema (gestión de emergencias) requiere alta cohesión y rendimiento, mientras que funciones como reportes y gestión de recursos pueden implementarse como servicios independientes para mejor escalabilidad. |
| Patrón de arquitectura | Capas vs. Microkernel vs. MVC | **Microkernel con MVC** | Permite tener un núcleo robusto para funciones críticas y agregar/modificar servicios satélite sin afectar el núcleo. El patrón MVC se aplicará en el frontend para separar presentación de lógica. |
| Arquitectura de datos | Base de datos relacional vs. NoSQL vs. Híbrida | **Híbrida (SQL + NoSQL)** | Datos estructurados críticos (pacientes, recursos) en SQL para garantizar ACID, datos de monitoreo en tiempo real y ubicación en NoSQL para mejor rendimiento. |
| Infraestructura | On-premises vs. Nube vs. Híbrida | **Híbrida con redundancia** | Servidores principales locales para garantizar funcionamiento en caso de pérdida de conectividad, con respaldo y escalabilidad en la nube. |
| Comunicación entre componentes | REST vs. Mensajería vs. Híbrido | **Híbrido (REST + Mensajería)** | REST para operaciones síncronas y comunicación con clientes, mensajería para eventos asíncronos y notificaciones en tiempo real. |
| Estrategia de seguridad | Centralizada vs. Por servicio | **Capa de seguridad centralizada con políticas específicas por servicio** | Garantiza consistencia en la seguridad mientras permite ajustes específicos para cada componente. |
| Interfaz de usuario | Aplicación web vs. Nativa vs. Híbrida | **Aplicación web progresiva con capacidades offline** | Facilita la accesibilidad desde diferentes dispositivos mientras mantiene funcionalidad básica sin conexión. |

## 3.3 Creación de Vistas Arquitectónicas

### Diagrama 1: Vista Física
Este diagrama muestra la infraestructura física del sistema con un enfoque híbrido (cloud y on-premises):
* **Dispositivos**: Se dividen en Dispositivos Móviles y Estaciones de Trabajo
* **AWS Cloud**:
   * API Gateway como punto de entrada
   * EC2 para los servidores de aplicación
   * RDS para la base de datos
   * S3 para almacenamiento
   * SQS para la cola de mensajes
* **On-Premises**:
   * Balanceador de Carga
   * Servidor de Aplicaciones
   * Base de Datos Principal

Este diseño implementa la decisión arquitectónica de utilizar una infraestructura híbrida con redundancia, donde los sistemas críticos tienen respaldo local y capacidades escalables en la nube.

### Diagrama 2: Vista Lógica
El diagrama representa la organización de los componentes lógicos del sistema siguiendo el patrón Microkernel:
* **InterfazUsuario**: Clase abstracta con cuatro especializaciones (Operador, PersonalMédico, Hospital, Administrador)
* **NúcleoGestiónEmergencias**: El componente central del sistema
* **Servicios Satélite**:
   * ServicioGestiónRecursos
   * ServicioMonitoreo
   * ServicioNotificaciones
   * ServicioReportes
* **SistemaBD**: Para persistencia de datos

El diagrama muestra claramente las relaciones entre componentes:
* "controla" entre interfaces y núcleo
* "genera" entre administrador y reportes
* "agregación", "composición" y "dependencia" entre servicios

### Diagrama 3: Vista de Desarrollo
Este diagrama muestra cómo se estructura el software en términos de capas y componentes:
* **Frontend**: Aplicación Web y Aplicación Móvil
* **Backend**:
   * API REST como punto de entrada
   * Servicios Core (Emergencias, Recursos, Notificaciones)
   * Capa de Infraestructura (Logs, Autenticación, Cola de Mensajes)
   * Capa de Datos (Acceso a Datos, Repositorios)

Esta estructura sigue un patrón de arquitectura en capas con una clara separación de responsabilidades.

### Diagrama 4: Vista de Procesos
El diagrama muestra el flujo de trabajo del sistema desde la recepción de una emergencia hasta su resolución:
* **Inicio**: Operadores del Centro de Control
* **Validación**: Verificación de la emergencia
* **Procesamiento**: Ingreso al SGEM, validación, asignación de recursos
* **Ejecución**: Despacho de ambulancias y personal
* **Confirmación**: Validación por el equipo médico
* **Cierre**: Atención médica, traslado y confirmación de recepción

Este flujo muestra las interacciones entre los diferentes actores y el sistema durante una emergencia.

## 3.4 Aplicación de Patrones Arquitectónicos

### Patrón Microkernel
El patrón Microkernel se ha seleccionado como la base de la arquitectura del SGEM debido a su capacidad para manejar sistemas que requieren un núcleo central confiable con extensiones modulares.

#### Estructura del Patrón:
- **Núcleo (Kernel)**: Contiene la funcionalidad mínima esencial para el sistema, incluyendo la gestión de emergencias y la asignación de recursos.
- **Adaptadores de Servicios**: Componentes que conectan el núcleo con servicios externos como hospitales, sistemas de geolocalización, etc.
- **Servicios Satélite**: Módulos complementarios como reportes, análisis estadísticos, visualización avanzada, que pueden desplegarse y actualizarse de forma independiente.

#### Aplicación en el SGEM:
- **Núcleo**: Gestión de llamadas de emergencia, clasificación de emergencias, asignación básica de recursos.
- **Adaptadores**: Conectores para sistemas hospitalarios, servicios de geolocalización, sistemas de notificaciones.
- **Servicios Satélite**: Reportes estadísticos, visualización de mapas, optimización avanzada de rutas, predicción de demanda.

#### Beneficios:
- Permite que el sistema central sea altamente confiable y de alto rendimiento.
- Facilita la extensión del sistema con nuevas funcionalidades sin afectar el núcleo.
- Permite la actualización de servicios satélite independientemente del núcleo.
- Proporciona resiliencia, ya que el núcleo puede seguir funcionando incluso si algunos servicios satélite fallan.

### Patrón Modelo-Vista-Controlador (MVC)
El patrón MVC se ha seleccionado para la implementación de las interfaces de usuario del SGEM, facilitando la separación entre la lógica de negocio y la presentación.

#### Estructura del Patrón:
- **Modelo**: Representa la información y las reglas de negocio del sistema.
- **Vista**: Presenta la información al usuario y maneja la interacción.
- **Controlador**: Actúa como intermediario entre el Modelo y la Vista, respondiendo a eventos del usuario.

#### Aplicación en el SGEM:
- **Modelo**: Representación de emergencias, recursos, pacientes y sus relaciones.
- **Vista**: Interfaces para operadores, personal médico y administradores.
- **Controlador**: Manejo de eventos como asignación de recursos, actualización de estados, generación de reportes.

#### Beneficios:
- Facilita el desarrollo y mantenimiento de interfaces complejas.
- Permite que diferentes vistas presenten la misma información de manera distinta (ej. vista para operadores vs. vista para administradores).
- Mejora la testabilidad al separar la lógica de negocio de la interfaz.
- Facilita la adaptación de la interfaz a diferentes dispositivos (responsive design).

## 3.5 Diseño de la Arquitectura de Aplicación

### Arquitectura de Aplicación para el SGEM

#### Capas de la Aplicación:

1. **Capa de Presentación**
   - **Interfaz Web para Operadores**: Aplicación web progresiva optimizada para operadores del centro de control.
   - **Aplicación Móvil para Personal Médico**: Interfaz simplificada para equipos médicos en campo.
   - **Portal para Hospitales**: Interfaz para gestión de recursos hospitalarios y recepción de información.
   - **Panel de Administración**: Herramientas de configuración y monitoreo del sistema.

2. **Capa de Aplicación**
   - **Controladores**: Gestionan las interacciones con las interfaces de usuario.
   - **Servicios de Aplicación**: Coordinan la lógica de negocio y la comunicación entre componentes.
   - **Gestión de Autenticación y Autorización**: Control de acceso y seguridad.

3. **Capa de Dominio (Núcleo Microkernel)**
   - **Gestión de Emergencias**: Clasificación, priorización y seguimiento de emergencias.
   - **Asignación de Recursos**: Algoritmos para asignar recursos óptimos.
   - **Reglas de Negocio**: Lógica crítica del sistema.

4. **Capa de Servicios Satélite**
   - **Servicio de Geolocalización**: Tracking de recursos y optimización de rutas.
   - **Servicio de Análisis y Reportes**: Generación de estadísticas e informes.
   - **Servicio de Notificaciones**: Gestión de alertas y comunicaciones.
   - **Servicio de Integración**: Conectores con sistemas externos.

5. **Capa de Persistencia**
   - **Repositorios de Datos**: Acceso a bases de datos y almacenes de datos.
   - **Mapeo Objeto-Relacional**: Conversión entre objetos de dominio y estructuras de datos.
   - **Caché**: Almacenamiento temporal para mejora de rendimiento.

6. **Capa de Infraestructura**
   - **Bases de Datos**: SQL para datos estructurados, NoSQL para datos en tiempo real.
   - **Mensajería**: Sistema de colas para comunicación asíncrona.
   - **Almacenamiento**: Gestión de archivos y datos históricos.
   - **Monitoreo y Logging**: Seguimiento del sistema y registro de eventos.

#### Componentes de Comunicación:

1. **API Gateway**
   - Punto único de entrada para clientes externos
   - Enrutamiento y balanceo de carga
   - Seguridad perimetral

2. **Bus de Servicios Empresariales (ESB)**
   - Comunicación entre componentes internos
   - Transformación de mensajes
   - Orquestación de servicios

3. **Sistema de Mensajería**
   - Comunicación asíncrona
   - Publicación/suscripción para notificaciones
   - Colas de mensajes para procesamiento diferido

## 3.6 Documentación y Retroalimentación

### Evaluación de la Arquitectura

#### Cumplimiento de Requerimientos No Funcionales

| Requerimiento | Cumplimiento | Implementación |
|---------------|--------------|----------------|
| Alta Disponibilidad (99.9%) | ✅ | Arquitectura redundante con núcleo on-premises y respaldo en nube |
| Escalabilidad | ✅ | Servicios satélite escalables independientemente, bases de datos distribuidas |
| Rendimiento | ✅ | Núcleo optimizado para operaciones críticas, uso de caché, comunicación asíncrona |
| Seguridad | ✅ | Capa de seguridad centralizada, cifrado de datos sensibles, autenticación robusta |
| Usabilidad | ✅ | Interfaces específicas para cada tipo de usuario, diseño optimizado para contexto de uso |
| Integración | ✅ | Servicios de integración dedicados, APIs estandarizadas |
| Operación Offline | ✅ | Aplicación web progresiva con almacenamiento local, sincronización posterior |

#### Riesgos y Mitigaciones

| Riesgo | Probabilidad | Impacto | Mitigación |
|--------|-------------|---------|------------|
| Fallo total de conectividad | Baja | Alto | Infraestructura local redundante, procedimientos manuales de respaldo |
| Sobrecarga del sistema | Media | Alto | Escalado automático, mecanismos de throttling, monitoreo proactivo |
| Violación de seguridad | Baja | Crítico | Auditorías regulares, cifrado end-to-end, principio de menor privilegio |
| Inconsistencia de datos | Media | Medio | Transacciones ACID para datos críticos, reconciliación periódica |
| Latencia en comunicaciones | Media | Alto | Optimización de red, priorización de tráfico crítico |

### Conclusiones y Recomendaciones

La arquitectura propuesta para el Sistema de Gestión de Emergencias Médicas (SGEM) se ha diseñado considerando los requerimientos críticos de disponibilidad, rendimiento y seguridad que exige un sistema de esta naturaleza. El enfoque híbrido con un núcleo Microkernel y servicios satélite proporciona un balance óptimo entre confiabilidad para las funciones críticas y flexibilidad para la evolución del sistema.

**Recomendaciones para la implementación:**

1. Implementar primero el núcleo Microkernel con funcionalidad mínima viable.
2. Desarrollar los servicios satélite de forma incremental, comenzando por los más críticos.
3. Establecer un riguroso plan de pruebas, especialmente para escenarios de alta carga y funcionamiento offline.
4. Implementar monitoreo continuo para detectar problemas de rendimiento o disponibilidad.
5. Realizar auditorías de seguridad periódicas, especialmente en aspectos relacionados con datos médicos sensibles.
6. Planificar sesiones de capacitación específicas para cada tipo de usuario del sistema.

La arquitectura propuesta no solo satisface los requerimientos actuales, sino que también proporciona una base sólida para la evolución futura del sistema, permitiendo la incorporación de nuevas tecnologías y funcionalidades sin comprometer la estabilidad del núcleo crítico.

# Propuesta de Desarrollo de Arquitectura para Diego Alonso Rojas Vera (20211223D)

## Documento SRS - Sistema de Monitoreo en Tiempo Real para Ciudades Inteligentes

### Vistas Arquitectónicas a Desarrollar

#### Vista Lógica

Se relacionarán los requerimientos del sistema con entidades como:

- Módulos de captura de datos de sensores
- Entidades de procesamiento de datos
- Componentes de análisis y detección de eventos
- Servicios de notificación y alertas
- Interfaces de usuario para monitoreo

#### Vista de Procesos

Se documentarán los comportamientos concurrentes y comunicación entre:

- Procesos de captura de datos en tiempo real
- Flujos de procesamiento paralelo
- Mecanismos de comunicación asíncrona
- Protocolos de transmisión de datos
- Procesos de respuesta a eventos críticos

#### Vista de Desarrollo

Se organizarán los módulos en el código, detallando:

- Estructura de paquetes y componentes
- Dependencias entre módulos
- Capas de la aplicación
- Interfaces y contratos entre módulos
- Organización de bibliotecas y frameworks

#### Vista Física

Se especificará el despliegue en hardware y topología, incluyendo:

- Distribución de sensores IoT
- Nodos edge de procesamiento local
- Servidores en la nube para almacenamiento
- Infraestructura de comunicación
- Dispositivos de monitoreo y control

### Arquitectura de Aplicación

Se diseñará una arquitectura basada en microservicios que:

- Integre los componentes de manera coherente
- Asegure escalabilidad para el crecimiento de la red de sensores
- Garantice mantenibilidad mediante componentes desacoplados
- Se alinee con los requerimientos de monitoreo en tiempo real
- Aplique patrones arquitectónicos relevantes para sistemas distribuidos

El documento SRS incluirá la justificación de decisiones, diagramas de cada vista, descripción de patrones aplicados y el diagrama final de la arquitectura de aplicación.

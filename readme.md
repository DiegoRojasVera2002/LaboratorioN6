# Diseño Arquitectónico - Sistema de Gestión de Emergencias Médicas
### Diego Alonso Rojas Vera (20211223D)

## Documento SRS - Sistema de Gestión de Emergencias Médicas (SGEM)

### Vistas Arquitectónicas

#### Vista Lógica
La vista lógica relaciona los requerimientos del sistema con entidades:

- **Interfaz de Usuario**: Componente central que se extiende en múltiples interfaces especializadas (Operador, Personal Médico, Hospital, Administrador).
- **Núcleo de Gestión de Emergencias**: Módulo central que maneja las funciones críticas como recepción, clasificación y seguimiento de emergencias.
- **Servicios Especializados**: Componentes satélite como Gestión de Recursos, Monitoreo, Notificaciones y Reportes.
- **Sistema BD**: Capa de persistencia para almacenamiento y recuperación de datos.
- **Relaciones Estructuradas**: Conexiones de control, agregación, composición, dependencia y asociación entre componentes que definen el flujo de trabajo del sistema.

#### Vista de Procesos
La vista de procesos representa los comportamientos concurrentes y la comunicación entre componentes:

- **Flujo de Trabajo Operativo**: Desde el ingreso de datos de emergencia por operadores hasta la confirmación de recepción en hospital.
- **Procesos de Validación**: Puntos de decisión críticos que aseguran la integridad de los datos y disponibilidad de recursos.
- **Gestión de Asignación**: Algoritmos de optimización para la distribución de recursos médicos.
- **Comunicación entre Actores**: Interacción entre operadores del centro, sistema SGEM, equipos médicos y hospitales.
- **Confirmación de Procesos**: Puntos de verificación que garantizan la trazabilidad completa del servicio médico.

#### Vista de Desarrollo
La vista de desarrollo organiza los módulos en el código:

- **Frontend**: Separación entre aplicaciones web y móviles que comparten acceso a servicios backend.
- **Backend**: Implementación de API REST como punto de entrada unificado a los servicios.
- **Servicios Core**: Implementación modular de funcionalidades críticas (Emergencias, Recursos, Notificaciones).
- **Capas de Infraestructura**: Componentes transversales como autenticación, mensajería, monitoreo y acceso a datos.
- **Repositorios**: Almacenamiento de datos estructurado con acceso controlado a través de la capa de datos.

#### Vista Física
La vista física especifica el despliegue en hardware y topología:

- **Dispositivos**: Separación entre dispositivos móviles para personal en campo y estaciones de trabajo para operadores.
- **Infraestructura Híbrida**: Combinación de componentes en AWS Cloud (alta escalabilidad) y On-Premises (alta disponibilidad).
- **Componentes Cloud**: API Gateway, servidores EC2, bases de datos RDS, almacenamiento S3 y colas de mensajes SQS.
- **Componentes On-Premises**: Balanceador de carga, servidor de aplicaciones principal y base de datos redundante.
- **Conexiones Redundantes**: Múltiples rutas de comunicación para garantizar la disponibilidad del sistema.

### Arquitectura de Aplicación
La arquitectura propuesta se basa en un modelo híbrido que combina:

- **Núcleo Microkernel**: Componente central que gestiona las funciones críticas del sistema.
- **Servicios Satélite**: Componentes modulares que pueden evolucionar independientemente.
- **Patrón MVC**: Separación clara entre datos, lógica de negocio e interfaces de usuario.
- **Infraestructura Redundante**: Combinación de despliegue cloud y on-premises.
- **Comunicación Asíncrona**: Sistema de mensajería para operaciones no críticas.
- **APIs RESTful**: Interfaces estandarizadas para la comunicación entre componentes.

El documento SRS completo incluye la justificación de decisiones arquitectónicas, diagramas detallados de cada vista, descripción de patrones aplicados y evaluación de la arquitectura contra los requerimientos no funcionales.

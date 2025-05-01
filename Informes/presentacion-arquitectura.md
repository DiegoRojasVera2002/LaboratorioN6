# Presentación: Diseño Arquitectónico
## Sistema de Gestión de Emergencias Médicas (SGEM)

---

## Análisis del Caso de Estudio

### Sistema de Gestión de Emergencias Médicas
- Sistema crítico para coordinación de atención médica urgente
- Gestión de recursos (ambulancias, personal, camas)
- Monitoreo en tiempo real
- Alta disponibilidad (99.9%)
- Datos sensibles de pacientes

### Stakeholders Principales
- Operadores del Centro de Control
- Personal Médico
- Hospitales
- Administradores del Sistema
- Pacientes
- Autoridades de Salud

---

## Decisiones Arquitectónicas

| Decisión | Elección | Justificación |
|----------|----------|---------------|
| Estilo arquitectónico | **Híbrido** | Núcleo crítico cohesivo + servicios modulares |
| Patrón principal | **Microkernel + MVC** | Núcleo robusto con extensibilidad |
| Arquitectura de datos | **Híbrida (SQL + NoSQL)** | ACID para datos críticos, NoSQL para tiempo real |
| Infraestructura | **Híbrida con redundancia** | Alta disponibilidad incluso con fallos |
| Comunicación | **REST + Mensajería** | Operaciones síncronas y eventos asíncronos |

---

## Vistas Arquitectónicas

### Vista Lógica
- **Núcleo de Gestión de Emergencias**: Recepción, clasificación, asignación
- **Servicios de Gestión de Recursos**: Ambulancias, personal, camas
- **Servicios de Monitoreo**: Geolocalización, telemetría, análisis
- **Servicios de Soporte**: Notificaciones, reportes, usuarios
- **Interfaces Externas**: APIs para sistemas externos

### Vista Física
- **Servidores On-Premises**: Para funciones críticas
- **Infraestructura en Nube**: Escalabilidad y respaldo
- **Dispositivos de Usuario Final**: Estaciones de trabajo, móviles, pantallas

---

## Patrones Arquitectónicos

### Patrón Microkernel
- **Núcleo**: Gestión de emergencias, clasificación, asignación básica
- **Adaptadores**: Conectores para sistemas externos
- **Servicios Satélite**: Reportes, visualización, optimización avanzada
- **Beneficios**: Alta confiabilidad, extensibilidad, resiliencia

### Patrón MVC
- **Modelo**: Emergencias, recursos, pacientes
- **Vista**: Interfaces específicas para cada tipo de usuario
- **Controlador**: Manejo de eventos del sistema
- **Beneficios**: Separación de responsabilidades, facilidad de mantenimiento

---

## Arquitectura de Aplicación

### Capas del Sistema
1. **Capa de Presentación**: Interfaces web y móviles
2. **Capa de Aplicación**: Controladores y servicios
3. **Capa de Dominio**: Núcleo Microkernel
4. **Servicios Satélite**: Geolocalización, reportes, notificaciones
5. **Capa de Persistencia**: Repositorios y mapeo
6. **Capa de Infraestructura**: Bases de datos, mensajería, monitoreo

### Componentes de Comunicación
- **API Gateway**: Punto único de entrada
- **Bus de Servicios Empresariales**: Comunicación interna
- **Sistema de Mensajería**: Comunicación asíncrona

---

## Evaluación de la Arquitectura

### Cumplimiento de Requerimientos
- ✅ **Alta Disponibilidad**: Arquitectura redundante
- ✅ **Escalabilidad**: Servicios satélite independientes
- ✅ **Rendimiento**: Núcleo optimizado, caché, comunicación asíncrona
- ✅ **Seguridad**: Capa centralizada, cifrado de datos sensibles
- ✅ **Usabilidad**: Interfaces específicas para cada usuario
- ✅ **Integración**: APIs estandarizadas
- ✅ **Operación Offline**: PWA con almacenamiento local

---

## Conclusiones y Recomendaciones

### Fortalezas de la arquitectura
- Balanceo entre confiabilidad y flexibilidad
- Alta disponibilidad incluso en situaciones críticas
- Seguridad adecuada para datos médicos sensibles
- Escalabilidad para manejar picos de demanda

### Recomendaciones
1. Implementar primero el núcleo con funcionalidad mínima viable
2. Desarrollar servicios satélite incrementalmente
3. Establecer plan riguroso de pruebas
4. Implementar monitoreo continuo
5. Realizar auditorías de seguridad periódicas
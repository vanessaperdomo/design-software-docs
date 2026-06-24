```markdown
# Domain map

> Estado: 🟡 En progreso | Última actualización: 2026-06-18
> Autor: vanessaperdomo | Equipo: Por definir

## Bounded contexts

| Contexto | Responsabilidad | Microservicio |
|----------|-----------------|---------------|
| Identidad y Acceso | Autenticación, autorización, roles y permisos | iam-service |
| Datos de Referencia | Estructura institucional, catálogos y parámetros | reference-data-service |
| Gestión Académica | Programas, competencias, RAPs, fichas y oferta | academic-management-service |
| Ambientes de Formación | Ambientes físicos, inventario, disponibilidad y reservas | training-environment-service |
| Horarios | Motor de asignación, validación de conflictos y sesiones | scheduling-service |
| Actores | Instructores, aprendices, empresas y etapa productiva | actors-service |
| Documentos | Plantillas, versiones, PDF y ciclo de vida documental | document-service |
| Seguimiento | KPIs, alertas, notificaciones y plan de mejoramiento | monitoring-service |
| Auditoría | Registro append-only de acciones sensibles | audit-service |

## Relaciones entre contextos

```
iam-service
    ↓ autentica a todos los servicios

reference-data-service
    ↓ provee catálogos a → academic-management-service
    ↓ provee catálogos a → training-environment-service
    ↓ provee catálogos a → scheduling-service
    ↓ provee catálogos a → actors-service

academic-management-service
    ↓ provee fichas y programas a → scheduling-service
    ↓ provee fichas a → monitoring-service

training-environment-service
    ↓ provee disponibilidad de ambientes a → scheduling-service

actors-service
    ↓ provee instructores y aprendices a → scheduling-service
    ↓ provee aprendices a → monitoring-service

scheduling-service
    ↓ publica eventos de sesión a → monitoring-service
    ↓ publica eventos a → audit-service

document-service
    ↓ genera reportes para → monitoring-service
    ↓ registra acciones en → audit-service

monitoring-service
    ↓ publica alertas a → notification (dentro del mismo servicio)
    ↓ registra acciones en → audit-service
```

## Regla de integración

Ningún servicio accede directamente a la base de datos de otro. La integración se realiza
exclusivamente mediante API REST, eventos de dominio o contratos explícitos. Todo acceso
lleva `correlation_id` para trazabilidad distribuida.

## Dominios SENA vs plataforma

| Tipo | Contextos |
|------|-----------|
| Dominio SENA (negocio) | Gestión Académica, Ambientes, Horarios, Actores, Seguimiento |
| Plataforma transversal | Identidad, Datos de Referencia, Documentos, Auditoría |
```

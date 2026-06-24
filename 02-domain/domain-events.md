# Domain events

> Estado: 🟡 En progreso | Última actualización: 2026-06-18
> Autor: vanessaperdomo | Equipo: Por definir

## Estructura base de un evento

Todo evento de dominio debe incluir:

| Campo | Tipo | Descripción |
|-------|------|-------------|
| event_id | UUID | Identificador único del evento |
| event_type | string | Nombre del evento en PascalCase |
| occurred_at | ISO 8601 | Fecha y hora de ocurrencia |
| source | string | Microservicio que publica el evento |
| correlation_id | UUID | ID de trazabilidad distribuida |
| actor_id | UUID | Usuario o sistema que originó la acción |
| data | object | Payload específico del evento |

## Catálogo de eventos por contexto

### Horarios
| Evento | Publicado por | Consumido por | Significado |
|--------|---------------|---------------|-------------|
| `SchedulePlanned` | scheduling-service | monitoring-service, audit-service | Se creó un nuevo bloque de horario válido |
| `ScheduleChanged` | scheduling-service | monitoring-service, audit-service | Se modificó un horario existente |
| `ScheduleCancelled` | scheduling-service | monitoring-service, audit-service | Se canceló un bloque de horario |
| `ConflictDetected` | scheduling-service | audit-service | Se detectó y bloqueó un intento de conflicto |

### Ejecución formativa
| Evento | Publicado por | Consumido por | Significado |
|--------|---------------|---------------|-------------|
| `TrainingSessionExecuted` | scheduling-service | monitoring-service, audit-service | Una sesión fue confirmada como ejecutada |
| `AttendanceTraceRegistered` | scheduling-service | monitoring-service | Se registró la asistencia de una sesión |
| `SessionNoveltyRegistered` | scheduling-service | monitoring-service | Se registró una novedad en una sesión |

### Evidencias y progreso
| Evento | Publicado por | Consumido por | Significado |
|--------|---------------|---------------|-------------|
| `EvidenceSubmitted` | academic-management-service | monitoring-service, audit-service | Un aprendiz entregó una evidencia |
| `EvidenceValidated` | academic-management-service | monitoring-service, audit-service | Una evidencia fue validada por el instructor |
| `LearnerProgressUpdated` | monitoring-service | audit-service | Se actualizó el avance de un aprendiz |

### Proyectos formativos
| Evento | Publicado por | Consumido por | Significado |
|--------|---------------|---------------|-------------|
| `FormativeProjectMilestoneReached` | academic-management-service | monitoring-service | Se alcanzó un hito del proyecto formativo |

### Documentos
| Evento | Publicado por | Consumido por | Significado |
|--------|---------------|---------------|-------------|
| `PdfGenerationRequested` | monitoring-service, scheduling-service | document-service | Se solicitó generación de un documento PDF |
| `PdfGenerated` | document-service | solicitante | El PDF fue generado y está disponible |

### Seguimiento y alertas
| Evento | Publicado por | Consumido por | Significado |
|--------|---------------|---------------|-------------|
| `AlertTriggered` | monitoring-service | audit-service | Se activó una alerta por desviación de KPI |
| `ImprovementPlanCreated` | monitoring-service | audit-service | Se creó un plan de mejoramiento |

### Auditoría
| Evento | Publicado por | Consumido por | Significado |
|--------|---------------|---------------|-------------|
| `AuditEvidenceRegistered` | audit-service | — | Registro inmutable de acción sensible (append-only) |
| `PolicyViolationDetected` | audit-service | — | Se detectó una violación de política |

## Principios de eventos

- Los eventos son hechos pasados e inmutables; nunca se modifican.
- La integración entre servicios no depende de joins entre bases de datos.
- Un consumidor puede ignorar eventos que no le conciernen sin afectar al publicador.
- El `correlation_id` debe propagarse en toda la cadena de eventos de una operación.
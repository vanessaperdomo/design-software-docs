# Entities and rules

> Estado: 🟡 En progreso | Última actualización: 2026-06-18
> Autor: vanessaperdomo | Equipo: Por definir

## Entidades principales por contexto

### Identidad y Acceso
| Entidad | Atributos clave | Invariantes |
|---------|-----------------|-------------|
| Usuario | id, nombre, email, rol | Un usuario tiene al menos un rol activo |
| Rol | id, nombre, permisos[] | Los permisos son inmutables una vez asignados a un rol en producción |
| Sesión | id, usuario_id, token, expira_en | Una sesión expira y no puede reutilizarse |

### Datos de Referencia
| Entidad | Atributos clave | Invariantes |
|---------|-----------------|-------------|
| Regional | id, nombre, código | El código es único a nivel nacional |
| Centro de formación | id, regional_id, nombre, código | Pertenece a exactamente una regional |
| Catálogo | id, tipo, código, nombre | El código es único dentro de su tipo |
| Parámetro | id, clave, valor, tipo | La clave es única dentro del sistema |

### Gestión Académica
| Entidad | Atributos clave | Invariantes |
|---------|-----------------|-------------|
| Programa de formación | id, nombre, código, duración_horas | El código es único institucional |
| Competencia | id, programa_id, nombre, código | Pertenece a exactamente un programa |
| RAP | id, competencia_id, descripción, criterios[] | Pertenece a exactamente una competencia |
| Ficha | id, programa_id, número, jornada, estado | El número de ficha es único institucional |
| Oferta | id, ficha_id, centro_id, periodo | Una oferta activa tiene exactamente una ficha |

### Ambientes de Formación
| Entidad | Atributos clave | Invariantes |
|---------|-----------------|-------------|
| Ambiente | id, nombre, tipo, capacidad, centro_id | La capacidad debe ser mayor a cero |
| Inventario | id, ambiente_id, recurso, cantidad | La cantidad no puede ser negativa |
| Disponibilidad | id, ambiente_id, fecha, franja_id, estado | Un ambiente no puede estar disponible y reservado simultáneamente |
| Reserva | id, ambiente_id, franja_id, motivo | Una reserva bloquea la disponibilidad del ambiente |

### Horarios
| Entidad | Atributos clave | Invariantes |
|---------|-----------------|-------------|
| Franja horaria | id, jornada, hora_inicio, hora_fin | hora_fin debe ser mayor a hora_inicio |
| Horario | id, ficha_id, instructor_id, ambiente_id, franja_id, fecha | **Triple restricción**: instructor, ambiente y ficha son únicos por franja y fecha |
| Sesión de clase | id, horario_id, fecha, estado | Una sesión programada no es una sesión ejecutada hasta confirmación |
| Conflicto | id, tipo, entidad_id, franja_id, fecha | El sistema impide persistir un horario con conflicto detectado |

### Actores
| Entidad | Atributos clave | Invariantes |
|---------|-----------------|-------------|
| Instructor | id, nombre, tipo_vinculación, horas_max_semana | Las horas máximas dependen del tipo de vinculación |
| Aprendiz | id, nombre, ficha_id, estado | Un aprendiz activo pertenece a exactamente una ficha vigente |
| Empresa | id, nombre, nit, sector | El NIT es único |
| Etapa productiva | id, aprendiz_id, empresa_id, fecha_inicio, fecha_fin | La fecha de fin debe ser posterior a la de inicio |

### Seguimiento
| Entidad | Atributos clave | Invariantes |
|---------|-----------------|-------------|
| Sesión ejecutada | id, sesion_clase_id, asistentes[], novedades, confirmada_por | Solo el instructor asignado puede confirmar |
| KPI | id, nombre, fórmula, baseline, meta_30d, meta_90d | El baseline se fija al momento del primer lanzamiento |
| Alerta | id, tipo, entidad_id, mensaje, estado | Una alerta abierta no puede cerrarse sin acción registrada |
| Plan de mejoramiento | id, alerta_id, acciones[], responsable, fecha_límite | Debe tener al menos una acción registrada |

## Reglas de negocio globales

1. **Triple restricción de horarios**: un instructor, un ambiente y una ficha no pueden coincidir en la misma franja horaria y fecha. El sistema rechaza la asignación antes de persistirla.
2. **Fuente maestra externa**: el sistema no reemplaza SOFIA Plus. Los datos maestros de fichas, programas e instructores se sincronizan desde fuentes autorizadas.
3. **Auditoría obligatoria**: toda acción sensible (creación, modificación o eliminación de horarios, actores o configuraciones) genera un registro de auditoría inmutable.
4. **Correlación distribuida**: toda operación entre servicios debe propagar `correlation_id`, `actor_id` y `source_service`.
5. **Carga horaria máxima**: el sistema valida que un instructor no supere su límite de horas semanales según tipo de vinculación.
6. **Sesión vs ejecución**: una sesión programada y una sesión ejecutada son entidades distintas. La ejecución requiere confirmación explícita del instructor.
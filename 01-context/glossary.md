# Glosario

> Estado: 🟡 En progreso | Última actualización: 2026-06-16
> Autor: vanessaperdomo | Equipo: Por definir

| Término | Definición | Contexto |
|---------|------------|----------|
| Ficha | Grupo de aprendices matriculados en un programa de formación específico, identificado con un número único institucional. Es la unidad operativa central de la formación SENA. | SENA |
| Jornada | Bloque de tiempo institucional en el que se ejecuta formación: mañana, tarde, noche o fin de semana. Cada jornada tiene franjas horarias predefinidas. | SENA |
| Horario | Asignación formal de una ficha a un instructor y un ambiente físico en una franja horaria específica. Constituye el objeto central del motor de programación. | Dominio |
| Instructor | Profesional del SENA responsable de ejecutar la formación en una o varias fichas. Tiene carga horaria semanal máxima definida según su tipo de vinculación. | SENA |
| Aprendiz | Persona matriculada en una ficha de formación del SENA. Tiene seguimiento de asistencia, avance por RAP y participación en proyectos formativos. | SENA |
| Ambiente | Espacio físico (salón, laboratorio, taller, aula virtual) donde se ejecuta la formación. Tiene capacidad, tipo de recursos y disponibilidad registrada. | SENA |
| Franja horaria | Intervalo de tiempo definido dentro de una jornada en el que se programa una sesión. Ejemplo: 06:00–08:00, 08:00–10:00. | Dominio |
| Conflicto | Situación en la que un instructor, ambiente o ficha queda asignado a dos o más sesiones simultáneas. El sistema previene su ocurrencia en tiempo real. | Dominio |
| Triple restricción | Regla de validación del motor de horarios: un instructor, un ambiente y una ficha no pueden estar asignados a más de una sesión en la misma franja horaria. | Dominio |
| RAP | Resultado de Aprendizaje del Proyecto. Unidad mínima de competencia evaluable dentro de un programa de formación. Cada competencia agrupa varios RAPs. | SENA |
| Competencia | Capacidad que el aprendiz debe desarrollar durante la formación, compuesta por varios RAPs con criterios de evaluación definidos. | SENA |
| Programa de formación | Diseño curricular aprobado por el SENA que define competencias, RAPs, duración total y perfil de egreso. Es la base del diseño pedagógico. | SENA |
| Proyecto formativo | Herramienta pedagógica que integra las competencias del programa mediante actividades, entregables e hitos reales. Tiene dependencias entre fases. | SENA |
| Evidencia | Producto o demostración entregada por el aprendiz que permite verificar el logro de un RAP. Puede ser documental, de desempeño o de conocimiento. | SENA |
| Oferta | Apertura institucional de un programa de formación en un centro específico para un periodo determinado. Origina las fichas asociadas. | SENA |
| Centro de formación | Unidad operativa del SENA donde se ejecuta la formación profesional integral. Agrupa fichas, instructores y ambientes bajo una dirección. | SENA |
| Regional | Unidad territorial del SENA que agrupa varios centros de formación. Nivel superior de la estructura institucional. | SENA |
| Coordinador académico | Funcionario responsable de la programación y seguimiento de la formación en el centro. Usuario principal del motor de horarios. | SENA |
| Etapa productiva | Fase de la formación en la que el aprendiz aplica competencias en una empresa o entidad. Tiene seguimiento diferenciado en el sistema. | SENA |
| Sesión | Ejecución real de un bloque de formación en una fecha, franja, ambiente e instructor determinados. Queda registrada con asistencia y novedades. | Dominio |
| Sesión de clase | Instancia programada de formación asociada a un horario. Se diferencia de la sesión ejecutada hasta que el instructor la confirma. | Dominio |
| Observación | Registro de un problema, novedad o comentario vinculado a una sesión, instructor, ficha o ambiente. Tiene estado: abierta o resuelta. | Dominio |
| Carga horaria | Total de horas semanales o periódicas asignadas a un instructor. El sistema la calcula y reporta automáticamente. | Dominio |
| Disponibilidad | Estado de un ambiente o instructor que indica si puede ser asignado en una franja horaria determinada. | Dominio |
| Asignación | Acto de vincular un instructor y un ambiente a una ficha en una franja horaria. Queda registrada en el motor de horarios tras pasar la validación. | Dominio |
| Plan de mejoramiento | Documento institucional que recoge acciones correctivas derivadas del seguimiento de KPIs y alertas de desviación formativa. | SENA |
| KPI | Indicador clave de desempeño. Métricas como tasa de conflictos, ocupación de ambientes y tiempo de planificación que miden la eficacia del sistema. | Dominio |
| Alerta | Notificación automática generada por el sistema cuando se detecta una desviación respecto a un umbral definido (conflicto, baja asistencia, KPI fuera de rango). | Dominio |
| Auditoría | Registro inmutable y trazable de todas las acciones sensibles realizadas en el sistema, con actor, timestamp y contexto. | Dominio |
| Correlation ID | Identificador único que se propaga en todas las llamadas entre microservicios para permitir trazabilidad distribuida de una operación de extremo a extremo. | Técnico |
| Bounded context | Frontera explícita dentro del dominio en la que un modelo de datos y sus reglas de negocio son consistentes y autónomos. Cada microservicio respeta su bounded context. | Técnico |
| Microservicio | Unidad de despliegue independiente con base de datos propia, contrato de API definido y responsabilidad acotada a un bounded context del dominio. | Técnico |
| Evento de dominio | Hecho relevante ocurrido en un microservicio que se publica para que otros servicios reaccionen sin acoplamiento directo. Ejemplo: `SchedulePlanned`, `AttendanceTraceRegistered`. | Técnico |
| Contrato | Especificación formal de la interfaz de un componente: endpoints, payloads, eventos y sus esquemas. Definido en OpenAPI o AsyncAPI. | Técnico |
| Worker | Componente que ejecuta tareas asíncronas en segundo plano: generación de PDF, validación de conflictos, envío de notificaciones. No expone API pública. | Técnico |
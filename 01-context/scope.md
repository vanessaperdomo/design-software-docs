# Alcance

> Estado: 🟡 En progreso | Última actualización: 2026-06-16
> Autor: vanessaperdomo | Equipo: Por definir

## En alcance

- Gestión de catálogos base: ambientes, fichas e instructores
- Motor de horarios con validación automática de conflictos bajo triple restricción
  (instructor + ambiente + ficha)
- Consulta de disponibilidad de ambientes por fecha y franja horaria
- Reporte de carga horaria acumulada por instructor
- Módulo de observaciones vinculadas a instructores, fichas o ambientes
- Trazabilidad de ejecución formativa: sesiones, asistencia, novedades e incidencias
- Gestión de proyectos formativos, entregables, hitos y dependencias
- Seguimiento de avance por aprendiz, ficha, RAP y evidencia
- Generación de reportes y documentos PDF exportables
- Auditoría completa de acciones sensibles
- Notificaciones y alertas de desviaciones

## Fuera de alcance

- Integración automática con sistemas ERP externos (SOFIA Plus, nómina, matrículas)
- Reemplazo de SOFIA Plus como fuente maestra institucional
- Notificaciones push / SMS / WhatsApp automáticas (fase 1)
- Aplicación móvil nativa (Android / iOS); el sistema será web-responsive
- Módulo de inasistencias o calificaciones de aprendices
- Operación offline

## Supuestos

- Los coordinadores adoptarán el sistema como fuente única de verdad,
  abandonando sus hojas de cálculo paralelas
- Las reglas de franjas horarias y jornadas son estandarizables y no varían
  caóticamente semana a semana para una misma ficha
- La validación instructor + ambiente + hora cubre el 95 %+ de los errores
  operativos actuales
- La información base (capacidad de ambientes, disponibilidad de instructores)
  se ingresará correctamente desde el inicio

## Restricciones

- El sistema no será fuente maestra de datos institucionales; los datos maestros
  provienen de fuentes externas autorizadas
- Toda regla institucional debe trazarse a fuente normativa, documento institucional
  o decisión explícita del product owner
- No se inventan campos, tablas, endpoints ni reglas no confirmadas
- Alineación obligatoria con Ley 1581 de 2012 (protección de datos personales)
  y Ley 594 de 2000 (gestión documental)
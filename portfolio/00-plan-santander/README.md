# Plan de desarrollo — Analista de Ciberseguridad

Este plan organiza evidencia para una postulación enfocada en gestión de vulnerabilidades, hardening, riesgos, KPIs/KRIs y seguimiento de remediaciones. La evidencia debe ser real, anonimizada y producida solo en entornos autorizados.

## Regla de trabajo

**Aprender → practicar → registrar evidencia → explicar el resultado.** Una competencia se considera cubierta solo si existe un artefacto revisable y se puede explicar sin apuntes.

## Fases y entregables

| Fase | Foco | Entregable verificable |
|---|---|---|
| 1 | Laboratorio base | Inventario, escaneo autorizado, priorización, remediación y re-escaneo |
| 2 | Hardening | Índice antes/después, cambios aplicados y excepciones justificadas |
| 3 | Riesgos y métricas | Registro de riesgos, KPIs/KRIs y decisiones asociadas |
| 4 | Frameworks | Mapeo de controles a CIS, NIST CSF e ISO 27001 |
| 5 | Coordinación | Ticket, RACI y reporte ejecutivo de remediación |

## Límites de seguridad

- Escanear exclusivamente VMs propias o activos con autorización explícita.
- Mantener objetivos vulnerables en una red aislada; nunca exponerlos a internet.
- Crear snapshots antes de aplicar cambios de hardening.
- No publicar credenciales, IPs públicas, tokens, rutas personales ni reportes sin anonimizar.

## Evidencia inicial

- [Guion Bitácora 2](bitacora_2_guion.md)
- [Matriz de competencias](matriz_competencias.md)
- [Registro semanal](registro_semanal.md)
- [Laboratorio de vulnerabilidades](../01-gestion-vulnerabilidades/lab-octubre/README.md)
- [Laboratorio de hardening](../02-hardening/lab-octubre-lynis/README.md)

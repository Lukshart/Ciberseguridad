# Registro de vulnerabilidades — ejemplo

| ID | Activo | Hallazgo | Prioridad | Estado | Control aplicado | Evidencia |
|---|---|---|---|---|---|---|
| VULN-001 | ACT-01 | Acceso SSH protegido solo por contraseña débil | Alta | Cerrado | MFA y limitación de intentos | [Lab 2](../../lab2_gestion_contraseñas/README.md) |
| VULN-002 | ACT-02 | Credenciales transmitidas por HTTP | Alta | Cerrado | HTTPS / túnel SSH | [Lab 3](../../lab3_protocolos_comunicacion/README.md) |
| VULN-003 | ACT-03 | Integridad de artefactos sin verificación | Alta | Cerrado | Firma y validación de manifiesto | [Lab 1](../../lab1_firma_digital/README.md) |

## Campos mínimos para nuevos hallazgos

ID, activo, fecha de detección, origen, descripción, evidencia, impacto, probabilidad, prioridad, responsable, fecha objetivo, estado, validación de cierre y riesgo residual.

# Línea base: Ubuntu y SSH

| Control | Objetivo | Verificación esperada |
|---|---|---|
| MFA para accesos administrativos | Reducir impacto de contraseñas comprometidas | SSH solicita segundo factor |
| Limitación de intentos | Mitigar fuerza bruta | Intentos repetidos son restringidos y quedan registrados |
| Registro de autenticaciones | Permitir detección e investigación | Eventos de éxito y falla disponibles para revisión |
| Gestión de privilegios mínimos | Limitar impacto de una cuenta comprometida | Cuentas administrativas justificadas y revisadas |
| Parches vigentes | Reducir exposición a vulnerabilidades conocidas | Actualizaciones aplicadas según ventana definida |

Referencia de implementación: [Lab 2 — MFA](../../lab2_gestion_contraseñas/README.md).

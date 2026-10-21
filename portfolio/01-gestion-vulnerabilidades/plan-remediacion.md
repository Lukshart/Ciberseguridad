# Plan de remediación — ejemplo

| ID | Acción | Responsable | Prioridad | Fecha objetivo | Verificación de cierre |
|---|---|---|---|---|---|
| VULN-001 | Exigir MFA y limitar intentos para SSH | Administración | Alta | 7 días | Intento de acceso con contraseña comprometida bloqueado |
| VULN-002 | Cifrar el servicio y redirigir HTTP a HTTPS | Administración web | Alta | 7 días | Captura de red sin credenciales legibles |
| VULN-003 | Firmar manifiestos y bloquear despliegues inválidos | Desarrollo / DevOps | Alta | 7 días | Verificación de firma y hash antes de desplegar |

Si una acción no puede completarse a tiempo, debe documentarse un control compensatorio y una excepción de riesgo mediante la [plantilla correspondiente](../plantillas/excepcion-riesgo.md).

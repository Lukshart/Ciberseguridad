# Evidencia: gestión de contraseñas y MFA

## Problema resuelto

Una contraseña débil permite que un atacante automatice intentos de acceso contra SSH. Depender de una contraseña como único factor aumenta la probabilidad de acceso no autorizado.

## Alcance y reglas

- Pruebas realizadas solo contra un servidor de laboratorio bajo control del autor.
- Las credenciales, usuarios y direcciones usadas son de prueba.
- No se ejecutan ataques de fuerza bruta contra sistemas externos o sin autorización.

## Hallazgos y riesgos

| Hallazgo | Riesgo asociado |
|---|---|
| Una contraseña débil puede ser identificada mediante diccionario. | Compromiso de una cuenta y acceso remoto no autorizado. |
| SSH sin segundo factor depende de un único secreto. | Reutilización, filtración o phishing de contraseña habilitan el acceso. |

## Evidencia reproducible

El [procedimiento original](README.md) documenta el escenario de laboratorio y la configuración posterior. Para reproducir de forma autorizada:

1. Preparar una VM de prueba con SSH y una cuenta no productiva.
2. Confirmar el riesgo usando un diccionario limitado y controlado.
3. Configurar MFA mediante PAM y Google Authenticator.
4. Habilitar limitación de intentos y revisar los logs.
5. Verificar que una contraseña comprometida sin el segundo factor no permite el acceso.

## Remediación propuesta

- Exigir MFA para accesos administrativos remotos.
- Aplicar limitación de intentos y monitoreo de autenticaciones fallidas.
- Eliminar contraseñas débiles y revisar periódicamente las cuentas con acceso SSH.

## Aprendizaje

MFA reduce de forma significativa el impacto de una contraseña comprometida, pero debe complementarse con registros, limitación de intentos y administración de privilegios.

**Riesgo residual:** el phishing del segundo factor o una sesión comprometida siguen siendo escenarios a considerar; se reducen con formación, monitoreo y controles de sesión.

# Evidencia: firma digital y verificación de integridad

## Problema resuelto

Un archivo o artefacto de despliegue puede modificarse entre su creación y su uso. Sin una verificación de integridad y autenticidad, la modificación puede pasar inadvertida.

## Alcance y reglas

- Escenario ejecutado únicamente con archivos y datos ficticios de laboratorio.
- No se utilizaron sistemas bancarios, cuentas reales ni claves de terceros.
- Las claves generadas para la demostración no deben reutilizarse en producción.

## Hallazgos y riesgos

| Hallazgo | Riesgo asociado |
|---|---|
| El hash cambia después de alterar el archivo. | Se puede desplegar una configuración o binario manipulado si no existe validación de integridad. |
| Un manifiesto sin firma no confirma quién lo generó. | Un actor no autorizado podría reemplazar el manifiesto y sus hashes. |

## Evidencia reproducible

El [procedimiento original](README.md) muestra cómo generar un hash SHA-256, firmar un archivo con una llave RSA y verificarlo con la llave pública. La evidencia de reproducción es:

1. Generar el hash de un archivo de prueba.
2. Modificar el archivo y comprobar que el hash cambia.
3. Firmar el archivo o manifiesto con la llave privada de laboratorio.
4. Verificar la firma con la llave pública.
5. Alterar el contenido y confirmar que la verificación falla.

## Remediación propuesta

- Firmar manifiestos de artefactos antes de su despliegue.
- Verificar firma y hashes como condición previa del pipeline.
- Almacenar claves privadas en un gestor de secretos y rotarlas según política.

## Aprendizaje

Un hash detecta cambios, pero la firma digital además aporta autenticidad. Para proteger un despliegue, ambos controles deben integrarse en un proceso verificable.

**Riesgo residual:** una llave privada comprometida invalidaría la confianza; se reduce mediante custodia, rotación y control de acceso.

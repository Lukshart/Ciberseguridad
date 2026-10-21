# Evidencia: protocolos de comunicación seguros

## Problema resuelto

Las credenciales transmitidas por HTTP pueden ser visibles para un actor que capture tráfico en la red. El problema se mitiga al cifrar la comunicación entre cliente y servicio.

## Alcance y reglas

- Capturas realizadas sobre tráfico de un laboratorio controlado.
- Se utilizaron credenciales ficticias y un servidor web de prueba.
- No se interceptó tráfico de terceros ni redes sin autorización.

## Hallazgos y riesgos

| Hallazgo | Riesgo asociado |
|---|---|
| HTTP transmite solicitudes y credenciales en texto plano. | Intercepción de credenciales y acceso no autorizado a cuentas. |
| Un servicio sin cifrado no protege la confidencialidad en tránsito. | Exposición de datos en redes compartidas o comprometidas. |

## Evidencia reproducible

El [procedimiento original](README.md) contiene los filtros y la configuración de laboratorio. Para reproducirlo de forma autorizada:

1. Levantar un servicio web de prueba que procese datos ficticios.
2. Capturar una solicitud HTTP y comprobar que el contenido es visible.
3. Configurar HTTPS con un certificado de laboratorio o crear un túnel SSH.
4. Repetir la captura y comprobar que el contenido de las credenciales no es legible.

## Remediación propuesta

- Exigir HTTPS en servicios que procesen credenciales o datos sensibles.
- Redirigir HTTP a HTTPS y mantener certificados válidos.
- Usar túneles SSH para accesos internos cuando corresponda.
- Revisar periódicamente la exposición de servicios y el tráfico no cifrado.

## Aprendizaje

El cifrado en tránsito debe verificarse, no solo configurarse. Una captura controlada permite comprobar la diferencia entre tráfico expuesto y tráfico protegido.

**Riesgo residual:** TLS no protege datos en un endpoint comprometido; debe acompañarse de controles de acceso, parcheo y monitoreo.

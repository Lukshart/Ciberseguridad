# Línea base: servicios web

| Control | Objetivo | Verificación esperada |
|---|---|---|
| HTTPS obligatorio | Evitar transmisión de credenciales en texto plano | Navegación cifrada y redirección desde HTTP |
| Gestión de certificados | Mantener identidad y cifrado válidos | Certificado vigente y nombre de servicio correcto |
| Cifrado en tránsito interno | Proteger conexiones de administración | Canal SSH o TLS para administración remota |
| Monitoreo de tráfico inseguro | Detectar configuraciones regresivas | Ausencia de credenciales legibles en capturas controladas |
| Integridad de despliegue | Prevenir artefactos manipulados | Firma y manifiesto verificados antes de publicar |

Referencias: [Lab 3 — HTTPS/SSH](../../lab3_protocolos_comunicacion/README.md) y [Lab 1 — integridad](../../lab1_firma_digital/README.md).

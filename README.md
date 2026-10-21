# Matías Eduardo Alamos Hinojosa

**Security Engineer en formación**

Estudiante del Instituto Profesional Santo Tomás, orientado a diseñar, implementar y verificar controles de seguridad. Este repositorio reúne mi formación aplicada en gestión de vulnerabilidades, hardening, riesgos y protección de sistemas.

[Perfil](#perfil) · [Competencias](#competencias) · [Evidencia práctica](#evidencia-práctica) · [Formación](#formación) · [Portafolio](#portafolio)

## Perfil

Mi objetivo es desarrollarme como **Security Engineer**, participando en la reducción de riesgos técnicos mediante controles de acceso, comunicaciones seguras, validación de integridad y gestión de vulnerabilidades.

La evidencia publicada corresponde exclusivamente a entornos de laboratorio y actividades académicas. No contiene secretos, datos personales ni información de sistemas reales.

## Competencias

- Gestión y priorización de vulnerabilidades.
- Hardening de servicios Linux, SSH y aplicaciones web.
- Autenticación multifactor, PAM y controles contra fuerza bruta.
- HTTPS, TLS y túneles SSH para proteger datos en tránsito.
- Integridad de artefactos mediante SHA-256 y firmas RSA.
- Evaluación de riesgos, tratamiento y documentación de riesgo residual.

## Evidencia práctica

### [Firma digital y verificación de integridad](lab1_firma_digital/README.md)

Demostración de integridad y autenticidad de archivos con SHA-256, RSA y manifiestos firmados. El caso relaciona la validación criptográfica con la protección de artefactos antes de un despliegue.

### [Gestión de contraseñas y MFA](lab2_gestion_contraseñas/README.md)

Escenario de acceso SSH con contraseña débil, seguido de hardening mediante MFA, PAM, limitación de intentos y revisión de registros de autenticación.

### [Protocolos de comunicación seguros](lab3_protocolos_comunicacion/README.md)

Comparación entre HTTP y comunicaciones protegidas mediante HTTPS o túneles SSH, orientada a evitar la exposición de credenciales en texto plano.

## Formación

**Instituto Profesional Santo Tomás**

Formación en ciberseguridad y desarrollo de actividades prácticas documentadas en este repositorio.

## Portafolio

El trabajo se organiza en cuatro áreas complementarias:

- [Gestión de vulnerabilidades](portfolio/01-gestion-vulnerabilidades/README.md): inventario, registro de hallazgos y remediación.
- [Hardening](portfolio/02-hardening/README.md): líneas base para Ubuntu/SSH y servicios web.
- [Gestión de riesgos](portfolio/03-gestion-riesgos/README.md): matriz, tratamiento y riesgo residual.
- [Métricas](portfolio/04-metricas/README.md): indicadores de cobertura, remediación y riesgo.

También están disponibles las [plantillas](portfolio/plantillas/) para documentar nuevos hallazgos, evidencias y excepciones de riesgo.

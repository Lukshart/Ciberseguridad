# Matías Eduardo Alamos Hinojosa

## Security Engineer en formación

![Enfoque](https://img.shields.io/badge/enfoque-Security%20Engineering-2ea44f)
![Evidencias](https://img.shields.io/badge/evidencias%20prácticas-3-blue)
![Dominios](https://img.shields.io/badge/dominios%20de%20seguridad-4-6f42c1)

Portafolio de formación aplicada en ciberseguridad, enfocado en diseñar, implementar y verificar controles que reduzcan el riesgo técnico. Mi objetivo profesional es desarrollarme como **Security Engineer**, combinando gestión de vulnerabilidades, hardening, protección de accesos y comunicaciones seguras.

> Trabajo documentado exclusivamente en entornos de laboratorio y con fines educativos. No se incluyen secretos, datos personales ni información de sistemas reales.

| 3 | 4 | 100 % |
|---:|---:|---:|
| Evidencias prácticas documentadas | Dominios de gestión de seguridad | Actividades realizadas en laboratorio |

## Sobre mí

Estudiante del **Instituto Profesional Santo Tomás**, orientado a Security Engineering. Construyo evidencia práctica a partir de escenarios controlados: identifico el riesgo, aplico controles defensivos, verifico su resultado y documento el riesgo residual.

Actualmente desarrollo mi base técnica mediante laboratorios, investigación guiada y documentación reproducible. Este repositorio muestra ese proceso, no certificaciones ni experiencia que aún no poseo.

## Competencias aplicadas

| Área | Prácticas y controles demostrados |
|---|---|
| Protección de accesos | MFA, PAM, limitación de intentos y análisis de registros de autenticación |
| Comunicaciones seguras | HTTPS, TLS, túneles SSH y verificación de tráfico cifrado |
| Integridad de software | SHA-256, firmas RSA y validación de manifiestos antes del despliegue |
| Gestión de seguridad | Priorización de hallazgos, tratamiento de riesgos y métricas de seguimiento |

## Evidencias prácticas

Los laboratorios son un mini portafolio de casos aplicados. Cada uno presenta el escenario, el riesgo, el control defensivo y su validación.

| Evidencia | Riesgo abordado | Control aplicado | Competencia demostrada |
|---|---|---|---|
| [Firma digital e integridad](lab1_firma_digital/README.md) | Manipulación de archivos y artefactos de despliegue | RSA, SHA-256 y manifiestos firmados | Integridad, autenticidad y despliegue seguro |
| [Gestión de contraseñas y MFA](lab2_gestion_contraseñas/README.md) | Contraseñas débiles y ataques de diccionario contra SSH | MFA, PAM, rate limiting y logs | Hardening de acceso y defensa de credenciales |
| [Protocolos de comunicación seguros](lab3_protocolos_comunicacion/README.md) | Exposición de credenciales en HTTP | HTTPS, TLS y túneles SSH | Protección de datos en tránsito |

## Portafolio profesional

El [portafolio de gestión de seguridad](portfolio/README.md) reúne las plantillas y artefactos que convierten las evidencias técnicas en un proceso trazable.

| Dominio | Qué contiene | Acceso |
|---|---|---|
| Gestión de vulnerabilidades | Inventario de activos, registro de hallazgos y plan de remediación | [Ver sección](portfolio/01-gestion-vulnerabilidades/README.md) |
| Hardening | Líneas base para Ubuntu/SSH y servicios web | [Ver sección](portfolio/02-hardening/README.md) |
| Gestión de riesgos | Matriz, tratamiento y riesgo residual | [Ver sección](portfolio/03-gestion-riesgos/README.md) |
| Métricas | Indicadores de cobertura, remediación y riesgo | [Ver sección](portfolio/04-metricas/README.md) |

### Cómo se conectan las evidencias

| Evidencia | Vulnerabilidades | Hardening | Riesgos | Métricas |
|---|:---:|:---:|:---:|:---:|
| Firma digital e integridad | ✓ | ✓ | ✓ | ✓ |
| MFA en SSH | ✓ | ✓ | ✓ | ✓ |
| HTTPS y túneles SSH | ✓ | ✓ | ✓ | ✓ |

## Formación

| Institución | Formación | Estado |
|---|---|---|
| Instituto Profesional Santo Tomás | Formación en ciberseguridad y actividades prácticas documentadas en este repositorio | En curso |

## Método de trabajo

1. Definir activo, alcance y riesgo del caso.
2. Registrar evidencia segura y anonimizada.
3. Aplicar un control o tratamiento.
4. Verificar el resultado.
5. Documentar el riesgo residual y actualizar las métricas.

Las [plantillas](portfolio/plantillas/) permiten mantener este formato en futuras evidencias.

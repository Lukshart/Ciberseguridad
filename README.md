# Portafolio de Gestión de Ciberseguridad

![Estado](https://img.shields.io/badge/portafolio-en%20desarrollo-yellow)
![Enfoque](https://img.shields.io/badge/enfoque-defensivo-2ea44f)
![Laboratorios](https://img.shields.io/badge/evidencias-3-blue)
![Licencia](https://img.shields.io/badge/licencia-MIT-green)

Repositorio orientado a demostrar competencias prácticas en gestión de vulnerabilidades, hardening, gestión de riesgos y métricas de seguridad. Cada caso se documenta con su contexto, controles aplicados, verificación y riesgo residual.

> Todo el contenido se desarrolla en entornos de laboratorio y con fines educativos. No se incluyen secretos, datos personales ni información de sistemas reales.

## Portafolio profesional

El [portafolio](portfolio/README.md) es el punto de partida del repositorio. Organiza el trabajo en un ciclo de seguridad trazable: identificar, priorizar, proteger, verificar y medir.

| Dominio | Qué demuestra | Acceso |
|---|---|---|
| Gestión de vulnerabilidades | Inventario de activos, registro de hallazgos y plan de remediación | [Ver sección](portfolio/01-gestion-vulnerabilidades/README.md) |
| Hardening | Líneas base para Ubuntu/SSH y servicios web | [Ver sección](portfolio/02-hardening/README.md) |
| Gestión de riesgos | Matriz, tratamiento y riesgo residual | [Ver sección](portfolio/03-gestion-riesgos/README.md) |
| Métricas | Indicadores de cobertura, tiempos de remediación y riesgo | [Ver sección](portfolio/04-metricas/README.md) |

## Competencias aplicadas

| Área | Prácticas y controles |
|---|---|
| Protección de accesos | MFA, limitación de intentos, registros de autenticación y mínimo privilegio |
| Comunicaciones seguras | HTTPS, TLS, túneles SSH y detección de tráfico en texto plano |
| Integridad de software | Hashes, firmas digitales y validación de manifiestos antes del despliegue |
| Gestión operativa | Priorización de hallazgos, tratamiento de riesgos y métricas de seguimiento |

## Evidencias prácticas

Los siguientes laboratorios constituyen un mini portafolio de evidencias. Cada uno expone un escenario, demuestra el riesgo de forma controlada, aplica un control defensivo y valida el resultado.

| Evidencia | Problema abordado | Control aplicado | Competencia demostrada |
|---|---|---|---|
| [Firma digital e integridad](lab1_firma_digital/README.md) | Manipulación de archivos y artefactos de despliegue | RSA, SHA-256 y manifiestos firmados | Integridad, autenticidad y despliegue seguro |
| [Gestión de contraseñas y MFA](lab2_gestion_contraseñas/README.md) | Contraseñas débiles y ataques de diccionario contra SSH | MFA, PAM, rate limiting y logs | Hardening de acceso y defensa de credenciales |
| [Protocolos de comunicación seguros](lab3_protocolos_comunicacion/README.md) | Exposición de credenciales en HTTP | HTTPS, TLS y túneles SSH | Protección de datos en tránsito |

### Relación entre evidencias y el portafolio

| Evidencia | Vulnerabilidades | Hardening | Riesgos | Métricas |
|---|:---:|:---:|:---:|:---:|
| Firma digital e integridad | ✓ | ✓ | ✓ | ✓ |
| MFA en SSH | ✓ | ✓ | ✓ | ✓ |
| HTTPS y túneles SSH | ✓ | ✓ | ✓ | ✓ |

## Estructura del repositorio

```text
portfolio/                         # Portafolio profesional y plantillas
├── 01-gestion-vulnerabilidades/  # Inventario, registro y remediación
├── 02-hardening/                 # Líneas base verificables
├── 03-gestion-riesgos/           # Matriz y tratamiento
├── 04-metricas/                  # Indicadores y tablero
└── plantillas/                   # Hallazgos, evidencias y excepciones

lab1_firma_digital/               # Evidencia: integridad y firma
lab2_gestion_contraseñas/         # Evidencia: MFA y SSH
lab3_protocolos_comunicacion/     # Evidencia: HTTPS y túneles SSH
```

## Forma de documentar nuevos casos

1. Definir activo, alcance y riesgo.
2. Registrar evidencia segura y anonimizada.
3. Aplicar un control o tratamiento.
4. Verificar el resultado.
5. Actualizar el indicador y documentar el riesgo residual.

Para mantener consistencia, usa las [plantillas del portafolio](portfolio/plantillas/).

# Matriz de riesgos — ejemplo de laboratorio

| ID | Escenario | Probabilidad | Impacto | Inherente | Tratamiento | Residual |
|---|---|---:|---:|---:|---|---:|
| RSK-001 | Contraseña SSH comprometida permite acceso no autorizado | 4 | 5 | 20 (Alto) | MFA, rate limiting y monitoreo | 8 (Medio) |
| RSK-002 | Intercepción de credenciales HTTP en red local | 4 | 4 | 16 (Alto) | HTTPS y túnel SSH | 4 (Bajo) |
| RSK-003 | Manipulación de artefacto durante despliegue | 3 | 5 | 15 (Alto) | Firma digital y verificación de manifiesto | 5 (Bajo) |

Estos valores son ejemplos educativos y deben reestimarse para cualquier entorno real.

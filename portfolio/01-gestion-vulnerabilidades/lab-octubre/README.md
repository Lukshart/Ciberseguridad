# Laboratorio: gestión de vulnerabilidades

## Objetivo

Demostrar el ciclo completo: inventariar → escanear en un entorno autorizado → analizar → priorizar → remediar → re-escanear → reportar.

## Alcance y reglas

- Solo VMs propias en red aislada.
- Usar datos, usuarios e IPs ficticios o anonimizados.
- Guardar snapshot antes de cambios relevantes.
- No subir reportes con secretos, credenciales ni información identificable.

## Entorno

| Elemento | Versión / detalle | Estado |
|---|---|---|
| Escáner | Pendiente de registrar | Pendiente |
| VM objetivo | Pendiente de registrar | Pendiente |
| Red | Aislada / Host-only | Pendiente de verificar |

## Hallazgos y priorización

Completar [inventario de activos](inventario_activos.csv) y [priorización](priorizacion_hallazgos.csv) con evidencia real. Para cada hallazgo registrar CVE/CWE cuando aplique, severidad, criticidad del activo, exposición, evidencia y SLA.

## Evidencia reproducible

1. Ejecutar escaneo inicial y exportar reporte anonimizando datos.
2. Repetir con credenciales solo sobre la VM autorizada y comparar cobertura.
3. Validar manualmente una muestra de hallazgos.
4. Aplicar una remediación documentada.
5. Re-ejecutar el mismo perfil de escaneo y registrar el resultado.

## Resultados y aprendizaje

**Pendiente de completar con resultados reales.** Distinguir entre hallazgo cerrado, nuevo, falso positivo y riesgo aceptado.

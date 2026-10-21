# Laboratorio: hardening Linux medido

## Objetivo

Medir una línea base de hardening, aplicar cambios justificados y comprobar su resultado sin perder trazabilidad operativa.

## Alcance y reglas

- Ejecutar solo en una VM Ubuntu de laboratorio.
- Mantener una segunda sesión antes de modificar SSH.
- Validar la configuración de SSH antes de reiniciar el servicio.
- Registrar toda desviación no corregida como excepción con fecha de revisión.

## Evidencia reproducible

1. Ejecutar una auditoría inicial y registrar el índice obtenido.
2. Revisar recomendaciones y seleccionar solo cambios con impacto comprendido.
3. Aplicar cambios, documentarlos en `cambios_hardening.csv` y verificar el servicio.
4. Ejecutar la misma auditoría y comparar el resultado.
5. Registrar excepciones y controles compensatorios en `excepciones.csv`.

## Resultado

**Pendiente de completar con valores antes/después y capturas anonimizadas.** Una mejora del índice no sustituye la revisión del impacto operativo de cada control.

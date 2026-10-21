# Matías Eduardo Alamos Hinojosa

Security Engineer en formación · Gestión de vulnerabilidades · Hardening · Gestión de riesgos

Estudiante del Instituto Profesional Santo Tomás, enfocado en construir y verificar controles de seguridad reproducibles en entornos de laboratorio.

La evidencia publicada documenta problemas, riesgos, controles y resultados de forma transparente. No representa experiencia profesional ni incluye información de sistemas reales.

## Enfoque actual

Estoy desarrollando competencias para aportar como Security Engineer en cuatro áreas: gestión de vulnerabilidades, hardening, protección de identidades y comunicaciones seguras. Mi objetivo es convertir hallazgos técnicos en decisiones de riesgo, remediaciones verificables y evidencia útil para revisión.

## Proyectos y evidencia práctica

Cada evidencia incluye problema, alcance, hallazgos vinculados a riesgos, pasos reproducibles, remediación y aprendizaje.

- [Firma digital y verificación de integridad](lab1_firma_digital/EVIDENCIA.md) — Protección de artefactos frente a modificaciones no autorizadas mediante SHA-256, RSA y manifiestos firmados.
- [Gestión de contraseñas y MFA](lab2_gestion_contraseñas/EVIDENCIA.md) — Reducción del riesgo de acceso SSH no autorizado con MFA, PAM, rate limiting y registros.
- [Protocolos de comunicación seguros](lab3_protocolos_comunicacion/EVIDENCIA.md) — Prevención de exposición de credenciales en tránsito mediante HTTPS y túneles SSH.

Los procedimientos completos originales permanecen disponibles en los [laboratorios](#laboratorios-originales).

## Metodología de evidencia

Para cada caso publicado se aplican estas reglas:

1. Explicar el problema que se resolvió y su contexto.
2. Conectar los hallazgos técnicos con riesgos para el activo.
3. Mostrar evidencia reproducible en un entorno autorizado.
4. Proponer o aplicar una remediación verificable.
5. Aclarar alcance, supuestos y reglas del laboratorio.
6. Registrar el aprendizaje y el riesgo residual.

Las [plantillas de documentación](portfolio/plantillas/) permiten extender este estándar a nuevos casos.

## Herramientas y fundamentos técnicos

- **Sistemas y acceso:** Linux, SSH, PAM, MFA y registros de autenticación.
- **Redes y comunicaciones:** HTTP/HTTPS, TLS, Wireshark y túneles SSH.
- **Criptografía aplicada:** SHA-256, RSA, OpenSSL y firmas digitales.
- **Gestión de seguridad:** inventario de activos, remediación, matrices de riesgo y métricas.

## Formación

**Instituto Profesional Santo Tomás**

Formación en ciberseguridad y desarrollo de actividades prácticas documentadas en este repositorio.

## Portafolio de gestión de seguridad

- [Gestión de vulnerabilidades](portfolio/01-gestion-vulnerabilidades/README.md)
- [Hardening](portfolio/02-hardening/README.md)
- [Gestión de riesgos](portfolio/03-gestion-riesgos/README.md)
- [Métricas](portfolio/04-metricas/README.md)

## Laboratorios originales

- [Lab 1: Firma digital y verificación de integridad](lab1_firma_digital/README.md)
- [Lab 2: Gestión de contraseñas y MFA](lab2_gestion_contraseñas/README.md)
- [Lab 3: Protocolos de comunicación seguros](lab3_protocolos_comunicacion/README.md)

# Listado de Stakeholders y Preocupaciones Arquitectónicas — PRCCD

---

## Clasificación general

| Categoría | Stakeholders |
|---|---|
| Directivos / Estratégicos | Secretaría General del SICA, Alta Dirección SICA |
| Financieros | Dirección Financiera del SICA |
| Operativos (internos) | Administradores TI del SICA, Auditores |
| Externos | Universidades (USAC, UCR, UES), Administradores TI universitarios, Estudiantes/Profesionales, Ministerios de Educación, Ministerios de Trabajo y Direcciones Financieras |

---

## Detalle por stakeholder

### S1 — Secretaría General del SICA (Directivo / Patrocinador)
- **Interés explícito:** lanzar la plataforma regional para emitir certificaciones tecnológicas unificadas en Centroamérica; unificar la región.
- **Necesidad / preocupación:** lograr la visión política sin obligar a las instituciones educativas a cambiar su forma de trabajar; que la primera versión esté lista en un plazo muy corto (3–4 semanas).
- **Impacto arquitectónico:** exige interoperabilidad nativa y una arquitectura que integre sistemas heterogéneos sin rediseñarlos; impone presión de tiempo sobre el alcance (MVP).

### S2 — Alta Dirección SICA (Directivo / Estratégico)
- **Interés explícito:** disponer de inteligencia de negocio sobre el estado de las competencias digitales en la región.
- **Necesidad / preocupación:** visualizar métricas segmentadas por país, carrera y género para la toma de decisiones.
- **Impacto arquitectónico:** requiere una capa analítica (dashboards) alimentada con datos agregados y anonimizados, separada de la operación transaccional.

### S3 — Dirección Financiera del SICA (Financiero)
- **Interés explícito:** mantener el proyecto dentro de un presupuesto máximo de USD 180,000 para el piloto.
- **Necesidad / preocupación:** previsibilidad y control de costos; evitar sobrecostos de licenciamiento.
- **Impacto arquitectónico:** obliga a priorizar tecnologías Open Source, a optimizar el almacenamiento (alta volumetría de evidencia) y a un escalamiento bajo demanda en lugar de sobredimensionar la plataforma.

### S4 — Administradores TI del SICA (Operativo / Interno)
- **Interés explícito:** operar y mantener la plataforma con un equipo de soporte limitado.
- **Necesidad / preocupación:** que la solución no aumente la complejidad de mantenimiento; capacidades técnicas heterogéneas y ecosistema fragmentado.
- **Impacto arquitectónico:** favorece una arquitectura modular por capas/servicios, administrable y con despliegue on-premise sobre la infraestructura existente, preparada para migrar a la nube en fases.

### S5 — Auditores (Operativo / Interno)
- **Interés explícito:** poder revisar la evidencia de las evaluaciones para detectar fraude académico.
- **Necesidad / preocupación:** auditar quién vio qué dato y cuándo, sin que nadie pueda evadirlo; contar con evidencia íntegra y conservada a largo plazo.
- **Impacto arquitectónico:** exige captura de evidencia anti-fraude, trazabilidad total, bitácora inmutable y retención de 5 años de la evidencia.

### S6 — Universidades USAC, UCR, UES (Externo / Pilares)
- **Interés explícito:** integrarse a la plataforma sin cambiar sus sistemas heredados ni su forma de trabajar.
- **Necesidad / preocupación:** cada institución opera como un silo tecnológico, con protocolos de autenticación distintos (LDAP, SAML, OAuth2) y formatos de datos dispares (JSON, XML, CSV).
- **Impacto arquitectónico:** obliga a una capa de integración con adaptadores por protocolo y pasarelas de formato, además de autenticación federada y aislamiento de datos por institución.

### S7 — Administradores TI universitarios (Externo / Operativo)
- **Interés explícito:** que la integración con la plataforma sea estable y no genere carga de soporte adicional.
- **Necesidad / preocupación:** ser notificados de errores de integración para poder resolverlos; tolerancia a fallos de red.
- **Impacto arquitectónico:** requiere gestión de errores de integración con notificación al administrador correspondiente y reintentos tolerantes a fallos.

### S8 — Estudiantes / Profesionales (Externo / Usuarios finales)
- **Interés explícito:** evaluarse y obtener un certificado de competencias digitales con validez regional.
- **Necesidad / preocupación:** una evaluación justa (examen adaptativo), un certificado que valga jurídicamente en varios países, y el respeto a sus datos personales (derecho al olvido, privacidad).
- **Impacto arquitectónico:** exige el motor de evaluación adaptativa, certificados verificables criptográficamente con validez transfronteriza, y mecanismos de privacidad y derecho al olvido.

### S9 — Ministerios de Educación (Externo / Estratégico)
- **Interés explícito:** conocer el estado de las competencias digitales de la región para orientar políticas educativas.
- **Necesidad / preocupación:** acceder a analítica confiable sin comprometer la privacidad de los individuos.
- **Impacto arquitectónico:** refuerza la necesidad de la capa analítica con anonimización y segmentación.

### S10 — Ministerios de Trabajo y Direcciones Financieras (Externo / Normativo)
- **Interés explícito:** confiar en la validez de los certificados emitidos para el ámbito laboral.
- **Necesidad / preocupación:** que cada certificado cuente con un rastro de auditoría inmutable respaldado por firmas electrónicas avanzadas que prevenga el fraude o la alteración de notas.
- **Impacto arquitectónico:** exige firma electrónica avanzada, bitácora inmutable y verificabilidad de los certificados.

### S11 — Equipo de Cumplimiento Legal del SICA (Operativo / Normativo)
- **Interés explícito:** que la plataforma cumpla las leyes de protección de datos.
- **Necesidad / preocupación:** evitar responsabilidad legal (incluso penal) por filtración de datos sensibles o por acceso indebido entre instituciones; garantizar el derecho al olvido.
- **Impacto arquitectónico:** exige encriptación en reposo y en tránsito, aislamiento de datos por institución, auditoría de accesos inviolable y cumplimiento de GDPR y de la Ley de Acceso a la Información Pública de Guatemala.

---

## Conflictos entre stakeholders

| Conflicto | Stakeholders en tensión | Naturaleza del conflicto | Resolución arquitectónica |
|---|---|---|---|
| Ambición vs. presupuesto | Secretaría General (S1) vs. Dirección Financiera (S3) | La visión política exige una plataforma ambiciosa y regional, mientras que el presupuesto del piloto es limitado (USD 180,000). | Priorizar Open Source, MVP acotado, escalamiento bajo demanda y reutilización de infraestructura on-premise existente. |
| Tiempo vs. completitud | Secretaría General (S1) vs. Administradores TI SICA (S4) | Se exige una primera versión en 3–4 semanas, pero el equipo de soporte es limitado y el ecosistema está fragmentado. | Arquitectura modular por servicios que permite trabajo en paralelo y entregas incrementales sobre lo existente. |
| Analítica vs. privacidad | Alta Dirección / Ministerios (S2, S9) vs. Cumplimiento Legal (S11) | La gerencia quiere métricas detalladas (país, carrera, género), pero la ley prohíbe exponer datos personales identificables. | Capa de datos con agregación y anonimización obligatorias antes de exponer métricas, y bloqueo de exposición si la anonimización falla. |
| Interoperabilidad vs. autonomía institucional | Secretaría General (S1) vs. Universidades (S6) | Se requiere integración nativa, pero las universidades no quieren cambiar sus sistemas ni protocolos. | Capa de integración con adaptadores por protocolo (LDAP/SAML/OAuth2) y pasarelas de formato (JSON/XML/CSV). |
| Control anti-fraude vs. privacidad del evaluado | Auditores / Ministerios de Trabajo (S5, S10) vs. Estudiantes (S8) y Cumplimiento Legal (S11) | La auditoría exige captura intensiva de evidencia (pantalla, tecleo, video), pero esto es información sensible del evaluado. | Almacenamiento seguro y encriptado, acceso restringido y auditado, retención controlada (5 años) y soporte al derecho al olvido sin romper la cadena de auditoría. |
| On-premise vs. preparación para la nube | Dirección Financiera / Administradores TI (S3, S4) vs. Alta Dirección (S2) | Por política y costo la primera versión debe ser on-premise, pero estratégicamente debe poder migrar a la nube. | Separación en capas y servicios que permite migrar componentes a la nube de forma gradual, sin rediseño completo. |

# Drivers RF, EaC y de Restricción por CDU Expandido — PRCCD

---

## Tablas consolidadas de Drivers únicos

### Drivers RF
| ID | Driver RF |
|---|---|
| RF-01 | Autenticación federada multi-protocolo (LDAP, SAML, OAuth2) con las universidades pilares |
| RF-02 | Sincronización e ingesta de datos académicos en formatos dispares (JSON, XML, CSV) |
| RF-03 | Motor de exámenes adaptativos con ajuste de dificultad en tiempo real |
| RF-04 | Captura concurrente de evidencia antifraude (pantalla, logs de tecleo, ráfagas de video) |
| RF-05 | Detección de patrones de comportamiento sospechoso durante la evaluación |
| RF-06 | Emisión de certificados digitales verificables criptográficamente (PKI / blockchain) |
| RF-07 | Registro en bitácora inmutable (certificados, reportes de auditoría, revocaciones) |
| RF-08 | Firma electrónica avanzada en certificados y reportes |
| RF-09 | Gestión de proceso de reintento (notificación, habilitación o bloqueo) |
| RF-10 | Habilitación de evaluaciones exclusivamente en la primera semana de cada mes |
| RF-11 | Consulta y verificación de autenticidad de certificados emitidos |
| RF-12 | Gestión de auditorías con consulta de evidencia y generación de reportes inmutables | 
| RF-13 | Escalamiento de caso por fraude confirmado (bloqueo de certificado + notificación a Secretaría SICA) | 
| RF-14 | Gestión del derecho al olvido (anonimización/eliminación conservando trazabilidad legal) | 
| RF-15 | Notificación de cambio en estado académico y evaluación de impacto sobre certificados vigentes | 
| RF-16 | Proceso de revocación de certificado con registro inmutable y notificación al titular | 
| RF-17 | Dashboards analíticos con métricas segmentadas por país, carrera y género | 
| RF-18 | Agregación y anonimización de datos antes de exposición a interfaces gerenciales | 
| RF-19 | Transformación y normalización de datos académicos al modelo interno de la plataforma | 
| RF-20 | Gestión de errores de integración con notificación al administrador TI universitario | 

### Drivers EaC
| ID | Atributo de calidad | Descripción |
|---|---|---|
| EaC-01 | Escalabilidad | Miles de usuarios simultáneos en picos de primera semana del mes |
| EaC-02 | Disponibilidad | Sistema operativo durante períodos de certificación |
| EaC-03 | Interoperabilidad (protocolos) | Protocolos dispares (LDAP, SAML, OAuth2) sin cambiar forma de trabajo de universidades |
| EaC-04 | Rendimiento (autenticación) | Autenticación federada en pocos segundos |
| EaC-05 | Interoperabilidad (datos) | Formatos JSON, XML, CSV desde sistemas legacy |
| EaC-06 | Rendimiento (examen) | Ajuste de dificultad en tiempo real sin demora perceptible |
| EaC-07 | Seguridad | Datos sensibles protegidos, acceso restringido, encriptación |
| EaC-08 | Durabilidad / Persistencia | Retención inalterable de evidencia por 5 años |
| EaC-09 | Eficiencia de costos | Almacenamiento optimizado para alta volumetría de telemetría |
| EaC-10 | Rendimiento (detección) | Análisis de fraude en tiempo real sin interrumpir evaluación |
| EaC-11 | Integridad | Certificados, reportes y revocaciones inalterables post-emisión |
| EaC-12 | Verificabilidad | Validación de certificados en pocos segundos por entidades externas |
| EaC-13 | Confiabilidad | Sin pérdida ni duplicación de datos en sincronizaciones |
| EaC-14 | Trazabilidad | Auditar quién vio/modificó qué dato, cuándo y por qué |
| EaC-15 | Privacidad | Anonimización obligatoria antes de exposición + derecho al olvido |
| EaC-16 | Tolerancia a fallos | Red inestable en integraciones con universidades |
| EaC-17 | Rendimiento (analítica) | Ejecución OLAP sin afectar OLTP transaccional |
| EaC-18 | Usabilidad | Dashboards intuitivos para alta gerencia sin conocimiento técnico |

### Drivers de Restricción
| ID | Tipo | Descripción |
|---|---|---|
| RES-01 | Operativa | Evaluaciones solo primera semana de cada mes |
| RES-02 | Presupuesto | Máximo USD 180,000 para el piloto |
| RES-03 | Tecnológica | Protocolos heterogéneos (LDAP, SAML, OAuth2) por universidad |
| RES-04 | Normativa | Protección de datos personales transfronteriza al transmitir credenciales |
| RES-05 | Tecnológica | Formatos heterogéneos de datos académicos (JSON, XML, CSV) |
| RES-06 | Normativa | GDPR + Ley de Acceso a la Información Pública de Guatemala |
| RES-07 | Tecnológica | Priorizar tecnologías Open Source para optimizar costos |
| RES-08 | Normativa | Validez jurídica transfronteriza de certificados en países del SICA |
| RES-09 | Normativa | Firmas electrónicas avanzadas + bitácora inmutable en certificados y reportes |
| RES-10 | Normativa | Encriptación de datos sensibles en reposo y en tránsito |
| RES-11 | Tecnológica | Primera versión on-premise (servidores físicos del SICA), arquitectura preparada para migración a nube |
| RES-12 | Temporal | Primera versión arquitectónica definida en máximo 3-4 semanas |

---
---

## Expandido 1: Gestionar evaluación adaptativa

### CDUE-00 — Gestionar evaluación adaptativa (CDU base)

**Drivers RF:**
- RF-03: Motor de exámenes adaptativos con ajuste de dificultad en tiempo real.
- RF-10: Habilitación de evaluaciones exclusivamente en la primera semana de cada mes.

**Drivers EaC:**
- EaC-01: Escalabilidad — soportar miles de usuarios simultáneos durante la primera semana de cada mes sin degradación del servicio.
- EaC-02: Disponibilidad — el sistema debe mantenerse operativo durante los períodos de certificación sin interrupciones.

**Drivers de Restricción:**
- RES-01: (Operativa) Las evaluaciones solo se habilitan la primera semana de cada mes (regla de negocio del SICA).
- RES-02: (Presupuesto) Presupuesto máximo de USD 180,000 para el piloto.

---

### CDUE-01 — Validar identidad federada del candidato

**Drivers RF:**
- RF-01: Autenticación federada multi-protocolo (LDAP, SAML, OAuth2) con las universidades pilares.
- RF-02: Sincronización e ingesta de datos académicos en formatos dispares (JSON, XML, CSV).

**Drivers EaC:**
- EaC-03: Interoperabilidad — interactuar con protocolos dispares sin requerir que las universidades cambien su forma de trabajar.
- EaC-04: Rendimiento (autenticación) — la autenticación debe completarse en pocos segundos.

**Drivers de Restricción:**
- RES-03: (Tecnológica) Cada universidad pilar usa un protocolo distinto (USAC: LDAP, UCR: SAML, UES: OAuth2).
- RES-04: (Normativa) Cumplimiento con leyes de protección de datos personales de cada país al transmitir credenciales.

---

### CDUE-02 — Sincronizar datos académicos

**Drivers RF:**
- RF-02: Sincronización e ingesta de datos académicos en formatos dispares (JSON, XML, CSV).
- RF-19: Transformación y normalización de datos académicos al modelo interno de la plataforma.

**Drivers EaC:**
- EaC-05: Interoperabilidad (datos) — procesar desde APIs modernas (JSON) hasta exportaciones manuales (CSV).

**Drivers de Restricción:**
- RES-05: (Tecnológica) Los datos académicos de las universidades vienen en formatos heterogéneos.

---

### CDUE-03 — Aplicar examen adaptativo

**Drivers RF:**
- RF-03: Motor de exámenes adaptativos con ajuste de dificultad en tiempo real.

**Drivers EaC:**
- EaC-06: Rendimiento (examen) — el ajuste de dificultad debe calcularse en tiempo real sin demora perceptible entre preguntas.
- EaC-01: Escalabilidad — soportar miles de evaluaciones concurrentes durante los picos.

**Drivers de Restricción:**
- (Ninguna restricción adicional específica a este CDU.)

---

### CDUE-04 — Capturar evidencia antifraude

**Drivers RF:**
- RF-04: Captura concurrente de evidencia antifraude (pantalla, logs de tecleo, ráfagas de video).

**Drivers EaC:**
- EaC-07: Seguridad — la evidencia biométrica y de comportamiento debe almacenarse de forma altamente segura.
- EaC-08: Durabilidad / Persistencia — retención inalterable por un período de 5 años.
- EaC-09: Eficiencia de costos — almacenamiento optimizado en costos dada la alta volumetría.

**Drivers de Restricción:**
- RES-06: (Normativa) Cumplir con el GDPR y con la Ley de Acceso a la Información Pública de Guatemala.
- RES-07: (Tecnológica) Priorizar tecnologías Open Source para optimizar costos de licenciamiento.

---

### CDUE-05 — Registrar evento sospechoso

**Drivers RF:**
- RF-05: Detección de patrones de comportamiento sospechoso durante la evaluación.

**Drivers EaC:**
- EaC-10: Rendimiento (detección) — la detección debe ejecutarse en tiempo real sin interrumpir la evaluación en curso.

**Drivers de Restricción:**
- (Ninguna restricción adicional específica.)

---

### CDUE-06 — Emitir credencial digital

**Drivers RF:**
- RF-06: Emisión de certificados digitales verificables criptográficamente (PKI / blockchain).
- RF-07: Registro en bitácora inmutable.
- RF-08: Firma electrónica avanzada en certificados.

**Drivers EaC:**
- EaC-11: Integridad — garantizar que ni la calificación ni la identidad del portador puedan alterarse.
- EaC-12: Verificabilidad — cualquier entidad debe poder verificar un certificado en pocos segundos.

**Drivers de Restricción:**
- RES-08: (Normativa) Los certificados deben tener validez jurídica transfronteriza dentro de los países del SICA.
- RES-09: (Normativa) Rastro de auditoría inmutable respaldado por firmas electrónicas avanzadas.

---

### CDUE-07 — Gestionar proceso de reintento

**Drivers RF:**
- RF-09: Gestión de proceso de reintento (notificación, habilitación o bloqueo).

**Drivers EaC:**
- (Ningún EaC crítico adicional específico.)

**Drivers de Restricción:**
- RES-01: (Operativa) Los reintentos solo pueden ocurrir en la primera semana del siguiente mes.

---

### CDUE-08 — Bloquear reintento por fraude

**Drivers RF:**
- RF-09: Gestión de proceso de reintento (notificación, habilitación o bloqueo).
- RF-13: Escalamiento de caso por fraude confirmado (bloqueo de certificado + notificación a Secretaría SICA).

**Drivers EaC:**
- EaC-07: Seguridad — el bloqueo debe aplicarse de forma inmediata e inviolable.

**Drivers de Restricción:**
- (Ninguna restricción adicional específica.)

---

### CDUE-09 — Habilitar reintento (si no hay fraude)

**Drivers RF:**
- RF-09: Gestión de proceso de reintento (notificación, habilitación o bloqueo).

**Drivers EaC:**
- (Ningún EaC crítico adicional específico.)

**Drivers de Restricción:**
- RES-01: (Operativa) La habilitación debe quedar registrada antes de la apertura del siguiente período.

---
---

## Expandido 2: Gestión de certificados regionales

### CDUE-10 — Gestión de certificados regionales (CDU base)

**Drivers RF:**
- RF-06: Emisión de certificados digitales verificables criptográficamente (PKI / blockchain).
- RF-11: Consulta y verificación de autenticidad de certificados emitidos.

**Drivers EaC:**
- EaC-11: Integridad — los certificados no pueden alterarse después de emitidos.
- EaC-12: Verificabilidad — respuesta de validación en pocos segundos.

**Drivers de Restricción:**
- RES-08: (Normativa) Validez jurídica transfronteriza.
- RES-09: (Normativa) Rastro de auditoría inmutable con firmas electrónicas avanzadas.

---

### CDUE-11 — Autenticar conexión institucional

**Drivers RF:**
- RF-01: Autenticación federada multi-protocolo (LDAP, SAML, OAuth2).

**Drivers EaC:**
- EaC-03: Interoperabilidad — soportar los diferentes protocolos de cada institución.
- EaC-07: Seguridad — garantizar que solo entidades autorizadas accedan a la información.

**Drivers de Restricción:**
- RES-03: (Tecnológica) Protocolos heterogéneos (LDAP, SAML, OAuth2).

---

### CDUE-12 — Sincronizar historial académico del estudiante

**Drivers RF:**
- RF-02: Sincronización e ingesta de datos académicos en formatos dispares (JSON, XML, CSV).
- RF-19: Transformación y normalización de datos académicos al modelo interno.

**Drivers EaC:**
- EaC-05: Interoperabilidad (datos) — formatos dispares.

**Drivers de Restricción:**
- RES-05: (Tecnológica) Formatos heterogéneos de datos académicos.

---

### CDUE-13 — Consultar certificados emitidos a sus estudiantes

**Drivers RF:**
- RF-11: Consulta y verificación de autenticidad de certificados emitidos.

**Drivers EaC:**
- EaC-12: Verificabilidad — respuesta rápida.
- EaC-07: Seguridad — aislamiento de datos por institución.

**Drivers de Restricción:**
- RES-04: (Normativa) Protección de datos personales; aislamiento por institución.

---

### CDUE-14 — Notificar cambio en estado académico del estudiante

**Drivers RF:**
- RF-15: Notificación de cambio en estado académico y evaluación de impacto sobre certificados vigentes.

**Drivers EaC:**
- EaC-13: Confiabilidad — los cambios no deben perderse ni procesarse duplicados.

**Drivers de Restricción:**
- (Ninguna restricción adicional específica.)

---

### CDUE-15 — Gestionar revocación de certificado

**Drivers RF:**
- RF-06: Emisión de certificados digitales verificables criptográficamente (gestión del ciclo de vida).
- RF-15: Notificación de cambio en estado académico y evaluación de impacto.

**Drivers EaC:**
- EaC-11: Integridad — la revocación debe registrarse en la bitácora inmutable.

**Drivers de Restricción:**
- RES-09: (Normativa) El rastro de revocación debe ser inalterable.

---

### CDUE-16 — Iniciar proceso de revocación de certificado

**Drivers RF:**
- RF-16: Proceso de revocación de certificado con registro inmutable y notificación al titular.
- RF-07: Registro en bitácora inmutable.
- RF-08: Firma electrónica avanzada.

**Drivers EaC:**
- EaC-11: Integridad — la revocación queda registrada inmutablemente.
- EaC-14: Trazabilidad — auditar quién, cuándo y por qué se revocó.

**Drivers de Restricción:**
- RES-09: (Normativa) Firmas electrónicas avanzadas en el registro de revocación.

---
---

## Expandido 3: Gestionar auditorías y evidencia anti-fraude

### CDUE-17 — Gestionar auditorías y evidencia anti-fraude (CDU base)

**Drivers RF:**
- RF-12: Gestión de auditorías con consulta de evidencia y generación de reportes inmutables.

**Drivers EaC:**
- EaC-14: Trazabilidad — auditar quién vio qué dato y cuándo, sin que nadie pueda evadirlo.
- EaC-08: Durabilidad — retención de evidencia por 5 años.

**Drivers de Restricción:**
- RES-06: (Normativa) GDPR y Ley de Acceso a la Información Pública de Guatemala.

---

### CDUE-18 — Autenticar y autorizar auditor

**Drivers RF:**
- RF-01: Autenticación federada multi-protocolo (aplicada al rol de auditor).

**Drivers EaC:**
- EaC-07: Seguridad — solo personal autorizado puede acceder a evidencia sensible.

**Drivers de Restricción:**
- (Ninguna restricción adicional específica.)

---

### CDUE-19 — Consultar evidencia capturada por evaluación

**Drivers RF:**
- RF-12: Gestión de auditorías con consulta de evidencia y generación de reportes inmutables.

**Drivers EaC:**
- EaC-08: Durabilidad — evidencia inalterable por 5 años.
- EaC-11: Integridad — verificar que la evidencia no ha sido modificada desde su captura.

**Drivers de Restricción:**
- RES-06: (Normativa) Retención conforme a GDPR y legislación local.

---

### CDUE-20 — Detectar patrones sospechosos

**Drivers RF:**
- RF-05: Detección de patrones de comportamiento sospechoso.

**Drivers EaC:**
- EaC-10: Rendimiento (detección) — el análisis debe ser eficiente.

**Drivers de Restricción:**
- (Ninguna restricción adicional específica.)

---

### CDUE-21 — Generar reporte de auditoría

**Drivers RF:**
- RF-12: Gestión de auditorías con consulta de evidencia y generación de reportes inmutables.
- RF-07: Registro en bitácora inmutable.
- RF-08: Firma electrónica avanzada en reportes.

**Drivers EaC:**
- EaC-14: Trazabilidad — cada reporte debe ser rastreable e inalterable.
- EaC-11: Integridad — la firma electrónica previene alteraciones.

**Drivers de Restricción:**
- RES-09: (Normativa) Firmas electrónicas avanzadas obligatorias en reportes de auditoría.

---

### CDUE-22 — Escalar caso como fraude confirmado

**Drivers RF:**
- RF-13: Escalamiento de caso por fraude confirmado (bloqueo de certificado + notificación a Secretaría SICA).
- RF-07: Registro en bitácora inmutable.

**Drivers EaC:**
- EaC-07: Seguridad — el bloqueo debe ser inmediato e irreversible hasta resolución.

**Drivers de Restricción:**
- RES-09: (Normativa) El bloqueo y la notificación deben quedar registrados inmutablemente.

---

### CDUE-23 — Gestionar derecho al olvido

**Drivers RF:**
- RF-14: Gestión del derecho al olvido (anonimización/eliminación conservando trazabilidad legal).

**Drivers EaC:**
- EaC-15: Privacidad — garantizar el derecho al olvido sin romper la cadena de auditoría.
- EaC-07: Seguridad — encriptación de datos sensibles en reposo y en tránsito.

**Drivers de Restricción:**
- RES-06: (Normativa) GDPR (derecho al olvido) y leyes locales de protección de datos.
- RES-10: (Normativa) Encriptación de datos sensibles en reposo y en tránsito.

---
---

## Expandido 4: Integrar información académica con universidades

### CDUE-24 — Integrar información académica con universidades (CDU base)

**Drivers RF:**
- RF-01: Autenticación federada multi-protocolo (LDAP, SAML, OAuth2).
- RF-02: Sincronización e ingesta de datos académicos en formatos dispares (JSON, XML, CSV).

**Drivers EaC:**
- EaC-03: Interoperabilidad — integración sin que las universidades cambien su forma de trabajar.
- EaC-16: Tolerancia a fallos — tolerar fallos temporales de red en las integraciones sin perder datos.

**Drivers de Restricción:**
- RES-03: (Tecnológica) Protocolos heterogéneos (LDAP, SAML, OAuth2).
- RES-05: (Tecnológica) Formatos de datos dispares (JSON, XML, CSV).

---

### CDUE-25 — Negociar protocolo de integración

**Drivers RF:**
- RF-01: Autenticación federada multi-protocolo (detección automática del protocolo de cada universidad).

**Drivers EaC:**
- EaC-03: Interoperabilidad — manejar múltiples protocolos de forma transparente.

**Drivers de Restricción:**
- RES-03: (Tecnológica) Cada universidad usa un protocolo distinto.

---

### CDUE-26 — Establecer autenticación federada

**Drivers RF:**
- RF-01: Autenticación federada multi-protocolo.

**Drivers EaC:**
- EaC-04: Rendimiento (autenticación) — la autenticación no debe retrasar el flujo.
- EaC-07: Seguridad — transmisión segura de credenciales entre sistemas.

**Drivers de Restricción:**
- RES-04: (Normativa) Protección de datos personales al transmitir credenciales entre países.

---

### CDUE-27 — Ingerir y exportar datos académicos

**Drivers RF:**
- RF-02: Sincronización e ingesta de datos académicos en formatos dispares (JSON, XML, CSV).

**Drivers EaC:**
- EaC-05: Interoperabilidad (datos) — procesar desde APIs modernas hasta exportaciones CSV manuales.

**Drivers de Restricción:**
- RES-05: (Tecnológica) Formatos heterogéneos.

---

### CDUE-28 — Validar y transformar formato de datos

**Drivers RF:**
- RF-19: Transformación y normalización de datos académicos al modelo interno de la plataforma.

**Drivers EaC:**
- EaC-13: Confiabilidad — rechazar datos malformados sin perder los válidos.

**Drivers de Restricción:**
- (Ninguna restricción adicional específica.)

---

### CDUE-29 — Gestionar error de integración

**Drivers RF:**
- RF-20: Gestión de errores de integración con notificación al administrador TI universitario.

**Drivers EaC:**
- EaC-16: Tolerancia a fallos — los errores de integración no deben tumbar el sistema ni perder datos.

**Drivers de Restricción:**
- (Ninguna restricción adicional específica.)

---
---

## Expandido 5: Analítica regional de competencias

### CDUE-30 — Analítica regional de competencias (CDU base)

**Drivers RF:**
- RF-17: Dashboards analíticos con métricas segmentadas por país, carrera y género.
- RF-18: Agregación y anonimización de datos antes de exposición a interfaces gerenciales.

**Drivers EaC:**
- EaC-15: Privacidad — los datos deben pasar por agregación y anonimización antes de exponerse.
- EaC-17: Rendimiento (analítica) — la ejecución no debe afectar el rendimiento de las operaciones transaccionales.

**Drivers de Restricción:**
- RES-06: (Normativa) Cumplimiento con leyes de protección de datos de múltiples países.

---

### CDUE-31 — Recopilar datos de evaluaciones y certificaciones

**Drivers RF:**
- RF-17: Dashboards analíticos con métricas segmentadas (la recopilación es el insumo).

**Drivers EaC:**
- EaC-17: Rendimiento (analítica) — la recopilación no debe impactar las operaciones transaccionales (separación OLTP/OLAP).

**Drivers de Restricción:**
- (Ninguna restricción adicional específica.)

---

### CDUE-32 — Ejecutar agregación y anonimización

**Drivers RF:**
- RF-18: Agregación y anonimización de datos antes de exposición a interfaces gerenciales.

**Drivers EaC:**
- EaC-15: Privacidad — ningún dato personal identificable puede llegar a los dashboards.

**Drivers de Restricción:**
- RES-06: (Normativa) GDPR y leyes locales de protección de datos.

---

### CDUE-33 — Segmentar información (país, carrera, género)

**Drivers RF:**
- RF-17: Dashboards analíticos con métricas segmentadas por país, carrera y género.

**Drivers EaC:**
- (Ningún EaC adicional específico.)

**Drivers de Restricción:**
- (Ninguna restricción adicional específica.)

---

### CDUE-34 — Exponer métricas en dashboards gerenciales

**Drivers RF:**
- RF-17: Dashboards analíticos con métricas segmentadas por país, carrera y género.

**Drivers EaC:**
- EaC-18: Usabilidad — los dashboards deben ser intuitivos para la alta gerencia.

**Drivers de Restricción:**
- (Ninguna restricción adicional específica.)

---

### CDUE-35 — Bloquear exposición por fallo de anonimización

**Drivers RF:**
- RF-18: Agregación y anonimización de datos antes de exposición (rama de fallo).

**Drivers EaC:**
- EaC-15: Privacidad — protección ante fallos del proceso de anonimización.

**Drivers de Restricción:**
- RES-06: (Normativa) Infringir la normativa acarrea sanciones legales.

---

### CDUE-36 — Configurar alertas por indicador clave

**Drivers RF:**
- RF-17: Dashboards analíticos con métricas segmentadas (extensión de alertas).

**Drivers EaC:**
- (Ningún EaC adicional específico.)

**Drivers de Restricción:**
- (Ninguna restricción adicional específica.)

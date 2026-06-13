# Análisis y Diseño de Sistemas 2
## Universidad San Carlos de Guatemala
### Facultad de Ingeniería — Ingeniería en Ciencias y Sistemas
 
---
 
# Proyecto Fase 1: SICA
## Plataforma Regional de Certificación de Competencias Digitales (PRCCD)
 
---
 
## Integrantes
 
| # | Nombre completo | Carnet |
|---|---|---|
| 1 | Luis Pablo Manuel García López|202200129 |
| 2 | Harold Alejandro Sánchez Herández|202200100 |
| 3 | Madeline Fabiola Prado Reyes|202100039|
| 4 | eysson Ezequiel Godoy Torres| 3429393512210 |
| 5 | Kenneth Isaí Aquino Ortiz| 202100678 |
| 6 | Diego Andres Aguilar Díaz | 2734901842001 |
| 7 | | |
 
---
 
## 1. Identificación del caso de negocio y Stakeholders

### 1.1 Listado de Stakeholders y preocupaciones arquitectónicas

#### Clasificación general

| Categoría | Stakeholders |
|---|---|
| Directivos / Estratégicos | Secretaría General del SICA, Alta Dirección SICA |
| Financieros | Dirección Financiera del SICA |
| Operativos (internos) | Administradores TI del SICA, Auditores |
| Externos | Universidades (USAC, UCR, UES), Administradores TI universitarios, Estudiantes/Profesionales, Ministerios de Educación, Ministerios de Trabajo y Direcciones Financieras |

#### Detalle por stakeholder

**S1 — Secretaría General del SICA (Directivo / Patrocinador)**
- **Interés explícito:** lanzar la plataforma regional para emitir certificaciones tecnológicas unificadas en Centroamérica; unificar la región.
- **Necesidad / preocupación:** lograr la visión política sin obligar a las instituciones educativas a cambiar su forma de trabajar; que la primera versión esté lista en un plazo muy corto (3–4 semanas).
- **Impacto arquitectónico:** exige interoperabilidad nativa y una arquitectura que integre sistemas heterogéneos sin rediseñarlos; impone presión de tiempo sobre el alcance (MVP).

**S2 — Alta Dirección SICA (Directivo / Estratégico)**
- **Interés explícito:** disponer de inteligencia de negocio sobre el estado de las competencias digitales en la región.
- **Necesidad / preocupación:** visualizar métricas segmentadas por país, carrera y género para la toma de decisiones.
- **Impacto arquitectónico:** requiere una capa analítica (dashboards) alimentada con datos agregados y anonimizados, separada de la operación transaccional.

**S3 — Dirección Financiera del SICA (Financiero)**
- **Interés explícito:** mantener el proyecto dentro de un presupuesto máximo de USD 180,000 para el piloto.
- **Necesidad / preocupación:** previsibilidad y control de costos; evitar sobrecostos de licenciamiento.
- **Impacto arquitectónico:** obliga a priorizar tecnologías Open Source, a optimizar el almacenamiento (alta volumetría de evidencia) y a un escalamiento bajo demanda en lugar de sobredimensionar la plataforma.

**S4 — Administradores TI del SICA (Operativo / Interno)**
- **Interés explícito:** operar y mantener la plataforma con un equipo de soporte limitado.
- **Necesidad / preocupación:** que la solución no aumente la complejidad de mantenimiento; capacidades técnicas heterogéneas y ecosistema fragmentado.
- **Impacto arquitectónico:** favorece una arquitectura modular por capas/servicios, administrable y con despliegue on-premise sobre la infraestructura existente, preparada para migrar a la nube en fases.

**S5 — Auditores (Operativo / Interno)**
- **Interés explícito:** poder revisar la evidencia de las evaluaciones para detectar fraude académico.
- **Necesidad / preocupación:** auditar quién vio qué dato y cuándo, sin que nadie pueda evadirlo; contar con evidencia íntegra y conservada a largo plazo.
- **Impacto arquitectónico:** exige captura de evidencia anti-fraude, trazabilidad total, bitácora inmutable y retención de 5 años de la evidencia.

**S6 — Universidades USAC, UCR, UES (Externo / Pilares)**
- **Interés explícito:** integrarse a la plataforma sin cambiar sus sistemas heredados ni su forma de trabajar.
- **Necesidad / preocupación:** cada institución opera como un silo tecnológico, con protocolos de autenticación distintos (LDAP, SAML, OAuth2) y formatos de datos dispares (JSON, XML, CSV).
- **Impacto arquitectónico:** obliga a una capa de integración con adaptadores por protocolo y pasarelas de formato, además de autenticación federada y aislamiento de datos por institución.

**S7 — Administradores TI universitarios (Externo / Operativo)**
- **Interés explícito:** que la integración con la plataforma sea estable y no genere carga de soporte adicional.
- **Necesidad / preocupación:** ser notificados de errores de integración para poder resolverlos; tolerancia a fallos de red.
- **Impacto arquitectónico:** requiere gestión de errores de integración con notificación al administrador correspondiente y reintentos tolerantes a fallos.

**S8 — Estudiantes / Profesionales (Externo / Usuarios finales)**
- **Interés explícito:** evaluarse y obtener un certificado de competencias digitales con validez regional.
- **Necesidad / preocupación:** una evaluación justa (examen adaptativo), un certificado que valga jurídicamente en varios países, y el respeto a sus datos personales (derecho al olvido, privacidad).
- **Impacto arquitectónico:** exige el motor de evaluación adaptativa, certificados verificables criptográficamente con validez transfronteriza, y mecanismos de privacidad y derecho al olvido.

**S9 — Ministerios de Educación (Externo / Estratégico)**
- **Interés explícito:** conocer el estado de las competencias digitales de la región para orientar políticas educativas.
- **Necesidad / preocupación:** acceder a analítica confiable sin comprometer la privacidad de los individuos.
- **Impacto arquitectónico:** refuerza la necesidad de la capa analítica con anonimización y segmentación.

**S10 — Ministerios de Trabajo y Direcciones Financieras (Externo / Normativo)**
- **Interés explícito:** confiar en la validez de los certificados emitidos para el ámbito laboral.
- **Necesidad / preocupación:** que cada certificado cuente con un rastro de auditoría inmutable respaldado por firmas electrónicas avanzadas que prevenga el fraude o la alteración de notas.
- **Impacto arquitectónico:** exige firma electrónica avanzada, bitácora inmutable y verificabilidad de los certificados.

**S11 — Equipo de Cumplimiento Legal del SICA (Operativo / Normativo)**
- **Interés explícito:** que la plataforma cumpla las leyes de protección de datos.
- **Necesidad / preocupación:** evitar responsabilidad legal (incluso penal) por filtración de datos sensibles o por acceso indebido entre instituciones; garantizar el derecho al olvido.
- **Impacto arquitectónico:** exige encriptación en reposo y en tránsito, aislamiento de datos por institución, auditoría de accesos inviolable y cumplimiento de GDPR y de la Ley de Acceso a la Información Pública de Guatemala.

#### Conflictos entre stakeholders

| Conflicto | Stakeholders en tensión | Naturaleza del conflicto | Resolución arquitectónica |
|---|---|---|---|
| Ambición vs. presupuesto | S1 vs. S3 | La visión política exige una plataforma ambiciosa y regional, mientras que el presupuesto del piloto es limitado (USD 180,000). | Priorizar Open Source, MVP acotado, escalamiento bajo demanda y reutilización de infraestructura on-premise existente. |
| Tiempo vs. completitud | S1 vs. S4 | Se exige una primera versión en 3–4 semanas, pero el equipo de soporte es limitado y el ecosistema está fragmentado. | Arquitectura modular por servicios que permite trabajo en paralelo y entregas incrementales sobre lo existente. |
| Analítica vs. privacidad | S2, S9 vs. S11 | La gerencia quiere métricas detalladas (país, carrera, género), pero la ley prohíbe exponer datos personales identificables. | Capa de datos con agregación y anonimización obligatorias antes de exponer métricas, y bloqueo de exposición si la anonimización falla. |
| Interoperabilidad vs. autonomía institucional | S1 vs. S6 | Se requiere integración nativa, pero las universidades no quieren cambiar sus sistemas ni protocolos. | Capa de integración con adaptadores por protocolo (LDAP/SAML/OAuth2) y pasarelas de formato (JSON/XML/CSV). |
| Control anti-fraude vs. privacidad del evaluado | S5, S10 vs. S8, S11 | La auditoría exige captura intensiva de evidencia (pantalla, tecleo, video), pero esto es información sensible del evaluado. | Almacenamiento seguro y encriptado, acceso restringido y auditado, retención controlada (5 años) y soporte al derecho al olvido sin romper la cadena de auditoría. |
| On-premise vs. preparación para la nube | S3, S4 vs. S2 | Por política y costo la primera versión debe ser on-premise, pero estratégicamente debe poder migrar a la nube. | Separación en capas y servicios que permite migrar componentes a la nube de forma gradual, sin rediseño completo. |

---

### 1.2 Core del negocio

La Plataforma Regional de Certificación de Competencias Digitales (PRCCD) permite evaluar, certificar y validar las competencias digitales de estudiantes y profesionales de Centroamérica. La plataforma integra a universidades de la región para autenticar usuarios, administrar procesos de evaluación adaptativa, emitir certificados digitales con validez regional y proporcionar información analítica a entidades educativas y gubernamentales para apoyar la toma de decisiones sobre el desarrollo de competencias digitales.

#### 1.2.1 Diagrama de casos de uso de negocio de alto nivel (CUN)

![Diagrama de Contexto — CUN](documentación/entregablesFinales/CDUS/Diagrama_Core.png)

#### 1.2.2 Primera descomposición del Core (CDU de negocio)

![CDU de Negocio — Primera Descomposición](documentación/entregablesFinales/CDUS/Primera_descomposicion.png)
 
---
 
## 2. Características del sistema y Drivers Arquitectónicos
 
### 2.a Listado de drivers RF (Requerimientos Funcionales)
 
### 2.b Listado de drivers EaC (Escenarios de Atributos de Calidad)
 
### 2.c Listado de drivers de Restricción (tecnológicos, normativos y operativos)
 
### 2.d Descripción de características principales de la PRCCD (priorizadas por impacto en el negocio)
 
---
 
## 3. Diagramas de CDU Expandidos
 
### 3.a Diagrama de casos de uso expandidos del sistema
 
### 3.b Detalle de drivers RF, EaC y de Restricción asociados a cada CDU
 
---
 
## 4. Matrices de Trazabilidad
 
### 4.a Stakeholders vs. Requerimientos
 
### 4.b Stakeholders vs. CDU
 
### 4.c Requerimiento vs. CDU
 
---
 
## 5. Selección Arquitectónica
 
### 5.1 Estilo(s) arquitectónico(s) seleccionado(s)
 
### 5.2 Argumentación técnica y económica
 
---
 
## 6. Vistas Arquitectónicas: Nivel de Sistema
 
### 6.1 Diagrama de bloques de la arquitectura de software
 
---
 
## 7. Vistas Arquitectónicas: Nivel de Infraestructura
 
### 7.1 Diagrama de despliegue
 
### 7.2 Diagrama de componentes
 
### 7.3 Diagrama de distribución
 
### 7.4 Justificación de frameworks y tecnologías en relación a los drivers arquitectónicos
 
---
 
## 8. Diseño de Datos
 
### 8.1 Diagrama Entidad-Relación (DER)

![Diagrama Entidad-Relación](documentación/DiagramaE-R.png)

---

### 8.2 Justificación — soporte a auditoría y almacenamiento a largo plazo

| Entidad | Justificación del enunciado |
|---|---|
| `EVIDENCIA_ANTIFRAUDE` | El enunciado exige *"retención inalterable por un período de 5 años para cumplir con el GDPR y legislaciones locales"*. El campo `fecha_expiracion` y `contenido_cifrado` soportan esto directamente. |
| `REGISTRO_BLOCKCHAIN` | El enunciado exige *"bitácora inmutable que demuestre que ni la calificación ni la identidad del portador han sido alteradas desde el momento de la emisión"*. El campo `hash_transaccion` garantiza la inmutabilidad. |
| `AUDITORIA` | El enunciado exige *"rastro de auditoría inmutable respaldado por firmas electrónicas avanzadas"*. Esta entidad registra cada revisión con su resultado y observaciones. |
| `CERTIFICADO.deleted_at` en `USUARIO` | El enunciado exige *"garantizar el derecho al olvido"*. El campo `deleted_at` permite soft delete cumpliendo GDPR sin romper la integridad referencial. |
| `RESPUESTA.timestamp_respuesta` | El enunciado exige trazabilidad completa para *"prevenir el fraude académico o la alteración de notas a nivel de base de datos"*. |

---
 
## 9. Diseño de Interfaces (UI/UX)
 
### 9.1 Prototipo: Registro y autenticación federada
 
### 9.2 Prototipo: Evaluación adaptativa
 
### 9.3 Prototipo: Gestión de certificados
 
### 9.4 Prototipo: Panel de auditoría
 
### 9.5 Prototipo: Dashboard analítico regional
 
### 9.6 Prototipo: Panel de administración TI
 
---
 
## 10. Patrones de Diseño
 
### 10.1 Patrón 1 — [Nombre]
 
### 10.2 Patrón 2 — [Nombre]
 
### 10.3 Patrón 3 — [Nombre]
 
### 10.4 Patrón 4 — [Nombre]
 
### 10.5 Patrón 5 — [Nombre]
 
---
 
## 11. Gestión del Proyecto (Enfoque Ágil)
 
### 11.1 Tablero Kanban

El proyecto se gestiona mediante un tablero Kanban con el flujo de trabajo: **To Do → Blocked → In Progress → Ready for Testing → Test/QA → Done**.

![Tablero Kanban](documentación/img/tablero-kanban.png)

### 11.2 Backlog del proyecto (historias de usuario y tareas de desarrollo)

El detalle del backlog, con las tareas de desarrollo de la arquitectura organizadas por columna y categoría, se encuentra en:

📋 [Backlog del proyecto — Tablero Kanban PRCCD](documentación/kanban-backlog.md)
 
---
 
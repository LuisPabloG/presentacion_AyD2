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
| 4 | Jeysson Ezequiel Godoy Torres| 3429393512210 |
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
![alt text](matriz1.png)
 
### 4.b Stakeholders vs. CDU
![alt text](matriz2.png)
 
### 4.c Requerimiento vs. CDU
![alt text](matriz3.png)
 
---
 
## 5. Selección Arquitectónica
 
### 5.1 Estilo(s) arquitectónico(s) seleccionado(s)
## Estilo principal: Arquitectura en Capas (Layered) combinada con Orientación a Servicios (SOA)

Para el PRCCD se selecciona como estilo principal la **arquitectura en capas**, sobre la cual se implementa un **enfoque orientado a servicios (SOA)** para los módulos que corresponden a procesos de negocio independientes. Esta combinación es coherente porque, como se vio en el curso, SOA no es un estilo que "viene solo": se implementa sobre una base de capas, donde aparece una capa de servicios adicional entre la lógica de negocio y la presentación.

La estructura general queda así:

- **Capa de presentación**: portal web para administradores/auditores del SICA, portal de consulta para universidades y ministerios, y la interfaz de evaluación para estudiantes/profesionales.
- **Capa de servicios (SOA)**: cada proceso de negocio de la primera descomposición se expone como un servicio independiente: Servicio de Evaluación Adaptativa, Servicio de Certificación Regional, Servicio de Auditoría Anti-fraude, Servicio de Integración Académica y Servicio de Analítica Regional.
- **Capa de lógica de negocio**: reglas de negocio de cada servicio (motor adaptativo, motor de emisión criptográfica, motor de detección de fraude, etc.).
- **Capa de integración**: pasarelas que traducen entre los protocolos de autenticación (LDAP, SAML, OAuth2) y formatos de datos (JSON, XML, CSV) de cada universidad hacia el formato interno de la plataforma.
- **Capa de datos**: bases de datos transaccionales (OLTP) para evaluación y certificación, almacenamiento de evidencia (optimizado en costos), y un repositorio analítico (OLAP) separado para los dashboards regionales.

## Estilo complementario: Basado en eventos (Event-Driven), para los flujos asíncronos

Se incorpora un componente basado en eventos para los flujos que no requieren respuesta inmediata y que deben tolerar fallos:

- Captura y envío de evidencia anti-fraude (telemetría) hacia el almacenamiento seguro.
- Notificaciones de cambio de estado académico desde las universidades hacia el módulo de certificados.
- Registro de certificados y revocaciones en la red de blockchain/PKI.
- Alimentación del repositorio analítico (ETL hacia la capa OLAP).

Estos estilos pueden coexistir porque técnicamente son compatibles: el bus de eventos se ubica entre la capa de servicios y la capa de datos, sin romper la separación por capas ni la independencia de los servicios.
 
### 5.2 Argumentación técnica y económica
## Argumentación técnica
La elección responde directamente a los drivers identificados a partir del enunciado:

**Correspondencia servicio-proceso de negocio.** Cada uno de los cinco procesos de negocio de la primera descomposición (evaluación adaptativa, certificación regional, auditoría anti-fraude, integración académica, analítica regional) se traduce en un servicio independiente. Esto permite hacer ingeniería inversa desde el despliegue hasta los casos de uso de negocio, lo cual es la prueba de que el estilo SOA está correctamente implementado.

**Aislamiento de fallos por capas e integración.** El requerimiento de tolerancia a fallos en las integraciones con universidades (RES-03, RES-05, EaC-16) se resuelve aislando toda la complejidad de protocolos y formatos en la capa de integración, sin que un fallo en una universidad afecte al resto del sistema.

**Escalabilidad concentrada en el servicio correcto.** El pico de tráfico de la primera semana de cada mes (EaC-01) afecta principalmente al Servicio de Evaluación Adaptativa. Con servicios independientes, este componente puede escalarse de forma aislada (más instancias, más recursos) sin necesidad de escalar toda la plataforma, lo cual es clave bajo un presupuesto limitado.

**Separación OLTP/OLAP para la analítica.** El requerimiento de que la analítica no afecte el rendimiento transaccional (EaC-17) se resuelve de forma natural separando el repositorio analítico de la capa de datos transaccional, alimentado mediante eventos.

**Modificabilidad para crecimiento regional.** El requerimiento implícito de incorporar nuevas universidades o tipos de certificación sin rediseño completo (EaC-19) se resuelve porque agregar una nueva universidad implica únicamente agregar un adaptador en la capa de integración, y agregar un nuevo tipo de certificación implica un nuevo servicio, sin tocar los servicios existentes.

**Preparación para migración a la nube.** La restricción de iniciar on-premise pero migrar a la nube en fases posteriores (RES-11) se resuelve porque la separación en capas y servicios permite migrar un servicio a la vez (por ejemplo, primero el repositorio analítico OLAP a la nube, manteniendo el resto on-premise), sin requerir un "big bang" de migración.

## Argumentación económica

**Aprovechamiento de infraestructura existente.** Al ser on-premise en su primera versión (RES-11), la arquitectura en capas permite distribuir los servicios sobre los servidores físicos existentes del SICA sin necesidad de inversión adicional en infraestructura para el piloto.

**Reducción de costos de licenciamiento.** La capa de integración y los servicios pueden construirse sobre tecnologías Open Source (RES-07): por ejemplo, un bus de mensajería open source para el componente basado en eventos, motores de bases de datos open source para OLTP y OLAP, y librerías open source de PKI para la firma electrónica de certificados, evitando licenciamiento costoso de plataformas SOA propietarias.

**Optimización del almacenamiento de evidencia.** Separar la evidencia anti-fraude (alta volumetría, retención de 5 años) en un almacenamiento propio dentro de la capa de datos permite aplicar políticas de almacenamiento en frío u optimizado en costos (EaC-09), sin que esa volumetría incremente el costo del almacenamiento transaccional principal.

**Escalamiento bajo demanda con control de presupuesto.** Al concentrar la escalabilidad en el Servicio de Evaluación Adaptativa, los recursos adicionales solo se requieren durante la primera semana de cada mes, lo que permite planificar el presupuesto de USD 180,000 alrededor de picos predecibles en lugar de sobredimensionar toda la plataforma de forma permanente.

**Viabilidad del equipo de desarrollo.** La separación en servicios independientes por capas permite que equipos pequeños trabajen en paralelo sobre módulos acotados (evaluación, certificación, auditoría, integración, analítica), lo cual es coherente con la realidad operativa descrita: "personal de soporte limitado" y capacidades técnicas heterogéneas.

---

## Conclusión de la selección

La combinación de **arquitectura en capas con orientación a servicios**, complementada con un **componente basado en eventos** para los flujos asíncronos de evidencia, notificaciones y analítica, es la que mejor refleja el negocio del PRCCD: cada servicio corresponde a un proceso de negocio identificable, los drivers críticos (escalabilidad en picos, tolerancia a fallos de integración, separación analítica, cumplimiento normativo) quedan resueltos por la propia estructura del estilo, y la combinación es viable dentro del presupuesto y del plazo de tres a cuatro semanas establecidos para esta primera versión.
 
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
 
### 10.1 Patrón 1 — Adapter (Adaptador)

### Punto de aplicación
**Capa de Integración con Universidades (USAC, UCR, UES)**

La plataforma debe conectarse con sistemas que utilizan:

- LDAP
- SAML
- OAuth2
- JSON
- XML
- CSV

El patrón Adapter permite que todos esos sistemas sean consumidos mediante una interfaz común.



### UML     

```text
                    +----------------------+
                    | IUniversidadAdapter  |
                    +----------------------+
                    | autenticar()         |
                    | obtenerDatos()       |
                    +----------+-----------+
                               ^
          +--------------------+--------------------+
          |                    |                    |
          |                    |                    |
+----------------+   +----------------+   +----------------+
| LDAPAdapter    |   | SAMLAdapter    |   | OAuthAdapter   |
+----------------+   +----------------+   +----------------+
| autenticar()   |   | autenticar()   |   | autenticar()   |
| obtenerDatos() |   | obtenerDatos() |   | obtenerDatos() |
+-------+--------+   +-------+--------+   +--------+-------+
        |                    |                    |
        v                    v                    v
   Sistema LDAP        Sistema SAML       Sistema OAuth2
```

### Justificación

Cada universidad expone mecanismos distintos de autenticación e intercambio de datos.

El patrón Adapter:

- evita modificar los sistemas externos;
- desacopla la PRCCD de tecnologías específicas;
- facilita incorporar nuevas universidades.
 
### 10.2 Patrón 2 — Strategy (Estrategia)

### Punto de aplicación

**Motor de Exámenes Adaptativos**

La dificultad de las preguntas cambia según el desempeño del candidato.

Cada algoritmo de adaptación puede implementarse como una estrategia diferente.

### UML

```text
                 +----------------------+
                 | DifficultyStrategy   |
                 +----------------------+
                 | calcularSiguiente()  |
                 +----------+-----------+
                            ^
        +-------------------+------------------+
        |                   |                  |
        |                   |                  |
+----------------+ +----------------+ +----------------+
| EasyStrategy   | | MediumStrategy | | HardStrategy   |
+----------------+ +----------------+ +----------------+
| calcular()     | | calcular()     | | calcular()     |
+----------------+ +----------------+ +----------------+

                 +----------------------+
                 | ExamEngine           |
                 +----------------------+
                 | strategy             |
                 +----------------------+
                 | evaluarRespuesta()   |
                 +----------------------+
```

### Justificación

Permite cambiar el algoritmo de evaluación sin modificar el motor principal.

Beneficios:

- flexibilidad;
- extensibilidad;
- mantenimiento sencillo.
 
### 10.3 Patrón 3 — Factory Method

### Punto de aplicación

**Generación de Certificados Digitales**

La plataforma puede emitir diferentes tipos de certificados:

- Certificado académico
- Certificado profesional
- Certificado regional
- Certificado blockchain

### UML

```text
                    +------------------+
                    | Certificate      |
                    +------------------+
                    | generar()        |
                    +--------+---------+
                             ^
        +--------------------+--------------------+
        |                    |                    |
        |                    |                    |
+----------------+  +----------------+  +----------------+
| AcademicCert   |  | Professional   |  | BlockchainCert |
+----------------+  +----------------+  +----------------+
| generar()      |  | generar()      |  | generar()      |
+----------------+  +----------------+  +----------------+

              +------------------------+
              | CertificateFactory     |
              +------------------------+
              | crearCertificado()     |
              +-----------+------------+
                          |
                          v
                    Certificate
```

### Justificación

La lógica de creación queda centralizada.

Beneficios:

- desacopla la creación del uso;
- facilita agregar nuevos tipos de certificación;
- mejora mantenibilidad.

 
### 10.4 Patrón 4 — Observer (Observador)

### Punto de aplicación

**Monitoreo, Auditoría y Notificaciones**

Cuando ocurre un evento relevante:

- examen aprobado;
- examen reprobado;
- certificado emitido;
- intento sospechoso de fraude;

varios módulos deben reaccionar automáticamente.

### UML

```text
                +--------------------+
                | Subject            |
                +--------------------+
                | attach()           |
                | detach()           |
                | notify()           |
                +---------+----------+
                          ^
                          |
                +---------+----------+
                | ExamEventManager   |
                +--------------------+

                          |
          ---------------------------------------
          |                 |                  |
          v                 v                  v

+----------------+ +----------------+ +----------------+
| AuditObserver  | | EmailObserver  | | DashboardObs.  |
+----------------+ +----------------+ +----------------+
| update()       | | update()       | | update()       |
+----------------+ +----------------+ +----------------+
```

### Justificación

Un mismo evento genera múltiples acciones.

Permite:

- registrar auditorías;
- enviar notificaciones;
- actualizar dashboards;

sin acoplar los componentes.

 
### 10.5 Patrón 5 — Singleton

### Punto de aplicación

**Servicio Central de Auditoría Inmutable**

La bitácora de auditoría debe ser única y consistente para toda la plataforma.

### UML

```text
                +----------------------+
                | AuditManager         |
                +----------------------+
                | instance             |
                +----------------------+
                | getInstance()        |
                | registrarEvento()    |
                +----------+-----------+
                           |
                           |
                     única instancia
```

### Justificación

La auditoría es un recurso compartido y crítico.

Beneficios:

- única fuente de verdad;
- evita inconsistencias;
- facilita trazabilidad y cumplimiento normativo.
 
---
 
## 11. Gestión del Proyecto (Enfoque Ágil)
 
### 11.1 Tablero Kanban

El proyecto se gestiona mediante un tablero Kanban con el flujo de trabajo: **To Do → Blocked → In Progress → Ready for Testing → Test/QA → Done**.

![Tablero Kanban](documentación/img/tablero-kanban.png)

### 11.2 Backlog del proyecto (historias de usuario y tareas de desarrollo)

El detalle del backlog, con las tareas de desarrollo de la arquitectura organizadas por columna y categoría, se encuentra en:

📋 [Backlog del proyecto — Tablero Kanban PRCCD](documentación/kanban-backlog.md)
 
---
 
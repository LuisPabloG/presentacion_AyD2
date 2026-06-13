# Selección Arquitectónica -- PRCCD

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
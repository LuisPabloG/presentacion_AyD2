# Patrones de Diseño para la PRCCD

## 1. Adapter (Adaptador)

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

---

## 2. Strategy (Estrategia)

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

---

## 3. Factory Method

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

---

## 4. Observer (Observador)

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

---

## 5. Singleton

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



 
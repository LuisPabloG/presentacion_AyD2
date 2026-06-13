# Requisitos Funcionales (RF)

| Codigo | Descripcion del Driver RF |
|--------|--------------------------|
| RF01 | Validar identidad federada del candidato antes de permitirle iniciar la evaluacion (autenticacion con universidad de origen). |
| RF02 | Presentar preguntas de evaluacion al candidato de forma secuencial durante el proceso de examen. |
| RF03 | Variar la dificultad de las preguntas en tiempo real segun las respuestas previas del candidato (motor adaptativo). |
| RF04 | Registrar y guardar las respuestas del candidato durante la evaluacion de forma persistente. |
| RF05 | Capturar pantalla del dispositivo del candidato durante la evaluacion como evidencia antifraude. |
| RF06 | Registrar logs de tecleo del candidato durante la evaluacion como evidencia antifraude. |
| RF07 | Capturar rafagas de video ocasional del candidato durante la evaluacion como evidencia antifraude. |
| RF08 | Registrar eventos sospechosos detectados durante la evaluacion (cambio de ventana, copia, comportamiento inusual). |
| RF09 | Validar que el candidato realice la evaluación dentro de un periodo de certificación vigente configurado por SICA. |
| RF10 | Determinar la aprobacion del candidato cuando su puntaje alcanza el umbral minimo requerido. |
| RF11 | Emitir la credencial/certificado digital oficial cuando el candidato aprueba la evaluacion. |
| RF12 | Generar el documento visual del certificado en formato descargable y verificable. |
| RF13 | Registrar el certificado en la red Blockchain/PKI para garantizar inmutabilidad y trazabilidad. |
| RF14 | Permitir que cualquier tercero verifique la autenticidad criptografica del certificado sin depender del SICA. |
| RF15 | Determinar la desaprobacion del candidato cuando su puntaje no alcanza el umbral minimo requerido. |
| RF16 | Notificar al candidato el resultado desaprobado con detalle del puntaje obtenido y proximo periodo. |
| RF17 | Evaluar las condiciones del candidato para determinar si puede acceder a un reintento de evaluación. |
| RF18 | Habilitar al candidato para reintentar la evaluacion en el siguiente periodo si no se detecto fraude. |
| RF19 | Bloquear la opcion de reintento del candidato cuando se confirma fraude en la evaluacion. |
| RF20 | Informar al candidato la fecha del proximo periodo de certificacion disponible. |
| RF21 | Autenticar la conexión institucional activa con cada universidad mediante el protocolo configurado. |
| RF22 | Establecer los parámetros generales de integración requeridos para una universidad incorporada a la PRCCD. |
| RF23 | Consultar el historial académico del candidato desde la universidad de origen durante el proceso de certificación. |
| RF24 | Transformar y normalizar los datos academicos recibidos al formato interno unificado de la PRCCD. |
| RF25 | Consultar los certificados emitidos a los estudiantes de una universidad desde la plataforma institucional. |
| RF26 | Verificar la autenticidad criptografica de un certificado consultado por una universidad. |
| RF27 | Evaluar el impacto sobre certificados vigentes cuando ocurre un cambio en el estado academico del estudiante. |
| RF28 | Iniciar el proceso de revocacion de un certificado cuando se requiere (cambio de estado, derecho al olvido). |
| RF29 | Registrar la revocacion del certificado en la red Blockchain/PKI de forma inmutable. |
| RF30 | Notificar la revocacion del certificado al titular correspondiente. |
| RF31 | Controlar el acceso autorizado del auditor al expediente de evidencia antifraude según su rol y permisos asignados. |
| RF32 | Consultar la evidencia antifraude capturada por evaluacion (pantalla, tecleo, video, eventos). |
| RF33 | Verificar la integridad de la evidencia almacenada para detectar posible manipulacion. |
| RF34 | Detectar patrones sospechosos en la evidencia capturada durante la evaluacion. |
| RF35 | Escalar un caso como fraude confirmado cuando se verifican las irregularidades detectadas. |
| RF36 | Bloquear el certificado asociado a una evaluacion cuando se confirma fraude. |
| RF37 | Notificar a la Secretaria SICA cuando se confirma un caso de fraude. |
| RF38 | Generar reporte de auditoria con firma electronica avanzada como documento oficial. |
| RF39 | Registrar el reporte de auditoria en una bitacora inmutable para cumplimiento legal. |
| RF40 | Gestionar la retención y disponibilidad de la evidencia antifraude almacenada.|
| RF41 | Ejecutar el derecho al olvido sobre los datos personales del candidato asociados a evaluaciones y evidencia antifraude, cuando corresponda. |
| RF42 | Registrar una nueva universidad en la plataforma como institucion integrante. |
| RF43 | Configurar el protocolo de autenticación institucional para cada universidad registrada. |
| RF44 | Definir el formato de intercambio de datos entre la PRCCD y cada universidad (JSON/XML/CSV). |
| RF45 | Ejecutar la sincronización institucional de datos académicos con las universidades registradas. |
| RF46 | Validar la integridad de los datos recibidos de cada universidad durante la sincronizacion. |
| RF47 | Actualizar la configuracion de integracion cuando cambian los parametros de una universidad. |
| RF48 | Notificar fallo de conexion al administrador TI de la universidad correspondiente. |
| RF49 | Gestionar el error de sincronizacion cuando la transferencia de datos falla parcial o totalmente. |
| RF50 | Monitorear el estado de las conexiones institucionales activas en tiempo real. |
| RF51 | Controlar el acceso autorizado del usuario gerencial al módulo de analítica regional según su rol institucional.|
| RF52 | Extraer datos de evaluaciones y certificaciones para generacion de reportes analiticos. |
| RF53 | Anonimizar los datos personales antes de incluirlos en cualquier reporte o dashboard. |
| RF54 | Verificar que el reporte generado no contenga datos personales identificables (cumplimiento GDPR). |
| RF55 | Generar dashboard gerencial con metricas regionales de competencias digitales. |
| RF56 | Segmentar metricas por pais, genero y carrera universitaria segun parametros del usuario. |
| RF57 | Agregar datos por multiples dimensiones de analisis para reportes estrategicos. |
| RF58 | Exportar reporte analitico en formatos descargables. |
| RF59 | Registrar cada acceso al modulo de analitica en la bitacora de auditoria. |
| RF60 | Ejecutar el derecho al olvido sobre los datos fuente utilizados para analítica regional, cuando corresponda según GDPR. |
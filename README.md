Detección de escalada de privilegios en Active Directory - Adición a Domain Admins

Este repositorio contiene una regla Sigma diseñada para detectar posibles intentos de escalada de privilegios en entornos Windows Active Directory, específicamente cuando un usuario es agregado al grupo "Domain Admins". Esta acción puede ser legítima, pero también puede ser indicativa de un ataque o una actividad sospechosa que busca obtener control total sobre el dominio.

Objetivo de la regla
La detección busca identificar eventos en los que un usuario es agregado al grupo Domain Admins, lo que podría representar una amenaza si el cambio no es autorizado. Esta regla es útil para:
- Monitorear actividades administrativas críticas en Active Directory.
- Detectar posibles ataques internos o movimientos laterales de un adversario.
- Mejorar la respuesta ante Amenazas Persistentes Avanzadas (APT) que intentan comprometer el directorio.

Origen de datos
La regla se basa en los eventos de seguridad de Windows:
- Event ID 4728: Se activa cuando un usuario es agregado a un grupo de seguridad global en Active Directory.
- Windows Security Log: Proporciona registros detallados sobre cambios en cuentas y grupos privilegiados.
- Herramientas SIEM como Splunk, Graylog, ELK o cualquier sistema compatible con Sigma pueden utilizar esta regla.

Etiquetas MITRE ATT&CK
Para mejorar la identificación de amenazas, la regla incorpora técnicas de MITRE ATT&CK:
- attack.persistence → La adición de usuarios a Domain Admins permite a atacantes mantener acceso prolongado.
- attack.privilege_escalation → Obtener acceso a Domain Admins concede permisos elevados en el dominio.
- attack.t1098 - Account Manipulation → Modificación de cuentas y grupos administrativos para obtener control.
- attack.t1078 - Valid Accounts → Uso indebido de cuentas legítimas para ganar acceso privilegiado.

Configuración de la regla Sigma
La regla filtra eventos específicos para mejorar la precisión y reducir falsos positivos:
- Eventos de adición a Domain Admins mediante el Event ID 4728.
- Exclusión de usuarios administrativos legítimos como Administrator y admin.
- Condiciones de ejecución que identifican cambios de permisos sospechosos.

Uso y despliegue
La regla puede ser utilizada en cualquier solución de seguridad compatible con Sigma, como:
- Splunk
- Elasticsearch (ELK)
- Graylog
- Windows Defender ATP
Para su implementación, se recomienda integrarla en herramientas de monitoreo y definir alertas personalizadas para una rápida respuesta ante posibles ataques.

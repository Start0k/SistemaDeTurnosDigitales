## Sistema de Gestion de Turnos Digitales

### Descripcion General del Sistema
Este proyecto corresponde al modelado arquitectónico completo de un Sistema de Gestión de Turnos Digitales (Tunomático), diseñado para optimizar y digitalizar la asignación de turnos en instituciones que requieren un flujo ordenado de atención, tales como clínicas, bancos, oficinas públicas y centros de servicios.

El objetivo principal del sistema es garantizar una experiencia eficiente, equitativa y trazable en la atención al público, mediante una plataforma adaptable, segura y fácil de operar tanto para usuarios como para administradores.

El sistema contempla funcionalidades clave como:

- Generación automatizada y manual de turnos por tipo de servicio.

- Priorización de turnos especiales (por edad, discapacidad, emergencia, etc.).

- Visualización en tiempo real de turnos activos y estados de atención.

- Administración de módulos de atención y personal asignado.

- Estadísticas de atención y tiempos promedio por módulo o servicio.

- Notificaciones visuales y/o sonoras en pantallas conectadas.

- Acceso diferenciado para usuarios, operadores y administradores del sistema.

- Escalabilidad para operar en múltiples sucursales o sedes de forma centralizada.

Este modelado abarca desde la visión funcional (mediante casos de uso UML) hasta la arquitectura física del sistema (diagrama de implementación UML), aplicando buenas prácticas de diseño orientado a objetos y utilizando patrones de diseño reconocidos como Singleton, Prototype, Adapter y Bridge, según corresponda.
### Objetivos del modelado
El presente trabajo tiene como finalidad ejercitar un enfoque integral de ingeniería de software, abordando todas las capas de abstracción de un sistema, desde su definición funcional hasta su arquitectura física. Los objetivos específicos del modelado son:

Desarrollar una transición completa desde la visión funcional hasta el despliegue físico, comenzando con los requerimientos del sistema (mediante casos de uso UML) y culminando en una arquitectura implementable y escalable.

Aplicar patrones de diseño reconocidos (Singleton, Prototype, Adapter, Bridge) en la construcción del modelo lógico (diagrama de clases), asegurando una arquitectura robusta, mantenible y orientada a la reutilización.

Ejercitar el pensamiento arquitectónico mediante la correcta separación de responsabilidades, fomentando la modularidad del sistema, la escalabilidad futura y la facilidad de integración con otros sistemas o tecnologías.

Este enfoque permite reflejar una solución madura y profesional a una problemática real, sirviendo como base sólida para una eventual implementación técnica en entornos productivos.

### Diagrama de Caso de Uso UML
![](https://github.com/Start0k/SistemaDeTurnosDigitales/blob/ea22ebd0498ccabc7cd0fea19ee71a509f8aa007/imagenes/Caso%20de%20Uso.png)
#### Descripcion General
El análisis funcional del Sistema Tunomático permitió identificar de forma clara los actores involucrados y los casos de uso esenciales para la gestión eficiente de turnos digitales. Se utilizaron relaciones `<<include>>` y `<<extend>>` siguiendo buenas prácticas de modelado UML, lo que permitió representar con precisión los flujos obligatorios y opcionales del sistema.
#### Actores Identificados
Cliente: Usuario que solicita atención mediante el sistema de turnos. Puede sacar, cancelar y consultar su turno.

Recepcionista: Personal encargado de registrar la atención cuando un cliente es llamado, verificando los datos previamente.

Administrador: Usuario con privilegios avanzados para gestionar usuarios del sistema y generar reportes sobre su funcionamiento.
#### Casos de uso destacados y relaciones aplicadas:
##### Sacar Turno

- `<<extend>>` Validar Datos: el sistema puede extender el proceso si requiere validar previamente la identidad del cliente.

- `<<extend>>` Enviar Notificación: se puede activar opcionalmente para informar al cliente sobre el número de turno asignado.

##### Cancelar Turno

- `<<include>>` Enviar Notificación: el sistema siempre notifica al cliente sobre la cancelación.

- `<<extend>>` Validar Datos: si hay dudas sobre la identidad, se solicita validación previa.

##### Registrar Atención

- `<<include>>` Validar Datos: el recepcionista siempre debe confirmar la identidad del cliente antes de continuar.

### Diagrama de Clases UML con Patrones Aplicados
![](https://github.com/Start0k/SistemaDeTurnosDigitales/blob/e889136a0d933eda857a14469e9e0353385be89f/imagenes/Diagrama%20de%20Clases.png)
#### Justificación Arquitectónica y Patrones Aplicados
##### Selección de patrones
La elección de los patrones de diseño no fue arbitraria, sino estratégica y alineada a las necesidades específicas del sistema y sus desafíos técnicos.

##### Singleton (Administrador)

Justificación: Se seleccionó Singleton para la gestión centralizada de la lógica de turnos. Este patrón permite garantizar que exista una única instancia accesible globalmente, evitando inconsistencias y facilitando la administración de turnos desde cualquier módulo del sistema.

##### Intención arquitectónica:

Centralizar el control de la lógica de turnos.

Facilitar la escalabilidad futura permitiendo la consulta distribuida.

Evitar múltiples puntos de configuración que pudieran provocar errores operacionales.

##### Prototype (Turno)

Justificación: La operación de solicitud de turnos exige rapidez y eficiencia en la gestión de turnos repetitivos. Se implementó Prototype para permitir la clonación de turnos base, permitiendo a los operadores agilizar las operaciones sin recrear turnos desde cero.

##### Intención arquitectónica:

Reducir la complejidad y tiempo de operaciones manuales.

Permitir la creación rápida de nuevas instancias de turnos desde plantillas base, manteniendo flexibilidad y control.

Facilitar la parametrización de campañas o protocolos especiales.

##### Adapter (Correo y Mensaje)

Justificación: Dado que el sistema debe notificar a los clientes, el uso de Adapter fue clave para desacoplar el núcleo del sistema de las APIs de notificación externas, permitiendo mantener la flexibilidad en caso de cambios o actualizaciones en los sistemas de notificación.

##### Intención arquitectónica:

Asegurar la independencia tecnológica del sistema interno.

Facilitar el mantenimiento y evolución del sistema de integración.

Permitir la adaptación a distintos sistemas externos sin impactar el dominio.

### Diagrama de Implementacion UML
![](https://github.com/Start0k/SistemaDeTurnosDigitales/blob/e889136a0d933eda857a14469e9e0353385be89f/imagenes/Implementacion.png)
#### Despliegue Físico y decisiones técnicas:
Para garantizar la seguridad, escalabilidad y disponibilidad del sistema, se han tomado las siguientes decisiones en el despliegue físico:

##### Nodos físicos diferenciados:
Se establecieron servidores dedicados para cada función clave del sistema, reforzando la separación de responsabilidades y minimizando riesgos. Esto permite distribuir la carga de trabajo y mejorar la resiliencia ante fallos.

##### Separación clara de responsabilidades:

- Servidor de aplicaciones: Maneja la lógica del sistema y las interacciones de los usuarios.

- Servidor de configuración: Gestiona parámetros críticos y ajustes globales.

- Servidor de integración ERP: Facilita la comunicación con sistemas externos como el ERP hospitalario.

- Servidor de bases de datos: Asegura el almacenamiento y consulta eficiente de la información.

##### Uso de protocolos estándar en integraciones externas: 
Se adoptaron REST y SOAP para garantizar la interoperabilidad con otros sistemas, asegurando comunicación segura y estructurada con el ERP y otros servicios externos.

##### Aislamiento de componentes críticos:

- Configuración del sistema (ConfiguracionSistema): Se aloja en un nodo dedicado para reforzar la estabilidad y el control de cambios.

- Seguridad: Implementación de medidas de acceso restringido y auditorías periódicas para mitigar riesgos.

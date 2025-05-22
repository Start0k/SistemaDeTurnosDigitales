## Sistema de Gestion de Turnos Digitales

### Descripcion General del Sistema
En este proyecto se presentará el modelado arquitectónico completo de un sistema de turnos digitales, diseñado para optimizar la asignación de turnos y adaptarlo a un entorno digitalizado. El objetivo principal del sistema es mejorar la experiencia de atención al público mediante una aplicación intuitiva, segura y fácil de operar. Este modelado abarca una visión funcional basada en casos UML, aplicando buenas prácticas en el diseño y empleando patrones de arquitectura como Singleton, Prototype y Adapter.
### Objetivos del modelado
- Aplicar Patrones de Diseño en la arquitectura, siguiendo buenas practicas.
- Fomentar el pensamiento arquitectonico con el objetivo de construir un sistema robusto capaz de adaptarse al futuro.- -

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

La eleccion de los patrones de diseños fue escogida segun la necesidad del sistema para que cumpla con las necesidades del sistema.

##### Singleton (Administrador)

Justificación: Se seleccionó Singleton para la gestión centralizada de la lógica de turnos. Este patrón permite garantizar que exista una única instancia accesible globalmente, evitando inconsistencias y facilitando la administración de turnos desde cualquier módulo del sistema.

##### Intención arquitectónica:

Centralizar el control de la lógica de turnos.

Facilitar la escalabilidad futura permitiendo la consulta distribuida.

Evitar múltiples puntos de configuración que pudieran provocar errores operacionales.

##### Prototype (Turno)

##### Justificación: 
La operación de solicitud de turnos exige rapidez y eficiencia en la gestión de turnos repetitivos. Se implementó Prototype para permitir la clonación de turnos base, permitiendo a los operadores agilizar las operaciones sin recrear turnos desde cero.

##### Intención arquitectónica:

Reducir la complejidad y tiempo de operaciones manuales.

Permitir la creación rápida de nuevas instancias de turnos desde plantillas base, manteniendo flexibilidad y control.

Facilitar la parametrización de campañas o protocolos especiales.

##### Adapter (Correo y Mensaje)

##### Justificación:
Dado que el sistema debe notificar a los clientes, el uso de Adapter fue clave para desacoplar el núcleo del sistema de las APIs de notificación externas, permitiendo mantener la flexibilidad en caso de cambios o actualizaciones en los sistemas de notificación.

##### Intención arquitectónica:

Asegurar la independencia tecnológica del sistema interno.

Facilitar el mantenimiento y evolución del sistema de integración.

Permitir la adaptación a distintos sistemas externos sin impactar el dominio.

### Diagrama de Implementacion UML
![](https://github.com/Start0k/SistemaDeTurnosDigitales/blob/e889136a0d933eda857a14469e9e0353385be89f/imagenes/Implementacion.png)
#### Despliegue Físico y decisiones técnicas:
Para garantizar la seguridad, escalabilidad y disponibilidad del sistema, se han tomado las siguientes decisiones en el despliegue físico:

- Nodos físicos diferenciados para reforzar seguridad, escalabilidad y disponibilidad del sistema de turnos digitales.

- Separación clara de responsabilidades entre servidores de aplicaciones, configuración, gestión de turnos, y bases de datos.

- Uso de protocolos estándar (REST, SOAP) en las integraciones externas, incluyendo sistemas de notificación y ERP hospitalario.

- Aislamiento de componentes críticos (como la gestión de configuración de turnos) en nodos dedicados para reforzar el control de cambios y estabilidad del sistema.

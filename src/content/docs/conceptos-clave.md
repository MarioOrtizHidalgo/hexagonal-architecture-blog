# Conceptos clave de la Arquitectura Hexagonal

Para comprender correctamente la arquitectura hexagonal es importante conocer los elementos principales que la componen. Estos conceptos definen cómo se organiza el sistema y cómo interactúan sus distintas partes.

## Dominio

El **dominio** representa el núcleo de la aplicación y contiene la lógica de negocio más importante. Aquí se definen las reglas, comportamientos y modelos que representan el problema que la aplicación intenta resolver.

En una arquitectura hexagonal, el dominio debe ser **independiente de cualquier tecnología externa**. Esto significa que no debería depender directamente de frameworks, bases de datos, APIs externas ni interfaces de usuario. De esta manera, el corazón de la aplicación permanece estable incluso si cambian los detalles técnicos de la infraestructura.

## Puertos

Los **puertos** son interfaces que definen cómo el mundo exterior puede interactuar con el dominio o cómo el dominio necesita interactuar con sistemas externos. Funcionan como contratos que establecen qué operaciones están disponibles, sin especificar cómo se implementan.

Existen dos tipos principales de puertos:

* **Puertos de entrada**: definen las acciones que pueden realizarse sobre la aplicación, como casos de uso o servicios de aplicación.
* **Puertos de salida**: definen las dependencias que el dominio necesita para funcionar, como acceder a una base de datos, enviar correos electrónicos o comunicarse con otros servicios.

Gracias a los puertos, el dominio permanece desacoplado de las implementaciones concretas.

## Adaptadores

Los **adaptadores** son las implementaciones concretas de los puertos. Su función es traducir la comunicación entre el mundo exterior y el dominio de la aplicación.

Por ejemplo:

* Un **controlador HTTP** puede actuar como adaptador de entrada que recibe peticiones desde una API REST y las transforma en llamadas al dominio.
* Un **repositorio que usa una base de datos** puede ser un adaptador de salida que implementa un puerto definido por el dominio para persistir información.

Los adaptadores permiten conectar diferentes tecnologías sin que el dominio tenga conocimiento directo de ellas.

## Aplicación / Casos de uso

Entre el dominio y los adaptadores suele existir una capa de **casos de uso** o **servicios de aplicación**. Esta capa coordina las operaciones necesarias para ejecutar acciones del sistema.

Los casos de uso se encargan de:

* Orquestar la lógica del dominio
* Invocar repositorios u otros puertos necesarios
* Definir el flujo de una operación de negocio

De esta forma, cada caso de uso representa una **acción concreta que el sistema puede realizar**.

## Infraestructura

La **infraestructura** incluye todos los detalles técnicos necesarios para que la aplicación funcione: bases de datos, frameworks web, sistemas de mensajería, servicios externos, etc.

En la arquitectura hexagonal, estos elementos se sitúan en los bordes del sistema y se conectan al dominio mediante adaptadores. Esto permite cambiar tecnologías sin afectar a la lógica central de la aplicación.

---

En conjunto, estos conceptos permiten construir aplicaciones donde la **lógica de negocio se mantiene aislada de los detalles técnicos**, facilitando el mantenimiento, las pruebas y la evolución del sistema.

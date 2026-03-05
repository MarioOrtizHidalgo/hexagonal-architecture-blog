---
titulo: Introducción
descripcion: Introducción a la arquitectura hexagonal
order: 1
---

# Introducción a la Arquitectura Hexagonal

La arquitectura hexagonal, también conocida como **Puertos y Adaptadores**, es un estilo de arquitectura de software propuesto por **Alistair Cockburn** cuyo objetivo principal es **desacoplar la lógica de negocio** del resto de la aplicación. En este enfoque, el núcleo de la aplicación —donde vive la lógica de dominio— permanece completamente **independiente** de elementos externos como bases de datos, interfaces de usuario, frameworks o servicios externos.

La idea central consiste en organizar el sistema alrededor de un **núcleo de dominio** que define las **reglas del negocio**, y permitir que todo lo externo se conecte a él a través de **puertos** (interfaces) y **adaptadores** (implementaciones concretas). Los puertos definen cómo puede interactuar el exterior con la aplicación, mientras que los adaptadores se encargan de traducir esas interacciones hacia el modelo interno del sistema.

El nombre de “hexagonal” no hace referencia estrictamente al número de lados del sistema, sino a una metáfora visual que ayuda a representar que la aplicación puede tener múltiples **puntos de entrada y salida**, todos ellos conectados al dominio mediante interfaces bien definidas. Esto permite que componentes como APIs, interfaces web, bases de datos o sistemas de mensajería se integren **sin afectar** directamente al corazón de la aplicación.

Uno de los principales beneficios de la arquitectura hexagonal es la **independencia tecnológica**. La lógica de negocio no depende de frameworks, bases de datos ni detalles de infraestructura, lo que **facilita cambiar o reemplazar** estos elementos sin modificar el dominio. Esto también mejora considerablemente la capacidad de realizar **pruebas**, ya que el núcleo de la aplicación puede testearse de forma aislada mediante adaptadores simulados o *mocks*.

Además, este enfoque favorece la **mantenibilidad** y evolución del sistema. Al mantener una separación clara de **responsabilidades**, el código se vuelve más **modular, comprensible y adaptable** a cambios futuros. Los desarrolladores pueden trabajar en distintas partes del sistema sin afectar otras áreas críticas, lo que resulta especialmente útil en proyectos grandes o con ciclos de vida largos.
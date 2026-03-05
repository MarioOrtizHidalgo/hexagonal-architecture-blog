# 🚀 Documentación sobre Arquitectura Hexagonal con Astro

Este proyecto es una web estática creada con el propósito principal de **aprender y practicar los conceptos fundamentales de Astro**. Al mismo tiempo, sirve como un espacio de investigación y documentación personal sobre la **Arquitectura Hexagonal**, un patrón de diseño de software introducido por Alistair Cockburn (también conocido como el patrón de Puertos y Adaptadores).

## 🎯 Objetivos del Proyecto

1. **Explorar Astro:** Entender su funcionamiento básico, simplicidad y ventajas para la creación de sitios web estáticos de alta velocidad.
2. **Renderizado con Markdown (MD):** Aprovechar la integración nativa y sencilla de Astro con archivos Markdown para renderizar y gestionar el contenido eficiente y ordenadamente.
3. **Investigar Arquitectura Hexagonal:** Crear un recurso detallado y completamente en **español** que sirva para estudiar y clarificar este patrón de arquitectura (separación por capas como Dominio, Aplicación e Infraestructura).

## 🛠️ Tecnologías Utilizadas

- **[Astro](https://astro.build/)**: Framework web optimizado para la entrega rápida de contenido.
- **Markdown**: Formato elegido para la escritura fluida de la base de conocimientos y artículos.
- **Desarrollo Web Base**: Html, CSS y Javascript estructurado dentro del potente sistema de componentes de extensión `.astro`.

## 📁 Estructura del Proyecto

A continuación, se detalla la estructura principal de la aplicación:

```text
/
├── public/           # Archivos estáticos e imágenes (favicon, etc.) accesibles públicamente
├── src/
│   ├── components/   # Componentes globales de interfaz (Header, Footer, etc.)
│   ├── layouts/      # Plantillas base (envoltorios) para definir el estilo de las páginas
│   └── pages/        # Rutas de la web (índice, aplicación, dominio, conceptos-clave, etc.)
└── package.json      # Control de dependencias y scripts de comandos
```

## 🧞 Despliegue y Comandos Locales

Todos los comandos se deben ejecutar desde la raíz del proyecto en la terminal.

| Comando                   | Acción                                                                 |
| :------------------------ | :--------------------------------------------------------------------- |
| `npm install`             | Instala todas las dependencias necesarias.                             |
| `npm run dev`             | Inicia el servidor de desarrollo local (normalmente en `localhost:4321`).|
| `npm run build`           | Construye la versión optimizada para producción del sitio en `./dist/`.|
| `npm run preview`         | Previsualiza el proyecto compilado antes de realizar el despliegue.    |

## 📚 Secciones del Sitio

El sitio expone el contenido segmentado por los niveles estructurales de la Arquitectura Hexagonal:

- **Conceptos Clave** (`/conceptos-clave`): Una introducción profunda a las razones y beneficios de este planteamiento de software.
- **Dominio** (`/dominio`): Documentación sobre el núcleo de la aplicación y donde reside la lógica de negocio purista e independiente.
- **Aplicación** (`/aplicacion`): Guía descriptiva sobre los Casos de Uso del usuario y cómo la información entra a nuestro sistema.

## ✒️ Motivación Original

La idea nace con la doble intención de encontrar un flujo de trabajo que permitiese estructurar contenido rápidamente y aprender una nueva tecnología. 

Investigar la **Arquitectura Hexagonal** en combinación con **Laravel** o de forma conceptual, requería de apuntes limpios y ordenados. Es aquí donde usar **Astro** junto con **Markdown** se convirtió en la mejor idea para el proyecto: una herramienta sencilla que permite centrarse un 100% en el contenido y aprender de forma práctica en el proceso.

---
# Vera · sitio de inscripción

Web pública de Vera, un newsletter diario de noticias en español: landing, formulario de inscripción, encuesta de investigación y backoffice del equipo.

**En vivo:** [holavera.news](https://holavera.news)

![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-vanilla-F7DF1E?logo=javascript&logoColor=black)
![Supabase](https://img.shields.io/badge/Supabase-supabase--js_v2-3FCF8E?logo=supabase&logoColor=white)
![GitHub Pages](https://img.shields.io/badge/GitHub_Pages-holavera.news-222222?logo=github)

## Qué es

Vera envía cada día un resumen de noticias con tres segmentos: Mundo, Chile y una sección personalizada según los temas que elige cada lector. Este repositorio contiene solo la cara pública del proyecto: las páginas donde la gente conoce Vera, se inscribe y responde la encuesta. Está dirigido a lectores en Chile y a chilenos que viven en el extranjero.

## Cómo funciona Vera

Cada edición la redacta un agente de IA (una rutina de Claude Code) a partir de una lista blanca de medios verificados. El pipeline de generación y envío vive en un repositorio privado aparte; este sitio solo recoge inscripciones y opiniones.

## Funcionalidades

- **Landing mobile-first:** réplica del diseño del equipo, escalada desde un lienzo de 1080 px con una variable CSS. Variantes en `/hola/`, `/unete/` y `/prueba/` con el mismo contenido y una URL de entrada distinta.
- **Formulario de inscripción** (`/formulario/`): nombre, correo, ciudad, región de Chile (u opción "vivo fuera de Chile") y de dos a tres subcategorías entre cinco áreas temáticas. Guarda la inscripción en Supabase y muestra una confirmación con los temas elegidos.
- **Encuesta** (`/encuesta/`): siete preguntas abiertas sobre cómo se informa la gente, más algunos datos de quien responde.
- **Backoffice** (`/backoffice/`): panel interno con acceso por enlace mágico de Supabase Auth, limitado a los socios. Muestra métricas de lectura y lectores, respuestas de la encuesta y registro de correcciones, y permite gestionar la lista de fuentes y los proyectos del equipo. Incluye los manuales editorial y de marca.
- **SEO y privacidad:** metadatos Open Graph en las páginas principales y `noindex` en el formulario, la encuesta y el backoffice.

## Stack

| Área | Tecnología |
|------|------------|
| Front | HTML, CSS y JavaScript sin framework ni paso de build |
| Datos y autenticación | Supabase (API REST de Postgres y Auth) mediante `@supabase/supabase-js` v2 desde jsDelivr |
| Hosting | GitHub Pages con dominio propio (`CNAME`) y `.nojekyll` |

## Estructura

```text
index.html               Landing principal
hola/ unete/ prueba/     Variantes de la landing, cada una con su formulario/
formulario/              Formulario de inscripción
encuesta/                Encuesta de investigación
backoffice/              Panel interno, docs/ (manuales) y medios.json (exportación de la lista de fuentes)
socios/                  Redirección a /backoffice/
CNAME                    Dominio holavera.news
```

## Ejecutar en local

No hay dependencias que instalar. Sirve la carpeta desde la raíz, porque las páginas usan rutas absolutas:

```bash
python3 -m http.server 8000
# abre http://localhost:8000
```

Ten en cuenta que el formulario y la encuesta escriben en el proyecto de Supabase configurado en cada página, no en un entorno de pruebas.

## Despliegue

GitHub Pages publica la rama `main` desde la raíz del repositorio, con HTTPS, en [holavera.news](https://holavera.news).

## Autor

Desarrollado por **Marcelo Garcés**, consultor de IA y desarrollo de producto digital. Diseño visual del equipo de Vera.
[LinkedIn](https://www.linkedin.com/in/marcelogarcesburgos) · [GitHub](https://github.com/MarceloG10)

## In English

Public website for Vera, a daily Spanish-language news newsletter with World, Chile and personalized sections, written each day by an AI agent (a Claude Code routine) from a whitelist of verified outlets. This repo holds the static front end: landing page, signup form, research survey and an internal backoffice behind Supabase magic-link auth. It is plain HTML, CSS and JavaScript using supabase-js, hosted on GitHub Pages at holavera.news. The generation pipeline lives in a separate private repository.

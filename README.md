# Vera

Sitio público de **Vera**, un newsletter diario de noticias en español.

🌐 [holavera.news](https://holavera.news)

---

## Cómo se publica este repo

Este repo **no se edita a mano**: lo genera el repo privado de Vera. Cada push a `main` que toque `pipeline/web/**`,
`pipeline/sources.json` o `pipeline/data/config.json` ejecuta el workflow `publicar-formulario.yml`, que corre
`python3 pipeline/web/publicar.py --out DIR` y sincroniza el resultado aquí con `rsync --delete` (commits de `vera-bot`,
«Actualiza formulario (GitHub Actions)»). Cualquier cambio hecho directamente aquí se pierde en la siguiente publicación;
corrígelo en el repo privado.

| Ruta | Origen en el repo privado |
|---|---|
| `/`, `/unete/`, `/hola/`, `/prueba/` | `pipeline/web/index.html` (la landing; las rutas alternativas existen porque WhatsApp cachea la vista previa por URL) |
| `/formulario/` y `/{unete,hola,prueba}/formulario/` | `pipeline/web/formulario.html` (copias idénticas con la URL y la anon key de Supabase inyectadas) |
| `/encuesta/` | `pipeline/web/encuesta.html` |
| `/backoffice/` (+ `docs/`, `medios.json`) | `pipeline/web/socios.html`, manuales y `pipeline/medios.json` |
| `/socios/` | redirección a `/backoffice/` |
| `README.md`, `.gitleaksignore` | `pipeline/web/sitio/` (se copian en cada publicación) |

## Seguridad

- La clave de Supabase que aparece en las páginas es la **anon** (pública por diseño). Lo que puede hacer está limitado
  por RLS en Supabase: el formulario y la encuesta solo pueden insertar. `.gitleaksignore` lista sus detecciones
  (falsos positivos) por huella.
- El backoffice exige un enlace mágico de un correo ya registrado (`shouldCreateUser: false`) **y** que ese correo esté
  en la tabla `socios`; la autorización real de lectura/escritura vive en las políticas RLS (`public.es_socio()`),
  no en este HTML.
- `supabase-js` se carga con versión exacta, `integrity` (SRI) y `crossorigin`. Al subir de versión hay que recalcular el
  hash (ver `pipeline/README.md` del repo privado).

---

Hecho por [Marcelo Garcés](https://www.linkedin.com/in/marcelogarcesburgos).

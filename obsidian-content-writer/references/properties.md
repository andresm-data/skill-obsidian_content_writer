# Propiedades estándar de los documentos de Obsidian

Todo documento lleva estas 11 propiedades en el frontmatter, en este orden. `title` siempre es la primera. Si una no aplica, se deja en blanco (sin borrar la línea). Todos los valores van en minúsculas e inglés, con las excepciones indicadas en la tabla.

## Tabla de propiedades

| Propiedad | Tipo de dato | Descripción | Valores permitidos |
|---|---|---|---|
| `title` | texto | Título del documento. Es el mismo texto del encabezado de nivel 1 del cuerpo. | Libre y obligatorio (nunca en blanco). Va en el idioma de la solicitud, con mayúsculas normales (excepción a minúsculas e inglés). Entre comillas dobles si contiene `:` o `#`. En templates: `"{{title}}"` (siempre entre comillas). |
| `type` | texto | Formato o naturaleza del documento. | `note`, `index`, `project`, `meeting`, `task`, `reference`, `course`, `log`, `decision`, `report`, `template`, `prompt` |
| `area` | texto | Contexto de vida o trabajo con el que se relaciona el documento. | `work`, `freelance`, `education`, `personal`, `productivity`, `health`, `finance`, `general` |
| `status` | texto | Estado del documento. Al crear o actualizar con esta skill siempre es `draft`. | `draft`, `active`, `review`, `archived` |
| `created` | fecha (`YYYY-MM-DD`) | Fecha de creación del documento. | Fecha real, o `{{date:YYYY-MM-DD}}` en templates. En blanco en actualizaciones. |
| `updated` | fecha (`YYYY-MM-DD`) | Fecha de la última modificación del documento. | Fecha real, o `{{date:YYYY-MM-DD}}` en templates. |
| `version` | número | Versión del documento. | `0.1` en documentos nuevos. `99` en actualizaciones (comodín que el usuario corrige). |
| `tags` | lista de texto | Temas transversales y libres para buscar. Describen de qué trata el documento, no qué es (eso lo indica `type`). | Libre. En minúsculas e inglés, sin espacios (usar guiones), sin `#`. Entre 2 y 6 etiquetas. |
| `related` | lista de enlaces | Notas hermanas o relevantes que no son jerárquicas. | Enlaces `"[[nombre de la nota]]"` entre comillas. Se conserva el nombre real de la nota (excepción a minúsculas e inglés). En blanco si no hay. |
| `project` | texto | Proyecto al que pertenece el documento. | Libre, en minúsculas e inglés (usar guiones). En blanco si no hay. |
| `source` | texto | Origen del contenido. | Ver lista de abajo. |

## Valores de `source`

| Valor | Cuándo usarlo |
|---|---|
| `ai` | El contenido lo generó Claude a partir de conocimiento general. |
| `personal` | Ideas, experiencias o reflexiones del propio usuario. |
| `website` | Página web o blog. |
| `article` | Artículo de prensa o revista. |
| `paper` | Artículo científico o académico. |
| `book` | Libro o ebook. |
| `video` | Video o conferencia grabada. |
| `podcast` | Podcast o audio. |
| `course` | Curso, clase o taller. |
| `documentation` | Documentación oficial o manual técnico. |
| `meeting` | Reunión o llamada. |
| `conversation` | Conversación informal o mensajería. |
| `email` | Correo electrónico. |
| `social-media` | Publicación de redes sociales. |
| `other` | Cualquier origen que no encaje en los anteriores. |

Regla para elegir: si el usuario indica el origen, se usa ese valor. Si el contenido son sus propias ideas, `personal`. Si lo genera Claude sin fuente externa, `ai`.

## Reglas de fecha y versión

| Situación | `created` | `updated` | `version` |
|---|---|---|---|
| Documento nuevo | fecha de hoy | fecha de hoy (igual a `created`) | `0.1` |
| Actualización de un documento existente | en blanco | fecha de hoy | `99` |
| Template nuevo | `{{date:YYYY-MM-DD}}` | `{{date:YYYY-MM-DD}}` | `0.1` |

Se considera actualización cuando el usuario habla de actualizar, modificar, revisar o mejorar un documento que ya existe, o entrega uno para cambiarlo.

## Variables del plugin de plantillas de Obsidian

Se usan solo cuando el documento es un template. Las reemplaza Obsidian al insertar la plantilla en una nota (requiere el plugin de plantillas activado).

| Variable | Qué inserta |
|---|---|
| `{{title}}` | El nombre de la nota donde se inserta la plantilla. |
| `{{date}}` | La fecha de hoy en el formato por defecto del plugin. |
| `{{date:YYYY-MM-DD}}` | La fecha de hoy en formato año-mes-día. |
| `{{time}}` | La hora actual en el formato por defecto del plugin. |
| `{{time:HH:mm}}` | La hora actual en formato 24 horas. |

## Formato YAML

- Las listas (`tags`, `related`) se escriben una por línea, con guion y sangría de dos espacios.
- Una propiedad en blanco se escribe con los dos puntos y nada más (por ejemplo `project:`).
- Los enlaces de `related` van entre comillas, porque YAML no acepta `[[` sin ellas.
- `title` es la primera línea del frontmatter. El mismo texto se repite como encabezado de nivel 1 al inicio del cuerpo.
- En templates, `title` se escribe `"{{title}}"` entre comillas, porque YAML no acepta `{{` sin ellas.

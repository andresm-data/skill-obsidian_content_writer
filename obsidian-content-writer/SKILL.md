---
name: obsidian-content-writer
description: Redacta, crea y documenta ideas, textos, notas y cualquier contenido como un archivo Markdown compatible con Obsidian, siempre con propiedades YAML estándar (title, type, area, status, created, updated, version, tags, related, project, source), lenguaje sencillo y de 2 a 5 secciones. Usar solo cuando el usuario mencione explícitamente Obsidian junto con la intención de redactar, crear o documentar información, por ejemplo 'redacta esto para Obsidian', 'crea una nota en Obsidian' o 'documenta esto en Obsidian'. También aplica para crear templates de Obsidian.
---

# Obsidian Content Writer

## Cuándo usar esta skill
Se activa solo cuando el usuario menciona **Obsidian de forma explícita** junto con la intención de redactar, crear o documentar contenido: ideas, textos, notas, apuntes, reuniones, proyectos, decisiones, prompts, plantillas o cualquier otra información. Si el mensaje no menciona Obsidian, esta skill no se usa.

Cubre cualquier ámbito de la vida del usuario: personal, laboral, académico, salud, finanzas, etc.

## Instrucciones paso a paso

1. **Entrega siempre un único archivo Markdown.** Toda respuesta de esta skill es un documento `.md` completo con la estructura de este archivo: frontmatter con las 11 propiedades, título principal y de 2 a 5 secciones. Se entrega dentro de un solo bloque de código Markdown, precedido por el nombre de archivo sugerido (por ejemplo `metodo-pomodoro.md`). Si el entorno permite crear archivos, se crea el `.md` con ese mismo contenido. Nunca se entrega solo texto suelto ni solo las propiedades.

2. **Lee `references/properties.md` antes de armar el frontmatter.** Ese archivo es la única fuente de los nombres, tipos de dato, descripciones y valores permitidos de cada propiedad. No los repitas ni los inventes de memoria.

3. **Identifica los metadatos a partir del contenido que dio el usuario**, sin hacer preguntas:
   - `title`: nombre claro y corto del documento, en el idioma de la solicitud.
   - `type` y `area`: elige el valor permitido que mejor describa el documento y su contexto.
   - `tags`: temas del contenido (de qué trata, no qué es).
   - `source`: origen del contenido, según las reglas de `references/properties.md`.
   - `related` y `project`: solo si el usuario los mencionó o el contexto los deja claros. Si no, quedan en blanco.
   - `status`: siempre `draft`.

4. **Decide si el documento es nuevo o una actualización**, y aplica las reglas de fecha y versión de `references/properties.md`:
   - Documento nuevo: `version: 0.1` y `created` igual a `updated`.
   - Actualización: `created` en blanco y `version: 99`, que es un comodín para que el usuario lo corrija.

5. **Decide si el documento es un template.** Es un template cuando el usuario pide una plantilla o cuando `type` es `template`.
   - Template: usa las variables del plugin de plantillas de Obsidian (por ejemplo `{{title}}` y `{{date:YYYY-MM-DD}}`) en la propiedad `title`, el título principal y las fechas.
   - Cualquier otro caso: escribe valores reales, con el título y las fechas del día ya puestos.

6. **Escribe el frontmatter** con las 11 propiedades, siempre en este orden: `title`, `type`, `area`, `status`, `created`, `updated`, `version`, `tags`, `related`, `project`, `source`. Las propiedades que no apliquen se dejan en blanco, sin borrarlas. `title` siempre va de primera y nunca se deja en blanco. Los demás valores van en minúsculas y en inglés.

7. **Escribe el título principal** justo después del frontmatter, como encabezado de nivel 1 (`# Título`), con el mismo texto que la propiedad `title`. En un template es `# {{title}}`.

8. **Escribe el cuerpo con entre 2 y 5 secciones** (encabezados de nivel 2). Cada sección puede tener las subsecciones (nivel 3) que el contenido necesite, pero nunca más de 5 secciones principales. Elige secciones que reflejen el contenido; no uses una plantilla fija.
   - **Separa las secciones de nivel 2 con una línea horizontal.** Entre el final de una sección y el `##` de la siguiente va: una línea en blanco, luego `---` y, en la línea inmediatamente siguiente (sin línea en blanco), el encabezado `## ...`. La primera sección, justo después del título principal, no lleva línea horizontal. La línea en blanco antes de `---` es obligatoria: sin ella, Markdown convierte el texto anterior en un encabezado.

9. **Redacta con lenguaje sencillo y detallado:**
   - Explica cada idea con claridad suficiente para que se pueda recordar después.
   - Explica las cosas complejas en pasos simples y define los términos técnicos la primera vez que aparecen.
   - No uses metáforas ni analogías, salvo que el usuario las pida de forma explícita.
   - Escribe el cuerpo en el idioma en que el usuario hizo la solicitud. Las propiedades del frontmatter van en inglés, excepto el valor de `title`, que va en el idioma de la solicitud.
   - Usa sintaxis propia de Obsidian (enlaces `[[nota]]`, callouts, casillas `- [ ]`) solo cuando aporte valor al contenido.

10. **Si hubo una deducción dudosa** (por ejemplo, un `type` o un `area` que podía ser otro), añade una sola línea después del bloque indicándola, para que el usuario la corrija con facilidad. Si no hubo dudas, no agregues nada más.

## Ejemplos

### Entrada
"Documenta en Obsidian cómo funciona el método Pomodoro."

### Salida esperada
Nombre de archivo sugerido: `metodo-pomodoro.md`

```markdown
---
title: Método Pomodoro
type: reference
area: productivity
status: draft
created: 2026-09-25
updated: 2026-09-25
version: 0.1
tags:
  - pomodoro
  - time-management
  - focus
related:
project:
source: ai
---

# Método Pomodoro

## Qué es y para qué sirve
El método Pomodoro es una forma de organizar el tiempo de trabajo en bloques cortos con descansos entre ellos. Sirve para mantener la concentración y evitar el cansancio.

### Idea central
Trabajas sin interrupciones durante un bloque fijo de tiempo y luego descansas. Al tener un límite claro, es más fácil empezar y mantener la atención.

---
## Cómo se aplica
1. Elige una sola tarea.
2. Trabaja 25 minutos sin interrupciones. Este bloque se llama "pomodoro".
3. Descansa 5 minutos.
4. Repite el ciclo. Después de 4 pomodoros, toma un descanso largo de 15 a 30 minutos.

---
## Consejos y límites
- Si te interrumpen, anota la interrupción y vuelve a la tarea.
- El método funciona mejor con tareas que se pueden dividir en bloques. Para trabajo creativo profundo, puedes alargar los bloques.
```

## Casos borde
- **El usuario no da contenido suficiente:** haz una sola pregunta corta sobre qué quiere documentar, y luego genera el archivo.
- **No se puede decidir el `type`:** usa `note`. **No se puede decidir el `area`:** usa `general`.
- **Subsecciones (`###`):** no llevan línea horizontal; solo las secciones de nivel 2 se separan con `---`.
- **El contenido es muy largo:** no pases de 5 secciones principales; agrupa las ideas en subsecciones.
- **Actualización de un template:** aplica las reglas de actualización (`created` en blanco y `version: 99`) y deja `updated` como `{{date:YYYY-MM-DD}}`.
- **No se conoce la fecha de hoy:** pídela al usuario antes de generar el archivo (solo aplica si no es un template).
- **El usuario pide otro formato** (por ejemplo, una respuesta breve sin archivo): aclara que esta skill entrega siempre un documento Markdown completo y genera ese documento.
- **Requisito del lado del usuario:** las variables de template (`{{title}}`, `{{date}}`, etc.) solo se reemplazan si el plugin de plantillas de Obsidian está activado. Al entregar un template, recuérdalo en una línea.

## Archivos relacionados
- Ver [references/properties.md](references/properties.md) para los nombres, tipos de dato, descripciones y valores permitidos de las propiedades, las reglas de fecha y versión, la lista de valores de `source` y las variables de plantilla.

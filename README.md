# Obsidian Content Writer

Skill para Claude que convierte ideas, textos, notas y plantillas en archivos Markdown listos para Obsidian. Cada documento incluye un frontmatter YAML con 11 propiedades estándar, un título principal y de 2 a 5 secciones redactadas en lenguaje sencillo. La skill se activa solo cuando mencionas Obsidian de forma explícita.

## Tabla de contenido

- [Descripción detallada](#descripción-detallada)
  - [Qué hace](#qué-hace)
  - [Propiedades del frontmatter](#propiedades-del-frontmatter)
  - [Reglas de redacción y estructura](#reglas-de-redacción-y-estructura)
  - [Documentos nuevos, actualizaciones y templates](#documentos-nuevos-actualizaciones-y-templates)
  - [Estructura del repositorio](#estructura-del-repositorio)
- [Uso](#uso)
  - [Instalación](#instalación)
  - [Cómo activarla](#cómo-activarla)
  - [Ejemplo](#ejemplo)
- [Licencia](#licencia)

## Descripción detallada

### Qué hace

La skill toma lo que le pides documentar (una idea, unos apuntes, una reunión, un proyecto, una decisión, un prompt o una plantilla) y entrega **un único archivo `.md`** con formato compatible con Obsidian. Sirve para cualquier ámbito: personal, laboral, académico, salud, finanzas, etc.

Deduce los metadatos a partir del contenido, sin hacer preguntas. Si alguna deducción es dudosa (por ejemplo, el `type` o el `area`), lo indica en una línea al final para que puedas corregirla.

### Propiedades del frontmatter

Todo documento lleva estas 11 propiedades, siempre en este orden. Las que no aplican se dejan en blanco, pero no se borran.

| Propiedad | Descripción |
|---|---|
| `title` | Título del documento, en el idioma de la solicitud. Nunca en blanco. |
| `type` | Naturaleza del documento: `note`, `index`, `project`, `meeting`, `task`, `reference`, `course`, `log`, `decision`, `report`, `template`, `prompt`. |
| `area` | Contexto: `work`, `freelance`, `education`, `personal`, `productivity`, `health`, `finance`, `general`. |
| `status` | Estado. Al crear o actualizar con la skill siempre es `draft`. |
| `created` | Fecha de creación (`YYYY-MM-DD`). |
| `updated` | Fecha de la última modificación (`YYYY-MM-DD`). |
| `version` | Versión del documento. |
| `tags` | De 2 a 6 temas, en minúsculas, inglés y con guiones. |
| `related` | Enlaces `"[[nota]]"` a notas relacionadas. |
| `project` | Proyecto al que pertenece el documento. |
| `source` | Origen del contenido (`ai`, `personal`, `book`, `video`, `meeting`, etc.). |

La referencia completa, con tipos de dato, valores permitidos y reglas de formato YAML, está en [`references/properties.md`](obsidian-content-writer/references/properties.md).

### Reglas de redacción y estructura

- Título principal (`#`) igual al valor de `title`, justo después del frontmatter.
- Entre 2 y 5 secciones de nivel 2 (`##`), con las subsecciones (`###`) que hagan falta.
- Las secciones de nivel 2 se separan con una línea horizontal (`---`), salvo la primera.
- Lenguaje sencillo y detallado: los temas complejos se explican en pasos y los términos técnicos se definen la primera vez que aparecen.
- Sin metáforas ni analogías, salvo que las pidas.
- El cuerpo va en el idioma de la solicitud; las propiedades, en inglés (excepto `title`).
- Usa sintaxis de Obsidian (enlaces `[[nota]]`, callouts, casillas `- [ ]`) solo cuando aporta valor.

### Documentos nuevos, actualizaciones y templates

| Situación | `created` | `updated` | `version` |
|---|---|---|---|
| Documento nuevo | fecha de hoy | fecha de hoy | `0.1` |
| Actualización | en blanco | fecha de hoy | `99` (comodín para que lo corrijas) |
| Template nuevo | `{{date:YYYY-MM-DD}}` | `{{date:YYYY-MM-DD}}` | `0.1` |

En los templates se usan variables del plugin de plantillas de Obsidian (`{{title}}`, `{{date:YYYY-MM-DD}}`, `{{time:HH:mm}}`). Solo se reemplazan si ese plugin está activado.

### Estructura del repositorio

```
obsidian-content-writer/
├── LICENSE
├── README.md
└── obsidian-content-writer/
    ├── SKILL.md                 # Instrucciones de la skill
    └── references/
        └── properties.md        # Propiedades, valores permitidos y reglas
```

## Uso

### Instalación

Copia la carpeta interna `obsidian-content-writer/` (la que contiene `SKILL.md`) en el directorio de skills de tu entorno:

- **Claude Code:** `~/.claude/skills/` (personal) o `.claude/skills/` dentro de un proyecto.
- **Claude.ai:** comprime la carpeta en un `.zip` y súbela desde la configuración de skills.

```bash
git clone https://github.com/andresm-data/skill-obsidian_content_writer.git
cp -r obsidian-content-writer/obsidian-content-writer ~/.claude/skills/
```

### Cómo activarla

Menciona **Obsidian** de forma explícita junto con la intención de redactar, crear o documentar. Por ejemplo:

- "Redacta esto para Obsidian: …"
- "Crea una nota en Obsidian sobre …"
- "Documenta en Obsidian la reunión de hoy: …"
- "Crea un template de Obsidian para reuniones semanales."
- "Actualiza esta nota de Obsidian: …"

Si el mensaje no menciona Obsidian, la skill no se activa.

### Ejemplo

**Entrada:**

> Documenta en Obsidian cómo funciona el método Pomodoro.

**Salida** (`metodo-pomodoro.md`, resumida):

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
El método Pomodoro es una forma de organizar el tiempo de trabajo en bloques cortos con descansos entre ellos.

---
## Cómo se aplica
1. Elige una sola tarea.
2. Trabaja 25 minutos sin interrupciones.
3. Descansa 5 minutos.
4. Repite el ciclo.
```

## Licencia

Distribuido bajo la licencia MIT. Consulta [LICENSE](LICENSE) para más detalles.

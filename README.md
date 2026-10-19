# Mis skills

Colección personal de skills para agentes de programación, escritas en castellano y organizadas según el [formato de Vercel Skills](https://github.com/vercel-labs/skills#creating-skills).

## Skills disponibles

| Skill | Descripción |
| --- | --- |
| [pau-workflow](skills/pau-workflow/SKILL.md) | Guiar el desarrollo, la validación y el flujo de ramas, commits y PRs, con aprobación del usuario antes del commit y publicación solo cuando se solicite. |

## Instalación

Una vez publicados los archivos en GitHub, puedes listar las skills:

```sh
npx skills add paucasanellas/skills --list
```

Instalar la skill de workflow en un proyecto:

```sh
npx skills add paucasanellas/skills --skill pau-workflow
```

Para instalarla de forma global, añade `-g` al comando anterior.

También puedes descubrir las skills desde este repositorio local, sin publicarlas:

```sh
npx skills add . --list
```

## Uso

Pídele a tu agente: «Usa pau-workflow para implementar este cambio». Por defecto, creará una rama antes de desarrollar y dejará el resultado listo para tu revisión, sin hacer commit hasta que apruebes el cambio realizado.

Las ramas usan tipos convencionales, como `feat/add-login`, y los commits siguen Conventional Commits en inglés, sin cuerpo descriptivo y con coautoría del modelo usado. El push, la creación de PRs y el merge requieren las instrucciones correspondientes del usuario. No se hace push a `main` salvo indicación explícita.

## Añadir otra skill

Usa [pau-skill-creator](.agents/skills/pau-skill-creator/SKILL.md) para crear o actualizar las skills de este repositorio.

Crea una carpeta `skills/pau-skill-name/` con un archivo `SKILL.md`. Todas las skills de este repositorio deben empezar por `pau-`, tanto en la carpeta como en el campo `name`. Usa el inglés para los nombres de skills y archivos, y el castellano para la descripción y las instrucciones. El idioma de los resultados que produce una skill depende de sus requisitos; por ejemplo, `pau-workflow` genera ramas y mensajes de commit en inglés. La cabecera YAML debe incluir `name` y `description`. Añade la skill también a la tabla de skills disponibles.

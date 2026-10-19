---
name: pau-skill-creator
description: >-
  Es una skill para crear y actualizar skills de este repositorio.
  Sigue buenas prácticas recomendadas por Vercel Skills.
  Úsala cuando se solicite crear una skill o modificar sus instrucciones, estructura o recursos.
---

# Crear y mantener skills

Convierte la petición del usuario en instrucciones reutilizables, concretas y suficientes para que otro agente complete la tarea, siguiendo las [buenas prácticas de Vercel Skills](https://github.com/vercel-labs/skills#creating-skills).

## Alcance

Crea y actualiza las skills de este repositorio. Limita cada skill a su propósito y conserva el comportamiento que no afecte a la petición.

La skill no debe atribuir autorización para publicar, enviar mensajes, hacer push o modificar sistemas externos por el mero hecho de estar activada. Si el usuario ya ha autorizado una acción, no impongas confirmaciones redundantes.

## Cómo actuar

1. Revisa las instrucciones del repositorio y las skills existentes para respetar sus convenciones y evitar duplicados.
2. Identifica la tarea, cuándo debe activarse la skill y el resultado esperado. Si falta un dato imprescindible, pregunta por él; resuelve las decisiones rutinarias con el contexto disponible.
3. Elige un nombre en inglés con el prefijo `pau-` y redacta una descripción en castellano que explique la capacidad y cuándo usarla. Mantén en el cuerpo las convenciones de idioma y los detalles de funcionamiento.
4. Puedes usar la estructura de esta misma skill como plantilla para crear nuevas skills. Adapta su contenido a la tarea, sin copiar instrucciones que solo correspondan a la creación de skills.
5. Redacta los apartados de la estructura común indicada abajo. Incluye criterios de decisión, restricciones reales y comprobación del resultado. Añade ejemplos solo si aclaran una elección relevante; evita explicaciones generales que el agente ya conoce y herramientas que no necesite.
6. Cuando cambies una ruta o el nombre de una skill, actualiza sus enlaces, ejemplos y comandos de instalación. Si pertenece a la colección de `skills/`, actualiza su entrada en el `README.md` de la raíz.

### Idioma y nombres

- Escribe en inglés el nombre de la skill, su carpeta y los nombres de todos sus archivos. Conserva nombres de formato como `SKILL.md`, `README.md` y `openai.yaml`.
- Todas las skills de este repositorio deben empezar por `pau-`, tanto en el campo `name` como en su carpeta.
- Usa un identificador breve en minúsculas, con palabras separadas por guiones, de hasta 64 caracteres. El campo `name` debe coincidir con el nombre de la carpeta.
- Escribe en castellano la descripción, los títulos, las instrucciones, los comentarios y el texto explicativo de los ejemplos. El idioma de los resultados y de los ejemplos de salida depende de los requisitos de cada skill; por ejemplo, `pau-workflow` genera ramas y mensajes de commit en inglés.
- Conserva las claves de formatos, comandos, API e identificadores técnicos en su idioma original. Por ejemplo, usa `name` y `description` como claves YAML, con la descripción en castellano.

### Ubicación y recursos

Respeta la ubicación solicitada por el usuario. Por defecto, guarda las skills de la colección en `skills/pau-skill-name/SKILL.md`. Esta skill de creación se mantiene en `.agents/skills/pau-skill-creator/SKILL.md`.

Añade `scripts/`, `references/` o `assets/` solo cuando aporten una utilidad concreta. Usa nombres de archivo en inglés y enlaza los recursos desde `SKILL.md`, indicando cuándo consultarlos. Mantén las instrucciones breves en el archivo principal y evita duplicarlas en otros documentos.

### Estructura común de las skills

Todas las skills deben incluir los siguientes elementos, en este orden. Esta es una convención de este repositorio:

1. **Cabecera YAML:** `name` y `description`. La descripción explica la capacidad y cuándo usarla.
2. **Título y propósito:** un título de nivel 1 y una explicación breve del resultado esperado.
3. **Alcance:** qué tareas cubre la skill, sus límites y las restricciones relevantes.
4. **Cómo actuar:** instrucciones para realizar la tarea, criterios de decisión y recursos necesarios.
5. **Cómo validar:** comprobaciones que permitan verificar el resultado y cómo proceder si fallan.
6. **Entrega:** qué resultado debe recibir el usuario y qué limitaciones o asuntos pendientes se deben comunicar.

Usa exactamente `## Alcance`, `## Cómo actuar`, `## Cómo validar` y `## Entrega` como apartados principales. Añade subapartados dentro de ellos cuando la tarea lo necesite. Mantén cada apartado conciso y adaptado a la skill.

Por ejemplo:

```markdown
---
name: pau-review-code
description: Revisa cambios de código para detectar errores y regresiones. Úsala cuando el usuario solicite revisar un diff o una propuesta de cambios.
---

# Revisar código

Detecta problemas concretos en los cambios solicitados y explica su efecto.

## Alcance

Revisa el diff solicitado y el contexto necesario para entenderlo.

## Cómo actuar

Inspecciona los cambios y comprueba las rutas de ejecución afectadas. Prioriza errores demostrables y regresiones.

## Cómo validar

Contrasta cada hallazgo con el código y las pruebas pertinentes. Si no puedes verificarlo, comunica la incertidumbre.

## Entrega

Presenta los hallazgos con su ubicación, efecto y prioridad. Si no encuentras problemas, indícalo y menciona las limitaciones de la revisión.
```

## Cómo validar

- Comprueba que la cabecera YAML se puede leer y contiene un `name` válido y una `description` no vacía.
- Verifica que la carpeta coincide con `name`, ambos empiezan por `pau-`, los nombres están en inglés y el contenido explicativo está en castellano. Comprueba también que el idioma de los resultados coincide con los requisitos de la skill.
- Comprueba que la skill sigue la estructura común, con los cuatro apartados principales en el orden indicado.
- Revisa los enlaces relativos, elimina marcadores pendientes y comprueba que las instrucciones se pueden seguir sin recursos inexistentes.
- Si has añadido scripts, verifica su comportamiento con un caso representativo y sin afectar datos reales. Para una skill de instrucciones sencilla, basta revisar su estructura y coherencia.
- Si hay un validador disponible, ejecútalo. Corrige los errores detectados y repite las comprobaciones afectadas antes de dar la skill por validada. Si no puedes completar alguna comprobación, indica la limitación.

## Entrega

Entrega la ubicación de la skill y un resumen breve de lo creado o corregido y de las comprobaciones realizadas. Comunica las limitaciones o los asuntos pendientes que afecten al resultado.

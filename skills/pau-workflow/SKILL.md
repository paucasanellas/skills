---
name: pau-workflow
description: Guía el desarrollo de cambios, su validación y el flujo de Git y GitHub. Úsala al implementar funcionalidades, corregir errores, modificar un proyecto o gestionar ramas, commits, pull requests y su integración.
---

# Seguir el flujo de desarrollo

Lleva cada cambio desde su preparación hasta el punto de entrega solicitado, preservando el trabajo existente y respetando la aprobación del usuario. Esta skill contiene el flujo completo y las reglas de commits; no depende de otra skill para ejecutarlos.

## Alcance

Aplica al desarrollo y mantenimiento de proyectos, incluidos código, documentación y configuración. Las instrucciones y la comunicación con el usuario están en castellano; los nombres de ramas y los mensajes de commit, en inglés.

### Acciones y autorización

| Acción | Regla |
| --- | --- |
| Crear una rama | Crea una nueva antes de empezar cualquier desarrollo, salvo que el usuario indique lo contrario. |
| Implementar y validar | Continúa dentro de la tarea solicitada hasta dejar un cambio concreto y revisable. |
| Crear un commit | Solo después de que el usuario apruebe explícitamente el cambio realizado. |
| Subir cambios a GitHub | Solo cuando el usuario lo indique. La aprobación del cambio o del commit no autoriza un push. |
| Crear una PR | Solo cuando el usuario lo indique. Un push autorizado no autoriza por sí solo una PR. |
| Hacer push a `main` | Prohibido por defecto; requiere una indicación explícita del usuario para esa rama. Aplica también a la rama predeterminada si tiene otro nombre. |
| Mergear una PR | Solo por indicación explícita del usuario y cumpliendo los requisitos del repositorio. Crear una PR no autoriza su merge. |
| Gestionar GitHub Projects | Solo si se ha solicitado el seguimiento en un proyecto; usa sus campos y estados reales. |

Una petición inicial de desarrollo, incluso si menciona un commit futuro, no sustituye la aprobación del cambio ya realizado. Presenta primero el resultado revisable. Si el usuario ya lo ha revisado y aprobado, aprovecha esa aprobación sin volver a pedirla; una petición de commit sobre cambios ya presentados cuenta como aprobación de esos cambios. Si después se modifica sustancialmente el resultado aprobado, presenta la nueva versión antes de hacer commit.

La aprobación habilita el commit cuando forme parte de lo solicitado; no obliga a crearlo si el usuario solo pide revisar o preparar. El silencio, el paso del tiempo y las pruebas superadas no son aprobación.

No descartes cambios ni reescribas historial con `reset --hard`, `clean`, `commit --amend`, rebase o push forzado sin una petición explícita. No cambies la identidad de Git para resolver bloqueos.

## Cómo actuar

### Entender y preparar

1. Lee las instrucciones del repositorio e identifica el objetivo, las restricciones y los criterios de finalización. Revisa los patrones existentes antes de proponer cambios.
2. Comprueba el repositorio, la rama actual, los remotos y el estado con `git status --short --branch`, `git diff` y `git diff --cached`. Revisa los archivos nuevos relevantes, que no aparecen en esos diffs. Consulta el historial si existe; un repositorio sin commits es válido.
3. Distingue los cambios de la tarea de los trabajos previos. No descartes, prepares ni incluyas cambios no relacionados. Si falta un dato imprescindible o hay conflictos que impiden trabajar con seguridad, explica el bloqueo y pide únicamente lo necesario.
4. Antes de editar archivos de desarrollo, crea una nueva rama desde la base adecuada para la tarea. Usa la base indicada por el usuario o la definida por el proyecto; en otro caso, identifica la rama predeterminada sin asumir que se llama `main`. Evita heredar cambios de otra rama de trabajo por accidente.
5. Conserva los cambios locales existentes al crear la rama. No hagas stash, reset ni un commit provisional para cambiar de base sin autorización. Si la base y el trabajo local son incompatibles, usa un entorno de trabajo separado cuando sea apropiado o aclara cómo continuar antes de alterar ese trabajo.

Si el usuario pide expresamente continuar en una rama existente o trabajar en la actual, respeta esa excepción. Las revisiones de solo lectura y la redacción aislada de mensajes no necesitan una rama nueva. Continúa las correcciones de una misma entrega en la rama creada para ella; una nueva tarea de desarrollo requiere una nueva rama por defecto.

### Nombrar ramas y commits

Usa los tipos de [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/): `feat` para funcionalidades, `fix` para errores y, según corresponda, `docs`, `refactor`, `test`, `chore`, `build`, `ci`, `perf`, `style` o `revert`.

Conventional Commits define mensajes, no nombres de ramas. Para las ramas, adapta la misma clasificación al formato `type/short-description` o `type/scope/short-description`. Usa palabras en inglés, en minúsculas y separadas por guiones. No copies los dos puntos ni los espacios del mensaje, que no son válidos en una referencia de Git.

```text
feat/add-google-sign-in
fix/api/reject-empty-email
docs/update-installation-guide
```

Verifica el nombre con `git check-ref-format --branch` y comprueba que no existe antes de crear la rama. Si existe, elige otro nombre descriptivo sin sobrescribirla.

### Implementar y presentar el cambio

1. Implementa el cambio siguiendo los patrones del proyecto. Ajusta las pruebas y la documentación cuando la tarea lo requiera, sin ampliar el alcance con refactorizaciones ajenas.
2. Ejecuta las comprobaciones pertinentes, revisa el diff y corrige los problemas dentro del alcance. Comunica los fallos que no puedas resolver.
3. Presenta qué ha cambiado, dónde revisarlo, las comprobaciones realizadas y las limitaciones relevantes. Deja los cambios sin commit hasta que el usuario los apruebe. No prepares archivos en el índice por defecto; hazlo si el usuario pide preparar un commit o ya ha autorizado su creación tras aprobar el cambio.
4. Cuando falte aprobación para un commit solicitado, pide la aprobación sobre el resultado concreto. No avances a commit, push, PR ni merge mientras falte la autorización correspondiente.

### Preparar y crear commits después de la aprobación

- Si solo se pide un mensaje, entrega el texto sin modificar archivos, índice ni historial. Si se pide preparar el commit, prepara los cambios pertinentes y propón el mensaje sin crearlo.
- Revisa `git diff --cached` y los cambios pendientes para seleccionar exactamente lo aprobado. Si hay cambios ya preparados ajenos al alcance, acláralo antes de alterar el índice o incluirlos en el commit.
- Usa `git add -- path/to/file` con rutas explícitas. Si un archivo mezcla trabajos distintos, prepara únicamente los fragmentos pertinentes; no vuelvas a añadir el archivo completo incorporando cambios excluidos.
- No añadas secretos, configuración local ni artefactos generados por accidente. Si detectas un secreto ya preparado, detén el commit e informa sin reproducirlo ni alterar cambios preparados ajenos.
- Si hay conflictos sin resolver o no hay cambios relevantes, no crees un commit. No crees commits vacíos para avanzar el flujo.

El mensaje debe usar siempre Conventional Commits en inglés, con este formato:

```text
type(scope): short summary in English

Co-authored-by: MODEL_NAME <ATTRIBUTION_EMAIL>
```

- El ámbito es opcional y debe estar en inglés. Respeta los tipos y ámbitos del repositorio que sean compatibles con estas reglas.
- Escribe el resumen en imperativo, como `add`, `fix`, `remove` o `simplify`; procura no superar 72 caracteres y no añadas punto final.
- No añadas cuerpo descriptivo, explicaciones, listas de cambios ni resultados de pruebas. El resumen del asunto es obligatorio; «sin descripción» significa sin descripción adicional debajo del asunto. El único pie requerido es la coautoría.
- Marca incompatibilidades con `!` antes de los dos puntos, por ejemplo `feat(api)!: remove legacy endpoint`. Explica la migración al usuario o en la PR, fuera del mensaje del commit.

Obtén el nombre y la versión del modelo del contexto de ejecución o la configuración explícita de la sesión. Usa el modelo que realizó el trabajo, sin confundirlo con la aplicación o el agente. Para el correo de atribución, usa las instrucciones del proyecto, la configuración de la sesión o documentación oficial del proveedor; no inventes versiones, correos ni asociaciones con cuentas de GitHub. Si falta un dato que no puedas verificar, pide solo ese dato antes del commit; en un borrador, señala que la atribución está pendiente.

Sigue el [formato de coautoría de GitHub](https://docs.github.com/en/pull-requests/how-tos/commit-changes/creating-a-commit-with-multiple-authors). Sustituye los marcadores del ejemplo por datos verificados. Mantén al usuario como autor principal según su configuración de Git, sin usar `--author` ni modificar `user.name` o `user.email` para atribuir el modelo.

Tras la aprobación y las comprobaciones previas, ejecuta `git commit` con el mensaje completo como texto literal, sin interpolación de comandos; puedes usar un archivo temporal fuera del repositorio y `git commit -F`.

Si un hook falla, revisa su salida y los cambios que haya generado. Corrige solo lo pertinente, vuelve a seleccionar los fragmentos y repite las comprobaciones afectadas. Si la corrección altera sustancialmente el cambio aprobado, preséntala de nuevo. No omitas hooks ni uses `--no-verify` para forzar el commit.

### Publicar, revisar e integrar cuando se solicite

1. Para un push autorizado, comprueba el remoto y la rama de destino. Publica únicamente la rama de trabajo; evita `git push --all`, `--mirror` y cualquier operación que pueda actualizar `main` o ramas no solicitadas. Si falta la aprobación previa del cambio, consíguela antes de crear el commit necesario para publicarlo.
2. Para una PR solicitada, busca primero una PR existente de esa rama y tarea. Actualízala cuando corresponda; no crees duplicados. Pedir crear una PR autoriza el push necesario de su rama de trabajo, siempre después de la aprobación del cambio; no autoriza publicar en `main` ni mergear.
3. Comprueba la base y el diff de la PR. Incluye un título claro y una descripción del problema, la solución y la validación, siguiendo la plantilla del proyecto. La regla de no añadir cuerpo descriptivo se aplica al mensaje de commit; la PR debe aportar contexto suficiente para revisarlo. Enlaza una issue cuando corresponda, sin crearla por defecto.
4. Si se solicita gestionar GitHub Projects, identifica el proyecto y sus campos reales. Reutiliza los elementos existentes, vincula la issue o PR y actualiza solo los estados y campos pertinentes. No crees proyectos, columnas ni campos por suposición. No marques la tarea como terminada mientras falte el resultado que el proyecto considere necesario.
5. Atiende los comentarios dentro del alcance. Presenta cualquier cambio nuevo al usuario y espera su aprobación antes de hacer otro commit; una revisión externa o CI en verde no sustituyen esa aprobación. Publica nuevas versiones solo dentro de la autorización vigente.
6. Para un merge solicitado, comprueba la PR, su rama base, el último commit, CI, revisiones requeridas y ausencia de conflictos. Respeta las protecciones y la estrategia de merge del repositorio; no fuerces la integración. Verifica que el mensaje resultante, incluido el de squash si se usa, conserve Conventional Commits en inglés, sin cuerpo descriptivo y con coautoría del modelo.
7. Confirma el resultado real de la operación. Un merge mediante PR autorizado no equivale a hacer push directo a `main`. No borres ramas ni despliegues por defecto; hazlo cuando el usuario lo solicite o forme parte de un procedimiento del proyecto ya autorizado.

Si no hay acceso a GitHub o faltan permisos, conserva el trabajo local y comunica el bloqueo. No cambies de remoto, omitas protecciones ni sustituyas una PR por un push a `main` para sortearlo.

## Cómo validar

### Antes de presentar el desarrollo

- Comprueba que se creó la rama antes de editar, o que existe una excepción indicada por el usuario. Revisa el nombre y la base.
- Revisa todos los cambios relevantes, incluidos archivos nuevos, y comprueba que el trabajo previo no se ha alterado por accidente. Usa `git diff --check` para detectar problemas de espacios y marcadores de conflicto en el diff no preparado.
- Ejecuta las comprobaciones exigidas por el proyecto y las pruebas proporcionales al cambio. Si las pruebas usan cambios ajenos presentes en el árbol de trabajo, indica que no validan de forma aislada la entrega.
- Si falla una comprobación, corrige lo que corresponda y repítela. Si no puedes resolver el fallo, comunica la limitación sin presentar el resultado como validado.

### Antes y después de cada transición

- **Commit:** confirma la aprobación del cambio realizado, revisa `git diff --cached`, `git diff --cached --stat` y `git diff --cached --check`, y valida el mensaje y su coautoría. Tras crearlo, comprueba `git log -1 --format='%h%n%B'`, `git show --stat --oneline HEAD` y `git status --short`. No confundas un commit anterior con uno nuevo si el comando falla.
- **Push:** confirma que el usuario lo ha solicitado, que destino y rama son correctos y que no se está actualizando `main` sin indicación explícita. Verifica que el remoto contiene el commit esperado.
- **PR:** confirma que se solicitó, que la base y el diff son correctos y que existe la PR esperada, conservando su enlace y estado real.
- **Merge:** confirma la instrucción del usuario y que las comprobaciones corresponden al último commit de la PR. Tras ejecutarlo, verifica que la PR aparece integrada en la base esperada. Activar auto-merge o entrar en una cola no equivale a estar mergeada.
- **Solo desarrollo, mensaje o preparación:** verifica que no se han creado commits, hecho push ni abierto PRs fuera del alcance. Un árbol limpio no es obligatorio si había cambios pendientes ajenos.

## Entrega

Comunica el punto alcanzado: cambio local listo para revisar, commit creado, rama publicada, PR abierta o merge confirmado. Incluye un resumen breve del resultado, la rama, las comprobaciones y las limitaciones relevantes.

Entrega el hash y asunto si hay commit, y los enlaces si hay PR o seguimiento solicitado en Projects. Distingue las comprobaciones superadas, fallidas y no ejecutadas. Si falta aprobación, deja el cambio revisable y pide aprobar ese resultado antes del commit; si falta otra instrucción, indica qué acción queda pendiente sin asumirla.

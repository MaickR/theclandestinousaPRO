# Instrucciones para agentes

Estas reglas aplican al trabajo en este repositorio. Para decisiones específicas, consulta [`docs/git-workflow.md`](docs/git-workflow.md), la documentación de arquitectura disponible y, cuando exista, [`DESIGN.md`](DESIGN.md).

## Forma de trabajar

- Antes de cambiar código, inspecciona el comportamiento y las fuentes de verdad pertinentes.
- Para cambios no triviales, comunica alcance, plan y verificaciones previstas antes de editar.
- Aplica `INSPECT → PLAN → MODIFY → VERIFY`. Cada cambio debe tener un objetivo y un criterio de finalización comprobable.
- Haz cambios acotados. Evita refactors ajenos al objetivo, abstracciones especulativas, capas vacías y dependencias sin necesidad demostrada.
- Si falta un requisito que pueda cambiar materialmente la solución, detente y solicita una decisión; no lo inventes.
- Conserva los cambios preexistentes del usuario. No sobrescribas ni elimines archivos sin necesidad confirmada.

## Arquitectura del proyecto

- El backend es Laravel; React se integra mediante Inertia en el mismo monolito.
- Laravel es responsable de rutas, autorización, validación, persistencia y lógica de negocio. React/Inertia es responsable de páginas, presentación e interacción de interfaz.
- Mantén TypeScript en modo estricto y MySQL como base objetivo.
- Usa Tailwind CSS para estilos. Los primitives locales de shadcn/ui están en `resources/js/components/ui/` y son código editable del proyecto.
- No introduzcas una SPA separada, una API REST paralela, microservicios, Bootstrap, SCSS 7-1 ni otro framework CSS sin una decisión explícita.
- No crees carpetas, módulos o componentes hipotéticos. Si una necesidad de marca se repite y justifica componentes propios, pueden ubicarse en `resources/js/components/marca/`.
- Mantén las páginas enfocadas en composición. Evita trasladarles reglas de negocio o lógica compleja que corresponde al backend.
- Sigue las convenciones de Laravel, React, Inertia y las herramientas generadoras cuando sean necesarias. No renombres código existente ni generado solo para uniformar el idioma.

## Código e idioma

- El código nuevo y la documentación técnica propia se escriben en español cuando la convención obligatoria del framework o herramienta no indique otra cosa.
- Mantén la interfaz visible al cliente en inglés por defecto. El contenido en otros idiomas se añade cuando el alcance lo requiera.
- Usa tipos explícitos donde aporten claridad y evita `any` salvo justificación técnica concreta.
- Valida y autoriza en el servidor toda operación sensible. Trata los datos del cliente como no confiables y minimiza la exposición de datos personales.
- No hardcodees ni publiques secretos. Los valores locales pertenecen a `.env`; no incluyas ese archivo en Git.

## Comentarios

- Comenta decisiones, restricciones y razones que no sean evidentes; no narres el código.
- Usa `!` para advertencias críticas, `?` para dudas explícitas y `TODO` solo para trabajo concreto y verificable.
- No uses comentarios como sustituto de documentación ni añadas TODO vagos.

## Verificación

- Ejecuta verificaciones proporcionales al cambio y reporta con precisión lo que pasó o falló.
- Backend: `php artisan test`, `composer types:check` y `composer lint:check` cuando sean pertinentes.
- Frontend: `pnpm types:check`, `pnpm check` y `pnpm build` cuando sean pertinentes. Usa `pnpm build:ssr` para cambios que afecten SSR.
- Usa PHPUnit para pruebas backend. No cambies la configuración de pruebas solo para hacer pasar una ejecución.
- Las pruebas usan MySQL `clandestino_testing`; nunca ejecutes pruebas contra la base local `clandestino`.
- No declares terminado un cambio solo porque compila; verifica el comportamiento afectado.

## Git y autorización

- Sigue [`docs/git-workflow.md`](docs/git-workflow.md) para ramas, integración y commits.
- No trabajes directamente sobre `main`. Usa ramas de trabajo según el propósito del cambio.
- Escribe mensajes Conventional Commits en español, breves y específicos, con un máximo aproximado de 72 caracteres.
- No hagas commit, push, merge o deploy sin autorización explícita para esa acción.
- No instales ni actualices dependencias, cambies tooling, ejecutes operaciones destructivas o alteres producción sin autorización explícita.
- No implementes trabajo fuera del alcance solicitado.

## Fuentes de verdad

- Este archivo define las reglas permanentes para agentes.
- `docs/git-workflow.md` define el flujo Git.
- `DESIGN.md`, cuando exista, definirá el sistema visual.
- La documentación de `docs/` registra arquitectura, decisiones y especificaciones existentes.
- El código define la implementación actual; los tests describen el comportamiento comprobable y CI ejecuta sus verificaciones.
- Las instrucciones de skills futuras no pueden contradecir estas reglas ni las fuentes específicas anteriores.

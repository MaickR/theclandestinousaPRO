# Workflow de Git

## Ramas base

- `main`: código estable y potencialmente desplegable.
- `develop`: integración del trabajo terminado antes de publicarlo.

Las ramas base no contienen funcionalidades de negocio por adelantado. Las ramas de trabajo se crean cuando existe una tarea concreta.

## Ramas de trabajo

Usar el prefijo que corresponda al propósito:

- `feature/<nombre>`: funcionalidad nueva.
- `fix/<nombre>`: corrección normal.
- `hotfix/<nombre>`: corrección urgente de producción.
- `refactor/<nombre>`: cambio estructural sin modificar el comportamiento intencional.
- `chore/<nombre>`: tooling, CI o mantenimiento.

Las subramas solo se crean cuando existe una razón real. Una subrama nace de su rama padre y vuelve a ella.

## Flujo de integración

```text
feature/*, fix/*, refactor/*, chore/* -> develop -> main
```

No integrar ramas de trabajo directamente en `main` salvo aprobación explícita para una situación excepcional.

Antes de integrar una rama deben pasar los tests, PHPStan, Pint, TypeScript, los checks frontend y los builds aplicables. La revisión del diff y la confirmación humana son obligatorias.

## Commits

Usar Conventional Commits en español:

```text
tipo(ámbito): descripción breve
```

Tipos permitidos: `feat`, `fix`, `refactor`, `docs`, `test`, `chore`, `build`, `ci`, `perf` y `style`.

Los commits deben ser pequeños, atómicos y describir un único propósito. No mezclar funcionalidades con limpieza, documentación o infraestructura si pueden separarse razonablemente.

## Producción

`main` representa el estado estable. No hacer push, merge o despliegue automático sin revisión y aprobación humana.

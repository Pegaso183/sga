# 0001 · Repositorio y flujo de trabajo

- **Fecha:** 2026-11-23
- **Estado:** Aceptada

## Contexto
El proyecto necesita control de versiones, copia de seguridad del código y trazabilidad de cambios,
y Claude participa en el desarrollo.

## Decisión
- Repositorio privado en GitHub: `Pegaso183/sga`, rama principal `main`.
- La app de Claude tiene acceso únicamente a este repositorio.
- La especificación se mantiene en `docs/` dentro del propio repositorio.
- Cambios mediante ramas y *pull requests*; tareas como Issues.

## Consecuencias
- Historial completo y posibilidad de volver atrás.
- El repositorio es autocontenido: código y especificación juntos.

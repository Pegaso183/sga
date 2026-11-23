# 0001 · Repositorio y flujo de trabajo

- **Fecha:** 2026-11-23
- **Estado:** Aceptada

## Contexto
El proyecto necesita control de versiones, copia de seguridad del código y trazabilidad de cambios,
y Claude participa en el desarrollo.

## Decisión
- Repositorio **público** en GitHub: `Pegaso183/sga`, rama principal `main` (público para poder proteger `main` con el plan Free).
- `main` protegida: solo se modifica mediante *pull request*, sin excepciones (tampoco administradores), sin *force push* ni borrado, y con las conversaciones resueltas antes de fusionar.
- La app de Claude tiene acceso únicamente a este repositorio.
- La especificación se mantiene en `docs/` dentro del propio repositorio.
- Cambios mediante ramas y *pull requests*; tareas como Issues, clasificadas con etiquetas `tipo:`, `prioridad:` y `módulo:`.

## Consecuencias
- Historial completo y posibilidad de volver atrás.
- El repositorio es autocontenido: código y especificación juntos.
- Al ser público, **nunca** debe contener secretos ni datos reales de clientes, proveedores o precios.

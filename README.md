# SGA · Sistema de Gestión de Almacén

Sistema de Gestión de Almacén (WMS) desarrollado a medida para un almacén de distribución B2B.

## Contexto

| Aspecto | Valor |
|---|---|
| Tipo de almacén | Distribución, logística B2B |
| Número de almacenes | 1 |
| Referencias | ~4.000 |
| Operarios | ~20 |
| Trazabilidad | Por número de serie (sin control de caducidades) |
| Conectividad | Buena cobertura wifi en todo el almacén |

## Estado

🟡 **Fase 1 – Definición** (alcance, requisitos y modelo de datos).
Detalle en [`docs/05-estado-y-roadmap.md`](docs/05-estado-y-roadmap.md).

## Estructura del repositorio

```
sga/
├── README.md            ← este archivo
├── CLAUDE.md            ← instrucciones para Claude (convenciones y forma de trabajo)
├── docs/                ← especificación funcional y técnica (fuente de verdad)
│   ├── 00-vision-y-alcance.md
│   ├── 01-requisitos-funcionales.md
│   ├── 02-modelo-de-datos.md
│   ├── 03-decisiones/   ← registro de decisiones (ADR), una por archivo
│   ├── 04-glosario.md
│   └── 05-estado-y-roadmap.md
└── src/                 ← código fuente (cuando se elija la tecnología)
```

## Forma de trabajo

- `main` contiene siempre una versión estable.
- Cada cambio se hace en una rama (`feature/…`, `fix/…`, `docs/…`) y entra en `main` mediante *pull request*.
- Las tareas y errores se registran como **Issues** en GitHub.
- Toda decisión relevante se documenta en `docs/03-decisiones/`.

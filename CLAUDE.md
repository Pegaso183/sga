# Instrucciones para Claude · Proyecto SGA

## Proyecto
WMS a medida para un único almacén de distribución B2B: ~4.000 referencias, ~20 operarios,
trazabilidad por número de serie, sin caducidades, buena cobertura wifi.
Responsable funcional: Jairo Martín Miguel (GitHub: Pegaso183).

## Idioma
- Documentación, Issues, *pull requests* y mensajes de *commit*: **español**.
- Código (nombres de variables, funciones, tablas): pendiente de decidir en un ADR.

## Fuente de verdad
- La especificación vive en `docs/`. Léela antes de proponer o programar cambios.
- Empieza siempre por `docs/05-estado-y-roadmap.md`.
- No des por cerrado un requisito sin confirmarlo con el responsable funcional; ante ambigüedad, pregunta.

## Flujo de trabajo
- No hagas *commit* directo a `main` salvo en la configuración inicial del repositorio.
- Ramas: `feature/<tema>`, `fix/<tema>`, `docs/<tema>`.
- Mensajes de *commit* cortos, en imperativo y en español (p. ej. "Añade entidad Ubicación al modelo de datos").
- Cada funcionalidad debe tener criterios de aceptación y pruebas.
- Las decisiones técnicas o funcionales relevantes se registran como ADR en `docs/03-decisiones/`
  (`NNNN-titulo-corto.md`, a partir de `0000-plantilla.md`).
- Al cerrar una sesión de trabajo, actualiza `docs/05-estado-y-roadmap.md`.

## Seguridad
- Nunca subas secretos (contraseñas, claves de API, cadenas de conexión). Usa variables de entorno y `.env` (ignorado por git).
- Nunca subas datos reales de clientes; usa datos de prueba o anonimizados.

## Tecnología
Pendiente de decidir (ver roadmap). Cuando se decida, documentar aquí: lenguaje, framework,
base de datos, cómo ejecutar el proyecto en local y cómo lanzar las pruebas.

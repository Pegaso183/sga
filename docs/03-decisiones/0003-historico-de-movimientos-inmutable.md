# 0003 · Histórico de movimientos inmutable

- **Fecha:** 2026-11-23
- **Estado:** Aceptada (provisional, versión preliminar de pruebas)

## Contexto
Hay que saber quién hizo cada operación, cuándo y sobre qué unidad. Esto sirve para resolver incidencias, analizar
diferencias de inventario y dar trazabilidad completa al cliente.

## Opciones consideradas
1. Guardar solo el estado actual de cada unidad (sin histórico).
2. Guardar un histórico que se puede corregir editando registros.
3. Guardar un histórico **solo de alta**: cada operación añade un movimiento y nunca se modifica ni se borra.

## Decisión
Opción 3. Cada cambio de ubicación, contenedor, situación o estado de una unidad genera un **Movimiento** con
usuario, fecha y hora, tipo, origen, destino y documento relacionado. Los ajustes y cambios de estado exigen un motivo.
Los errores se corrigen con un movimiento nuevo, nunca editando el anterior.

## Consecuencias
- Auditoría completa y fiable.
- El estado actual de la unidad y el último movimiento deben actualizarse siempre juntos, en la misma transacción.
- La base de datos deberá impedir modificar o borrar movimientos (permisos o reglas), no solo la aplicación.
- La tabla crecerá con el tiempo; se estudiará el archivado de movimientos antiguos en la fase de tecnología.

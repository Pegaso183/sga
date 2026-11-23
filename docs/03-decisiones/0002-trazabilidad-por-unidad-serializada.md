# 0002 · Trazabilidad por unidad serializada

- **Fecha:** 2026-11-23
- **Estado:** Aceptada (provisional, versión preliminar de pruebas)

## Contexto
Todos los artículos llevan número de serie, este se registra **al recibir** la mercancía y es **único en todo el almacén**.
Hay que decidir cómo guardar el stock y cómo se relaciona con los números de serie.

## Opciones consideradas
1. **Stock por cantidad + series aparte:** una tabla con «artículo, ubicación, cantidad» y otra con los números de serie.
   Dos fuentes de verdad que pueden contradecirse (la cantidad dice 5, pero hay 4 series en esa ubicación).
2. **Una fila por unidad física:** cada número de serie es un registro con su artículo, ubicación y estado;
   el stock se obtiene contando unidades.
3. **Series solo en la expedición:** más sencillo en la entrada, pero no permite saber dónde está cada unidad.

## Decisión
Opción 2. La **Unidad** es la entidad central: una fila por unidad física, con número de serie único global.
Además:
- La **reserva** de pedidos se hace por cantidad (todo o nada por pedido); el número de serie se asigna al
  hacer el picking, cuando el operario escanea la unidad.
- Las unidades pueden estar sueltas en una ubicación o dentro de un **contenedor** (palet, caja o bulto); nunca en ambos.

## Consecuencias
- Una única fuente de verdad: el stock no puede descuadrarse respecto a las series.
- Trazabilidad completa: de qué proveedor y recepción llegó cada unidad, por dónde pasó y a qué cliente se envió.
- Los recuentos y devoluciones se hacen por número de serie, sin ambigüedad.
- Cada unidad debe escanearse en recepción, picking y devoluciones (necesita escáneres: Issue #4).
- Las consultas de stock son agregaciones; con los volúmenes previstos no supone un problema, pero se validará
  con datos reales en la fase de tecnología (Issue #5).

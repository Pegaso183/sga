# 01 · Requisitos funcionales

_Versión 0.1 · 2026-11-23 · Estado: **versión preliminar de pruebas** (Issue #1)._

> Estos requisitos se han redactado a partir de **supuestos**, tomando como referencia las funciones básicas que comparten
> los WMS mejor valorados del mercado (Manhattan, Blue Yonder, SAP EWM, Oracle, Infor…), adaptadas a un único almacén B2B
> con ~4.000 referencias, ~20 operarios y trazabilidad por número de serie.
> Se validarán con el responsable del almacén usando la guía de reunión. Todo puede modificarse.

## 1. Criterio para definir el MVP

El **MVP** (producto mínimo viable) es la primera versión con lo imprescindible para trabajar en el almacén.
Debe cubrir **el flujo completo de la mercancía con trazabilidad por número de serie**:

```
Pedido de compra → Recepción → Ubicación → Stock → Pedido de cliente → Picking → Embalaje → Expedición → Devolución
```

Se incluye lo que todos los WMS de referencia consideran básico: recepción con escáner, ubicación confirmada,
stock por ubicación en tiempo real, trazabilidad, recuentos cíclicos, picking agrupado, verificación en embalaje,
expedición y devoluciones.
Se deja para después lo que aporta eficiencia pero no es necesario para operar: optimización automática,
integraciones en tiempo real, gestión de productividad, automatización o inteligencia artificial.

## 2. Supuestos generales

| # | Supuesto |
|---|---|
| SG1 | Los operarios usan **terminales móviles con escáner** y un navegador web. El escáner funciona como un teclado (lee el código y lo «escribe»). |
| SG2 | La oficina usa el sistema desde un **navegador web** en un ordenador normal. No hay que instalar programas. |
| SG3 | Hay al menos una **impresora de etiquetas** en recepción y otra en expedición. |
| SG4 | En el MVP **no hay conexión automática con el ERP**: los datos se cargan y se descargan con **ficheros Excel/CSV**. La integración automática llega después (Issue #3). |
| SG5 | Perfiles del MVP: **operario**, **jefe de almacén** y **administrador** (ver RF-001). |
| SG6 | Interfaz en **español**. Un único almacén. |
| SG7 | El stock que ya existe se cargará al arrancar con un **inventario inicial escaneando cada unidad** (RF-045). |

## 3. Requisitos

Formato: cada requisito tiene un código, descripción, criterios de aceptación y prioridad (**MVP** o **Posterior**).
Los supuestos del modelo de datos (S1–S6) se indican donde aplican.

### Transversales

#### RF-001 · Acceso y perfiles
- **Descripción:** cada persona entra con su usuario y contraseña. Lo que puede hacer depende de su perfil.
- **Criterios de aceptación:**
  - [ ] Sin usuario y contraseña válidos no se accede a nada.
  - [ ] **Operario:** recibir, ubicar, trasladar, preparar, embalar, cargar, devolver, contar y consultar.
  - [ ] **Jefe de almacén:** todo lo del operario, más liberar pedidos, crear oleadas, cambiar estados, ajustar stock, aprobar recuentos y decidir el destino de las devoluciones.
  - [ ] **Administrador:** todo lo anterior, más maestros, usuarios, importaciones y configuración.
  - [ ] Un usuario desactivado no puede entrar, pero su histórico se conserva.
- **Prioridad:** MVP

#### RF-002 · Pantallas para terminal móvil
- **Descripción:** las operaciones de almacén tienen pantallas sencillas, pensadas para terminal con escáner y uso con una mano.
- **Criterios de aceptación:**
  - [ ] Cada operación se completa escaneando, con el mínimo de teclado.
  - [ ] Tras cada escaneo, el sistema confirma o rechaza en menos de 1 segundo, con mensaje claro y aviso visual (y sonoro si el terminal lo permite).
  - [ ] Un error de escaneo nunca deja la operación a medias: se puede volver a escanear.
- **Prioridad:** MVP

#### RF-003 · Histórico de movimientos
- **Descripción:** toda operación sobre una unidad queda registrada con usuario, fecha y hora, origen, destino y documento (ADR 0003).
- **Criterios de aceptación:**
  - [ ] No existe ninguna pantalla ni opción para modificar o borrar un movimiento.
  - [ ] Los errores se corrigen con un movimiento nuevo.
- **Prioridad:** MVP

#### RF-004 · Impresión de etiquetas
- **Descripción:** el sistema imprime etiquetas con código de barras de números de serie, ubicaciones y bultos.
- **Criterios de aceptación:**
  - [ ] Se puede imprimir una etiqueta o un lote (p. ej. todas las ubicaciones de un pasillo).
  - [ ] Se puede reimprimir cualquier etiqueta.
- **Prioridad:** MVP

#### RF-005 · Importación y exportación de ficheros
- **Descripción:** carga de datos desde Excel/CSV y descarga de listados, mientras no haya integración con el ERP (SG4).
- **Criterios de aceptación:**
  - [ ] Se pueden importar artículos, proveedores, clientes, direcciones, ubicaciones, pedidos de compra y pedidos de cliente.
  - [ ] Antes de guardar, el sistema valida el fichero y muestra los errores fila a fila; si hay errores, no se importa nada.
  - [ ] Importar dos veces el mismo fichero no duplica datos (actualiza los existentes).
  - [ ] Todos los listados se pueden descargar en Excel/CSV.
- **Prioridad:** MVP

### Maestros

#### RF-010 · Artículos
- **Descripción:** alta, modificación, desactivación y consulta de artículos.
- **Criterios de aceptación:**
  - [ ] No se pueden repetir el código ni el código de barras.
  - [ ] Se puede buscar por código, código de barras o descripción.
  - [ ] Se asigna la zona de picking de cada artículo (S4).
  - [ ] Un artículo con stock no se puede desactivar.
- **Prioridad:** MVP

#### RF-011 · Zonas y ubicaciones
- **Descripción:** definición de zonas y de ubicaciones con el esquema zona → pasillo → estantería → nivel → hueco.
- **Criterios de aceptación:**
  - [ ] Alta masiva por rangos (p. ej. zona A, pasillos 1–10, estanterías 1–20, niveles 1–5, huecos 1–3) con el código generado automáticamente.
  - [ ] Bloquear o desbloquear una ubicación; en una ubicación bloqueada no se puede ubicar ni extraer.
  - [ ] Impresión de etiquetas de ubicación (RF-004).
  - [ ] Una ubicación con stock no se puede desactivar.
- **Prioridad:** MVP

#### RF-012 · Proveedores, clientes y direcciones de entrega
- **Descripción:** alta, modificación, desactivación y consulta. Un cliente puede tener varias direcciones.
- **Criterios de aceptación:**
  - [ ] No se pueden repetir los códigos.
  - [ ] Un pedido solo puede usar direcciones de su propio cliente.
- **Prioridad:** MVP

#### RF-013 · Usuarios y motivos
- **Descripción:** gestión de usuarios con su perfil, y del catálogo de motivos (ajuste, bloqueo, devolución, recuento).
- **Criterios de aceptación:**
  - [ ] Solo el administrador gestiona usuarios y motivos.
  - [ ] Un motivo en uso no se borra: se desactiva.
- **Prioridad:** MVP

### Recepción

#### RF-020 · Pedidos de compra
- **Descripción:** registro de los pedidos de compra, a mano o por importación (RF-005).
- **Criterios de aceptación:**
  - [ ] Se ve el estado de cada pedido (pendiente, parcial, completo, cerrado, cancelado) y lo pendiente de recibir por línea.
  - [ ] Un pedido con recepciones no se puede borrar, solo cerrar o cancelar lo pendiente.
- **Prioridad:** MVP

#### RF-021 · Recepción contra pedido con escáner
- **Descripción:** el operario elige el pedido (o escanea su número) y escanea cada unidad recibida.
- **Criterios de aceptación:**
  - [ ] Por cada unidad: se escanea el código de barras del artículo y su número de serie.
  - [ ] Si la unidad no trae número de serie, el sistema lo genera e imprime su etiqueta (S1).
  - [ ] Se rechaza un número de serie que ya exista en el almacén.
  - [ ] Se rechaza un artículo que no esté en el pedido o que supere la cantidad pedida (S5).
  - [ ] Un pedido puede recibirse en varias recepciones (entregas parciales).
  - [ ] Las unidades recibidas quedan `disponibles` en la zona de recepción hasta que se ubican.
  - [ ] Al cerrar la recepción se muestra el resumen de lo recibido frente a lo pedido.
- **Prioridad:** MVP

#### RF-022 · Mercancía dañada en recepción
- **Descripción:** una unidad que llega dañada se recibe igualmente, pero marcada.
- **Criterios de aceptación:**
  - [ ] El operario puede marcar la unidad como `danada` al recibirla, indicando el motivo.
  - [ ] Las unidades dañadas no se pueden reservar ni preparar.
- **Prioridad:** MVP

#### RF-023 · Justificante de recepción
- **Descripción:** documento con lo recibido en cada recepción, incluidos los números de serie.
- **Criterios de aceptación:**
  - [ ] Se puede ver en pantalla, imprimir y descargar en PDF.
- **Prioridad:** MVP

### Ubicación y movimientos internos

#### RF-030 · Ubicación con sugerencia
- **Descripción:** el operario escanea una unidad de la zona de recepción y el sistema le sugiere dónde guardarla.
- **Criterios de aceptación:**
  - [ ] La sugerencia está en la zona de picking del artículo: primero un hueco que ya tenga ese artículo y, si no hay, un hueco vacío (S4).
  - [ ] El operario confirma escaneando la etiqueta de la ubicación.
  - [ ] Puede elegir otra ubicación; el sistema lo permite (salvo si está bloqueada) y lo registra.
  - [ ] Se pueden ubicar varias unidades seguidas del mismo artículo en la misma ubicación sin repetir pasos.
- **Prioridad:** MVP

#### RF-031 · Traslados
- **Descripción:** mover unidades de una ubicación a otra.
- **Criterios de aceptación:**
  - [ ] Se escanea la ubicación de origen, las unidades y la ubicación de destino.
  - [ ] No se pueden trasladar unidades reservadas a una tarea de picking en curso.
- **Prioridad:** MVP

#### RF-032 · Palets y cajas con etiqueta propia
- **Descripción:** agrupar unidades en un palet o caja para moverlo todo con un solo escaneo.
- **Prioridad:** Posterior (el modelo de datos ya lo permite)

#### RF-033 · Reposición desde reserva
- **Descripción:** mover stock de las zonas de reserva a la zona de picking cuando baje de un mínimo.
- **Prioridad:** Posterior (pendiente de confirmar si hay reserva)

### Inventario y trazabilidad

#### RF-040 · Consulta de stock
- **Descripción:** ver qué hay, dónde y en qué estado.
- **Criterios de aceptación:**
  - [ ] Por artículo: unidades por ubicación y estado, total disponible, total reservado para pedidos y stock libre.
  - [ ] Por ubicación: artículos y números de serie que contiene.
  - [ ] Por zona: resumen de su contenido.
  - [ ] La consulta está disponible en el terminal móvil y en la oficina.
- **Prioridad:** MVP

#### RF-041 · Trazabilidad de un número de serie
- **Descripción:** historia completa de una unidad.
- **Criterios de aceptación:**
  - [ ] Escaneando o tecleando un número de serie se ve: artículo, situación y estado actuales, proveedor y recepción de entrada, todos sus movimientos, y el cliente y pedido de salida si ya salió.
  - [ ] Se puede consultar qué números de serie se enviaron en un pedido o a un cliente.
- **Prioridad:** MVP

#### RF-042 · Cambios de estado
- **Descripción:** bloquear, poner en cuarentena, marcar como dañada o liberar stock.
- **Criterios de aceptación:**
  - [ ] Solo el jefe de almacén puede hacerlo, siempre con motivo.
  - [ ] Se puede aplicar a una unidad, a todas las de una ubicación o a todas las de un artículo.
  - [ ] Solo las unidades `disponibles` cuentan para reservar pedidos.
- **Prioridad:** MVP

#### RF-043 · Ajustes de inventario
- **Descripción:** dar de alta una unidad encontrada o de baja una perdida.
- **Criterios de aceptación:**
  - [ ] Solo el jefe de almacén puede hacerlo, siempre con motivo.
  - [ ] La baja no borra la unidad: queda en situación `baja` con su historial.
- **Prioridad:** MVP

#### RF-044 · Recuentos cíclicos por zona
- **Descripción:** contar una zona sin parar el resto del almacén.
- **Criterios de aceptación:**
  - [ ] El jefe crea el recuento de una zona; mientras está abierto, se avisa de que hay movimientos en esa zona.
  - [ ] El operario recorre las ubicaciones y escanea cada número de serie que encuentra; da por terminada cada ubicación.
  - [ ] El sistema clasifica cada resultado: correcta, no encontrada, mal ubicada o desconocida.
  - [ ] El jefe revisa las diferencias y las aprueba o las rechaza; las aprobadas generan traslados o ajustes con motivo.
- **Prioridad:** MVP

#### RF-045 · Inventario inicial
- **Descripción:** carga del stock existente al poner en marcha el sistema.
- **Criterios de aceptación:**
  - [ ] Se recorre el almacén por ubicaciones escaneando artículo y número de serie de cada unidad (o generando la serie y su etiqueta si no tiene).
  - [ ] Las unidades quedan dadas de alta en su ubicación con un movimiento de tipo `ajuste_alta` y motivo «inventario inicial».
  - [ ] Se puede hacer por zonas, en varios días.
- **Prioridad:** MVP

### Preparación de pedidos (picking)

#### RF-050 · Pedidos de cliente
- **Descripción:** registro de pedidos de cliente, a mano o por importación (RF-005).
- **Criterios de aceptación:**
  - [ ] Cada pedido tiene cliente, dirección de entrega (del mismo cliente), fecha de servicio y líneas.
  - [ ] Se ve el estado de cada pedido y se puede filtrar por estado, cliente y fecha.
  - [ ] Se puede cancelar un pedido que no haya salido; lo ya preparado vuelve a stock.
- **Prioridad:** MVP

#### RF-051 · Liberación de pedidos (reserva todo o nada)
- **Descripción:** un pedido solo pasa a preparación si hay stock libre para todas sus líneas.
- **Criterios de aceptación:**
  - [ ] El jefe libera pedidos uno a uno o en bloque, ordenados por fecha de servicio.
  - [ ] Si falta stock en alguna línea, el pedido queda `pendiente` y se indica qué falta.
  - [ ] Al liberar, la cantidad queda reservada y deja de estar libre para otros pedidos.
  - [ ] Se puede deshacer la liberación de un pedido que aún no ha empezado a prepararse.
- **Prioridad:** MVP

#### RF-052 · Oleadas
- **Descripción:** agrupar varios pedidos liberados para prepararlos en una misma ronda.
- **Criterios de aceptación:**
  - [ ] El jefe selecciona pedidos liberados (filtrando por fecha de servicio, cliente…) y crea la oleada.
  - [ ] El sistema genera las tareas de picking agrupadas por artículo y ubicación, ordenadas por el código de ubicación para hacer un recorrido lógico.
  - [ ] Las tareas pueden asignarse a un operario o quedar libres para quien las coja.
- **Prioridad:** MVP

#### RF-053 · Ejecución del picking
- **Descripción:** el operario sigue sus tareas en el terminal.
- **Criterios de aceptación:**
  - [ ] El terminal indica la ubicación; el operario la confirma escaneándola.
  - [ ] El operario escanea el número de serie de cada unidad que coge.
  - [ ] Se rechaza una unidad de otro artículo, que no esté en esa ubicación o que no esté `disponible`.
  - [ ] Al escanearla, la unidad se asigna a una línea de un pedido de la oleada, y el terminal indica a qué pedido va.
  - [ ] Cuando todas las unidades de un pedido están cogidas, el pedido pasa a `preparado`.
- **Prioridad:** MVP

#### RF-054 · Incidencias de picking
- **Descripción:** qué ocurre si en la ubicación no está lo que debería.
- **Criterios de aceptación:**
  - [ ] El operario marca la tarea con incidencia («falta», «dañada») y puede seguir con las demás.
  - [ ] El sistema propone otra ubicación con stock libre del mismo artículo, si la hay.
  - [ ] El jefe ve las incidencias abiertas y la ubicación queda señalada para recontar.
- **Prioridad:** MVP

#### RF-055 · Orden de salida de las unidades (la más antigua primero)
- **Descripción:** sugerir que salgan primero las unidades que llevan más tiempo en el almacén.
- **Prioridad:** Posterior

### Embalaje y expedición

#### RF-060 · Embalaje con verificación
- **Descripción:** los pedidos preparados se embalan en bultos comprobando cada unidad.
- **Criterios de aceptación:**
  - [ ] Se crea un bulto para el pedido y se escanea cada unidad que se mete; se rechazan unidades de otro pedido.
  - [ ] Un pedido puede tener varios bultos.
  - [ ] Al cerrar el bulto se puede indicar el peso y se imprime su etiqueta (nº de pedido, cliente, dirección, bulto x de n).
  - [ ] El pedido no puede expedirse si falta alguna unidad por embalar.
- **Prioridad:** MVP

#### RF-061 · Albarán de entrega con números de serie
- **Descripción:** documento que acompaña al pedido.
- **Criterios de aceptación:**
  - [ ] Incluye cliente, dirección, líneas, bultos y la lista de números de serie enviados.
  - [ ] Se puede imprimir y descargar en PDF.
- **Prioridad:** MVP

#### RF-062 · Expedición
- **Descripción:** registro de la salida física de los pedidos.
- **Criterios de aceptación:**
  - [ ] Se crea una expedición (p. ej. un camión) y se escanea cada bulto al cargarlo.
  - [ ] Solo se aceptan bultos de pedidos completos y embalados.
  - [ ] Se puede indicar el transportista y el número de seguimiento.
  - [ ] Al confirmar la salida, las unidades pasan a `expedida` y los pedidos a `expedido`.
- **Prioridad:** MVP

#### RF-063 · Integración con transportistas
- **Descripción:** etiquetas oficiales de cada agencia y número de seguimiento automático.
- **Prioridad:** Posterior

### Devoluciones

#### RF-070 · Recepción de devoluciones
- **Descripción:** registro de la mercancía devuelta contra su pedido.
- **Criterios de aceptación:**
  - [ ] Se indica el pedido y se escanea cada número de serie devuelto, con su motivo.
  - [ ] Se rechaza un número de serie que no saliera en ese pedido.
  - [ ] La unidad vuelve al almacén en la zona de devoluciones, en estado `cuarentena`.
- **Prioridad:** MVP

#### RF-071 · Destino de la mercancía devuelta
- **Descripción:** el jefe decide qué se hace con cada unidad devuelta.
- **Criterios de aceptación:**
  - [ ] Destinos: **volver a stock** (pasa a `disponible` y se ubica), **desecho** o **devolución al proveedor** (en ambos casos, baja con motivo).
  - [ ] Se puede consultar qué devoluciones tienen unidades pendientes de decidir.
- **Prioridad:** MVP

### Informes

#### RF-080 · Listados básicos
- **Descripción:** listados con filtros y descarga a Excel/CSV (RF-005).
- **Criterios de aceptación:**
  - [ ] Stock (por artículo, ubicación, zona y estado).
  - [ ] Movimientos (por fechas, usuario, tipo, artículo y número de serie).
  - [ ] Pedidos de compra pendientes de recibir y pedidos de cliente por estado.
  - [ ] Incidencias abiertas (picking, recuentos, devoluciones pendientes de decidir).
- **Prioridad:** MVP

#### RF-081 · Panel de indicadores
- **Descripción:** pedidos al día, unidades movidas, exactitud del inventario, actividad por operario.
- **Prioridad:** Posterior

### Integraciones

#### RF-090 · Integración automática con el ERP
- **Descripción:** intercambio automático de artículos, terceros, pedidos, recepciones, expediciones y ajustes.
- **Prioridad:** Posterior (Issue #3). En el MVP se usa RF-005.

## 4. Requisitos no funcionales (MVP)

| # | Requisito |
|---|---|
| RNF1 | **Rendimiento:** respuesta a un escaneo en menos de 1 segundo con 20 usuarios trabajando a la vez. |
| RNF2 | **Disponibilidad:** el sistema debe estar disponible durante todo el horario del almacén. |
| RNF3 | **Copias de seguridad:** diarias y probadas; recuperación sin pérdida de más de un día de datos (Issue #6). |
| RNF4 | **Seguridad:** contraseñas cifradas, conexión cifrada (HTTPS), cada acción ligada a un usuario. |
| RNF5 | **Integridad:** las reglas del modelo de datos (series únicas, movimientos inmutables…) se garantizan en la base de datos. |
| RNF6 | **Usabilidad:** un operario nuevo debe poder hacer una recepción o un picking tras una formación corta. |

## 5. Fuera del MVP

Se deja para versiones posteriores (resumen de lo marcado como **Posterior** y de otras funciones habituales en los WMS avanzados):

- Palets y cajas con etiqueta propia (RF-032) y reposición desde reserva (RF-033).
- Orden de salida automático de las unidades más antiguas (RF-055).
- Integración con transportistas (RF-063) y con el ERP (RF-090).
- Panel de indicadores y control de productividad de operarios (RF-081).
- Optimización automática de huecos (*slotting*), citas de muelle y gestión de patio.
- *Cross-docking*, montaje de kits, portal para clientes, picking por voz, automatización e inteligencia artificial.
- Varios almacenes, valoración del stock y facturación.

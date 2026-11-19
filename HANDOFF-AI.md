# HANDOFF-AI.md — Registro de Pagos

Última actualización: 2026-11-19.

## Qué es

App web de un solo archivo para llevar el registro de pagos por comercio
electrónico (códigos QR) y transferencias directas de BANDEC. Se pega el
mensaje tal como llega y la app saca los datos sola.

## Los dos formatos que aprende

**1. Transferencia directa a tarjeta** («La Transferencia fue completada»):
Fecha, Beneficiario, Ordenante, Monto, Nro. Transacción, Saldo restante.

**2. Pago QR / comercio electrónico** («Pago completado»):
Fecha, Entidad (nombre del comercio), Id Compra, Importe, Importe pagado,
No. Transacción, Saldo disponible. Si el importe pagado es menor que el
importe, muestra la diferencia como bonificación/descuento.

## Funciones

- Pegar mensaje → detecta el tipo y llena los campos (editables antes de guardar).
- Botones de ejemplo para probar los dos formatos.
- Aviso si el Nro. Transacción ya está registrado (duplicado).
- Lista con búsqueda, filtro por tipo y por mes.
- Totales: transferencias, pagos QR, bonificación en QR, último saldo conocido.
- Detalle con el mensaje original.
- Exportar a CSV (para Excel/Sheets) y respaldo JSON reimportable.
- Editar y borrar registros.
- Campos manuales del pago QR (añadidos 2026-11-19, iguales a la planilla
  en papel «Control de QR»): Nombre y apellidos, CI y # teléfono. El
  mensaje de BANDEC no trae esos datos: se llenan a mano tras la lectura
  automática. Se guardan, se ven en la tarjeta, entran en la búsqueda y
  salen en el CSV (orden: fecha, tipo, entidad, nombre y apellidos, CI,
  teléfono, importe, importe pagado, descuento, Id Compra, transacción,
  saldo, moneda, nota). Los registros viejos quedan con esos campos vacíos.

## Sección «Beneficios y descuentos del pago QR» (añadida 2026-11-19)

Datos verificados el 19/11/2026: cliente 4 % hasta 210 CUP por operación
(desde 1/8/2026, antes 6 %); comercio 2 % hasta 105 CUP y comisión 0,8 %
(antes 1,5 %); acreditación en tiempo real en el mismo banco. Solo vale
para Pago en Línea por QR ligado a la Cuenta Bancaria Fiscal, no para
transferencia directa. Incluye calculadora (mínimo entre 4 % y 210 CUP),
Caja Extra (1,00 CUP + 0,5 %), límite 120.000 CUP de cuentas personales,
Resolución 111/2023, Decreto-Ley 91/2024 (multas hasta 60.000 CUP) y el
3 % de descuento de la ONAT por pagar tributos por vía electrónica.

## Archivos

- `registro-de-pagos.html`: la app completa, un solo archivo, sin conexión.
- `HANDOFF-AI.md`: este documento.

## Limitación conocida

Es una página estática sin servidor. En la vista del chat los registros
viven en la sesión: hay que exportar el CSV o el respaldo JSON para
conservarlos. En el archivo abierto en el teléfono, los datos quedan en
el navegador de ese equipo.

## Pendiente

- Leonardo debe probarla con mensajes reales y decir si algún dato no se
  llena bien.
- Publicarla en GitHub Pages solo si Leonardo lo pide (como sus otras apps).

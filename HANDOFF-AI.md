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

## Publicación y base de datos (2026-11-19)

- GitHub: repositorio público `registro-de-pagos`, rama main, commit
  inicial `c6b64706` (index.html, README.md, HANDOFF-AI.md). Pages
  activado y verificado en vivo:
  https://negociosparticularescubanos.github.io/registro-de-pagos/
  Fuente local para republicar: `~/workspace/registro-pagos-repo/`
  (copiar el HTML exportado como index.html). Registro de sincronización:
  `~/workspace/registro-pagos-repo.muse-github-snapshot-sync.json`.
- Google Sheets «Registro de Pagos QR» (cuenta de negocios):
  https://docs.google.com/spreadsheets/d/17CY_m1W6V0QhJGd0OXKHGTzcrqAwGogrvqfLAhwy13M/edit
  Hoja «Pagos»: 17 columnas (Fecha, Tipo, Entidad, Nombre y apellidos,
  CI, Teléfono, Importe, Importe pagado, Descuento, Monto, Beneficiario,
  Ordenante, Id Compra, Nro. Transacción, Saldo, Moneda, Nota), con 2
  filas de ejemplo (una transferencia real y un pago QR de ejemplo para
  borrar). Hoja «Consultar»: filtros por nombre, teléfono, CI, fecha
  desde/hasta, mes, año y día exacto, con resumen (cantidad, total
  pagado QR, total descuento, total transferencias). Fórmulas en español
  (separador «;»). Filtro probado: buscar «cliente» devuelve solo su fila.

## Conexión con Google Sheets (2026-11-19)

- Apps Script ligado a la hoja (Extensiones → Apps Script): `doGet`
  (salud) y `doPost` (guarda el pago en «Pagos», sin duplicados por
  Nro. Transacción). Aplicación web desplegada, acceso «Cualquier
  usuario», ejecutar como el usuario:
  https://script.google.com/macros/s/AKfycbyrQ4Jh8L0g4SPWCbmT1zH3ujQYeoAbycXaMI5NYNETYCKX4jXc4G5Rd92rr_Y-YkKSDw/exec
  Probado: un pago de prueba llegó a «Pagos», el segundo envío del mismo
  Nro. Transacción no duplicó, la fila de prueba se borró.
- La app tiene sección «Guardar en Google Sheets»: URL ya puesta por
  defecto (editable, se guarda en el equipo), casilla de envío automático
  (activada por defecto), botón «Probar conexión» e indicador
  verde/rojo. Al guardar, avisa «Guardado en Sheets ✓», «Ya estaba en
  Sheets» o «No se pudo enviar a Sheets; el registro quedó guardado en
  este equipo». Cada tarjeta no enviada tiene botón «Enviar a Sheets»;
  las enviadas llevan «✓ En Sheets». Sin Sheets, la app sigue solo en
  local.

## Corrección del lector (2026-11-19)

- La prueba en vivo encontró que el lector multiplicaba todos los montos
  por 100 (500.00 lo leía como 50000, 2500.00 como 250000) y dejaba un
  punto al final del Nro. Transacción, el Beneficiario y el Ordenante.
  Causa: la coma con que el SMS separa los campos se tragaba como coma
  decimal cubana. Corregido: punto con 2 cifras al final es decimal
  («2500.00» = 2500), punto con 3 cifras es miles («2.500» = 2500);
  códigos sin punto final; en Sheets el tipo va como «Pago QR» o
  «Transferencia» y el Monto solo en transferencias. El indicador de
  Sheets se comprueba solo al cargar la app. Verificado en vivo con el
  código real (34 comprobaciones) y en la hoja tras republicar.

## Foto al SMS y pestañas (2026-11-19)

- Dos pestañas: «Trabajo» (por defecto: pegar mensaje, foto al SMS,
  revisar datos, guardar, registro, totales y Sheets) y «Formación»
  (beneficios y descuentos del pago QR con su calculadora). Diseño de una
  columna en el teléfono y dos en PC.
- «Foto al SMS»: abre la cámara trasera o la galería, vista previa en
  grises con más contraste, giro e inversión (modo oscuro); «Leer texto
  de la foto» reconoce el texto en el teléfono con Tesseract.js 5.1.1 en
  español (modelo rápido spa, ~1,1 MB), sin subir la foto a ningún
  sitio; el texto sale en un cuadro editable y «Usar este texto» lo pasa
  al lector de siempre. La foto nunca guarda sola: siempre se revisan los
  datos antes de guardar.
- Archivos OCR autoalojados en el repo, carpeta `ocr/` (tesseract.min.js,
  worker.min.js, núcleos WASM y `lang/spa.traineddata.gz`); la app los
  carga por rutas relativas, sin CDN. Los binarios (.wasm, .gz) se suben
  por la web de GitHub, no por el conector (que solo admite texto).
  OJO: Tesseract.js 5.1.1 pide en el navegador el núcleo
  `tesseract-core-simd-lstm` (3 archivos: .wasm.js, .wasm y .js); sin
  ellos la lectura falla con «importScripts … failed to load». Verificado
  en vivo el 2026-11-19: la foto se lee en menos de 1 minuto la primera
  vez; puede confundir algún dígito («ld» por «Id», un «1» de más en un
  código) y se corrige a mano antes de guardar; el registro llega a
  Sheets y la prueba se borró. En PC se ve bien; el ancho de teléfono
  queda por comprobar en el teléfono de Leonardo.

## Pendiente

- Leonardo debe probarla con mensajes reales y fotos reales y decir si
  algún dato no se llena bien.

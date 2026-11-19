# Registro de Pagos

App web de un solo archivo para llevar el registro de pagos por comercio electrónico (códigos QR) y transferencias directas de BANDEC.

## Uso

1. Abre `index.html` en el navegador (funciona sin conexión).
2. Pega el mensaje de BANDEC tal como llegó.
3. La app detecta si es transferencia directa o pago por QR y llena los datos sola: fecha, montos, Nro. Transacción, saldo, entidad e Id Compra.
4. En el pago QR, llena a mano Nombre y apellidos, CI y # teléfono (el mensaje no trae esos datos).
5. Guarda el registro. Los datos quedan en el navegador de ese equipo.

## Funciones

- Búsqueda por nombre, CI, teléfono, transacción o nota.
- Filtros por tipo y por mes.
- Totales de transferencias, pagos QR y bonificación.
- Exportar a CSV y respaldo JSON.
- Sección de beneficios y descuentos del pago QR en Cuba (datos verificados el 19/11/2026).

## Publicación

GitHub Pages: https://negociosparticularescubanos.github.io/registro-de-pagos/

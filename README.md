# Atletix Horse Sales Report — GitHub Native

Esta versión **ya no usa Google Apps Script**. Todo funciona con:

- **GitHub Pages** para mostrar el reporte.
- **GitHub Actions** para leer Shopify y generar `public/data/report.json`.
- **GitHub Secrets / Variables** para guardar credenciales y configuración.

## Importante sobre el botón Refresh

En una app 100% GitHub Pages no se puede llamar Shopify directamente desde el navegador sin exponer el token. Por seguridad, el botón **Refresh** del reporte recarga el último JSON generado por GitHub Actions.

La actualización real desde Shopify ocurre:

1. Automáticamente cada 2 días por GitHub Actions.
2. Manualmente desde GitHub → Actions → **Build data and deploy GitHub Pages** → **Run workflow**.

Esto evita el error de cuota de Apps Script porque ya no se usa Apps Script ni UrlFetch.

## Setup

1. Crea un repo nuevo en GitHub.
2. Sube estos archivos.
3. Ve a **Settings → Pages** y selecciona **GitHub Actions** como source.
4. Ve a **Settings → Secrets and variables → Actions**.

### Secrets requeridos

- `SHOPIFY_STORE` = `your-store.myshopify.com`
- `SHOPIFY_TOKEN` = token Shopify Admin API con `read_orders`

### Variables opcionales

- `SHOPIFY_API_VERSION` = `2024-01`
- `ATLETIX_UNIT_COGS` = `89`
- `ATLETIX_INITIAL_STOCK` = `100`
- `ATLETIX_STOCK_RECEIVED_DATE` = `2025-12-26`
- `ATLETIX_SKU` = `ATLETIX60`

## Cómo refrescar datos

- Automático: cada 2 días por cron.
- Manual: GitHub → Actions → Build data and deploy GitHub Pages → Run workflow.
- En la pantalla del reporte: Refresh solo recarga el JSON ya publicado.

## Datos manuales incluidos

- Mirko Midili queda como fila manual editable en H1 2026:
  - Qty: 4
  - Shipping: 17.33
  - Address/phone en Note
- Sebastian Petroll / order 152336 se marca como Atletix Request con shipping 70.26 cuando aparece en Shopify.

Los cambios manuales hechos en la pantalla se guardan en el navegador con `localStorage` y salen en el CSV.

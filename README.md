# Atletix Horse Sales Report — GitHub Native v3

Esta versión no usa Google Apps Script. Está preparada para **GitHub Pages desde branch/root**.

## Por qué antes veías el README

GitHub Pages estaba publicando desde `main / (root)`, pero el repo no tenía `index.html` en la raíz. Cuando no hay `index.html`, GitHub Pages puede mostrar el README. Esta versión trae `index.html` en la raíz.

## Configuración de GitHub Pages

Settings → Pages:

- Source: `Deploy from a branch`
- Branch: `main`
- Folder: `/ (root)`
- Save

## Secrets requeridos

Settings → Secrets and variables → Actions → Secrets:

- `SHOPIFY_STORE` = `your-store.myshopify.com`
- `SHOPIFY_TOKEN` = token Admin API con `read_orders`

## Variables opcionales

Settings → Secrets and variables → Actions → Variables:

- `SHOPIFY_API_VERSION` = `2024-01`
- `ATLETIX_UNIT_COGS` = `89`
- `ATLETIX_INITIAL_STOCK` = `100`
- `ATLETIX_STOCK_RECEIVED_DATE` = `2025-12-26`
- `ATLETIX_SKU` = `ATLETIX60`

## Cómo refrescar Shopify data

Actions → Build Shopify data → Run workflow.

También corre automáticamente cada 2 días.

El workflow genera y guarda:

- `data/report.json` para el sitio en root.
- `public/data/report.json` como copia de compatibilidad.

## Botón Refresh en el sitio

El botón Refresh del sitio no llama Shopify directamente. Solo recarga el último `data/report.json` publicado. Esto mantiene seguro el token de Shopify.

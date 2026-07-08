# Atletix Horse Sales Report — GitHub Native

This version no longer uses Google Apps Script. It is prepared to run entirely with GitHub Pages and GitHub Actions.

## Why the README was showing before

GitHub Pages was publishing from `main / (root)`, but the repository did not have an `index.html` file in the root. When there is no `index.html`, GitHub Pages can display the README. This package includes `index.html` in the repository root.

## GitHub Pages setup

Use this setup:

1. Go to `Settings → Pages`.
2. Source: `Deploy from a branch`.
3. Branch: `main`.
4. Folder: `/ (root)`.
5. Save.

The published site should open the report at:

```text
https://equestrian-labs-dashboard.github.io/Atletix_Corro/
```

## Required secrets

Go to `Settings → Secrets and variables → Actions → Secrets` and add:

```text
SHOPIFY_STORE = your-store.myshopify.com
SHOPIFY_TOKEN = Shopify Admin API token with read_orders permission
```

## Optional variables

Go to `Settings → Secrets and variables → Actions → Variables` and add any of these if needed:

```text
SHOPIFY_API_VERSION = 2024-01
ATLETIX_UNIT_COGS = 89
ATLETIX_INITIAL_STOCK = 100
ATLETIX_STOCK_RECEIVED_DATE = 2025-12-26
ATLETIX_SKU = ATLETIX60
```

## How Shopify data refresh works

The real Shopify refresh is handled by GitHub Actions:

- Automatic refresh: every 2 days.
- Manual refresh: `Actions → Build Shopify data → Run workflow`.

The site button named `Refresh` does not call Shopify directly. It only reloads the latest published `data/report.json`. This keeps the Shopify token secure because the token never reaches the browser.

## Manual data included

The report supports manual review rows for H1/H2 reconciliation.

Current manual support:

- Mirko Midili can be added as a manual editable row in H1 2026.
  - Qty: 4
  - Shipping: 17.33
  - Address and phone can be kept in the note field.
- Sebastian Petroll / order 152336 is marked as `Atletix Request` with shipping 70.26 when it appears in Shopify.

Manual changes made in the browser are saved locally with `localStorage` and are included in the downloaded CSV.

## H1/H2 Invoice Formula

The H1/H2 review cards use this calculation:

- Total COGS / COX = Total units sold × Unit COGS / COX
- COGS Excluded = Units removed or marked as Atletix Request × Unit COGS / COX
- Final Invoice Due = Total COGS / COX - COGS Excluded + Total Shipping Charges

Example: 41 units × $89 = $3,649.00; 9 excluded/request units × $89 = $801.00; shipping = $87.59; final invoice due = $3,649.00 - $801.00 + $87.59 = $2,935.59.

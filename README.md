# WixSale Exporter for OpenCart 2.x

Official migration exporter for OpenCart 2.0 through 2.3.x. Exports your complete product catalogue to WixSale-ready JSON — fast, complete, and secure.

**[WixSale](https://wixsale.com)** is a modern e-commerce platform. This module is purpose-built to help store owners move from OpenCart to WixSale quickly and easily, without manual data entry or fragile CSV workarounds.

---

## Why use this exporter?

OpenCart stores product data across categories, options, attributes, manufacturers, and multi-language descriptions. The WixSale Exporter consolidates everything into a single, structured JSON feed that WixSale imports natively.

- **Complete catalogue coverage** — products, options/variants, stock, prices, categories, manufacturers, attributes, images, downloads, dimensions, weights, SEO URLs, filter tags, and multi-language descriptions
- **OpenCart 2.x native** — compatible with the `url_alias` SEO schema used in OpenCart 2.0–2.3
- **WixSale-optimised output** — flat aliases (`featured_image`, `categories_feed`, `name_bg`, `seo_url_en`, …) alongside the full OpenCart record
- **Built for large stores** — batched processing (20 products per step) avoids request timeouts
- **Administrator-only access** — exports are stored in a protected directory under `system/storage/`

---

## Requirements

| Component | Version |
|-----------|---------|
| OpenCart | 2.0 – 2.3.x |
| PHP | 5.4 or later |

This package ships dual admin entry points for maximum compatibility:

- `admin/controller/module/` — OpenCart 2.0–2.2
- `admin/controller/extension/module/` — OpenCart 2.3

---

## Installation

### Option A — Extension Installer (OpenCart 2.3+)

1. Download `wixsale-exporter-opencart2-1.0.0.ocmod.zip` from the releases page.
2. In admin, go to **Extensions → Extension Installer**.
3. Upload the ZIP and confirm the installation.

### Option B — Manual upload (all 2.x versions)

1. Extract the `upload/` folder from the release ZIP.
2. Upload its contents to your OpenCart root via FTP, merging with existing directories.
3. In admin, go to **Extensions → Modules** (or **Extensions → Extensions → Modules** on 2.3).

### Activate the module

1. Find **WixSale Exporter** in the module list.
2. Click **Install**, then **Edit**.
3. Set status to **Enabled** and save.

---

## Generating an export

1. Open **WixSale Exporter** from the module configuration screen.
2. Optionally set **export filters**:
   - **Category** — export a single category branch (child categories included)
   - **Product status** — enabled, disabled, or all
   - **Stock status** — in stock, out of stock, or all
   - **Products per feed** — single file, or split into feeds of 100 / 300 / 500 / 1000 products
3. Review the live product count for your selected filters.
4. Click **Generate JSON export** and keep the page open until completion.
5. Download one or more generated JSON files.

---

## Importing into WixSale

1. Sign in to your store at **[wixsale.com](https://wixsale.com)**.
2. Go to **Catalog → Imports → New import**.
3. Choose **URL or file**, format **JSON**, item path **`products`**.
4. Upload your export file (or provide a URL) and follow the import wizard.

If you split the export into multiple feeds, import each file in order.

---

## JSON format

Exports are UTF-8 JSON with:

```json
{
  "schema": "wixsale.opencart.catalogue",
  "schema_version": 1,
  "products": [ … ]
}
```

The header includes site metadata, languages, categories, manufacturers, and attributes/options. Each product entry contains the full OpenCart data structure plus WixSale flat aliases for straightforward field mapping during import.

---

## Security

- Export files are written to `system/storage/wixsale-exports/` inside a randomly named subdirectory.
- `.htaccess` and `index.php` guard against direct web access.
- Downloads require an authenticated administrator session.

---

## Building a release ZIP

```bash
cd wixsale-exporter-opencart2
zip -r ../wixsale-exporter-opencart2-1.0.0.ocmod.zip upload install.xml
```

The file name **must** end in `.ocmod.zip` when using the Extension Installer (OpenCart 2.3+). A plain `.zip` will be rejected with “Invalid file type!”.

---

## Support

For migration assistance and WixSale platform help, visit **[wixsale.com](https://wixsale.com)**.

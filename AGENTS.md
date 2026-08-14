# AGENTS.md

## What this is

Static HTML/CSS/JS site built from the **Vuexy Bootstrap 4 admin template** (Pixinvent). Pure static files — **no build system**: no package.json, npm, gulp, CI, tests, or lint. Served by XAMPP Apache. Nothing is compiled at dev time; editing the page shows up on refresh.

## Layout

- `html/rtl/vertical-menu-template-bordered/` — the actual site pages (115 self-contained `.html` files). `index.html` is the entrypoint (it's the ecommerce dashboard). This is the only layout variant in use; there is no LTR or root `index.html`.
- `app-assets/` — compiled theme assets consumed by the pages: `css-rtl/`, `js/`, `vendors/`, `images/`, `fonts/`, `data/` (JSON demo data, plus `data/fullcalendar/php/` endpoints and `data/ajax.php`).
- `src/` — SCSS/JS **sources** the template was compiled from. Editing here does **not** affect the served site (no compiler in this repo). Do not edit unless someone explicitly adds a build step.
- `assets/` — the designated place for **custom code** (per template comments): `assets/js/scripts.js` (custom JS), `assets/css/style.css` and `assets/css/style-rtl.css` (custom CSS, loaded last, override theme). SCSS sources for these live in `assets/scss/`.

## Site is RTL

`<html data-textdirection="rtl">` and pages load the `app-assets/css-rtl/*` bundle plus `assets/css/style-rtl.css`. Any custom CSS must work in RTL and be added to both `style.css` and `style-rtl.css`.

## Editing pages — gotchas

- Every page is standalone markup; the navbar, sidebar menu, and footer are **duplicated inline in each file**. There are no includes/templates. To change navigation, update every page.
- Asset links are relative `../../../app-assets/...` and `../../../assets/...` because pages sit 3 levels deep. Copy this pattern for any new asset.
- Pages need jQuery + feather icons: `app-assets/vendors/js/vendors.min.js` at bottom, then `feather.replace()` on `$(window).load`. Page-specific JS goes in `app-assets/js/scripts/pages/` and is referenced per page.
- Theme color palette is `window.colors` in `app-assets/js/core/app.js` (primary `#7367F0`, etc.).

## Workflow

No commands exist. Serve via `http://localhost/ChekimSite/html/rtl/vertical-menu-template-bordered/index.html` (XAMPP). Verify changes by opening the page in a browser; check both default and dark/semi-dark/bordered layouts if the change affects theming.

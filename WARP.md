# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

Project type: Static export of a WordPress site (WordPress 6.8.x). Pages are pre-rendered HTML that reference WordPress theme and plugin assets bundled in the repo.

Commands
- Preview locally (serve from repo root so absolute paths like /wp-content/... resolve):
  - PowerShell (Windows): py -m http.server 8080
  - Python (any OS): python -m http.server 8080
  - Node (if installed): npx serve -l 8080 .
  Then open http://localhost:8080
- There is no build, lint, or test tooling in this repo (no package.json/composer.json). Edit HTML/CSS/JS directly and preview via a static server.

High-level architecture
- Entry point: index.html (front page) built with Gutenberg blocks and the “bakery-and-pastry” theme. It pulls block styles/scripts from wp-includes and wp-content/plugins/gutenberg.
- Content pages: standalone directories with index.html (e.g., contenido-dinamico/, cv-digital/, privacidad/, produccion/, footer/, plantilla-pastel/). Navigation between pages uses normal links and on-page anchors.
- Theme: wp-content/themes/bakery-and-pastry provides fonts (Outfit, Source Sans 3) and global CSS used throughout the site.
- Plugins (static assets only):
  - wp-content/plugins/gutenberg: block styles/scripts referenced by pages.
  - contact-form-7, superb-blocks, pojo-accessibility, sticky-block, simply-static, etc.: their JS/CSS assets are referenced from pages; only the front-end pieces are present here.
- Media: images/videos under media/ and uploads/YYYY/MM/. Paths are used directly by pages; no image pipeline.

Development notes specific to this repo
- Absolute URLs: Many links and asset references start with /. Always serve from the repo root during local preview so paths resolve.
- Static export: The presence of simply-static indicates these files were exported from a WordPress instance. Regenerating pages must be done in WordPress; this repo does not contain the PHP backend.
- Forms/dynamic features: Any features depending on server-side WordPress (e.g., Contact Form 7 submissions) won’t function in this static export unless replaced with a client-side or external service.

Important files to know
- index.html: front page with SEO meta and JSON-LD schema.
- wp-content/themes/bakery-and-pastry/: theme CSS, fonts, and images.
- wp-content/plugins/: front-end assets for Gutenberg and other blocks referenced by pages.
- media/, uploads/: site media referenced across pages.

README
- README.md is minimal; it does not document commands or structure beyond the project name. This WARP.md supersedes it for operational guidance.

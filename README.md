# abrisuite.com (static mirror)

Static, WordPress-free mirror of [abrisuite.com](https://www.abrisuite.com/),
captured from the live site on 2026-05-05 and adapted for Cloudflare Pages.

## Deployment

Cloudflare Pages serves the contents of the repo root directly. No build step
is required.

- **Build command:** *(none)*
- **Build output directory:** `/`
- **Production branch:** `main`

## How this was generated

1. `wget --mirror --page-requisites --convert-links --adjust-extension` against
   `https://www.abrisuite.com/`, with WooCommerce, `wp-admin`, `wp-json`, and
   feed paths excluded.
2. Spurious legacy URLs (`?p=N`, `?e-page=N`) deleted.
3. Absolute self-URLs rewritten to root-relative so the site is portable.
4. `_headers` file added for Cloudflare Pages cache + security headers.

## What works / what doesn't

**Visual rendering:** identical to the live WP site (Elementor pages, header,
footer, blog listings, individual posts, services pages).

**Will not work statically:**
- Contact forms (Gravity Forms POST → admin-ajax.php) — wire to a Pages
  Function or third-party form handler if needed.
- Search.
- Comments.
- WP-JSON / oEmbed.
- WooCommerce shop — intentionally excluded from this mirror.
- Anything that relied on `/wp-admin/admin-ajax.php`.

## Re-mirroring

If content changes on the live WP site, regenerate by running the same wget
flow against the origin. See `wordpress1:/tmp/abrisuite_mirror.sh` and
`wordpress1:/tmp/abrisuite_clean.sh` (or any successor scripts).

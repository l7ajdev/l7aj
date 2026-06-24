# Ataa.ma Design Template Extract

This is a cleaned, trimmed version of the ataa.ma site mirror, kept purely for reusing the **visual design and front-end behavior** (CSS, JS, layout, cart-like donation UI) on a different nonprofit/charity website. It is not a working copy of ataa.ma and has no backend.

## Folder structure

- `pages/` — six representative HTML templates, pulled from different sections of the site and flattened into one folder so they're easy to browse and copy from:
  - `home.html` — homepage: slider, project cards, CTA sections
  - `about.html` — text + image content page layout
  - `contact.html` — contact form layout
  - `projects-listing.html` — project grid with filters (the page that lets you browse and "add to cart" for donations)
  - `project-details.html` — single project page with donation form / add-to-cart button
  - `sponsorship-cart-example.html` — sponsorship/subsidy flow with a recaptcha-gated payment form (`sihaty.html` originally), good second example of the cart UI
- `assets/`, `static/`, `lib/`, `src/` — all CSS, JS, fonts, and third-party libraries (jQuery, Bootstrap 5.1.3, jQuery Validation, jQuery Calendars/Hijri calendar plugins, Select2, FontAwesome). This is the actual design system.
- `sample-content-images/` — a handful of ataa's real project/slider photos, kept only so the templates don't show broken images when you open them. Swap these for your own charity's photography.

## What was removed and why

**WinHTTrack's own files** (mirror tool artifacts, not part of the real site): the top-level `index.html` "list of mirrored projects" pages, `backblue.gif`/`fade.gif`, `hts-cache/`, `hts-log.txt`, `cookies.txt`, `ataa.whtt`.

**Cloudflare / reCAPTCHA scripts**: removed since they depend on ataa.ma's own Cloudflare account and won't function (and aren't useful for reuse anyway). One harmless empty `<div class="g-recaptcha">` placeholder remains in the sponsorship template; the script that would render it is gone, so it just sits inert.

**ataa.ma branding & content photos**: their logo files, the 25MB of homepage banner photography, and the ~78MB of project photos in the original mirror were dropped (kept 4 sample project images only, for preview purposes). These are content, not design, you'll be replacing them with your own brand and project photos regardless.

**`backoffice.ataa.ma/` admin panel (218MB)**: not copied at all. That's ataa's admin dashboard, not reusable front-end design, just their data/CMS.

**`dashboard/` folder inside `ataa.ma/`**: also not copied; it's the user-facing admin dashboard UI, only relevant if you specifically want an admin panel skin too. Ask if you want this added back in.

## What still needs rebuilding (no backend exists here)

This was a static mirror, so anything server-side is gone:

- **Login / register / payment forms**: the HTML/CSS is intact, but `action` attributes were changed from `https://ataa.ma/...` to `action="#"` so they don't accidentally submit to the live site. You'll need your own backend (or a service like Firebase/Supabase, given your usual stack) to actually process these.
- **Project data**: project cards, listings, and detail pages currently show ataa's real project content hardcoded into the HTML. You'll need to template this with your own data source instead of static text.
- **Donation/payment processing**: the "add to cart" UI is real and client-side only (see below), but actually charging a card or processing a donation needs a real payment gateway integration; none exists here.

## What works out of the box (no backend needed)

- **The cart-like donation UI is fully client-side**, using `sessionStorage` under the key `ihsan_cart`. Look for `addCartToStorage`, `getCartObj`, `window.updateCart` in the page `<script>` blocks — that's the logic for adding/removing donation items and updating the cart count badge. This will work immediately on a new site, no server required.
- **All CSS styling, Bootstrap 5 theme, RTL (Arabic) layout, sliders, and Hijri calendar widgets** work standalone since they're pure front-end libraries.
- **Responsive nav, dropdown menus, offcanvas mobile menu** all work as-is.

## Suggested next steps

1. Open `pages/home.html` directly in a browser to sanity-check the design renders correctly with the trimmed assets.
2. Strip out ataa-specific text/links (project names, social share URLs, footer copyright) and replace with your charity's content.
3. Decide on your own color/brand palette — check `static/css/app2979.css` and `assets/css/` for the main color variables to retheme.
4. If you want the admin dashboard skin too, let me know and I'll extract `dashboard/` the same way.

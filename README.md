# Sendy Errands — marketing site

A single-page static marketing site for Sendy Errands. No build step, no
framework, no server: one `index.html` plus images.

## What's here

```
index.html           the whole site — markup, CSS and ~20 lines of JS
assets/images/       brand photography, logo badge, app mockup, avatars
assets/icons/        favicon
.nojekyll            tells GitHub Pages to serve the files as-is
```

## Running it locally

Open `index.html` in a browser, or serve the folder:

```bash
python -m http.server 8000
# then http://localhost:8000
```

## Deploying

The site is static, so anything that serves files will host it.

**GitHub Pages:** Settings → Pages → Source: *Deploy from a branch*, branch
`main`, folder `/ (root)`. To serve it on `sendyerrands.com`, add a `CNAME`
file containing `sendyerrands.com` and point the domain's DNS at GitHub Pages.
That domain currently serves the existing PHP site, so switching it is a
deliberate cutover, not something this repo does on its own.

**Anywhere else** (Vercel, Netlify, Cloudflare Pages): deploy the repo root
with no build command and no output directory.

## Scope: marketing only

This site has no login, no registration, no booking form, no order tracking
and no payment flow. Every call to action goes to WhatsApp or the phone line,
which is how bookings are actually taken — the price is agreed in chat before
a rider moves.

That is a deliberate constraint. **Don't add a control here that doesn't do
anything yet.** If a feature isn't live, either leave it off the page or label
it plainly, the way the app section says "coming soon" in text instead of
showing dead store buttons.

## Editing

Everything is in `index.html`, in source order: design tokens → base styles →
components → markup. Sections are commented and the markup matches the order
they appear on the page.

**Colours** are CSS custom properties at the top of the `<style>` block, taken
from the real brand materials — the magenta of the polo and poly-mailer, the
black tape strip across the mailer seal, the cobalt studio backdrop the rider
photography was shot on. Change a value in `:root` and it updates everywhere.

**Dark mode** is handled at token level. Each colour is declared three times:
in `:root` (light), in `@media (prefers-color-scheme: dark)` guarded by
`:root:not([data-theme="light"])`, and in `:root[data-theme="dark"]`. If you
add a colour, add it to all three blocks — a colour defined only in one of them
will break the other themes.

**Prices, phone number, hours and address** appear in more than one place
(cards, FAQ, contact, footer, and the JSON-LD block in `<head>`). Search for
the value and update each hit, including the structured data.

## Content that needs a real answer before launch

- The testimonials are placeholder copy carried over from the previous site.
  Swap in real customer quotes, or cut the section.
- `568+ errands`, `30+ riders` and the `4.6` rating are the figures from the
  previous site. Confirm they're current before publishing.

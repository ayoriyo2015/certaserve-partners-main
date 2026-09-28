# CertaServe Partners website

Marketing site for CertaServe Partners, a CPA-led business advisory firm
(buy-side, sell-side, due diligence and valuation, strategic advisory).
Live at https://certaservepartners.ca (see `CNAME`).

## Stack

- Plain static HTML + one shared stylesheet (`styles.css`). No build step, no
  package manager, no framework.
- Hosted on GitHub Pages (`.nojekyll` disables Jekyll processing).
- Contact form posts to Formspree (`contact.html`, form ID `xdkqjoqy`).

## Layout

- `index.html`, `about.html`, `services-advisory.html`, `buy-business.html`,
  `sell-business.html`, `due-diligence-valuation.html`,
  `strategic-advisory.html`, `pricing.html` ("Engagement" in the nav),
  `contact.html`: the pages.
- `styles.css`: all styling. Colours, shadows and radii are CSS variables on
  `:root`; reuse them rather than hard-coding values.
- `assets/images/`: hero and section photos.
- `thank-you.html`: Formspree redirect target after a contact form submission
  (noindex, not in the sitemap).
- `sitemap.xml`: keep in sync when pages are added, renamed or removed.
- `CHECKLIST.md`, `PRD-certaserve-website.md`, `SITEMAP.md`,
  `portal-login.html`: currently empty placeholders.

## Conventions

- Every page repeats the same header/nav (with the "Advisory Services"
  dropdown) and footer, plus an inline `toggleDropdown()` script at the bottom.
  There are no includes, so a nav or footer change must be made in every
  `.html` file. Mark the current page's nav link with `class="active"`.
- Each page needs a unique `<title>` and `<meta name="description">`.
- Use relative links between pages (`about.html`, not absolute URLs), except
  where an absolute URL is required (sitemap, Formspree redirect).
- Canadian spelling and Canadian context (CAD, Ontario). Content is
  professional advisory copy: do not invent credentials, client names,
  results, fees or testimonials.

## Previewing

```sh
python3 -m http.server 8000   # then open http://localhost:8000
```

Before committing, check that every internal link and image path resolves
(file names are case-sensitive on GitHub Pages).

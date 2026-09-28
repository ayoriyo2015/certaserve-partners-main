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

- Every page repeats the same `<head>` font links (Google Fonts: Cormorant
  Garamond for headings, Inter for body), header/nav (mobile `nav-toggle`
  button plus the "Advisory Services" dropdown), footer, and an inline script
  at the bottom (`toggleNav()`, `toggleDropdown()`, footer year). There are no
  includes, so a change to any of these must be made in every `.html` file,
  including `thank-you.html`. Page content sits inside `<main>`.
- Mark the current page's nav link with `class="active" aria-current="page"`;
  for advisory service pages, mark the dropdown item and add `active` to the
  `.dropbtn` too.
- Design: navy/ivory/gold "premium advisory" theme. Build sections from the
  existing classes (`section`, `section-light`, `section-dark`,
  `section-heading`, `feature-grid`/`feature-card`, `value-grid`,
  `process-grid`, `bullets`, `cta-panel`, `btn-primary`/`btn-outline`/
  `btn-dark`, `text-link`) and avoid inline styles.
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

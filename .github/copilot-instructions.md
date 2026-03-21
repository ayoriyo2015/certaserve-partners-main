---
name: CertaServe Partners Workspace Instructions
description: "Workspace instructions for static HTML website. Use when: editing HTML files, updating navigation/headers, modifying styles, adding pages, deploying website."
---

# CertaServe Partners Website — Workspace Instructions

**CertaServe Partners** is a static HTML website for an Ottawa-based professional services firm. The site runs on **pure static HTML** deployed to **GitHub Pages** with no build tools or backend.

---

## 🚀 Quick Start

- **Tech Stack**: HTML, CSS (no preprocessor or framework), minimal JavaScript
- **Deployment**: GitHub Pages (CNAME: certaservepartners.ca)
- **All content**: Root directory + assets/
- **CSS**: Single file: `styles.css` (~800 lines)
- **No build step**: Edit files and deploy directly

---

## 📂 Project Structure

```
certaserve-partners-main/
├── index.html                          # Homepage
├── styles.css                          # Single stylesheet (all responsive CSS here)
├── assets/
│   ├── images/                         # All images used on site
│   └── logo-*.svg                      # Logo variants
├── planning/                           # Reference/planning docs (not deployed)
├── CNAME                               # GitHub Pages custom domain
├── sitemap.xml                         # SEO sitemap
├── SITEMAP.md                          # Sitemap reference
│
├── Business Advisory Pages:
├── services-advisory.html
├── sell-business.html
├── buy-business.html
├── due-diligence-valuation.html
├── business-plans-suv.html
├── strategic-advisory.html
│
└── Legal Support Pages:
    ├── process-serving.html
    ├── court-filing.html
    ├── legal-courier.html
    ├── document-management.html
    ├── e-discovery.html
    ├── commissioner-oaths.html
    ├── about.html
    ├── contact.html
    └── pricing.html
```

**Total Pages**: 17 HTML files (all independent, no template engine)

---

## 🎯 Core Patterns & Conventions

### Navigation & Header (⚠️ Critical)

**Problem**: Header, navigation, and footer are **duplicated in every HTML file** (copy-paste pattern). This means:
- Navigation changes require editing **17 files**
- Easy to forget a file and create menu inconsistencies

**Header Structure** (identical across all pages):
```html
<header class="site-header">
  <div class="container header-inner">
    <div class="logo">
      <span class="logo-mark">C</span>
      <span class="logo-text">CertaServe<span> Partners</span></span>
    </div>

    <nav class="main-nav">
      <a href="index.html">Home</a>
      <a href="about.html">About</a>

      <div class="dropdown">
        <button class="dropbtn" type="button">Services ▾</button>
        <div class="dropdown-content">
          <div class="dropdown-title">Business Advisory & Brokerage</div>
          <a href="services-advisory.html">Advisory & Brokerage Hub</a>
          <a href="sell-business.html">Sell a Business</a>
          <a href="buy-business.html">Buy a Business</a>
          <a href="due-diligence-valuation.html">Due Diligence & Valuation</a>
          <a href="business-plans-suv.html">Business Plans (SUV)</a>
          <a href="strategic-advisory.html">Strategic Advisory</a>

          <div class="dropdown-divider"></div>

          <div class="dropdown-title">Legal Support Services</div>
          <a href="process-serving.html">Process Serving</a>
          <a href="court-filing.html">Court Filing</a>
          <a href="legal-courier.html">Legal Courier</a>
          <a href="document-management.html">Document Management</a>
          <a href="e-discovery.html">E-Discovery Support</a>
          <a href="commissioner-oaths.html">Commissioner of Oaths</a>
        </div>
      </div>

      <a href="pricing.html">Pricing</a>
      <a href="contact.html">Contact</a>
      <a href="contact.html" class="nav-cta">Request Service</a>
    </nav>
  </div>
</header>
```

**Active Page Marker** (⭐ Important):
- Add `class="active"` to the `<a>` tag for the current page in the header
- Example: On `due-diligence-valuation.html`, mark that link as active:
  ```html
  <a href="due-diligence-valuation.html" class="active">Due Diligence & Valuation</a>
  ```
- The CSS styles `.active` with an underline for visual feedback

### Footer (Standard on All Pages)

```html
<footer class="site-footer">
  <div class="container footer-inner">
    <div class="footer-section">
      <h4>CertaServe Partners</h4>
      <p>
        CPA-led firm offering business advisory, brokerage,<br />
        due diligence &amp; valuation, alongside legal support services.
      </p>
      <p class="fineprint">
        &copy; <span id="year"></span> CertaServe Partners. All rights reserved.
      </p>
    </div>

    <div class="footer-section">
      <h4>Services</h4>
      <!-- Links organized by category -->
    </div>

    <div class="footer-section">
      <h4>Contact</h4>
      <p><strong>Phone:</strong> +1-416-822-3991</p>
      <p><strong>Email:</strong> info@certaservepartners.ca</p>
    </div>
  </div>
</footer>

<script>
  document.getElementById("year").textContent = new Date().getFullYear();
</script>
```

**⚠️ Pitfall**: The `<script>` tag sets the copyright year dynamically. If you forget this script, the year will show as blank.

---

## 🎨 CSS & Styling

### Architecture
- **Single file**: `styles.css` (~800 lines)
- **CSS Variables**: Color palette, shadows, spacing
- **Component-based**: Reusable classes for cards, buttons, grids
- **Responsive**: Single breakpoint at `900px` for mobile

### CSS Variables (Color Palette)
```css
:root {
  --color-primary: #0066cc;           /* Main accent blue */
  --color-primary-dark: #004499;      /* Darker blue for hover */
  --color-primary-light: #e6f2ff;     /* Light blue background */
  
  --color-text-dark: #1a1a1a;         /* Main text */
  --color-text-light: #666;           /* Secondary text */
  --color-bg-dark: #f5f5f5;           /* Background sections */
  
  --color-success: #28a745;
  --color-warning: #ffc107;
  --color-danger: #dc3545;
  
  --shadow-soft: 0 2px 8px rgba(0,0,0,0.08);
  --shadow-card: 0 4px 12px rgba(0,0,0,0.1);
}
```

### Utility Classes

| Class | Purpose |
|-------|---------|
| `.container` | Max-width wrapper (1200px, 90% mobile) |
| `.section` | Content section with padding |
| `.section-light` | Light gray background variant |
| `.card` | White box with shadow and rounded corners |
| `.btn .btn-primary` | Primary CTA button (blue) |
| `.btn .btn-outline` | Ghost/outline button variant |
| `.grid-2`, `.grid-3` | 2/3-column layouts (single-column on mobile) |
| `.feature-grid` | Auto-layout grid for feature cards |
| `.process-steps` | Numbered process visualization |
| `.muted` | Gray secondary text |
| `.lead` | Larger intro paragraph |
| `.fineprint` | Small legal/copyright text |

### Component Examples

**Button**:
```html
<a href="contact.html" class="btn btn-primary">Book a Consultation</a>
```

**Card Grid**:
```html
<div class="grid-3">
  <div class="card">
    <h3>Service Name</h3>
    <p>Description here.</p>
  </div>
</div>
```

**Section with CTA**:
```html
<section class="section section-light">
  <div class="container">
    <h2>Section Title</h2>
    <p>Content here.</p>
    <a href="page.html" class="btn btn-primary">Action</a>
  </div>
</section>
```

### Responsive Design
- **Breakpoint**: `@media (max-width: 900px)`
- **Changes on mobile**: Grids collapse to 1 column, font sizes reduce, padding adjusts
- **Test**: Use browser DevTools at 900px and smaller

---

## 📝 Common Editing Tasks

### Task 1: Edit Page Content

1. Open the relevant `.html` file (e.g., `due-diligence-valuation.html`)
2. Update content within `<section>` blocks (don't touch header/footer)
3. Keep heading hierarchy: one `<h1>` per page
4. Use semantic HTML: `<h2>`, `<h3>`, paragraphs, lists
5. For CTAs, use: `<a href="contact.html" class="btn btn-primary">Text</a>`
6. Test links locally before deploying

### Task 2: Add a New Service Page

1. **Copy a template file**: Duplicate `due-diligence-valuation.html` (or similar service page)
2. **Update header/footer**: Leave as-is (duplicated pattern)
3. **Set `class="active"`**: Mark the new page's nav link as active
4. **Replace page title & meta**: Update `<title>` and `<meta name="description">`
5. **Update schema.org**: If it's an important page, add LegalService schema (see index.html)
6. **Use the correct heading hierarchy**: One `<h1>` with page title
7. **Update navigation on other pages**: If adding to the dropdown, edit all 17 `<header>` blocks
8. **Update sitemap.xml**: Add the new page to SEO sitemap
9. **Link correctly**: Use relative paths: `href="page.html"` (same directory)

### Task 3: Update Navigation (All 17 Pages)

⚠️ This requires editing **every HTML file**.

**Option A: Find & Replace** (Fast, requires care):
1. In VS Code, press `Ctrl+H` (Find & Replace)
2. Find the old nav link code
3. Replace with new code
4. Replace All in all files (use `*.html` includePattern)
5. Verify the 17 corrections applied

**Option B: Manual** (Safer, slower):
1. Open each HTML file
2. Find the `<header>` block
3. Update the specific `<a>` tag
4. Commit with a "Navigation update" message

### Task 4: Update Contact Link in Schema

**Location**: `index.html`, inside `<script type="application/ld+json">`

```json
{
  "telephone": "+1-416-822-3991",
  "url": "https://certaservepartners.ca"
}
```

⚠️ This only appears on the homepage. If updating phone/URL, manually update footers on pages too.

### Task 5: Add a New Image

1. Optimize image for web (compress, resize appropriately)
2. Place in `assets/images/`
3. Reference in HTML: `<img src="assets/images/my-image.jpg" alt="Description">`
4. Use descriptive alt text for accessibility and SEO

### Task 6: Modify Styles

1. Open `styles.css`
2. Find the relevant component section (they're organized by component name)
3. Update CSS rules
4. **Never use inline styles** (`style="..."`) — update the .css file
5. Test responsive behavior at the 900px breakpoint in DevTools
6. Deploy and verify in browser

---

## 🔗 Links & File Paths

### Relative Paths (All Pages Use These)
- Same directory: `href="contact.html"`
- Root: `href="index.html"` (even from nested pages, because all are in root)
- Assets: `href="assets/images/logo.svg"`

### Important: Always Test Links
Before deploying, open each edited page in a browser and click links to verify they work.

### External URLs
- Production site: `https://certaservepartners.ca`
- Contact form: Uses Formspree (configured in contact.html)

---

## 🔍 SEO & Schema

### Schema.org Structured Data
- **Homepage** has `LegalService` schema (`index.html`, `<script type="application/ld+json">`)
- **Services**: Each page should have a descriptive `<meta name="description">`
- **Sitemaps**: Maintain `sitemap.xml` when adding/removing pages

### Meta Tags (Every Page Must Have)
```html
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Page Title | CertaServe Partners</title>
<meta name="description" content="Brief 150-160 char description." />
```

### Robots & Indexing
- No `robots.txt` — all pages are indexable
- `.nojekyll` file present — prevents GitHub Pages Jekyll processing
- CNAME file handles domain routing to `certaservepartners.ca`

---

## 🚀 Deployment

### How the Site Goes Live
1. Push changes to GitHub (`main` branch)
2. GitHub Pages automatically deploys (watch Actions tab for status)
3. Changes appear at `certaservepartners.ca` (via CNAME)

### Pre-Deployment Checklist
- [ ] All pages load without 404s (test relative links)
- [ ] Navigation menu is consistent across all pages
- [ ] Active nav link is set correctly on current page
- [ ] Footer copyright script is present on all pages
- [ ] New pages are added to sitemap.xml
- [ ] Contact form (contact.html) is functional
- [ ] Responsive design tested at 900px breakpoint
- [ ] Images are optimized and paths are correct

---

## ⚠️ Common Pitfalls & Solutions

| Pitfall | Risk | Solution |
|---------|------|----------|
| Forgot to update nav on one page | Menu inconsistency across site | Use Find & Replace for nav changes across all files |
| Missing `<script>` with year in footer | Copyright shows blank | Copy footer block exactly from another page |
| Forgot `class="active"` on current page | User doesn't know which page they're on | Check every page has one `.active` class in header |
| Used absolute path instead of relative | Links break on GitHub Pages | Use `href="page.html"` not `href="/page.html"` |
| Added inline CSS instead of using classes | Hard to maintain, overrides global styles | Update styles.css and use class names |
| Didn't update sitemap.xml | Google doesn't find new pages | Add all new pages to sitemap.xml manually |
| Image paths broken (`images/logo.svg` instead of `assets/images/`) | Images don't load | Always use: `assets/images/filename` |
| Forgot footer "current year" script | Copyright shows old year | Include: `<script>` with `document.getElementById("year").textContent = new Date().getFullYear();</script>` |

---

## 📋 Reference: All 17 Pages at a Glance

| Page | File | Nav Category | Purpose |
|------|------|--------------|---------|
| Home | `index.html` | — | Homepage with hero + schema.org |
| About | `about.html` | About (top nav) | Company info |
| Advisory Hub | `services-advisory.html` | Services → Advisory | Main advisory page |
| Sell a Business | `sell-business.html` | Services → Advisory | Transaction support |
| Buy a Business | `buy-business.html` | Services → Advisory | Acquisition services |
| Due Diligence & Valuation | `due-diligence-valuation.html` | Services → Advisory | DD & valuation services |
| Business Plans (SUV) | `business-plans-suv.html` | Services → Advisory | SUV planning |
| Strategic Advisory | `strategic-advisory.html` | Services → Advisory | Strategic consulting |
| Process Serving | `process-serving.html` | Services → Legal | Legal process service |
| Court Filing | `court-filing.html` | Services → Legal | Court document filing |
| Legal Courier | `legal-courier.html` | Services → Legal | Courier services |
| Document Management | `document-management.html` | Services → Legal | Doc management |
| E-Discovery Support | `e-discovery.html` | Services → Legal | E-discovery services |
| Commissioner of Oaths | `commissioner-oaths.html` | Services → Legal | Commissioner services |
| Pricing | `pricing.html` | Top nav | Service pricing |
| Contact | `contact.html` | Top nav | Contact form (Formspree) |

---

## 💡 Tips for Efficient Editing

1. **Use VS Code Find & Replace** (`Ctrl+H`) for multi-file updates (nav, footer patterns)
2. **Open DevTools** (F12) to test responsive design and verify element visibility
3. **Use relative paths** everywhere (never absolute paths)
4. **Copy navigation from an existing page** when creating a new one — it's guaranteed correct
5. **Commit frequently** with clear messages: "Update due-diligence page content", "Fix nav link"
6. **Test on mobile** — open in browser at 900px width to verify responsive behavior

---

## Questions or Issues?

If anything is unclear:
- Check the HTML structure in an existing page (they all follow the same pattern)
- Verify CSS classes in styles.css before adding custom styles
- Test links locally before pushing to GitHub
- Use this guide as the single source of truth for project conventions

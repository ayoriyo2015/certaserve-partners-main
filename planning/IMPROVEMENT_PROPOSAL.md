# CertaServe Partners Website — Comprehensive Improvement Proposal

**Date**: March 21, 2026  
**Status**: Proposal for Review  
**Scope**: Website Architecture, UX, Content, Performance, and Marketing

---

## Executive Summary

The current CertaServe Partners website is **well-structured, clean, and functional** for static content delivery. However, it faces **maintainability challenges** and **missing features** that could improve user engagement, conversion, and market positioning.

This proposal identifies **8 key improvement areas** with prioritized recommendations, cost-benefit analysis, and a phased implementation roadmap.

---

## 1. Architecture & Maintainability 🏗️

### Current State
- **Pure static HTML** with duplicated header/footer/nav across 17 files
- **Single CSS file** (~800 lines, well-organized)
- **No template engine** — editing navigation requires manual updates to every page
- **GitHub Pages deployment** with CNAME for custom domain

### Problems
| Issue | Impact | Severity |
|-------|--------|----------|
| Navigation changes require editing 17 files | High risk of inconsistencies | **HIGH** |
| Duplicated footer script on every page | Risk of missing copyright year on some pages | **MEDIUM** |
| No centralized header/nav management | Scalability breaks above ~20 pages | **HIGH** |
| No component reuse system | Difficult to maintain consistent patterns | **MEDIUM** |

### Recommendations

#### **Option A: Migrate to Static Site Generator (SSG)** ⭐ Recommended
**Tools**: Hugo, Eleventy (11ty), Jekyll, or Astro

**Pros:**
- ✅ Single source of truth for header/footer
- ✅ Template inheritance for page layouts
- ✅ Automatic sitemap generation
- ✅ Built-in image optimization
- ✅ Component-based architecture
- ✅ Still deploys to GitHub Pages (zero cost)
- ✅ Faster development & fewer bugs

**Cons:**
- ⚠️ Requires build step (`npm run build`)
- ⚠️ Learning curve for team members
- ⚠️ Requires refactoring all 17 pages (4-6 hours one-time)
- ⚠️ More complex local development setup

**Implementation Timeline**: 1-2 weeks  
**Cost**: Free (open source)  
**ROI**: High — saves ~30 minutes per nav change, better maintenance long-term

**Recommended Stack**: **Eleventy (11ty)** with Nunjucks templates
- Zero-config, minimal learning curve
- Supports HTML/Nunjucks for templates
- Fast builds, excellent documentation

---

#### **Option B: Keep Static HTML + Document Patterns** ⭐ Low-effort interim
**If not ready for SSG migration**

**Improvements:**
- Add a `.github/EDIT_GUIDE.md` with Find & Replace instructions
- Create a `_header.html` and `_footer.html` reference files
- Add pre-commit hook to validate header/footer consistency
- Document active nav link requirements

**Pros:**
- ✅ Zero learning curve
- ✅ No build step changes
- ✅ Easier to implement immediately

**Cons:**
- ⚠️ Still requires manual updates across 17 files
- ⚠️ Doesn't solve the core problem

**Implementation Timeline**: 1 day  
**Cost**: Free  
**ROI**: Low — temporary solution, still error-prone

---

### Recommendation
**Short-term**: Use Option B for next 2-3 months  
**Long-term**: Plan SSG migration (Eleventy) for Q2 2026

---

## 2. Content Strategy & Information Architecture 📝

### Current State
- 17 pages covering advisory & legal services
- Service pages are descriptive but lack depth
- No blog/resource center
- Limited case studies or client testimonials
- Portal login page exists but isn't integrated with main content

### Problems
- **Missing content types** that drive SEO and lead generation
- **No thought leadership** to establish authority
- **Limited conversion opportunities** (only "Contact" CTA)
- **Service pages lack specificity** for different buyer personas

### Recommendations

#### **1. Add Service-Specific Resource Pages**

Create detailed resource hubs for top services:
- **Due Diligence & Valuation Guide** (long-form, downloadable PDF)
- **Mergers & Acquisitions Checklist**
- **Due Diligence Cost Calculator** (interactive tool)
- **Business Valuation Methods Explained** (educational)

**Benefits:**
- ✅ Improves SEO (long-tail keywords, backlink potential)
- ✅ Establishes expertise
- ✅ Captures leads via downloadable resources
- ✅ Better Google SERP ranking

**Timeline**: 2-3 weeks (requires SME input)  
**Effort**: Medium (content creation + design)

---

#### **2. Add Testimonials/Case Studies Section**

Create a dedicated "Success Stories" or "Client Results" page.

**Components:**
- 4-6 anonymized case studies (1-2 paragraphs each)
- Client logos/industry sectors
- Results metrics (timeline saved, valuation accuracy, etc.)
- CTAs to similar service pages

**Benefits:**
- ✅ Builds trust and credibility
- ✅ Social proof improves conversion
- ✅ Differentiates from competitors

**Timeline**: 1-2 weeks (interviews + writing)  
**Effort**: Medium

---

#### **3. Add Blog/Resource Hub** (Optional)

**Consider if**: You have regular content from CPAs/advisors

**Benefits:**
- ✅ Weekly/monthly content for SEO
- ✅ Authority signaling
- ✅ Email list building
- ✅ Social media content

**Challenges:**
- ⚠️ Requires SSG migration (or external blog tool like Medium)
- ⚠️ Ongoing content commitment (4-8 posts/month)
- ⚠️ Moderation/updating needs

**Alternative**: Link to LinkedIn articles instead (lower effort)

---

### Recommendation
**Priority 1** (Do this month): Add 3 Service Resource Pages + Testimonials  
**Priority 2** (Next quarter): Blog/Resource Hub (if content capacity exists)

---

## 3. SEO & Structured Data 🔍

### Current State
- Homepage has `LegalService` schema.org markup
- Pages have descriptive meta tags
- sitemap.xml maintained manually
- No schema on service pages
- No local business schema despite Ottawa location

### Problems
- **Limited schema coverage** (only homepage has structured data)
- **Mobile-unfriendly meta tags** (no Open Graph for social sharing)
- **No local SEO signals** (no local business schema, address, hours)
- **Manual sitemap maintenance** (error-prone)

### Recommendations

#### **1. Expand Structured Data**

Add schema to all service pages:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "LocalBusiness",
  "name": "CertaServe Partners",
  "address": {
    "@type": "PostalAddress",
    "addressLocality": "Ottawa",
    "addressRegion": "Ontario",
    "postalCode": "[AREA_CODE]",
    "addressCountry": "CA"
  },
  "geo": {
    "@type": "GeoCoordinates",
    "latitude": 45.4215,
    "longitude": -75.6972
  },
  "telephone": "+1-416-822-3991",
  "openingHoursSpecification": {
    "@type": "OpeningHoursSpecification",
    "dayOfWeek": "Monday",
    "opens": "09:00",
    "closes": "17:00"
  }
}
</script>
```

**Benefits:**
- ✅ Better Google knowledge panel
- ✅ Improved local search rankings
- ✅ Rich snippets in SERPs
- ✅ Voice search compatibility

**Timeline**: 3-4 hours  
**Effort**: Low (copy-paste + customize)

---

#### **2. Add Open Graph Meta Tags**

Enable rich previews on LinkedIn, Twitter, Facebook:

```html
<meta property="og:title" content="Page Title">
<meta property="og:description" content="Description">
<meta property="og:image" content="https://certaservepartners.ca/assets/images/og-image.jpg">
<meta property="og:url" content="https://certaservepartners.ca/page">
```

**Benefits:**
- ✅ Better social sharing appearance
- ✅ Increased click-through on social
- ✅ Professional branding

**Timeline**: 2 hours  
**Effort**: Low

---

#### **3. Set Business Hours & Address**

Add to footer and schema (if office-based):

```html
<p><strong>Address:</strong> [Office Address], Ottawa, ON</p>
<p><strong>Hours:</strong> Mon–Fri, 9AM–5PM EST</p>
```

**Timeline**: 1 hour (if info available)  
**Effort**: Minimal

---

### Recommendation
Implement all three (2-4 hours total effort). High ROI for local SEO.

---

## 4. User Experience & Conversion 💻

### Current State
- Clean, minimalist design
- Responsive layout (900px breakpoint)
- Dropdown navigation works via CSS
- Single primary CTA: "Request Service"
- Contact form uses Formspree

### Problems
- **Mobile nav dropdowns** hard to use on touchscreen
- **Limited conversion funnels** (only contact form)
- **No sticky CTA** above fold
- **Service pages lack urgency** (no pricing preview, no clear next steps)
- **Portal login page** disconnected from main site
- **Form doesn't qualify leads** (no fields asking about need/budget)

### Recommendations

#### **1. Improve Mobile Navigation** ⭐ Quick Win

**Current**: Dropdown works on hover (desktop only)  
**Issue**: Tap doesn't work well on mobile

**Solution**: Add hamburger menu for mobile

```html
<!-- Mobile menu button -->
<button class="mobile-menu-toggle" aria-label="Toggle menu">☰</button>

<!-- JavaScript to handle click -->
<script>
  document.querySelector('.mobile-menu-toggle').addEventListener('click', () => {
    document.querySelector('.main-nav').classList.toggle('open');
  });
</script>
```

**CSS to add**:
```css
@media (max-width: 768px) {
  .mobile-menu-toggle {
    display: block;
  }
  .main-nav {
    display: none;
  }
  .main-nav.open {
    display: flex;
    flex-direction: column;
  }
}
```

**Timeline**: 2-3 hours  
**Effort**: Low  
**Impact**: High (better mobile UX)

---

#### **2. Enhanced Contact Form** ⭐ Quick Win

**Current**: Formspree generic form  
**Issue**: Doesn't capture lead intent

**Improvements:**
```html
<form action="https://formspree.io/f/YOUR_KEY" method="POST">
  <input type="text" name="name" placeholder="Your Name" required />
  <input type="email" name="email" placeholder="Email" required />
  
  <!-- New: Service interest -->
  <select name="service" required>
    <option>Select Service...</option>
    <option>Due Diligence & Valuation</option>
    <option>Business Advisory</option>
    <option>Legal Support</option>
  </select>
  
  <!-- New: Timeline -->
  <select name="timeline" required>
    <option>Timeline...</option>
    <option>Within 1 month</option>
    <option>3-6 months</option>
    <option>6+ months</option>
  </select>
  
  <textarea name="message" placeholder="Tell us about your needs..."></textarea>
  <button type="submit" class="btn btn-primary">Request Consultation</button>
</form>
```

**Benefits:**
- ✅ Better lead qualification
- ✅ Targeted follow-up
- ✅ Improved conversion tracking

**Timeline**: 1-2 hours  
**Effort**: Low

---

#### **3. Add Sticky CTA Bar**

Floating button or bar at bottom of page:

```html
<div class="sticky-cta">
  <p>Ready to discuss your business goals?</p>
  <a href="contact.html" class="btn btn-primary">Schedule Consultation</a>
</div>
```

**CSS**:
```css
.sticky-cta {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  background: var(--color-primary);
  color: white;
  padding: 1rem;
  text-align: center;
  z-index: 100;
}

@media (max-width: 900px) {
  .sticky-cta {
    bottom: 56px; /* Above mobile nav if applicable */
  }
}
```

**Benefits:**
- ✅ Persistent CTA visibility
- ✅ Improves conversion rate
- ✅ Better on mobile

**Timeline**: 1 hour  
**Effort**: Low

---

#### **4. Service Page Improvements**

Each service page should have:

**Add to each service page:**
1. **Quick stats** (# of transactions, avg timeline, client satisfaction)
2. **Clear pricing tier** (e.g., "Starting at $X,000")
3. **Process steps** (visual roadmap: Discovery → Analysis → Delivery)
4. **Compare to alternatives** (DIY vs professional help)
5. **Stronger CTAs** throughout (not just at bottom)
6. **FAQ section** (address buyer objections)

**Example structure**:
```html
<section class="service-overview">
  <h1>Service Name</h1>
  <div class="service-stats">
    <div>50+ Transactions</div>
    <div>6-12 Week Timeline</div>
    <div>98% Satisfaction</div>
  </div>
</section>

<section class="process-steps">
  <h2>Our Process</h2>
  <!-- Visual steps -->
</section>

<section class="pricing-preview">
  <h2>Pricing</h2>
  <p>Starting at $X,000</p>
  <a href="pricing.html">View Full Pricing →</a>
</section>

<section class="faq">
  <h2>Frequently Asked Questions</h2>
  <!-- Accordion with Q&A -->
</section>
```

**Timeline**: 4-6 hours (across all service pages)  
**Effort**: Medium

---

### Recommendation
**Priority 1** (Do this week): Mobile nav + Form improvements + Sticky CTA (4-5 hours)  
**Priority 2** (Next 2 weeks): Service page enhancements (4-6 hours)

---

## 5. Performance & Technical SEO 🚀

### Current State
- Fast load times (static HTML)
- Single CSS file (efficient)
- No image optimization mentioned
- Basic responsive design

### Problems
- **No image compression** (if images are large)
- **No critical CSS** (entire stylesheet loaded)
- **No lazy loading** for images
- **No caching headers** configured
- **No performance metrics** tracked (Lighthouse, Core Web Vitals)

### Recommendations

#### **1. Image Optimization**

- Use **WebP format** with JPG fallback
- Compress all images (tools: TinyPNG, Squoosh)
- Use `srcset` for responsive images

```html
<picture>
  <source srcset="image.webp" type="image/webp" />
  <source srcset="image.jpg" type="image/jpeg" />
  <img src="image.jpg" alt="Description" />
</picture>
```

**Timeline**: 2-3 hours  
**Effort**: Low  
**Impact**: 20-30% faster image load

---

#### **2. Add Caching Headers (GitHub Pages)**

Via `.github/workflows/deploy.yml`:

```yaml
- name: Set Cache-Control headers
  run: |
    find ./dist -type f -name "*.html" -exec curl -H "Cache-Control: public, max-age=300" {} \;
```

**Timeline**: 1 hour  
**Effort**: Low

---

#### **3. Lazy Load Images**

Add `loading="lazy"` to below-fold images:

```html
<img src="image.jpg" alt="Description" loading="lazy" />
```

**Timeline**: 1 hour  
**Effort**: Low

---

#### **4. Monitor Performance**

Set up **Google Lighthouse CI** to track metrics:

```yaml
# .github/workflows/lighthouse.yml
- uses: treosh/lighthouse-ci-action@v9
  with:
    configPath: './lighthouserc.json'
```

**Benefits:**
- ✅ Catch performance regressions
- ✅ Track Core Web Vitals
- ✅ Data-driven optimization

**Timeline**: 2 hours  
**Effort**: Medium (one-time setup)

---

### Recommendation
Implement image optimization + lazy loading immediately (3 hours). Monitor with Lighthouse CI.

---

## 6. Analytics & Conversion Tracking 📊

### Current State
- No Google Analytics (or not mentioned)
- No conversion tracking
- No event logging
- No A/B testing infrastructure

### Problems
- **No visibility into user behavior**
- **Can't measure conversion funnel**
- **No ROI tracking for marketing**
- **Can't optimize based on data**

### Recommendations

#### **1. Add Google Analytics 4**

```html
<!-- Add to <head> on all pages -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

**Track**:
- Page views
- Scroll depth
- Contact form submissions
- External link clicks
- Service page interest

**Timeline**: 1 hour  
**Effort**: Low  
**Cost**: Free

---

#### **2. Set Up Conversion Goals**

In Google Analytics, define:
- "Contact Form Submission" (goal)
- "Downloaded Resource" (goal)
- "Service Page Visit" (event)
- "Chat Started" (if applicable)

**Benefits:**
- ✅ Measure ROI
- ✅ Identify top-performing pages
- ✅ Optimize based on data

**Timeline**: 1 hour  
**Effort**: Low

---

#### **3. Integrate with CRM** (Optional)

If using HubSpot, Salesforce, etc.:

```html
<!-- HubSpot example -->
<script>
  hbspt.forms.create({
    portalId: 'XXXXXXX',
    formId: 'XXXXXXX'
  });
</script>
```

**Benefits:**
- ✅ Auto-sync leads
- ✅ Sales visibility
- ✅ Nurture workflows

**Timeline**: 2-3 hours  
**Effort**: Medium

---

### Recommendation
Add Google Analytics 4 + basic conversion tracking (1-2 hours). Integrate CRM if sales team is ready.

---

## 7. Accessibility & Compliance ♿

### Current State
- Basic semantic HTML (`<header>`, `<footer>`, `<nav>`, `<section>`)
- Alt text on images (assumes present)
- Responsive design
- No accessibility audit

### Problems
- **Unknown WCAG compliance** (2.1 A/AA?)
- **Color contrast** may fail on some elements
- **Keyboard navigation** untested
- **Form labels** may not be properly associated
- **No skip links** for keyboard users
- **Dropdown menu** not keyboard accessible

### Recommendations

#### **1. Accessibility Audit**

Use free tools:
- **WAVE** (browser extension)
- **Axe DevTools** (browser extension)
- **Lighthouse** (built into Chrome DevTools)

**Timeline**: 2 hours  
**Effort**: Low

---

#### **2. Fix Critical Issues**

Likely issues:
- **Color contrast**: Ensure text/background contrast ≥ 4.5:1
- **Keyboard nav**: Test Tab key navigation
- **Form labels**: `<label for="id">` must match input ID
- **Dropdown accessible**: Add `aria-expanded`, `role="menu"`
- **Skip link**: Add "Skip to main content" link at top

```html
<a href="#main-content" class="skip-link">Skip to main content</a>
<main id="main-content">
  <!-- Page content -->
</main>
```

```css
.skip-link {
  position: absolute;
  top: -40px;
  left: 0;
  background: #000;
  color: white;
  padding: 8px;
  z-index: 100;
}

.skip-link:focus {
  top: 0;
}
```

**Timeline**: 3-4 hours  
**Effort**: Medium

---

#### **3. Test with Screen Reader**

Use NVDA (Windows, free) or JAWS to verify:
- Page structure readability
- Form field labels
- Button/link purposes
- Image alt text

**Timeline**: 2 hours  
**Effort**: Low (one-time)

---

### Recommendation
Do accessibility audit + fix critical issues (5-6 hours total). Aim for WCAG 2.1 AA compliance.

---

## 8. Marketing & Brand Position 📢

### Current State
- Clean, professional website
- Clear service categorization
- Professional branding (logo, colors)
- No visible marketing differentiators

### Problems
- **No unique value proposition** emphasized
- **No credibility signals** (team bios, certifications)
- **Limited trust-building** (no testimonials, no awards)
- **No content marketing** presence
- **Weak competitive differentiation**

### Recommendations

#### **1. Add Team/Leadership Page**

Create `team.html` with:
- **Founder/Principal** (photo, bio, credentials)
- **Team members** (role, expertise, LinkedIn)
- **Certifications** (CPA, CFA, etc.)

```html
<div class="team-grid">
  <div class="team-member">
    <img src="assets/images/person.jpg" alt="Name">
    <h3>Name, CPA, CA</h3>
    <p>Principal Advisor</p>
    <p>10+ years in M&A</p>
    <a href="#">LinkedIn →</a>
  </div>
</div>
```

**Benefits:**
- ✅ Builds trust and credibility
- ✅ Personal connection
- ✅ Highlights expertise

**Timeline**: 2-3 weeks (photos, bios)  
**Effort**: Medium

---

#### **2. Add Logo to Navigation**

Make logo clickable and **differentiate** it visually:

```html
<a href="index.html" class="logo">
  <span class="logo-mark">C</span>
  <span class="logo-text">CertaServe<span> Partners</span></span>
</a>
```

**Benefits:**
- ✅ Standard UX (users expect clickable logo)
- ✅ Better brand visibility

**Timeline**: 1 hour  
**Effort**: Low (likely already done)

---

#### **3. Add "Why CertaServe?" Page**

Create value proposition page highlighting:
- **Unique approach** (CPA-led vs traditional consultants)
- **Success metrics** (# of deals, success rate)
- **Industry expertise** (sectors served)
- **Client testimonials** alongside

**Timeline**: 1-2 weeks  
**Effort**: Medium

---

#### **4. Social Proof Integration**

Add **Google Reviews widget** or **client logos**:

```html
<section class="social-proof">
  <h2>Trusted by Leading Businesses</h2>
  <div class="client-logos">
    <img src="logo1.png" alt="Client 1">
    <img src="logo2.png" alt="Client 2">
    <!-- etc -->
  </div>
</section>
```

**Timeline**: 1-2 hours (if logos available)  
**Effort**: Low

---

### Recommendation
**Priority 1**: Add team bios + LinkedIn links (2-3 weeks, drives credibility)  
**Priority 2**: Add "Why CertaServe?" page (1-2 weeks, clarifies differentiation)

---

## Implementation Roadmap 🗓️

### **Phase 1: Quick Wins (Week 1-2)** ⚡
*Low effort, high impact*

- [ ] Enhanced contact form (lead qualification fields)
- [ ] Mobile navigation improvements
- [ ] Sticky CTA bar
- [ ] Google Analytics 4 setup
- [ ] SEO schema expansion (local business)
- [ ] Image lazy loading
- [ ] Accessibility audit

**Effort**: 10-12 hours  
**Expected Impact**: 15-25% improvement in conversions

---

### **Phase 2: Content & Experience (Week 3-6)** 📝
*Medium effort, sustained impact*

- [ ] Add service resource pages (3 pages)
- [ ] Testimonials/case studies page
- [ ] Service page enhancements (6 service pages)
- [ ] Accessibility fixes (WCAG 2.1 AA)
- [ ] Image optimization (WebP, compression)
- [ ] Lighthouse CI setup

**Effort**: 15-18 hours  
**Expected Impact**: 20-30% improvement in engagement metrics

---

### **Phase 3: Infrastructure (Month 2) 🏗️
*Higher effort, long-term value*

- [ ] Migrate to Eleventy (SSG)
- [ ] Add team/leadership page
- [ ] Add "Why CertaServe?" page
- [ ] Set up blog infrastructure
- [ ] Implement CRM integration

**Effort**: 30-40 hours  
**Expected Impact**: 50% reduction in maintenance time, better scalability

---

## Success Metrics 📈

Track these metrics post-implementation:

| Metric | Target | Timeline |
|--------|--------|----------|
| **Page Load Time** (Lighthouse) | <3s | Week 1-2 |
| **Mobile Usability** (no errors) | 100% | Week 1-2 |
| **Contact Form Submissions** | +30% | Month 1 |
| **Google Organic Traffic** | +25% | Month 2-3 |
| **Time on Page** (service pages) | +40% | Month 1-2 |
| **Bounce Rate** (homepage) | -15% | Month 1-2 |
| **WCAG Compliance** | 2.1 AA | Week 4-6 |
| **Maintenance Time** (nav changes) | -70% (post-SSG) | Month 2 |

---

## Cost-Benefit Summary 💰

### Quick Wins (Phase 1)
- **Cost**: Free (internal labor 10-12 hours)
- **Benefit**: 15-25% conversion lift, better UX
- **ROI**: **Immediate** (start in 1-2 weeks)

### Content Enhancements (Phase 2)
- **Cost**: Free (internal labor 15-18 hours + SME time)
- **Benefit**: 20-30% engagement improvement, stronger SEO
- **ROI**: **High** (3-6 month payback)

### Infrastructure Modernization (Phase 3)
- **Cost**: Free (internal labor 30-40 hours, one-time)
- **Benefit**: 50% faster maintenance, better scalability, improved team productivity
- **ROI**: **Very High** (long-term, 12+ month horizon)

---

## Risks & Mitigation

| Risk | Mitigation |
|------|-----------|
| **SSG migration breaks links** | Set up automated redirects, test thoroughly before go-live |
| **Lost traffic during migration** | Use DNS failover, test staging site extensively |
| **Team unfamiliar with new tools** | Training session, documentation, gradual rollout |
| **Performance regression** | Lighthouse CI monitors regressions, rollback procedure |
| **Form misconfiguration** | Test on staging, verify Formspree integration before deploy |

---

## Conclusion

The CertaServe Partners website is a **solid foundation** but has significant growth opportunities:

1. **Immediate** (2 weeks): Focus on UX/conversion improvements (quick wins)
2. **Short-term** (1-2 months): Enhance content and SEO signals
3. **Long-term** (quarter 2): Plan SSG migration for scalability

**Expected Outcomes**:
- ✅ 30-50% increase in lead generation
- ✅ Improved user experience (mobile, forms, CTAs)
- ✅ 70% reduction in maintenance burden
- ✅ Better SEO positioning and organic traffic
- ✅ Enhanced credibility and trust signals

---

## Questions for Stakeholders

Before implementation, clarify:

1. **Team bandwidth**: How many hours/week can be allocated?
2. **Budget**: Any budget for tools, design, or content creation?
3. **Timeline**: When do you need improvements to be live?
4. **Priorities**: Which improvements matter most to business?
5. **Content**: Can team provide testimonials, case studies, team bios?
6. **Technical**: Is team comfortable with SSG migration, or prefer to stay static?
7. **Analytics**: Are you currently tracking conversions? Which metrics matter most?

---

## Appendix: Tool Recommendations

### Static Site Generators
- **Eleventy (11ty)**: Best for HTML/CSS focus, minimal learning curve ⭐
- **Hugo**: Fastest build times, large ecosystem
- **Astro**: Modern, component-friendly, great for mixed content

### Performance Tools
- **TinyPNG/Squoosh**: Image compression
- **Lighthouse**: Performance audits (free, built-in)
- **WebPageTest**: In-depth performance analysis

### Analytics
- **Google Analytics 4**: Free, comprehensive
- **Hotjar**: Heatmaps, session recording (paid)
- **Plausible**: Privacy-focused alternative (paid)

### CRM/Forms
- **Formspree**: Current (free tier sufficient)
- **HubSpot**: Full CRM + forms
- **Typeform**: Beautiful forms (higher engagement)

### Accessibility
- **WAVE**: Browser extension, free audit
- **Axe DevTools**: Comprehensive accessibility testing
- **NVDA**: Free screen reader (Windows)

---

**Document Version**: 1.0  
**Last Updated**: March 21, 2026  
**Next Review**: April 21, 2026

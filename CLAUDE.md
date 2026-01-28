# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a static HTML website for Metro TV & Appliance, a factory-authorized appliance, television, and audio repair business in Lincoln, Nebraska. The site is a multi-page informational website designed to build trust and guide customers through the repair service process.

## Technology Stack

- **HTML5**: Standard semantic HTML
- **Tailwind CSS**: Via CDN (https://cdn.tailwindcss.com) - no build process required
- **JavaScript**: Vanilla JavaScript for basic interactivity (mobile navigation, copyright year)
- **Fonts**: Google Fonts (Inter family)
- **No build tools or frameworks**: This is a pure static site

## Site Structure

The site consists of 7 HTML pages:

### Main Pages
- `index.html` - Home page with hero, trust badges, services overview, brands overview, FAQ section, and testimonials
- `services.html` - Detailed service offerings (Appliance, TV, Audio) with workflow explanation and service guarantees
- `brands.html` - List of factory-authorized brands with explanation of authorization benefits
- `about.html` - Company history, story, team profiles, and certifications
- `contact.html` - Contact information with Google Maps embed and service initiation instructions

### Legal Pages
- `privacy.html` - Privacy policy (noindex)
- `terms.html` - Terms of service (noindex)

## Design System

### Color Palette
The site uses a "Nebraska Red" theme:
- Primary red: `bg-red-600` and `bg-red-900` (headers, CTAs, accents)
- Hover states: `bg-red-700`, `text-red-300`
- Backgrounds: `bg-gray-50` (light sections), `bg-white` (cards/sections)
- Text: `text-gray-700`, `text-gray-800`, `text-red-900`

### Typography
- Font family: Inter (weights: 400, 500, 600, 700)
- Headings use bold weights with red-900 color
- Body text uses gray-700/800

### Shared Components

All pages share identical:
- **Header/Navigation**: Sticky top navigation with mobile hamburger menu, company name, links to all pages, and prominent phone number CTA
- **Footer**: Three-column layout with company info, contact details, and business hours; includes dynamic copyright year
- **Mobile Navigation**: Toggle functionality using vanilla JavaScript

## Key Business Logic

### Service Workflow Distinction
The site emphasizes two different service paths:
1. **Warranty Service (Appliance/TV)**: Customer must contact manufacturer first, request Metro TV & Appliance, then company calls customer
2. **Audio/Out-of-Warranty Service**: Customer contacts Metro TV & Appliance directly

This workflow distinction appears on both `services.html` and `contact.html`.

### Factory Authorization
A key selling point emphasized throughout the site. Benefits include:
- Exclusive manufacturer training
- Proprietary diagnostic tools
- Genuine parts access
- Warranty preservation

## Common Tasks

### Opening the Site
Simply open any HTML file in a web browser. No local server required, though one can be used:
```bash
python3 -m http.server 8000
```

### Editing Content
All content is inline within HTML files. No separate data files or CMS. To update:
1. Locate the relevant HTML file
2. Find the section by searching for heading text or section ID
3. Edit HTML directly

### Testing
- Test all pages in browser (desktop and mobile responsive)
- Verify mobile navigation toggle works
- Check all internal links navigate correctly
- Verify external links (brand URLs, Google Maps) open correctly
- Confirm phone links (`tel:402-466-9090`) work on mobile

### Consistency Checks
When modifying shared components (header, footer, navigation), update across ALL 7 HTML files:
- Navigation links and active state classes (including aria-current="page")
- Contact information (phone, email, address, hours) - NAP consistency is critical for SEO
- Footer content (including Privacy Policy and Terms of Service links)
- Skip navigation links
- Meta tags and schema markup patterns

## SEO & Performance Optimization (2026)

The site has been optimized for Google's 2026 algorithm with focus on:

### Core Files
- `robots.txt` - Crawl directives and sitemap location
- `sitemap.xml` - Complete URL list with priorities (update lastmod dates when pages change)
- `.htaccess` - Browser caching, GZIP compression, HTTPS redirect, security headers (Apache only)
- `manifest.json` - PWA manifest for mobile optimization
- `humans.txt` - Team credits

### JSON-LD Schema Markup
All pages include structured data:
- **index.html**: LocalBusiness, Organization, BreadcrumbList, FAQPage
- **Other pages**: BreadcrumbList with proper hierarchy
- Schema validates at: https://search.google.com/test/rich-results

### Core Web Vitals Optimization
- **Inline Critical CSS**: Prevents render blocking, improves LCP
- **Font Optimization**: Preconnect to Google Fonts, font-display: swap
- **JavaScript Optimization**: INP-focused with immediate visual feedback
- **Layout Shift Prevention**: Explicit dimensions, proper styling
- Target metrics: LCP < 2.5s, INP < 200ms, CLS < 0.1

### Accessibility (WCAG 2.2 Level AA)
- Skip navigation links on all pages
- ARIA labels and landmarks (aria-current, aria-expanded, aria-controls, aria-label)
- Semantic HTML (nav, main, article, section, figure, address tags)
- Proper heading hierarchy (h1, h2, h3)
- Color contrast compliance (4.5:1 ratio)
- Keyboard navigation support

### E-E-A-T Signals (Experience, Expertise, Authoritativeness, Trustworthiness)
- **Trust Badges**: BBB, Factory Authorized, Licensed & Insured, Google Reviews
- **FAQ Section**: Answers common questions, triggers rich snippets
- **Team Profiles**: Gary (Lead Technician), Gail (Service Coordinator) on about.html
- **Certifications Display**: Factory authorizations, years in business
- **Service Guarantees**: Warranty information, satisfaction promise on services.html
- **Testimonials**: Customer reviews with proper attribution

### Local SEO
- **NAP Consistency**: Name, Address, Phone exactly the same across all pages and schema
- **Geo Tags**: Lincoln, NE coordinates in meta tags
- **Google Maps Embed**: On contact.html for location signals
- **Local Schema**: areaServed includes Lincoln and Omaha
- **Google Business Profile Integration**: Ready for linking

### Meta Tags
All pages include comprehensive meta tags:
- Primary meta (title, description, keywords)
- Open Graph (Facebook/social sharing)
- Twitter Cards
- Canonical URLs
- Robots directives
- Geo tags
- Theme color for mobile browsers

## Important Constraints

- **NO SVG graphics used** (Unicode icons with aria-hidden="true" instead)
- **NO Mermaid JS used**
- **NO form submission** - Contact page is informational only (fully static)
- The "Book Repair" functionality was intentionally removed and replaced with Contact page

## Contact Information
- Phone: (402) 466-9090
- Email: service@metrotv-audiotech.com
- Address: 1107 North Cotner Blvd, Lincoln, NE 68505
- Hours: Monday-Friday 8:30 AM - 6:00 PM (Closed weekends)

## Brands Serviced
Samsung, LG, Whirlpool, GE Appliances, Sony, Electrolux, Maytag, KitchenAid, JennAir, Amana, Frigidaire, and more.

## Post-Launch Tasks

### Immediate (Required)
- [ ] Submit sitemap.xml to Google Search Console (https://search.google.com/search-console)
- [ ] Request indexing for all 7 pages
- [ ] Verify schema markup with Rich Results Test (https://search.google.com/test/rich-results)
- [ ] Run Lighthouse audits on all pages (target: 90+ all categories)
- [ ] Test accessibility with axe DevTools (target: 0 critical issues)
- [ ] Validate HTML at https://validator.w3.org/ (target: 0 errors)
- [ ] Test Core Web Vitals at https://pagespeed.web.dev/
- [ ] Verify mobile-friendly at https://search.google.com/test/mobile-friendly

### Google Business Profile Setup
- [ ] Claim/verify Google Business Profile
- [ ] Complete all profile sections (100% completion)
- [ ] Add business description with "factory-authorized" and "since 1947"
- [ ] Select categories: Appliance Repair (primary), TV Repair, Audio Equipment Repair
- [ ] Add photos (storefront, team, completed repairs)
- [ ] Enable messaging
- [ ] Request reviews from satisfied customers
- [ ] Respond to all reviews within 24 hours

### Ongoing Maintenance
- [ ] Update sitemap.xml lastmod dates when pages change
- [ ] Monitor Core Web Vitals in Google Search Console monthly
- [ ] Check for indexing issues monthly
- [ ] Add new testimonials/reviews quarterly
- [ ] Update content for freshness quarterly
- [ ] Post Google Business Profile updates weekly

## Testing Checklist

### Manual Testing
- [ ] All internal links work (7 pages)
- [ ] All external links open correctly (Google Maps, reviews)
- [ ] Phone links work on mobile (tel: protocol)
- [ ] Email links work (mailto: protocol)
- [ ] Mobile navigation toggle works
- [ ] Active page highlighting correct
- [ ] Skip navigation link appears on Tab key
- [ ] Test at multiple widths: 320px, 768px, 1024px, 1920px
- [ ] Test in Chrome, Firefox, Safari, Edge
- [ ] Keyboard navigation (Tab, Enter, Escape)
- [ ] Zoom to 200% maintains readability

### Automated Testing
- Lighthouse (per page): Performance 90+, Accessibility 95+, Best Practices 90+, SEO 95+
- axe DevTools: 0 critical issues, 0 serious issues
- HTML Validator: 0 errors, 0 warnings
- Schema Validator: Valid LocalBusiness, Organization, FAQPage, BreadcrumbList
- Mobile-Friendly Test: Passed
- PageSpeed Insights: All Core Web Vitals "Good"

## Content Updates

When updating content:
1. Update relevant HTML file(s)
2. Update sitemap.xml lastmod date for changed page
3. Test changes in browser
4. Request re-indexing in Google Search Console
5. Monitor search performance after 2-4 weeks

## Troubleshooting

### Schema Validation Errors
- Use Google Rich Results Test: https://search.google.com/test/rich-results
- Verify JSON-LD syntax (proper commas, quotes)
- Check that URLs are absolute (https://metrotv-audiotech.com/...)

### Core Web Vitals Issues
- Check .htaccess is working (browser caching, compression)
- Verify inline critical CSS loads first
- Test with throttled network in DevTools
- Use Lighthouse in incognito mode for accurate results

### Accessibility Issues
- Run axe DevTools on each page
- Check color contrast in DevTools
- Test keyboard navigation without mouse
- Verify skip links appear on Tab key focus

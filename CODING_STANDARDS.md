# Metro TV & Appliance - Coding Standards

**Version:** 1.0
**Last Updated:** 2026-01-28
**Purpose:** Establish rigorous, professional coding standards for the Metro TV & Appliance website that prioritize accessibility, semantic correctness, and trust-building.

---

## Table of Contents
1. [HTML Standards](#html-standards)
2. [CSS Standards](#css-standards)
3. [JavaScript Standards](#javascript-standards)
4. [Accessibility Standards](#accessibility-standards)
5. [Performance Standards](#performance-standards)
6. [SEO Standards](#seo-standards)
7. [Security Standards](#security-standards)
8. [Code Review Checklist](#code-review-checklist)

---

## HTML Standards

### 1.1 Document Structure

**REQUIRED** on every page:

```html
<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="[Page-specific description 150-160 chars]">
    <title>[Page Title] - Metro TV & Appliance</title>

    <!-- Preconnect to external resources -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

    <!-- Canonical URL -->
    <link rel="canonical" href="https://[domain]/[page].html">

    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>

    <!-- Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">

    <!-- Structured Data (index.html only) -->
    <script type="application/ld+json">
    {JSON-LD structured data}
    </script>
</head>
```

### 1.2 Semantic HTML

**ALWAYS use semantic HTML5 elements:**

```html
<!-- ✅ CORRECT -->
<header>
    <nav aria-label="Main navigation">
        <a href="index.html" aria-current="page">Home</a>
    </nav>
</header>

<main id="main-content">
    <article>
        <h2>Service Information</h2>
        <p>Content...</p>
    </article>
</main>

<aside aria-labelledby="trust-heading">
    <h3 id="trust-heading">Why Trust Us</h3>
</aside>

<footer>
    <p>&copy; 2026 Metro TV & Appliance</p>
</footer>

<!-- ❌ WRONG -->
<div class="header">
    <div class="nav">
        <a href="index.html">Home</a>
    </div>
</div>
```

**Semantic element usage:**

| Element | Use Case | Required Attributes |
|---------|----------|---------------------|
| `<header>` | Site/page header with logo and navigation | None |
| `<nav>` | Navigation blocks | `aria-label` |
| `<main>` | Primary page content | `id="main-content"` |
| `<article>` | Self-contained content (services, testimonials) | Optional `aria-labelledby` |
| `<section>` | Thematic grouping of content | `aria-labelledby` or `aria-label` |
| `<aside>` | Tangentially related content (trust badges, sidebars) | `aria-labelledby` or `aria-label` |
| `<footer>` | Site/page footer | None |
| `<figure>` | Content with caption (testimonials, images) | None |
| `<figcaption>` | Caption for figure | None |

### 1.3 Heading Hierarchy

**MUST maintain logical heading hierarchy:**

```html
<!-- ✅ CORRECT -->
<h1>Lincoln's Factory-Authorized Repair Experts</h1>
<section>
    <h2>Our Services</h2>
    <article>
        <h3>Appliance Repair</h3>
        <h4>Refrigerators & Freezers</h4>
    </article>
</section>

<!-- ❌ WRONG - Skips h2 -->
<h1>Main Title</h1>
<h3>Subsection</h3>

<!-- ❌ WRONG - Multiple h1 tags -->
<h1>Page Title</h1>
<h1>Section Title</h1>
```

**Rules:**
- ONE `<h1>` per page
- No skipped heading levels (h1 → h3)
- Headings convey document structure, not just styling
- Use CSS classes for styling, not heading level

### 1.4 Links and Buttons

**Links (`<a>`):**
```html
<!-- Internal link -->
<a href="services.html">Our Services</a>

<!-- External link -->
<a href="https://example.com" target="_blank" rel="noopener noreferrer">
    External Site
    <span class="sr-only">(opens in new window)</span>
</a>

<!-- Phone link -->
<a href="tel:+14024669090">(402) 466-9090</a>

<!-- Email link -->
<a href="mailto:service@metrotv-audiotech.com">service@metrotv-audiotech.com</a>

<!-- Active/current page -->
<a href="index.html" aria-current="page">Home</a>
```

**Buttons (`<button>`):**
```html
<!-- Interactive button -->
<button type="button"
        aria-label="Toggle navigation menu"
        aria-expanded="false"
        aria-controls="nav-content">
    <span aria-hidden="true">☰</span>
</button>

<!-- Form submit -->
<button type="submit">Send Message</button>

<!-- NEVER use <a> styled as button unless it navigates -->
```

**Rules:**
- Use `<a>` for navigation
- Use `<button>` for actions
- All external links: `target="_blank" rel="noopener noreferrer"`
- All external links: Include screen reader text "(opens in new window)"
- Phone/email links: Always use `tel:` and `mailto:` protocols

### 1.5 Forms

**All form inputs MUST have associated labels:**

```html
<!-- ✅ CORRECT -->
<form action="https://formspree.io/f/xyzabc" method="POST">
    <div class="form-group">
        <label for="customer-name">Name *</label>
        <input type="text"
               id="customer-name"
               name="name"
               required
               aria-required="true"
               aria-describedby="name-help">
        <span id="name-help" class="form-help">First and last name</span>
    </div>

    <button type="submit">Send Message</button>
</form>

<!-- ❌ WRONG - No label -->
<input type="text" placeholder="Name">

<!-- ❌ WRONG - Label not associated -->
<label>Name</label>
<input type="text" name="name">
```

**Form standards:**
- All inputs have explicit `<label>` with matching `for`/`id`
- Required fields marked with `required` attribute AND `aria-required="true"`
- Required fields indicated visually with `*` in label
- Error messages use `aria-describedby` to associate with input
- Submit buttons use clear action verbs ("Send Message", not "Submit")

### 1.6 Lists

**Use appropriate list elements:**

```html
<!-- Unordered list for non-sequential items -->
<ul>
    <li>Refrigerators & Freezers</li>
    <li>Washers & Dryers</li>
</ul>

<!-- Ordered list for sequential steps -->
<ol>
    <li>Contact Your Manufacturer</li>
    <li>Open a Service Claim</li>
    <li>Request Metro TV & Appliance</li>
</ol>

<!-- Definition list for key-value pairs -->
<dl>
    <dt>Phone:</dt>
    <dd>(402) 466-9090</dd>
    <dt>Email:</dt>
    <dd>service@metrotv-audiotech.com</dd>
</dl>
```

### 1.7 Images and Icons

**All images MUST have alt text:**

```html
<!-- Informative image -->
<img src="technician.jpg" alt="Certified technician repairing Samsung refrigerator">

<!-- Decorative image -->
<img src="decorative-pattern.png" alt="" role="presentation">

<!-- Logo -->
<img src="logo.png" alt="Metro TV & Appliance logo">
```

**SVG icons:**
```html
<!-- Decorative icon with adjacent text -->
<svg aria-hidden="true" class="icon">
    <use href="#calendar-icon"></use>
</svg>
<span>Since 1947</span>

<!-- Standalone icon (functional) -->
<svg aria-label="Calendar" role="img">
    <use href="#calendar-icon"></use>
</svg>
```

**Rules:**
- Decorative images: `alt=""` and `aria-hidden="true"` or `role="presentation"`
- Functional images: Descriptive alt text
- Icons with adjacent text: `aria-hidden="true"` on icon
- Unicode emoji: **NEVER USE** - replace with SVG

### 1.8 Tables (if needed)

```html
<table>
    <caption>Business Hours</caption>
    <thead>
        <tr>
            <th scope="col">Day</th>
            <th scope="col">Hours</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th scope="row">Monday-Friday</th>
            <td>8:30 AM - 6:00 PM</td>
        </tr>
    </tbody>
</table>
```

---

## CSS Standards

### 2.1 Tailwind CSS Usage

**Primary styling method: Tailwind utility classes**

```html
<!-- ✅ CORRECT -->
<div class="bg-white rounded-lg shadow-lg p-8 hover:shadow-xl transition-shadow duration-300">
    <h3 class="text-2xl font-bold text-red-900 mb-4">Service Title</h3>
</div>
```

**Custom CSS only for:**
1. Design tokens (CSS custom properties)
2. Complex animations
3. Print styles
4. Styles not available in Tailwind

### 2.2 Design Tokens

**REQUIRED: Define in every page's `<style>` block:**

```css
:root {
    /* Brand Colors */
    --color-primary-600: #dc2626;  /* red-600 */
    --color-primary-700: #b91c1c;  /* red-700 */
    --color-primary-900: #7f1d1d;  /* red-900 */
    --color-gray-50: #f9fafb;
    --color-gray-700: #374151;
    --color-gray-800: #1f2937;
    --color-gray-900: #111827;

    /* Typography */
    --font-family-base: 'Inter', sans-serif;
    --font-size-hero: clamp(2.5rem, 5vw, 3.75rem);
    --font-size-h2: clamp(1.875rem, 4vw, 2.25rem);
    --font-size-body: 1rem;
    --line-height-tight: 1.25;
    --line-height-relaxed: 1.75;

    /* Spacing */
    --spacing-section-sm: 4rem;   /* 64px / py-16 */
    --spacing-section-md: 5rem;   /* 80px / py-20 */
    --spacing-section-lg: 6rem;   /* 96px / py-24 */

    /* Shadows */
    --shadow-sm: 0 1px 2px 0 rgb(0 0 0 / 0.05);
    --shadow-md: 0 4px 6px -1px rgb(0 0 0 / 0.1);
    --shadow-lg: 0 10px 15px -3px rgb(0 0 0 / 0.1);
    --shadow-xl: 0 20px 25px -5px rgb(0 0 0 / 0.1);

    /* Transitions */
    --transition-fast: 150ms ease-in-out;
    --transition-base: 200ms ease-in-out;
    --transition-slow: 300ms ease-in-out;
}

body {
    font-family: var(--font-family-base);
}
```

### 2.3 Component Patterns

**Consistent classes for common components:**

```html
<!-- Card (service, testimonial) -->
<div class="bg-white rounded-lg shadow-lg p-8 hover:shadow-xl transition-shadow duration-300">
    <!-- Content -->
</div>

<!-- Primary CTA Button -->
<a href="#" class="inline-block bg-red-600 hover:bg-red-700 text-white text-lg font-semibold py-3 px-8 rounded-lg shadow-lg transition-colors duration-200">
    Call to Action
</a>

<!-- Secondary Button -->
<a href="#" class="inline-block bg-white hover:bg-gray-50 text-red-900 text-lg font-semibold py-3 px-8 rounded-lg border-2 border-red-900 transition-colors duration-200">
    Secondary Action
</a>

<!-- Section Container -->
<section class="py-20 bg-gray-50">
    <div class="container mx-auto px-6">
        <!-- Content -->
    </div>
</section>
```

### 2.4 Responsive Design

**Mobile-first approach with Tailwind breakpoints:**

```html
<!-- Mobile: Stack vertically, Desktop: 3 columns -->
<div class="grid grid-cols-1 md:grid-cols-3 gap-8">
    <!-- Items -->
</div>

<!-- Mobile: Full width, Desktop: Side padding -->
<div class="px-4 sm:px-6 lg:px-8">
    <!-- Content -->
</div>

<!-- Responsive text sizes -->
<h1 class="text-3xl sm:text-4xl md:text-5xl lg:text-6xl">
    Hero Title
</h1>
```

**Breakpoints:**
- `sm`: 640px (tablets portrait)
- `md`: 768px (tablets landscape)
- `lg`: 1024px (laptops)
- `xl`: 1280px (desktops)

### 2.5 Accessibility in CSS

```css
/* Skip to main content link (hidden until focused) */
.skip-link {
    position: absolute;
    top: -40px;
    left: 0;
    background: var(--color-primary-900);
    color: white;
    padding: 0.5rem 1rem;
    text-decoration: none;
    z-index: 100;
}

.skip-link:focus {
    top: 0;
}

/* Screen reader only text */
.sr-only {
    position: absolute;
    width: 1px;
    height: 1px;
    padding: 0;
    margin: -1px;
    overflow: hidden;
    clip: rect(0, 0, 0, 0);
    white-space: nowrap;
    border-width: 0;
}

/* Focus indicators */
a:focus,
button:focus,
input:focus,
textarea:focus,
select:focus {
    outline: 3px solid var(--color-primary-600);
    outline-offset: 2px;
}

/* Remove focus outline only when using mouse */
:focus:not(:focus-visible) {
    outline: none;
}

:focus-visible {
    outline: 3px solid var(--color-primary-600);
    outline-offset: 2px;
}
```

### 2.6 Print Styles

```css
@media print {
    /* Hide navigation and footer */
    header nav,
    footer {
        display: none;
    }

    /* Ensure content fits page */
    body {
        font-size: 12pt;
        line-height: 1.5;
        color: black;
        background: white;
    }

    /* Show link URLs after link text */
    a[href]:after {
        content: " (" attr(href) ")";
    }

    /* Prevent page breaks inside elements */
    article,
    section {
        page-break-inside: avoid;
    }
}
```

---

## JavaScript Standards

### 3.1 Vanilla JavaScript Only

**No frameworks or libraries except where absolutely necessary**

```javascript
// ✅ CORRECT - Modern vanilla JavaScript
document.addEventListener('DOMContentLoaded', () => {
    const navToggle = document.getElementById('nav-toggle');
    const navContent = document.getElementById('nav-content');

    if (navToggle && navContent) {
        navToggle.addEventListener('click', () => {
            const isExpanded = navToggle.getAttribute('aria-expanded') === 'true';
            navToggle.setAttribute('aria-expanded', !isExpanded);
            navContent.classList.toggle('hidden');
        });
    }
});
```

### 3.2 Progressive Enhancement

**Site must function without JavaScript**

```html
<!-- ✅ CORRECT - Works without JS -->
<nav>
    <a href="index.html">Home</a>
    <a href="services.html">Services</a>
</nav>

<!-- ❌ WRONG - Requires JS -->
<nav>
    <div onclick="navigate('index.html')">Home</div>
</nav>
```

### 3.3 Accessibility in JavaScript

```javascript
// Update ARIA attributes when toggling
function toggleMenu() {
    const button = document.getElementById('nav-toggle');
    const menu = document.getElementById('nav-content');
    const isExpanded = button.getAttribute('aria-expanded') === 'true';

    // Update ARIA state
    button.setAttribute('aria-expanded', !isExpanded);

    // Toggle visibility
    menu.classList.toggle('hidden');

    // Manage focus
    if (!isExpanded) {
        menu.querySelector('a')?.focus();
    }
}

// Trap focus within modal/menu
function trapFocus(element) {
    const focusableElements = element.querySelectorAll(
        'a[href], button:not([disabled]), input:not([disabled]), select:not([disabled]), textarea:not([disabled])'
    );
    const firstElement = focusableElements[0];
    const lastElement = focusableElements[focusableElements.length - 1];

    element.addEventListener('keydown', (e) => {
        if (e.key === 'Tab') {
            if (e.shiftKey && document.activeElement === firstElement) {
                lastElement.focus();
                e.preventDefault();
            } else if (!e.shiftKey && document.activeElement === lastElement) {
                firstElement.focus();
                e.preventDefault();
            }
        }

        if (e.key === 'Escape') {
            closeMenu();
        }
    });
}
```

### 3.4 Code Quality

```javascript
// ✅ Use const/let, never var
const API_URL = 'https://api.example.com';
let currentPage = 1;

// ✅ Use arrow functions
const calculateTotal = (items) => items.reduce((sum, item) => sum + item.price, 0);

// ✅ Use template literals
const greeting = `Welcome to ${companyName}`;

// ✅ Handle errors
try {
    const data = JSON.parse(response);
} catch (error) {
    console.error('Failed to parse response:', error);
}

// ✅ Null-safe operations
const phone = user?.contact?.phone ?? '(402) 466-9090';
```

---

## Accessibility Standards

### 4.1 WCAG 2.2 Level AA Compliance

**REQUIRED: All pages must meet WCAG 2.2 Level AA**

### 4.2 Color Contrast

**Minimum contrast ratios:**
- Normal text: 4.5:1
- Large text (18pt+): 3:1
- Interactive elements: 3:1

**Test all color combinations:**
```css
/* ✅ PASS - 7.22:1 contrast */
.text-red-900 { color: #7f1d1d; } /* on white */

/* ✅ PASS - 4.52:1 contrast */
.text-gray-700 { color: #374151; } /* on white */

/* ⚠️ VERIFY - May fail */
.text-red-200 { color: #fecaca; } /* on red-900 background */
```

**Tools:**
- WebAIM Contrast Checker: https://webaim.org/resources/contrastchecker/
- Chrome DevTools Accessibility Panel

### 4.3 Keyboard Navigation

**All interactive elements must be keyboard accessible:**

```html
<!-- ✅ Keyboard accessible -->
<button onclick="doSomething()">Click Me</button>
<a href="page.html">Go to Page</a>

<!-- ❌ NOT keyboard accessible -->
<div onclick="doSomething()">Click Me</div>
<span onclick="navigate()">Go to Page</span>
```

**Keyboard requirements:**
- Tab: Move to next interactive element
- Shift+Tab: Move to previous interactive element
- Enter: Activate links and buttons
- Space: Activate buttons, toggle checkboxes
- Escape: Close dialogs/menus
- Arrow keys: Navigate within menus/radios

### 4.4 Screen Reader Support

**ARIA landmarks:**
```html
<header role="banner">
    <nav aria-label="Main navigation" role="navigation">
        <!-- Nav items -->
    </nav>
</header>

<main role="main" id="main-content">
    <!-- Main content -->
</main>

<aside role="complementary" aria-labelledby="sidebar-heading">
    <h2 id="sidebar-heading">Related Information</h2>
</aside>

<footer role="contentinfo">
    <!-- Footer content -->
</footer>
```

**Dynamic content updates:**
```html
<!-- Announce updates to screen readers -->
<div aria-live="polite" aria-atomic="true">
    <p>Form submitted successfully!</p>
</div>

<!-- Alert for errors -->
<div role="alert" aria-live="assertive">
    <p>Error: Please fill in all required fields.</p>
</div>
```

### 4.5 Skip Navigation

**REQUIRED on every page:**
```html
<body>
    <a href="#main-content" class="skip-link">Skip to main content</a>

    <header>...</header>

    <main id="main-content" tabindex="-1">
        <!-- Main content -->
    </main>
</body>
```

---

## Performance Standards

### 5.1 Target Metrics

**Lighthouse scores (minimum):**
- Performance: 90+
- Accessibility: 95+
- Best Practices: 90+
- SEO: 95+

### 5.2 Optimization Techniques

```html
<!-- Preconnect to external domains -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<!-- Lazy load images (when images added) -->
<img src="image.jpg" alt="Description" loading="lazy">

<!-- Defer non-critical JavaScript -->
<script src="analytics.js" defer></script>

<!-- Inline critical CSS (above-the-fold) -->
<style>
    /* Critical styles here */
</style>
```

---

## SEO Standards

### 6.1 Meta Tags

**REQUIRED on every page:**
```html
<head>
    <title>Page Title - Metro TV & Appliance</title>
    <meta name="description" content="Specific 150-160 character description with keywords">
    <link rel="canonical" href="https://example.com/page.html">

    <!-- Open Graph (social sharing) -->
    <meta property="og:title" content="Page Title">
    <meta property="og:description" content="Description">
    <meta property="og:type" content="website">
    <meta property="og:url" content="https://example.com/page.html">
    <meta property="og:image" content="https://example.com/social-image.jpg">
</head>
```

### 6.2 Structured Data

**JSON-LD on homepage (index.html):**
- LocalBusiness schema
- Organization schema
- AggregateRating schema (when reviews available)

**Validation:**
- Google Rich Results Test: https://search.google.com/test/rich-results

---

## Security Standards

### 7.1 External Links

```html
<!-- ALWAYS use rel="noopener noreferrer" with target="_blank" -->
<a href="https://external.com" target="_blank" rel="noopener noreferrer">
    External Site
</a>
```

### 7.2 Forms

```html
<!-- Use HTTPS form endpoints only -->
<form action="https://formspree.io/f/xyzabc" method="POST">
    <!-- Validate on server side -->
</form>

<!-- NEVER include in HTML: -->
<!-- - API keys -->
<!-- - Passwords -->
<!-- - Private tokens -->
```

---

## Code Review Checklist

Before committing code, verify:

**HTML:**
- [ ] Valid HTML5 (W3C Validator)
- [ ] Semantic elements used correctly
- [ ] One `<h1>` per page, logical heading hierarchy
- [ ] All images have alt text
- [ ] All forms have labels
- [ ] All links have descriptive text (no "click here")

**Accessibility:**
- [ ] ARIA labels on interactive elements
- [ ] `aria-expanded` on toggles
- [ ] `aria-current="page"` on active nav links
- [ ] Skip navigation link present
- [ ] Color contrast meets WCAG AA (4.5:1)
- [ ] Keyboard accessible (test with Tab/Enter/Space/Escape)
- [ ] No Unicode emoji (use SVG instead)

**CSS:**
- [ ] Uses Tailwind utility classes
- [ ] Design tokens defined
- [ ] Consistent spacing (py-20, py-16, py-24)
- [ ] Consistent shadows (shadow-lg, shadow-md)
- [ ] Focus indicators visible
- [ ] Responsive (mobile-first)

**JavaScript:**
- [ ] Progressive enhancement (works without JS)
- [ ] ARIA attributes updated on interactions
- [ ] No console errors
- [ ] Uses modern ES6+ syntax

**SEO:**
- [ ] Meta description present
- [ ] Title tag descriptive and unique
- [ ] Canonical URL set
- [ ] Structured data valid (if applicable)

**Performance:**
- [ ] Preconnect to external domains
- [ ] Images lazy loaded (if applicable)
- [ ] Lighthouse score 90+ in all categories

**Cross-browser:**
- [ ] Tested in Chrome
- [ ] Tested in Firefox
- [ ] Tested in Safari
- [ ] Tested in Edge

**Responsive:**
- [ ] Mobile (320px-767px)
- [ ] Tablet (768px-1023px)
- [ ] Desktop (1024px+)

---

## Tools and Validation

**Required testing tools:**
1. **W3C HTML Validator**: https://validator.w3.org/
2. **axe DevTools**: Browser extension for accessibility testing
3. **WebAIM Contrast Checker**: https://webaim.org/resources/contrastchecker/
4. **Google Lighthouse**: Built into Chrome DevTools
5. **Google Rich Results Test**: https://search.google.com/test/rich-results
6. **WAVE**: https://wave.webaim.org/

**Browser DevTools:**
- Chrome DevTools: Elements > Accessibility panel
- Firefox DevTools: Accessibility Inspector
- Responsive design testing: DevTools > Toggle device toolbar

---

## Enforcement

- All code must pass automated accessibility testing (axe DevTools: 0 critical issues)
- All pages must achieve Lighthouse accessibility score of 95+
- All HTML must validate with W3C Validator
- Manual keyboard navigation testing required before deployment
- Screen reader testing recommended for major changes

---

**Last Review:** 2026-01-28
**Next Review:** Quarterly or when WCAG standards update

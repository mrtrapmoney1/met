# Metro TV & Appliance - Workflow Standards

**Version:** 1.0
**Last Updated:** 2026-01-28
**Purpose:** Define development processes, testing protocols, and deployment procedures for maintaining the Metro TV & Appliance website.

---

## Table of Contents
1. [Development Workflow](#development-workflow)
2. [File Management](#file-management)
3. [Version Control (Git)](#version-control-git)
4. [Testing Protocol](#testing-protocol)
5. [Deployment Process](#deployment-process)
6. [Maintenance Schedule](#maintenance-schedule)
7. [Emergency Procedures](#emergency-procedures)

---

## Development Workflow

### 1.1 Development Process Overview

```
1. Requirements → 2. Planning → 3. Development → 4. Testing → 5. Review → 6. Deployment → 7. Monitoring
```

### 1.2 Pre-Development Checklist

Before starting any development work:

- [ ] Review CODING_STANDARDS.md
- [ ] Review MESSAGING_STANDARDS.md
- [ ] Understand the trust-building goal
- [ ] Identify which pages will be affected
- [ ] Create a backup of current files
- [ ] Set up local testing environment

### 1.3 Development Steps

**Step 1: Create Feature Branch** (if using Git)
```bash
git checkout -b feature/add-trust-badges
```

**Step 2: Make Changes**
- Edit HTML/CSS/JS files
- Follow CODING_STANDARDS.md precisely
- Update one page at a time
- Test after each change

**Step 3: Self-Review**
- Run through Code Review Checklist (CODING_STANDARDS.md, Section 8)
- Validate HTML: https://validator.w3.org/
- Test accessibility: axe DevTools
- Check responsive design: Browser DevTools

**Step 4: Cross-Page Consistency Check**

When modifying shared components (header, footer, navigation):

```bash
# Check for consistency across all pages
grep -n "bg-red-900" *.html  # Verify header color
grep -n "402-466-9090" *.html  # Verify phone number
grep -n "1107 North Cotner Blvd" *.html  # Verify address
```

Verify manually:
- [ ] All 5 pages have identical header structure
- [ ] All 5 pages have identical footer content
- [ ] All 5 pages have identical navigation links
- [ ] Active navigation state (`aria-current="page"`) set correctly per page

**Step 5: Commit Changes** (if using Git)
```bash
git add filename.html
git commit -m "Add trust badges section to homepage

- Added BBB certification badge
- Added factory-authorized badges
- Implemented semantic HTML structure
- Added ARIA labels for accessibility
- Tested with axe DevTools (0 issues)"
```

### 1.4 Peer Review (If Team)

If working with a team:
- Submit for code review
- Reviewer uses Code Review Checklist
- Address feedback
- Re-test after changes

---

## File Management

### 2.1 File Naming Conventions

**HTML Pages:**
```
index.html          # Homepage
services.html       # Services page
brands.html         # Brands page
about.html          # About page
contact.html        # Contact page
privacy.html        # Privacy policy (new)
terms.html          # Terms of service (new)
```

**Naming rules:**
- Lowercase only
- Hyphens for multi-word files (not underscores)
- Descriptive names
- `.html` extension

**Documentation:**
```
CLAUDE.md                 # Repository guide for AI
CODING_STANDARDS.md       # HTML/CSS/JS standards
WORKFLOW_STANDARDS.md     # This file
MESSAGING_STANDARDS.md    # Trust messaging guidelines
README.md                 # Project overview (if needed)
```

**Assets (when added):**
```
/assets/
  /images/
    logo.png
    trust-badge-bbb.png
    technician-photo-1.jpg
  /icons/
    calendar.svg
    certificate.svg
```

### 2.2 Backup Strategy

**Before making changes:**
```bash
# Create backup folder with timestamp
mkdir backups/backup-2026-01-28

# Copy all HTML files to backup
cp *.html backups/backup-2026-01-28/
```

**Backup schedule:**
- Before any major changes
- Weekly automated backup (if server configured)
- Before deployment

### 2.3 File Organization

```
/met/
├── index.html
├── services.html
├── brands.html
├── about.html
├── contact.html
├── privacy.html (new)
├── terms.html (new)
├── favicon.ico
├── CLAUDE.md
├── CODING_STANDARDS.md
├── WORKFLOW_STANDARDS.md
├── MESSAGING_STANDARDS.md
├── /backups/
│   └── /backup-YYYY-MM-DD/
└── /assets/ (future)
    ├── /images/
    ├── /icons/
    └── /documents/
```

---

## Version Control (Git)

### 3.1 Git Setup (If Not Already Initialized)

```bash
# Initialize repository
cd /mnt/c/Users/metro/projects/met
git init

# Add all files
git add .

# Initial commit
git commit -m "Initial commit: Metro TV & Appliance website

- 5 HTML pages (index, services, brands, about, contact)
- Tailwind CSS via CDN
- Vanilla JavaScript for mobile navigation
- Includes CLAUDE.md documentation"
```

### 3.2 Branch Strategy

**Main branch:** `main` or `master`
- Production-ready code only
- Never commit directly to main (use feature branches)

**Feature branches:** `feature/description`
```bash
git checkout -b feature/add-trust-badges
git checkout -b fix/header-color-consistency
git checkout -b enhance/accessibility-aria-labels
```

**Naming conventions:**
- `feature/` - New features or enhancements
- `fix/` - Bug fixes
- `enhance/` - Improvements to existing features
- `docs/` - Documentation updates

### 3.3 Commit Message Standards

**Format:**
```
<type>: <subject>

<body>

<footer>
```

**Types:**
- `feat:` - New feature
- `fix:` - Bug fix
- `docs:` - Documentation changes
- `style:` - Formatting, no code change
- `refactor:` - Code restructuring
- `test:` - Adding tests
- `chore:` - Maintenance tasks

**Examples:**
```bash
git commit -m "feat: Add JSON-LD structured data to homepage

- Added LocalBusiness schema with complete business info
- Added Organization schema with founding date
- Added AggregateRating placeholder for future reviews
- Validated with Google Rich Results Test
- Improves SEO and search result appearance"

git commit -m "fix: Correct header color inconsistency

- Changed index.html header from bg-red-600 to bg-red-900
- Now matches all other pages
- Maintains brand consistency across site"

git commit -m "enhance: Improve keyboard navigation accessibility

- Added aria-expanded to mobile nav toggle
- Added aria-current to active navigation links
- Added skip navigation link
- Tested with keyboard only (Tab/Enter/Escape)
- Passes axe DevTools accessibility audit"
```

### 3.4 Merge Strategy

```bash
# Update main branch
git checkout main
git pull origin main

# Merge feature branch
git merge feature/add-trust-badges

# Delete feature branch after merge
git branch -d feature/add-trust-badges

# Push to remote
git push origin main
```

---

## Testing Protocol

### 4.1 Required Testing Phases

**Phase 1: Automated Testing**
**Phase 2: Manual Testing**
**Phase 3: Accessibility Testing**
**Phase 4: Cross-Browser Testing**
**Phase 5: User Acceptance Testing** (if applicable)

### 4.2 Phase 1: Automated Testing

**HTML Validation:**
```bash
# 1. Open W3C Validator
# https://validator.w3.org/

# 2. Upload file or validate by URL
# Target: 0 errors, 0 warnings

# 3. Fix all issues before proceeding
```

**Lighthouse Audit:**
```bash
# In Chrome DevTools:
# 1. Right-click page → Inspect
# 2. Lighthouse tab
# 3. Generate report (Mobile + Desktop)
# 4. Target scores:
#    - Performance: 90+
#    - Accessibility: 95+
#    - Best Practices: 90+
#    - SEO: 95+
```

**Accessibility Scan:**
```bash
# Using axe DevTools browser extension:
# 1. Install axe DevTools extension
# 2. Open DevTools → axe DevTools tab
# 3. Click "Scan ALL of my page"
# 4. Target: 0 critical issues, 0 serious issues
# 5. Document any moderate issues and plan fixes
```

### 4.3 Phase 2: Manual Testing

**Visual Inspection Checklist:**
- [ ] All text readable and correctly styled
- [ ] All links work and go to correct destinations
- [ ] All images display (when added)
- [ ] No broken layouts
- [ ] Colors consistent with brand (red-900, red-600, gray tones)
- [ ] Spacing consistent across sections
- [ ] Shadows consistent on cards
- [ ] Buttons styled correctly (primary vs secondary)

**Functional Testing:**
- [ ] Mobile navigation toggle works
- [ ] All navigation links navigate correctly
- [ ] Active page highlighted in navigation
- [ ] Phone links open phone dialer (on mobile)
- [ ] Email links open email client
- [ ] External links open in new tab with rel="noopener"
- [ ] Google Maps link works (Contact page)
- [ ] Contact form submits successfully (if added)

**Content Verification:**
- [ ] Phone number correct: (402) 466-9090
- [ ] Email correct: service@metrotv-audiotech.com
- [ ] Address correct: 1107 North Cotner Blvd, Lincoln, NE 68505
- [ ] Hours correct: Monday-Friday 8:30 AM - 6:00 PM
- [ ] No typos in headings or body text
- [ ] Testimonials display correctly
- [ ] Brand names spelled correctly

### 4.4 Phase 3: Accessibility Testing

**Keyboard Navigation Test:**
```
1. Start at top of page
2. Press Tab repeatedly
3. Verify:
   - All interactive elements reachable
   - Focus indicator visible
   - Logical tab order
   - Skip link appears on first Tab
4. Test interactive elements:
   - Enter activates links
   - Space activates buttons
   - Escape closes mobile menu
5. Test Shift+Tab (reverse navigation)
```

**Screen Reader Test (Optional but Recommended):**
```
Windows (NVDA):
1. Download NVDA screen reader (free)
2. Start NVDA
3. Navigate page with keyboard
4. Verify:
   - All content announced
   - Headings read in order
   - Links have descriptive text
   - Images have alt text
   - ARIA labels read correctly

Mac (VoiceOver):
1. Press Cmd+F5 to start VoiceOver
2. Use VO+Arrow keys to navigate
3. Verify same as above
```

**Color Contrast Test:**
```
1. Open WebAIM Contrast Checker
   https://webaim.org/resources/contrastchecker/
2. Test all color combinations:
   - red-900 (#7f1d1d) on white (#ffffff)
   - gray-700 (#374151) on white (#ffffff)
   - white (#ffffff) on red-600 (#dc2626)
   - red-200 (#fecaca) on red-900 (#7f1d1d)
3. Verify all pass WCAG AA (4.5:1 for text)
```

**Zoom Test:**
```
1. Zoom to 200% (Ctrl/Cmd + +)
2. Verify:
   - No horizontal scrolling
   - Text remains readable
   - Layout doesn't break
   - All content accessible
3. Test at 300% and 400% as well
```

### 4.5 Phase 4: Cross-Browser Testing

**Desktop Browsers:**
| Browser | Version | Test | Pass/Fail |
|---------|---------|------|-----------|
| Chrome | Latest | All pages functional | ☐ |
| Firefox | Latest | All pages functional | ☐ |
| Safari | Latest | All pages functional | ☐ |
| Edge | Latest | All pages functional | ☐ |

**Mobile Browsers:**
| Device | Browser | Test | Pass/Fail |
|--------|---------|------|-----------|
| iPhone | Safari | All pages functional | ☐ |
| Android | Chrome | All pages functional | ☐ |

**Responsive Testing (Chrome DevTools):**
```
1. Open DevTools → Toggle device toolbar (Ctrl+Shift+M)
2. Test breakpoints:
   - 320px (iPhone SE)
   - 375px (iPhone 12 Pro)
   - 768px (iPad portrait)
   - 1024px (iPad landscape)
   - 1280px (Desktop)
   - 1920px (Large desktop)
3. Verify:
   - Mobile navigation works
   - Images responsive (when added)
   - Text readable at all sizes
   - No horizontal overflow
```

### 4.6 Phase 5: Testing Checklist Template

Copy this checklist for each major change:

```markdown
# Testing Checklist - [Feature/Change Name] - [Date]

## Automated Testing
- [ ] HTML validated (0 errors)
- [ ] Lighthouse: Performance 90+
- [ ] Lighthouse: Accessibility 95+
- [ ] Lighthouse: Best Practices 90+
- [ ] Lighthouse: SEO 95+
- [ ] axe DevTools: 0 critical/serious issues

## Manual Testing
- [ ] Visual inspection complete
- [ ] All links work
- [ ] Mobile navigation works
- [ ] Content accurate

## Accessibility Testing
- [ ] Keyboard navigation works
- [ ] Focus indicators visible
- [ ] Color contrast passes WCAG AA
- [ ] Zoom to 200% works
- [ ] (Optional) Screen reader tested

## Cross-Browser Testing
- [ ] Chrome (latest)
- [ ] Firefox (latest)
- [ ] Safari (latest)
- [ ] Edge (latest)
- [ ] Mobile Safari
- [ ] Mobile Chrome

## Responsive Testing
- [ ] 320px (mobile)
- [ ] 768px (tablet)
- [ ] 1024px (laptop)
- [ ] 1920px (desktop)

## Issues Found
[Document any issues and their resolutions]

## Tester: [Name]
## Date: [YYYY-MM-DD]
## Status: ☐ Pass | ☐ Fail | ☐ Pass with Notes
```

---

## Deployment Process

### 5.1 Pre-Deployment Checklist

- [ ] All testing complete and passed
- [ ] Code reviewed (if team)
- [ ] Backup of current production files created
- [ ] Deployment plan documented
- [ ] Rollback plan prepared

### 5.2 Deployment Steps

**Step 1: Create Deployment Backup**
```bash
# On production server
mkdir ~/backups/pre-deploy-YYYY-MM-DD
cp /var/www/html/*.html ~/backups/pre-deploy-YYYY-MM-DD/
```

**Step 2: Upload Files**
```bash
# Via FTP/SFTP or SSH
# Upload modified files to production server
# Example using SCP:
scp index.html user@server:/var/www/html/
scp services.html user@server:/var/www/html/
```

**Step 3: Verify Deployment**
```bash
# 1. Visit live website
# 2. Test all modified pages
# 3. Verify no broken links
# 4. Check mobile navigation
# 5. Test on mobile device
```

**Step 4: Monitor**
```bash
# Check for errors in first 24 hours
# Monitor server logs
# Check for user reports
```

### 5.3 Rollback Procedure

If issues discovered after deployment:

```bash
# Restore from backup
cp ~/backups/pre-deploy-YYYY-MM-DD/*.html /var/www/html/

# Verify rollback successful
# Investigate issue
# Fix in development
# Re-test
# Re-deploy
```

### 5.4 Deployment Log Template

```markdown
# Deployment Log - [Date]

## Changes Deployed
- [ ] File 1: Brief description
- [ ] File 2: Brief description

## Testing Summary
- Automated tests: PASS
- Manual tests: PASS
- Accessibility tests: PASS
- Cross-browser tests: PASS

## Deployment Time
- Started: [YYYY-MM-DD HH:MM]
- Completed: [YYYY-MM-DD HH:MM]
- Downtime: [None / X minutes]

## Post-Deployment Verification
- [ ] Homepage loads correctly
- [ ] All pages accessible
- [ ] Mobile navigation works
- [ ] Forms functional (if applicable)
- [ ] No console errors

## Issues Encountered
[None / List issues and resolutions]

## Deployed By: [Name]
## Verified By: [Name]
```

---

## Maintenance Schedule

### 6.1 Regular Maintenance Tasks

**Daily:**
- Monitor for user-reported issues
- Check contact form submissions (if applicable)

**Weekly:**
- Review website for broken links
- Test contact form
- Check mobile navigation
- Verify business information accuracy

**Monthly:**
- Full accessibility audit with axe DevTools
- Lighthouse performance audit
- Update copyright year (if new year)
- Review and update testimonials
- Check for outdated content

**Quarterly:**
- Comprehensive cross-browser testing
- Mobile device testing
- Review and update privacy policy (if needed)
- Update CODING_STANDARDS.md if new best practices
- Review MESSAGING_STANDARDS.md for accuracy

**Annually:**
- Major content review
- Update "Since 1947" to current year span
- Review all trust elements for accuracy
- Update structured data (JSON-LD)
- Comprehensive SEO audit

### 6.2 Maintenance Checklist Template

```markdown
# Monthly Maintenance - [Month YYYY]

## Content Review
- [ ] Phone number correct: (402) 466-9090
- [ ] Email correct: service@metrotv-audiotech.com
- [ ] Address correct: 1107 North Cotner Blvd, Lincoln, NE 68505
- [ ] Hours correct: Monday-Friday 8:30 AM - 6:00 PM
- [ ] All links work (no 404s)
- [ ] Testimonials current

## Technical Review
- [ ] axe DevTools scan (0 critical issues)
- [ ] Lighthouse audit (all scores 90+)
- [ ] Mobile navigation works
- [ ] Contact form works (if applicable)
- [ ] No console errors

## Trust Elements
- [ ] Certifications up to date
- [ ] BBB link works (if applicable)
- [ ] Manufacturer badges current
- [ ] Guarantee information accurate

## Notes
[Any observations or issues to address]

## Completed By: [Name]
## Date: [YYYY-MM-DD]
```

---

## Emergency Procedures

### 7.1 Website Down

**Immediate Actions:**
1. Check server status
2. Verify DNS resolution
3. Check hosting account status
4. Contact hosting provider if needed
5. Restore from most recent backup if corrupted

**Communication:**
- Update Google Business Profile with temporary message
- Post on social media (if active)
- Set up voicemail message

### 7.2 Critical Bug Found

**Severity 1 (Critical - Site Unusable):**
1. Immediately rollback to last known good version
2. Investigate root cause
3. Fix in development
4. Test thoroughly
5. Deploy fix

**Severity 2 (High - Feature Broken):**
1. Document issue
2. Determine if immediate fix needed
3. Schedule fix within 24 hours
4. Deploy during low-traffic period

**Severity 3 (Medium - Minor Issue):**
1. Document issue
2. Add to maintenance backlog
3. Fix in next scheduled update

### 7.3 Security Issue

**If security vulnerability discovered:**
1. Immediately take site offline if actively exploited
2. Identify vulnerability
3. Apply fix
4. Scan for any compromised data
5. Update security practices
6. Document incident

### 7.4 Content Error

**Incorrect business information (phone, address, hours):**
1. **HIGH PRIORITY** - Fix immediately
2. Update all affected pages
3. Test all pages
4. Deploy ASAP
5. Verify on live site

---

## Quality Assurance

### 8.1 Definition of Done

A change is considered "done" when:
- [ ] Code follows CODING_STANDARDS.md
- [ ] Messaging follows MESSAGING_STANDARDS.md
- [ ] All automated tests pass
- [ ] All manual tests complete
- [ ] Accessibility requirements met (WCAG 2.2 AA)
- [ ] Cross-browser testing complete
- [ ] Responsive design verified
- [ ] Code reviewed (if team)
- [ ] Deployed to production
- [ ] Post-deployment verification complete
- [ ] Documentation updated

### 8.2 Quality Metrics

Track these metrics for each release:

| Metric | Target | Actual |
|--------|--------|--------|
| HTML Validation Errors | 0 | |
| Lighthouse Performance | 90+ | |
| Lighthouse Accessibility | 95+ | |
| axe Critical Issues | 0 | |
| Broken Links | 0 | |
| Browser Compatibility | 100% | |
| Mobile Responsive | 100% | |

---

## Tools Reference

**Required Tools:**
1. **Code Editor**: VS Code, Sublime Text, or similar
2. **Browser**: Chrome (primary), Firefox, Safari, Edge
3. **Version Control**: Git
4. **Validators**:
   - W3C HTML Validator: https://validator.w3.org/
   - axe DevTools: Browser extension
   - WebAIM Contrast Checker: https://webaim.org/resources/contrastchecker/
5. **Testing**:
   - Chrome Lighthouse: Built into DevTools
   - Google Rich Results Test: https://search.google.com/test/rich-results

**Optional Tools:**
1. **Screen Readers**: NVDA (Windows), VoiceOver (Mac)
2. **Link Checkers**: Broken Link Checker (online tools)
3. **Performance**: GTmetrix, WebPageTest

---

## Document History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-01-28 | Initial | Created workflow standards document |

---

**Questions or Issues?**
Document workflow process improvements and update this document quarterly.

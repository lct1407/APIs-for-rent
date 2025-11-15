---
description: Review UI components for design quality and consistency
---

Perform a comprehensive UI/UX review of components or pages.

Analyze the following aspects:

## 1. Visual Consistency

Check that components follow the design system:

```bash
# Review design tokens
cat client/src/index.css
cat client/tailwind.config.js

# Check component usage
grep -r "className=" client/src/components/
grep -r "className=" client/src/pages/
```

**Look for**:
- Consistent color usage (using CSS variables)
- Consistent spacing (using spacing scale)
- Consistent border radius
- Consistent shadows
- Consistent typography

## 2. Accessibility Audit

Check for common a11y issues:

```bash
# Check for missing alt text
grep -r "<img" client/src/ | grep -v "alt="

# Check for proper button labels
grep -r "<button" client/src/ | grep -v "aria-label"

# Check for heading hierarchy
grep -r "<h[1-6]" client/src/
```

**Verify**:
- [ ] All images have alt text
- [ ] Buttons have accessible labels
- [ ] Proper heading hierarchy (h1 → h2 → h3)
- [ ] Form inputs have labels
- [ ] Color contrast meets WCAG AA (4.5:1 for text)
- [ ] Keyboard navigation works
- [ ] Focus indicators visible

## 3. Responsive Design

Check responsive behavior:

**Test breakpoints**:
- Mobile: 375px - 640px
- Tablet: 640px - 1024px
- Desktop: 1024px+

**Common issues**:
- [ ] Text wrapping properly
- [ ] Images scaling correctly
- [ ] Layout adapts to screen size
- [ ] Touch targets at least 44x44px on mobile
- [ ] No horizontal scrolling on mobile

## 4. Dark Mode

Verify dark mode implementation:

```bash
# Check dark mode classes
grep -r "dark:" client/src/
```

**Verify**:
- [ ] All components have dark mode variants
- [ ] Text readable in dark mode
- [ ] Sufficient contrast in dark mode
- [ ] Images/icons visible in dark mode
- [ ] Borders visible in dark mode

## 5. Component Quality

Review individual components:

**Cards**:
- [ ] Proper shadow/elevation
- [ ] Consistent padding
- [ ] Clear visual hierarchy
- [ ] Hover states defined

**Buttons**:
- [ ] All variants styled consistently
- [ ] Hover/active/disabled states
- [ ] Loading states
- [ ] Proper focus indicators

**Forms**:
- [ ] Error states styled
- [ ] Success states styled
- [ ] Floating labels or proper labels
- [ ] Input validation feedback

**Tables**:
- [ ] Responsive (scroll or stack)
- [ ] Header styling
- [ ] Row hover states
- [ ] Pagination styled

## 6. Performance

Check for performance issues:

- [ ] No large image files (>200KB)
- [ ] Animations use CSS/Tailwind (not inline styles)
- [ ] No layout shifts on load
- [ ] Lazy loading for images
- [ ] Code splitting for heavy components

## 7. User Experience

**Navigation**:
- [ ] Clear active state
- [ ] Breadcrumbs if needed
- [ ] Back buttons where appropriate

**Feedback**:
- [ ] Loading states for async operations
- [ ] Success/error messages
- [ ] Toast notifications
- [ ] Progress indicators

**Empty States**:
- [ ] Helpful empty state messages
- [ ] Clear call-to-action
- [ ] Illustrations or icons

## 8. Design Trends

Check for modern design patterns:

- [ ] Appropriate use of whitespace
- [ ] Consistent icon style (Lucide)
- [ ] Smooth transitions (200-300ms)
- [ ] Micro-interactions on hover
- [ ] Gradient accents (if appropriate)
- [ ] Glass morphism effects (if appropriate)

## Output Format

Provide a report with:

### ✅ Strengths
- List what's working well
- Praise good implementations

### ⚠️ Issues Found

For each issue:
- **Severity**: Critical / High / Medium / Low
- **Component**: Which component/page
- **Issue**: Description
- **Fix**: Code example or suggestion
- **File**: Location in codebase

### 💡 Recommendations

- Design improvements
- Modern patterns to adopt
- Consistency improvements
- Accessibility enhancements

### 📊 Score

Rate each category 0-10:
- Visual Consistency: X/10
- Accessibility: X/10
- Responsive Design: X/10
- Dark Mode: X/10
- User Experience: X/10

**Overall UI/UX Score**: XX/50

### 🎯 Priority Actions

Top 3-5 things to fix immediately

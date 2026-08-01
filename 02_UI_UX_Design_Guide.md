# 02 - UI/UX Design Guide

## Designing Interfaces Humans Love and Cannot Stop Using

> Great UI is invisible. The user never thinks about the interface;
> they only think about their goal. This guide shows you how to
> build interfaces that feel like magic.

---

## Table of Contents

1. [Cognitive Psychology Foundations](#1-cognitive-psychology)
2. [Design System Architecture](#2-design-system)
3. [Layout and Visual Hierarchy](#3-layout)
4. [Color, Typography, and Spacing](#4-color-typography)
5. [Micro-Interactions and Motion](#5-micro-interactions)
6. [Accessibility - WCAG 2.2](#6-accessibility)
7. [Responsive and Adaptive Design](#7-responsive)
8. [User Feedback Loops](#8-feedback)
9. [Performance as UX](#9-performance)
10. [UI/UX Checklist](#10-checklist)

---

## 1. Cognitive Psychology Foundations

### Hick's Law
More choices = longer decision time. Limit options per screen to 5-7.
Group related actions. Use progressive disclosure.

### Fitts's Law
Larger, closer targets are faster to click.
- Primary CTA: minimum 48x48px touch target.
- Primary actions where the thumb rests (bottom on mobile).
- Destructive actions smaller and farther from primary.

### Miller's Law
Working memory holds 7 plus/minus 2 items.
- Chunk information: 555-0123, not 5550123.
- Dashboard: max 7 KPI cards without scrolling.
- Navigation: max 7 top-level items.

### Jakob's Law
Users expect your site to work like every other site they know.
- Standard patterns: hamburger menu, search icon, cart icon.
- Innovation goes in VALUE, not navigation.

### Von Restorff Effect
The item that stands out is remembered.
- ONE accent color for CTAs. Everything else neutral.

### Doherty Threshold
Response under 400ms feels instant.
- Optimistic UI updates. Skeleton screens over spinners.
- Debounce search input (300ms).

---

## 2. Design System Architecture

### Token Hierarchy (3 Layers)

    Layer 1 - Global Tokens (primitives)
      color-blue-500: #3B82F6
      space-4: 16px
      font-size-lg: 18px

    Layer 2 - Semantic Tokens (meaning)
      color-primary: {color-blue-500}
      color-danger: {color-red-500}

    Layer 3 - Component Tokens
      button-primary-bg: {color-primary}
      button-primary-radius: 8px

### Component Rules
- Every component: default, hover, active, focus, disabled states.
- Light AND dark mode.
- Keyboard navigable.
- Documented in Storybook with props table and live examples.

---

## 3. Layout and Visual Hierarchy

### Scan Patterns
- Landing pages: Z-pattern (logo top-left, CTA bottom-right).
- Content pages: F-pattern (scan top, then left column down).
- Most important element at the END of the scan path.

### 8px Grid
All spacing is a multiple of 8:
    4px (half-step), 8, 16, 24, 32, 48, 64, 96

### Hierarchy Checklist
1. Size: most important = largest.
2. Color: primary action = strongest contrast.
3. Position: key content top-left.
4. Whitespace: important elements get MORE space.
5. Typography: headings bold and larger.

---

## 4. Color, Typography, and Spacing

### Color
- Max 3 colors: Primary, Secondary, Neutral.
- Contrast: 4.5:1 text, 3:1 large text (WCAG AA).
- Never color alone for meaning (add icons/labels).
- Dark mode: dark grays (#121212, #1E1E1E), not pure black.
- Test with color blindness simulators.

### Typography
- Max 2 font families. Scale ratio: 1.25 or 1.333.
- Body: 16px min. Line height: 1.5-1.6. Line length: 60-75ch.
- Use font-weight for hierarchy, not just size.

### Spacing
- Related items: 8-16px. Unrelated: 32-48px.
- Card padding: 16-24px. Section padding: 48-96px.

---

## 5. Micro-Interactions and Motion

### 4 Parts
1. Trigger (click, hover, scroll).
2. Rules (animation, state change).
3. Feedback (visual confirmation).
4. Loops (repeat behavior, edge cases).

### Animation Rules
- Duration: 150-300ms. Never exceed 500ms.
- Easing: ease-out (enter), ease-in (exit), ease-in-out (move).
- Animate transform and opacity ONLY (GPU-accelerated).
- Respect prefers-reduced-motion.

### Essential Micro-Interactions
- Button press: scale(0.97) + shadow reduction.
- Form success: green check + subtle confetti for milestones.
- Loading: skeleton screens. Progress bars for known durations.
- Toggle: smooth slide + color transition.
- Delete: shrink + fade, remaining items slide up.

---

## 6. Accessibility - WCAG 2.2

### Keyboard
- All interactive elements focusable via Tab.
- Visible focus indicator (2px outline, high contrast).
- Logical tab order. Skip-to-content link.
- Modal traps focus. Escape closes.

### Screen Readers
- Semantic HTML: header, nav, main, section, article, footer.
- Descriptive alt text. Decorative: alt="".
- Labels on all inputs (label for="id").
- ARIA only when HTML is insufficient.
- aria-live for dynamic content.

### Visual
- Contrast: 4.5:1 text, 3:1 UI components.
- Text resizable to 200% without breakage.
- No color-only information.
- Focus visible on all interactives.

### Motor
- Touch targets: 44x44px minimum (WCAG 2.2).
- No time limits without extend option.
- No precise mouse movement required.

### Testing Tools
- axe DevTools, Lighthouse, WAVE
- NVDA (Windows), VoiceOver (Mac), TalkBack (Android)

---

## 7. Responsive and Adaptive Design

### Breakpoints
    Mobile:  320-767px
    Tablet:  768-1023px
    Desktop: 1024-1439px
    Wide:    1440px+

### Mobile-First
- Design 375px first, enhance upward.
- Touch targets 48px on mobile.
- Bottom nav for primary actions (thumb zone).
- Swipe gestures for common actions.

### Container Queries
Use container queries for component-level responsiveness.
Components adapt to their container, not the viewport.

---

## 8. User Feedback Loops

### In-App
- After key actions: "How was this?" (1-5 stars or emoji).
- Contextual: ask at the moment, not via popup later.
- NPS: quarterly, 1 question + optional text.

### Google Form Integration

    <a href="https://forms.gle/YOUR_FORM_ID"
       target="_blank" rel="noopener noreferrer"
       class="feedback-btn">
      Send Feedback
    </a>

Or embed:

    <iframe
      src="https://docs.google.com/forms/d/e/YOUR_FORM_ID/viewform?embedded=true"
      width="100%" height="600" frameborder="0">
      Loading...
    </iframe>

### Processing
- Route to shared inbox or project board.
- Categorize: Bug, Feature, UX Issue, Praise.
- Respond within 48 hours. Review weekly. Prioritize top 3.

---

## 9. Performance as UX

### Core Web Vitals

| Metric | Good | Poor |
|--------|------|------|
| LCP | < 2.5s | > 4s |
| INP | < 200ms | > 500ms |
| CLS | < 0.1 | > 0.25 |

### Optimization
- Lazy load images and below-fold content.
- WebP/AVIF images. Preload critical resources.
- Code-split JS by route. CDN for static assets.
- Minify CSS/JS/HTML. Service worker caching.

---

## 10. UI/UX Checklist

- [ ] Touch targets 48px+ on mobile
- [ ] Contrast passes WCAG AA
- [ ] Keyboard navigation works everywhere
- [ ] Screen reader tested
- [ ] Animations respect prefers-reduced-motion
- [ ] Dark mode tested
- [ ] Responsive at 320, 768, 1024, 1440px
- [ ] LCP < 2.5s, INP < 200ms, CLS < 0.1
- [ ] Error states for every form and API call
- [ ] Empty states designed
- [ ] Loading states (skeletons) for async content
- [ ] Feedback mechanism (Google Form) visible
- [ ] No color-only information
- [ ] Focus indicators visible
- [ ] Body text 16px min, 1.5 line-height, 65ch max width

---

> The best interface is the one the user never notices.
> Design for the goal, not for the screen.

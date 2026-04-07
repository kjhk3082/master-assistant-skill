---
name: ui-ux
description: "You MUST use this when designing, building, or reviewing user interfaces. Enforces design consistency, accessibility, and modern aesthetics."
---

# UI/UX Design & Implementation

Guidelines for creating high-quality, consistent user interfaces.

<HARD-GATE>
Do NOT use inline styles or hardcoded colors unless absolutely necessary. Always use the project's design system (e.g., Tailwind classes, CSS variables).
</HARD-GATE>

## Design Principles

1. **Consistency**: Follow the established design language (colors, typography, spacing)
2. **Accessibility**: Ensure sufficient contrast, semantic HTML, and keyboard navigability
3. **Responsiveness**: Design for mobile-first, then scale up to desktop
4. **Modern Aesthetics**: Prefer clean, minimalist designs with appropriate whitespace

## Implementation Checklist

- [ ] Use semantic HTML elements (`<button>`, `<nav>`, `<main>`, etc.)
- [ ] Apply consistent spacing (e.g., Tailwind's `p-4`, `m-2`)
- [ ] Ensure interactive elements have clear hover/focus states
- [ ] Check color contrast ratios for text readability
- [ ] Test layout on different screen sizes (mobile, tablet, desktop)

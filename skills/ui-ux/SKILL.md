---
name: ui-ux
description: "[EN] You MUST use this when designing, building, or reviewing user interfaces. Enforces design consistency, accessibility, and modern aesthetics. [KO] 사용자 인터페이스를 설계, 구축 또는 검토할 때 반드시 사용해야 합니다. 디자인 일관성, 접근성 및 현대적인 미학을 강제합니다."
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

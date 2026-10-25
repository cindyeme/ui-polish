---
name: ui-polish
description: "Audit, fix and polish user interfaces so they feel clear, calm, trustworthy and premium. Use when designing or building any UI screen or component (web or mobile), reviewing a screenshot, Figma frame or front-end code, or when asked why a UI looks off, cluttered or amateur and how to improve its hierarchy, alignment, spacing, color, typography, icons, labels or primary action. Includes a dedicated playbook for e-commerce product pages."
license: MIT
metadata:
  version: "1.1.0"
  category: "ui-ux-design"
---

# UI Polish

Turn a rough interface into one that feels calm, intentional and easy to use. Good UI is not decoration: every decision should make the screen easier to understand, easier to trust or easier to act on. Explain fixes in those terms, not just "it looks nicer."

Treat every screen as part of a **system**, not a single mockup. Real screens get filled with different images, long text, big numbers and missing data. A decision that only works for the sample content is a bug.

## When to use this skill

- Building a new screen or component and wanting it to look professional from the start.
- Reviewing or auditing an existing UI: screenshot, Figma frame, live page or front-end code.
- Fixing a UI that feels cluttered, unbalanced, loud, cramped or "off" without an obvious reason.

**Context-specific playbooks.** Load the matching reference when it applies:
- E-commerce product pages, product cards, add-to-cart or checkout steps → [references/product-pages.md](references/product-pages.md)

For a full, item-by-item audit of any screen, load [references/audit-checklist.md](references/audit-checklist.md).

## Workflow

1. **Understand the context.** What is the screen for, who uses it, what is the one main action, and what mood fits the brand and category? Which platform (mobile, desktop, both)?
2. **Stress-test with real content.** Swap in a very bright and a very dark image, text two or three times longer, a large number, an empty or missing state. Note what breaks.
3. **Audit** against the principles below (or the full checklist).
4. **Prioritize**: first anything that blocks understanding or the main action, then trust and clarity, then visual polish.
5. **Fix** each issue with the smallest change that solves it, and state *why* it helps the user.
6. **Go one step further.** Once the basics are clean, look for experience improvements: fewer taps, information shown at the moment it's needed, the main action always within reach.
7. **Verify** against the quality bar and re-run the stress test.

## Core principles

### 1. Design for the system, not the screenshot
- Anything placed over imagery or variable backgrounds (icons, text, buttons) must stay legible on *any* content. Give it a container (e.g. a semi-opaque or blurred circle or pill), enough contrast and a subtle outline or shadow. Never rely on the current image happening to be dark.
- Imagery across a collection should follow one visual spec (background, lighting, framing, crop) so lists and grids feel calm instead of messy. A beautiful one-off image can still be the wrong image.
- Prefer images with one clear focal point that shows the actual subject, and that feel honest for the context.

### 2. Alignment and grid
- Put every element on one layout grid with consistent outer margins (e.g. 16–24px on mobile).
- Text, icons, numbers, badges and buttons share the same edges unless there is a deliberate reason not to. Users rarely notice misalignment consciously, but they feel it as less structured and less trustworthy.

### 3. Spacing
- Use spacing to express relationships: related items close together, separate groups further apart.
- Use a consistent spacing scale (4 or 8px based). Too much space in the wrong place makes a layout feel disconnected; too little makes it cramped. Good spacing is about the right relationships, not simply more white space.

### 4. Color
- Color supports the content; it never competes with it. Prefer a restrained palette that fits the product's mood.
- Reserve strong or saturated color for what matters most, usually the primary action and key status. When many elements are bright, nothing stands out and hierarchy collapses.
- Use additional colors only with intent (status, categories), never decoration-by-default.

### 5. Typography
- One strong font family is usually enough. Build hierarchy with **size, weight, color and line height**, not more typefaces.
- **Headings** are clear and scannable; they stand out without shouting. Balance size and weight against the rest of the scale.
- **Body text** gets generous line height (about 1.5× the font size) and slightly lower contrast than headings, while still meeting WCAG AA. Headlines attract attention; paragraphs support understanding.
- **Small uppercase labels** get some letter spacing (about 0.05–0.1em) so they breathe.

### 6. Labels, badges and copy economy
- Badges and tags must be readable in a glance: one short phrase, no redundant words, no decorative icon. "20% off", not "20% off discount" plus an icon.
- Remove labels the content already makes obvious (e.g. "Price:" before "$12.00", "Email:" inside an email-shaped field that already has a placeholder and an icon).
- Be consistent: if you label one element, its neighbors need labels too. Needing to label everything is often a sign none of it needs labels.

### 7. Information placement
- Put information where the user needs it at that moment of the decision. Trust signals (ratings, reviews, verification) go next to the thing being judged, not far below it.
- The first screen should answer the user's key questions together. For a product: what is it, can I trust it, what does it cost. For a dashboard: what's the status, what changed, what needs my attention.
- Names and titles describe the thing itself. Values the user can change (quantity, size, date range) live with their controls, otherwise the title becomes misleading.

### 8. Icons and supporting elements
- All icons in a set share one style (all outlined or all filled), one stroke weight and one color logic. Mixed heavy and light, filled and outlined icons look accidental.
- Supporting sections (feature lists, benefits, metadata) inform; they shouldn't dominate. Restrain their color and tighten their spacing.
- **Dividers** are light and subtle (a low-contrast hairline) or replaced by spacing. Heavy dark dividers chop the page into harsh blocks; small details like this are often what make an interface feel premium.

### 9. The primary action
- There is one primary action per screen, and it is the most prominent element: clear accent color, appropriate size, **sentence case**, not ALL CAPS. Prominent, but refined rather than aggressive.
- Inputs that feed the action sit right next to it, in the order users use them (choose, then confirm).
- Show the consequence before the click: the total, the recipient, the date, what will happen. Removing uncertainty increases confidence.
- On long scrolling screens, consider keeping the primary action reachable (sticky bar) so users can act whenever they're ready, not only at the top or bottom.

## Output format

When **auditing**, return:
1. A one-line verdict naming the screen's biggest problem.
2. A numbered list of issues, most impactful first. For each: what's wrong → why it hurts the user or the business → the specific fix, with concrete values (spacing, sizes, colors, copy) where possible.
3. Optional experience improvements, clearly separated from fixes.

When **building or redesigning**, produce the UI (code or design), then a short list of key decisions and the principle each follows. Use realistic placeholder content and test it against the stress cases.

## Quality bar

Before finishing, confirm:
- [ ] Elements over imagery are legible on light, dark and busy content.
- [ ] Everything sits on one grid with consistent margins and a spacing scale.
- [ ] One font family; hierarchy comes from size, weight, color and line height.
- [ ] Only the primary action and key status use strong color.
- [ ] Icons share one style, weight and color logic; dividers are subtle.
- [ ] No redundant labels; badges are one short phrase.
- [ ] The first screen answers the user's key questions together.
- [ ] The primary action is clear, refined, next to its inputs and shows its consequence.
- [ ] The design still works with long, missing and unusual content.

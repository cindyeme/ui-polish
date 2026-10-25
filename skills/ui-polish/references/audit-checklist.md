# UI Audit Checklist

Use for a full review of any screen. Each check has a test, the common failure and the fix. Report failures most-impactful first, not in this order. For product pages, also run the commerce checks in [product-pages.md](product-pages.md).

## A. Visual system

### 1. Elements over imagery
- **Test:** Swap the image or background for a very bright one and a busy one. Are overlaid icons, text and buttons still clearly visible?
- **Common failure:** They sit directly on the image and only work because the sample is dark.
- **Fix:** Container behind each element (e.g. 40px circle, white at ~80–90% opacity or blurred backdrop), contrast of at least 3:1 for icons and 4.5:1 for text, plus a 1px subtle outline or soft shadow.

### 2. Imagery consistency
- **Test:** Place the image next to others from the same collection. Do they share background, lighting, framing and crop? Does each have one clear focal point showing the real subject?
- **Common failures:** Busy frame with no focal point; props or hands stealing focus; artificial backgrounds; each image styled differently.
- **Fix:** Define an image spec and apply it to everything; choose the version that fits the system, not the prettiest standalone shot.

### 3. Alignment
- **Test:** Draw vertical lines at the content edges. Does every element start and end on them?
- **Common failure:** Elements a few pixels off; inconsistent margins between sections.
- **Fix:** One content margin (e.g. 24px mobile) and a column grid; snap every element to it.

### 4. Color
- **Test:** Squint at the screen. Does the eye land on the content and the primary action, or is it pulled in many directions?
- **Common failure:** Bright, saturated colors on secondary elements; too many accents.
- **Fix:** Restrained palette suited to the mood; one accent reserved for the primary action and key status.

### 5. Typography
- **Test:** Count font families and styles. Is hierarchy clear from size and weight alone?
- **Common failure:** Several fonts or inconsistent styles.
- **Fix:** One family (a clean sans such as Lato, Inter or similar); a small type scale; hierarchy via size, weight, color and line height.

## B. Content hierarchy

### 6. Labels and badges
- **Test:** Can each badge be read in under a second? Do small uppercase labels look cramped?
- **Common failures:** Redundant badge copy plus an icon; tight letter spacing on uppercase labels.
- **Fix:** Shortest clear phrase, no icon; ~0.05–0.1em letter spacing on small caps labels.

### 7. Headings
- **Test:** Is the main heading the clearest text without overpowering everything else?
- **Common failure:** Bold but poorly sized, so it either shouts or gets lost.
- **Fix:** Tune size and weight within the type scale (e.g. 22–28px semibold for a mobile page title).

### 8. Body text
- **Test:** Is longer text comfortable to read?
- **Common failure:** Tight line height; body as dark and heavy as headings.
- **Fix:** Line height ~1.5; slightly lower contrast than headings (still WCAG AA 4.5:1); line length around 45–75 characters.

### 9. Information placement
- **Test:** Does the first screen answer the user's key questions together? Are trust signals next to what they qualify?
- **Common failure:** Key information or trust signals buried further down or far from their subject.
- **Fix:** Group the answers to the key questions near the top; move trust signals beside the item they describe.

### 10. Redundant labels
- **Test:** Is any label stating what the content already makes obvious?
- **Fix:** Remove it, and keep labeling consistent across neighboring elements.

## C. Layout

### 11. Icon sets
- **Test:** Do all icons share one style, weight and color logic?
- **Common failure:** Mixed filled/outlined, heavy/light, many colors; the section dominates.
- **Fix:** One icon set and stroke, one or two restrained colors, tighter even spacing.

### 12. Dividers
- **Test:** Do dividers draw the eye?
- **Common failure:** Thick dark lines cutting the page into blocks.
- **Fix:** Light neutral hairline, or replace with spacing.

### 13. Spacing balance
- **Test:** Do related elements look grouped and sections look connected?
- **Common failure:** Over-large or uneven gaps that make the screen feel disconnected.
- **Fix:** A 4/8px spacing scale; tighter within groups, larger between sections, used consistently.

## D. Primary action

### 14. Prominence and tone
- **Test:** Is there exactly one obvious primary action? Does it shout?
- **Common failure:** ALL CAPS, oversized, competing with other loud buttons.
- **Fix:** Sentence case, accent color, appropriate size; demote secondary actions.

### 15. Inputs and consequence
- **Test:** Are the inputs for the action right beside it, in order of use? Can the user see what will happen before tapping?
- **Common failures:** Controls separated from the button; no total, recipient or summary shown.
- **Fix:** Group inputs with the action; show the consequence in or next to the button.

## Stress-test set

Re-check the finished design with:
- A very bright image, a very dark image and a busy image.
- Text two or three times longer than the sample.
- Large numbers and long names.
- Empty, missing or zero states.
- The smallest and largest supported screen widths.

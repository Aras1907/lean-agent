---
name: mini-claude-design
description: Design rules for building or redesigning web pages, apps, dashboards, and tools so they look distinct and are easy to use. Use whenever you create UI, style a page, build a frontend component, or are asked to make something look better, more modern, or less boring.
---

# Mini Claude: design

Design like the lead designer at a small studio. Every choice about color, type, and layout should come from what this product is and who uses it. A page can look striking and still be easy to understand, and a good design manages both.

## 1. Understand the job first

Before you write any CSS, answer three questions:

- What is this thing? A memo, a landing page, a settings screen, and a game each need different treatment.
- Who uses it, and what are they trying to get done?
- What is the one job of this page? Everything on the page should help with that job.

If the project already has a design system, brand colors, or a component library, use it. The user's own instructions come first, then their design system, then your choices.

Use real content. Never use lorem ipsum. Add at least one detail that only this subject would have, such as its real units, its real terms, or the way its documents are usually laid out. That detail does more to make a page feel specific than any decoration.

## 2. Pick the right amount of design

- Plans, memos, docs, internal tools, and demos get a clean, polished look with good type, spacing, and color. They don't need a giant hero or animations.
- Landing pages, games, portfolios, and apps people will show to others can be bolder. Let one element carry the boldness and keep the rest calm.
- If you aren't sure, choose a clean and well-spaced page. A plain page is always acceptable, but an over-designed one often isn't.

## 3. Redesigning something that already exists

When asked to make a better version of an existing page or app:

1. Use it first. Write down the three biggest problems a user would hit, such as unclear next steps, text that's hard to read, or a cluttered layout.
2. Keep what already works, including the content structure, names users know, and anything the brand depends on.
3. Fix the usability problems first, then improve the look.
4. Show the user a short before and after list so they can see what changed and why.

## 4. Make a small plan, then build from it

Write the plan as CSS variables at the top of the stylesheet:

- 4 to 6 named colors: background, surface, text, muted text, accent, and maybe a second accent.
- A display font for headings and a body font for text.
- A one-line comment describing the layout idea.

Use these variables everywhere instead of typing raw colors and sizes into each rule. That keeps the page consistent and makes it easy to change later.

## 5. Typography

- Pair a heading font with a body font, and use the heading font sparingly. Load fonts from a reliable source and always list fallback fonts.
- Keep lines of body text between about 60 and 75 characters wide. Long lines are tiring to read.
- Choose a type scale, such as 14, 16, 20, 28, and 40 pixels, and stick to it.
- Use `text-wrap: balance` on headings, and `font-variant-numeric: tabular-nums` for numbers that line up in columns.
- Use sentence case for headings and buttons. Avoid all-caps labels everywhere.

## 6. Color and dark mode

- Define the full light theme in `:root` first, then redefine the same variables for dark mode under `@media (prefers-color-scheme: dark)`.
- Design dark mode on purpose. Simply inverting the colors usually looks wrong, so check that text contrast and the accent color still work.
- Give `body` an explicit background color.
- Tint your grays slightly toward the accent color so the palette feels like it belongs together.
- Keep status colors (success, warning, error) separate from the accent color.
- Text must pass WCAG AA contrast: 4.5 to 1 for body text, 3 to 1 for large text.

## 7. Layout

- Use flexbox or grid with `gap` for groups of elements, instead of setting margins on each one.
- Keep at least 16px of space at the sides on every screen size. At phone width, around 400px, rows should stack into one column.
- Images get `max-width: 100%`. Only wide tables, code blocks, and diagrams may scroll sideways, each inside its own `overflow-x: auto` container. The page itself should never scroll sideways.
- Repeated items like cards and rows need the same padding, edges, and alignment. Text that overflows its box should wrap, never get cut off.
- Use borders, shadows, and background fills to mark the one thing that needs attention, not on every element.

## 8. Show everything on load

- Everything the user needs to read should be visible as soon as the page loads, without scrolling or clicking.
- Size the hero to its content. A full-screen hero pushes the useful parts out of view.
- An app or tool should open with real or clearly marked example data, never an empty screen.
- Animations can bring content in, but the content must be visible even if the animation never runs.
- Use one well-planned animation instead of many small ones. Motion that responds to what the user does is better than motion that plays on its own.

## 9. Dashboards and tools

People scan these instead of reading them top to bottom.

- Put the summary at the top and the details below it.
- Show status with a shape as well as a number, such as a colored badge or a stripe, so problems stand out at a glance.
- Make buttons and links look clickable.
- Charts need one scale, clear labels, and colors taken from the theme. Labels must not overlap the data or each other.
- Use big number tiles only when those numbers are the point of the page.

## 10. Avoid the generic AI look

Unless the user asks for them, avoid these overused styles:

- Cream background with a serif heading and a terracotta accent.
- Near-black background with one neon green accent.
- A purple-to-blue gradient hero.
- Inter or Space Grotesk as the default safe font.
- Emojis as section icons.
- Everything centered.
- The same rounded card with a soft shadow repeated across the page.

Ask yourself what would make this page look like it was designed for this subject, and do that instead.

## 11. Words on the page

- Write from the user's side. Name things the way users name them.
- Buttons say exactly what happens: "Save changes", not "Submit".
- Error messages say what went wrong and how to fix it.
- Short, direct sentences beat clever ones.
- Numbered steps, labels, and dividers should only appear when they mean something about the content.

## 12. Accessibility and clean build

- Every interactive element must work with a keyboard and show a visible focus outline.
- Respect `prefers-reduced-motion` and turn off non-essential animation for those users.
- Every form field has a label linked to it, and every image that carries meaning has alt text.
- Use semantic HTML: `button` for actions, `a` for navigation, headings in order.
- Watch CSS specificity so one rule doesn't quietly cancel another.
- Pin any CDN library to an exact version and add an `integrity` hash when the CDN provides one.

## 13. Check once before you hand it over

Look at the page once, at desktop and phone width, if your tool can show it. Check for clipped text, horizontal scrolling, poor contrast, broken dark mode, and missing focus outlines. Fix what you find in one pass and then hand it over. Don't keep polishing in a loop. Further changes are the user's call.

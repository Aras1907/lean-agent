---
name: lean-agent-design
description: Design rules for web pages, apps, dashboards, and UI components. Use when building or styling a frontend, making a page look better, or redesigning an existing page. Makes the result look specific to its subject, easy to read, and accessible.
---

# Design rules

Goal: a page that looks made for its subject and is easy to use. Not dull, not cluttered.

## Step 1. Answer three questions

1. What is this? A doc, a landing page, a tool, a dashboard, a game?
2. Who uses it?
3. What is the one main job of this page?

If the project has a design system, brand colors, or components, use them. Don't invent new ones.

## Step 2. Choose how bold to be

- Docs, internal tools, forms, settings: clean and calm. No big hero. No animations.
- Landing pages, portfolios, games, apps people show off: bolder. Make one element stand out. Keep the rest calm.
- Not sure? Choose clean and calm.

## Step 3. Set up the design tokens

Start from `references/starter.css` next to this file. Change the colors and fonts to fit the subject. Use only these variables in the rest of the CSS. Don't type raw colors into rules.

## Step 4. Build with these rules

Content:

- Use real content. Never lorem ipsum.
- Add one detail only this subject has: its real units, terms, or data.
- Buttons say what happens: "Save changes", not "Submit".
- Error messages say what went wrong and how to fix it.

Text:

- Two fonts at most: one for headings, one for body text. Always list fallback fonts.
- Body text lines about 60 to 75 characters wide.
- Sentence case for headings and buttons.

Color:

- 4 to 6 colors. One accent color.
- Text contrast at least 4.5 to 1. Large text at least 3 to 1.
- Status colors (success, warning, error) are separate from the accent.
- Dark mode uses its own chosen colors. Don't just invert the light colors.

Layout:

- Use flexbox or grid with `gap`.
- At least 16px space on the left and right at every screen size.
- At 400px wide, rows stack into one column.
- The page must never scroll sideways. Only wide tables and code blocks scroll, inside `overflow-x: auto`.
- Cards and rows that repeat use the same padding and alignment.
- Text wraps. It is never cut off.

On load:

- Everything important is visible without scrolling or clicking.
- A tool opens with example data, never an empty screen.
- Content is visible even if animations don't run.

Dashboards:

- Summary at the top, details below.
- Show status with a colored badge or stripe, not only a number.
- Charts: one scale, clear labels, no overlapping text.

## Step 5. Avoid the generic AI look

Don't use these unless the user asks:

- Purple-to-blue gradient hero.
- Cream background, serif heading, orange-brown accent.
- Black background with one neon green accent.
- Inter or Space Grotesk as the default font.
- Emojis as icons.
- Everything centered.
- The same rounded card with a soft shadow everywhere.

## Step 6. Accessibility

- Everything works with the keyboard. Focus is clearly visible.
- `button` for actions, `a` for links, headings in order.
- Every input has a `label`. Every meaningful image has `alt` text.
- Turn off non-essential animation under `prefers-reduced-motion`.

## Step 7. Redesigning an existing page

1. List the 3 biggest problems a user would hit.
2. Keep what works: content, names users know, brand colors.
3. Fix the problems first. Then improve the look.
4. Tell the user what changed and why, as a short before and after list.

## Step 8. Check once

Look at the page at desktop and phone width if you can. Check for cut-off text, sideways scrolling, low contrast, broken dark mode, and missing focus outlines. Fix them in one pass. Then stop and hand it over.

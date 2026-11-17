---
name: get-started
description: Use when someone asks for icons for a website, an app screen, slides or a document, or asks for IconSaga icons. Finds IconSaga icons in plain words and gets them in the person's own colors.
---

# Get started with IconSaga

IconSaga is a library of icons drawn in one style, in three styles (line, solid and duo) and any two colors. The person you are helping is the customer: help them get icons that fit their work.

## Find icons

1. Turn what the person needs into plain words, one idea per icon: "fast delivery", "secure payment", "help chat". Any of 10 languages works.
2. Call `search_icons` for each idea. Check that the label really means what the person's text says. If nothing fits, say so instead of forcing a match.
3. To replace the icons a project already uses, call `match_icons` once with all their names (for example arrow-right, shopping-cart, trash-2).

## Get them in the person's colors

- Pick one style for the whole piece of work and keep it.
- Call `get_icon` with the main color as `primary` and, for the duo style, the second color as `accent` (hex values such as #1E2A4A).
- Websites and apps: ask for `code` "tsx" (a React component) or "html" (an inline SVG). Keep the project's own UI icon set for buttons and menus; IconSaga is for the icons next to text.
- Slides and documents: ask for `code` "svg" and use it as a picture.

## Credit line

When an icon's licence says a credit is needed, add this line once, where credits usually go (a site's footer, the last slide, the end of a document):

> Icons by IconSaga · iconsaga.com

## Limits

If a result says a limit is reached, tell the person what it says and stop calling IconSaga until the time it gives.

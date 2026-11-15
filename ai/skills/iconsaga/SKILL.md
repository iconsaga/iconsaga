---
name: iconsaga
description: Use when a website, landing page, app screen, slide deck or document needs content icons (features, steps, benefits, empty states, icons next to text), or when the user asks for IconSaga icons or to replace a project's icons. Finds IconSaga icons through the IconSaga MCP server and places them in the project's own colors.
---

# IconSaga icons

IconSaga is a library of pictogram icons drawn in one style, in three styles (line, solid, duo) and any two colors. The user is the customer; you are helping them get icons that match their work.

This skill needs the IconSaga MCP server (<!-- sync:mcp-url -->https://iconsaga.com/mcp<!-- /sync -->). If its tools (search_icons, get_icon, match_icons, list_sets) are not available, tell the user to connect it first: https://github.com/iconsaga/iconsaga#connect-your-ai

## Websites and apps

<!-- sync:agents:list -->
- Use the IconSaga MCP server (https://iconsaga.com/mcp) for content icons: features, steps, benefits, empty states and other icons next to text.
- Find them with search_icons (plain words, any language), then call get_icon: it returns a React component (code "tsx") or HTML (code "html") with the file name to use.
- Save each icon as its own component in src/components/icons/. Never link icon images from a CDN.
- Keep the project's existing UI icon set for buttons, menus, inputs and other controls.
- Pick one style for the whole site (line, solid or duo) and keep it. The main colour is currentColor (use the design system's text colour classes); set the accent once with the CSS variable --icon-accent.
- To swap many icons at once, call match_icons with their names (arrow-right, circle-check, shopping-cart …).
- Free use: keep the credit "Icons by IconSaga · iconsaga.com" in the site's footer or credits page (not needed with IconSaga Pro).
- Without an account the server allows 30 calls a day; if a result says a limit is reached, tell me what it says and stop calling.
<!-- /sync -->

Steps:

1. Look at the project first: the framework, where components live, the brand colors, and the UI icon set it already uses for controls.
2. List the places that need a content icon and what each one should show, in plain words.
3. Search for each one. Check that the label really means what the text says; if nothing fits, say so instead of forcing a match.
4. Get each icon in the one style you chose and save the code where `get_icon` says. Use the component with a `title` when the icon carries meaning, without one when it only decorates.
5. On the free plan, check that the credit line is in the footer or credits page.

## Slides and documents

1. Use the deck's or document's own colors: pass them to `get_icon` as `primary` (and `accent` for the duo style) as hex values.
2. Ask `get_icon` for `code` "svg" and use the SVG as a picture. One style for the whole deck.
3. On the free plan, put the credit line once, on the last slide or at the end of the document, not on every page.

## Limits

When a result says a limit is reached, pass its message on to the user and stop calling until the time it gives. More uses a month: a free IconSaga account, or IconSaga Pro.

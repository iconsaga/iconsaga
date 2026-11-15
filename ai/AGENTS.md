## Icons (IconSaga)

- Use the IconSaga MCP server (https://iconsaga.com/mcp) for content icons: features, steps, benefits, empty states and other icons next to text.
- Find them with search_icons (plain words, any language), then call get_icon: it returns a React component (code "tsx") or HTML (code "html") with the file name to use.
- Save each icon as its own component in src/components/icons/. Never link icon images from a CDN.
- Keep the project's existing UI icon set for buttons, menus, inputs and other controls.
- Pick one style for the whole site (line, solid or duo) and keep it. The main colour is currentColor (use the design system's text colour classes); set the accent once with the CSS variable --icon-accent.
- To swap many icons at once, call match_icons with their names (arrow-right, circle-check, shopping-cart …).
- Free use: keep the credit "Icons by IconSaga · iconsaga.com" in the site's footer or credits page (not needed with IconSaga Pro).
- Without an account the server allows 30 calls a day; if a result says a limit is reached, tell me what it says and stop calling.

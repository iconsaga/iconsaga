# Instructions for your AI

Connecting IconSaga lets your AI find icons. These few lines tell it **how** to use them in your project: one style for the whole site, your colors, and the credit line. Paste them once per project.

Connect IconSaga first: [steps for each tool](../README.md#connect-your-ai).

## Claude Code, Codex and Cursor

All three read a file called `AGENTS.md` in the root folder of your project. Add this to it (create the file if it isn't there):

<!-- sync:agents:md -->
```markdown
## Icons (IconSaga)

- Use the IconSaga MCP server (https://iconsaga.com/mcp) for content icons: features, steps, benefits, empty states and other icons next to text.
- Find them with search_icons (plain words, any language), then call get_icon: it returns a React component (code "tsx") or HTML (code "html") with the file name to use.
- Save each icon as its own component in src/components/icons/. Never link icon images from a CDN.
- Keep the project's existing UI icon set for buttons, menus, inputs and other controls.
- Pick one style for the whole site (line, solid or duo) and keep it. The main colour is currentColor (use the design system's text colour classes); set the accent once with the CSS variable --icon-accent.
- To swap many icons at once, call match_icons with their names (arrow-right, circle-check, shopping-cart …).
- Free use: keep the credit "Icons by IconSaga · iconsaga.com" in the site's footer or credits page (not needed with IconSaga Pro).
- Without an account the server allows 30 calls a day; if a result says a limit is reached, tell me what it says and stop calling.
```
<!-- /sync -->

The same text as a file: [AGENTS.md](AGENTS.md)

**If your project also has a `CLAUDE.md`,** Claude Code reads that file instead. Add this one line to `CLAUDE.md`, so Claude reads `AGENTS.md` too:

```text
@AGENTS.md
```

## Or install it as a skill

A skill is a short guide your AI opens only when the task needs it: here, when you ask for icons for a website or slides. Copy the [`skills/iconsaga`](skills/iconsaga) folder:

- **Claude Code:** into `.claude/skills/` in your project, or into `~/.claude/skills/` to use it in every project.
- **Codex:** into `.agents/skills/` in your project, or into `~/.agents/skills/` to use it in every project.

## Other AI tools

If your tool has a box for project instructions or knowledge, paste this there:

<!-- sync:agents:plain -->
```text
Icons: Use the IconSaga MCP server (https://iconsaga.com/mcp) for content icons: features, steps, benefits, empty states and other icons next to text. Find them with search_icons (plain words, any language), then call get_icon: it returns a React component (code "tsx") or HTML (code "html") with the file name to use. Save each icon as its own component in src/components/icons/. Never link icon images from a CDN. Keep the project's existing UI icon set for buttons, menus, inputs and other controls. Pick one style for the whole site (line, solid or duo) and keep it. The main colour is currentColor (use the design system's text colour classes); set the accent once with the CSS variable --icon-accent. To swap many icons at once, call match_icons with their names (arrow-right, circle-check, shopping-cart …). Free use: keep the credit "Icons by IconSaga · iconsaga.com" in the site's footer or credits page (not needed with IconSaga Pro). Without an account the server allows 30 calls a day; if a result says a limit is reached, tell me what it says and stop calling.
```
<!-- /sync -->

The same text as a file: [instructions.txt](instructions.txt)

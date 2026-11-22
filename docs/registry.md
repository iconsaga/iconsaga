# Where IconSaga is listed

Notes for whoever lists IconSaga's MCP server in registries and directories, and keeps those listings up to date.
Every listing is added by hand, by a person.

## Listed now

| Where | Entry | Date |
|---|---|---|
| Official MCP Registry | [`com.iconsaga/icons`](https://registry.modelcontextprotocol.io/v0.1/servers?search=com.iconsaga/icons) 1.0.0 | published 2026-11-16 |
| Claude's connector directory | [IconSaga](https://claude.ai/directory/iconsaga), the sign-in connector `https://iconsaga.com/mcp/account` | published 2026-11-17 |
| mcpservers.org | free listing | approved 2026-11-17 |
| mcptry | listed on its own, score 90/100 | seen 2026-11-17 |
| MCP Marketplace (mcp-marketplace.io) | imported on its own from the official registry; a claim is offered, not claimed | seen 2026-11-17 |
| Docker MCP Catalog | [docker/mcp-registry#7223](https://github.com/docker/mcp-registry/pull/7223), updated after the automated review, waiting for review | opened 2026-11-16 |

Pending: **Glama** (copies from the official registry; not listed yet when last checked). Skipped: **mcp.so** (its form offers only a paid $39 listing).

To publish a new version of the card: raise `version` in `server.json`, then `mcp-publisher login dns --domain iconsaga.com --private-key <hex>` (the key's owner has it) and `mcp-publisher publish`.

## The server card (`server.json`)

[`server.json`](../server.json) in this repository is the card for the official MCP Registry. It validates against the current official schema, [2025-12-11](https://static.modelcontextprotocol.io/schemas/2025-12-11/server.schema.json) (still the latest released version; the registry's [schema changelog](https://github.com/modelcontextprotocol/registry/blob/main/docs/reference/server-json/CHANGELOG.md) only has a draft after it).

What changed from the first draft of the card:

| Field | Before | Now | Why |
|---|---|---|---|
| `description` | "Pictogram icons for AI-built websites: React, HTML or SVG in your brand colours, 10 languages." | "Icons that match, in your colors. Your AI finds them for your website or slides, in 10 languages." | Talks to people, not about file formats. Still under the 100-character limit. |
| `repository` | none | this repository, with GitHub's repository id | Directories link to it for the setup steps. The id lets the registry notice if the repository is ever deleted and made again. |
| `icons` | none | the logo (SVG, and PNG 512 × 512) | Registries and apps show it next to the name. |
| `Authorization` header | the person had to type the whole value, `Bearer <key>` | `"value": "Bearer {iconsaga_key}"`, with the key as a secret variable | Apps ask for the key alone and add `Bearer` themselves. |
| header description | "free 1,000 calls a month, Pro 20,000. Without it: 30 calls a day." | "gives your AI more uses a month. Without one: 30 a day." | Plain words. The monthly numbers live on the Pro page, so the card can't go out of date. |

Kept as they were: `name` (see below), `title`, `version` 1.0.0 (the card's own version, not the icon release), `websiteUrl`, and both remotes (`/mcp` without sign-in, `/mcp/account` with sign-in).

### Name and how it is verified

**Recommended: `com.iconsaga/icons`, verified through DNS.**

- The name matches the domain the server runs on, and it stays the same whatever happens to the GitHub organization.
- Verification is one TXT record on the apex of iconsaga.com (not on a subdomain): `iconsaga.com. IN TXT "v=MCPv1; k=ed25519; p=<public key, base64>"`. It also covers subdomains. The matching private key stays with the owner (password manager) and is only typed into `mcp-publisher`; it never goes into a file in any repository.
- The key pair is Ed25519. macOS's built-in `openssl` can't make one; use Homebrew's `openssl@3`.

The other ways, and why not:

- **`io.github.iconsaga/iconsaga` through GitHub:** it needs an owner of the `iconsaga` organization, and `mcp-publisher login github` (the browser device flow) currently can't grant organization names ([registry issue #1468](https://github.com/modelcontextprotocol/registry/issues/1468), open). It works only with a workaround: a token with `read:org`, or a GitHub Actions workflow. That's more moving parts than one DNS record.
- **`com.iconsaga/icons` through HTTP:** the site would serve `https://iconsaga.com/.well-known/mcp-registry-auth` (status 200, no redirects). That means a code change and a deploy of the site, and it covers only the exact domain. Use it only if a DNS record can't be added.

### Publishing rules worth knowing

- The registry does **not** contact the server when you publish; it only checks that the address is https. But its policy says remote servers must be publicly reachable, so publish when https://iconsaga.com/mcp answers. The DNS record can be added any time before.
- Every publish needs a new `version`, and a published version can never change. For a change to the card alone, use a pre-release such as `1.0.0-1`. Old versions can be marked deprecated, never erased.
- The registry is still a preview; its data may be reset. If IconSaga disappears from it, publish again.
- Sources (read 2026-11-15): [quickstart](https://modelcontextprotocol.io/registry/quickstart) · [authentication](https://modelcontextprotocol.io/registry/authentication) · [remote servers](https://modelcontextprotocol.io/registry/remote-servers) · [versioning](https://modelcontextprotocol.io/registry/versioning) · [FAQ](https://modelcontextprotocol.io/registry/faq) · [registry source code](https://github.com/modelcontextprotocol/registry) (validators and DNS/HTTP/GitHub sign-in)

## Descriptions, ready to paste

**Name:** IconSaga

**Short (100 characters or fewer):**

> Icons that match, in your colors. Your AI finds them for your website or slides, in 10 languages.

**Longer:**

> IconSaga is a library of <!-- sync:icons -->5,517<!-- /sync --> free icons, all drawn in one style so they belong together. Connect it to your AI and ask in your own words, in any of 10 languages: it finds icons that fit, in your brand colors, and puts them into your website or slides. No account needed to start. Free use needs a one-line credit; IconSaga Pro removes it.

**What your AI can do with it (tools):**

| Tool | In plain words |
|---|---|
| `search_icons` | Find icons by meaning, in any of 10 languages |
| `get_icon` | Get one icon in your style and colors, ready to put in a website (React or HTML) or a slide (SVG) |
| `match_icons` | Swap all the icons of a project at once, by their names |
| `list_sets` | See all the icon sets |

All four only read; none changes anything.

**Server address:** `https://iconsaga.com/mcp` (no sign-in) · `https://iconsaga.com/mcp/account` (sign in with an IconSaga account)
**Website:** https://iconsaga.com · **Setup steps:** https://github.com/iconsaga/iconsaga#connect-your-ai · **License:** https://iconsaga.com/license
**Logo:** https://iconsaga.com/brand/icon-512.png (512 × 512) · https://iconsaga.com/favicon.svg
**Categories, where a directory asks:** Design · Developer tools · Productivity
**Tags:** icons, pictograms, design, web design, presentations, brand colors

When the icon count changes with a new release, update the number in the longer description on each listing that shows it.

## Where to list it

Checked 2026-11-15. "Live" means https://iconsaga.com/mcp must answer before the listing goes through.

| # | Where | How | Needs | Live? | Notes |
|---|---|---|---|---|---|
| 1 | **Official MCP Registry** | `mcp-publisher publish` (CLI) | the DNS record above | Policy: yes (not checked by the tool) | The source most other directories copy from. Do this first. |
| 2 | **Glama** | Nothing to do: it copies from the official registry every hour. Or Connectors → Add Server → Hosted endpoint | name, short description, the server address | **Yes**: it checks the server and lists only healthy ones | Claim the listing with a TXT record at `_glama-claim.iconsaga.com` or `/.well-known/glama.json`. Its connector badge is needed for list 6. |
| 3 | **mcp.so** | Form at [mcp.so/submit](https://mcp.so/submit), "Remote Server" tab | name, links | Not stated | Free listings are reviewed (no time stated). A paid $39 option skips review: it needs the owner's OK. |
| 4 | **mcpservers.org** | Form at [mcpservers.org/submit](https://mcpservers.org/submit) | name, category, short description, website link, official registry name, "supports remote connections", a contact email (use support@iconsaga.com) | Not stated | Free review "within 2 weeks"; a paid $39 option takes 24 hours (needs the owner's OK). |
| 5 | **Docker MCP Catalog** | Pull request to [docker/mcp-registry](https://github.com/docker/mcp-registry): `servers/iconsaga/server.yaml` (`type: remote`, transport, url), an empty `tools.json`, a `readme.md` | a GitHub account | **Yes** | No container needed for a remote server. Listed within 24 hours of approval. |
| 6 | **awesome-remote-mcp-servers** (GitHub list) | Pull request | a Glama connector badge (CI checks it), entry of 3 lines | **Yes**: CI calls the server | The big awesome-mcp-servers list doesn't take remote-only servers; this one does. Their CONTRIBUTING asks automated agents to add "🤖🤖🤖" to the PR title: ignore that, a person opens the PR. |
| 7 | **Claude's connector directory** (Anthropic) | [claude.ai/directory/manage](https://claude.ai/directory/manage) → Submit new → MCP connector | a paid Claude plan; per tool a title and read-only/destructive hints (IconSaga has both); name, one-liner (≤200), description (≤2,000), 1–5 categories, docs, privacy policy and support links, icon, a permanent slug | **Yes**: tools are read from the live server | Test IconSaga as a custom connector in claude.ai first (not tested yet). |
| 8 | **ChatGPT apps** (OpenAI) | Plugins dashboard on platform.openai.com → "With MCP" | identity and domain verification; website, support, privacy and terms links; 5 positive and 3 negative test cases; a video walkthrough | **Yes**, scanned daily | Heavy. Leave until after launch, and do it when people ask for IconSaga in ChatGPT. |

Not now:

- **PulseMCP:** paused ("not accepting new MCP server or client submissions right now"). It will import from the official registry when it reopens. Nothing to do.
- **Smithery:** joined Arcade; accounts, CLI and submissions closed on 31 Oct 2026. It stays as a read-only registry. No way to submit found.
- **Cursor:** no MCP directory. The Cursor Marketplace takes *plugins*: an open-source Git repository with a plugin file and an `mcp.json`, reviewed by hand. This repository could become one later (a decision for later). Its docs point community servers to cursor.directory, which could not be checked.
- **GitHub MCP Registry:** curated, not self-serve. The route given is an email to GitHub partnerships. Optional, after launch.
- **LobeHub:** no way to submit found.

### Ready to paste

- **awesome-remote-mcp-servers entry** (match the file's format at the time; description ≤120 characters):
  - name: `IconSaga`, linked to https://iconsaga.com
  - endpoint: `https://iconsaga.com/mcp`
  - auth: none needed (an IconSaga account with sign-in is optional)
  - description: "Icons that match, in your colors: your AI finds them for websites and slides, in 10 languages." (94 characters)
- **Claude directory one-liner** (≤200): "Icons that match, in your colors. Ask in your own words and Claude finds icons for your website or slides, in 10 languages."
- **Privacy:** https://iconsaga.com/privacy · **Terms:** https://iconsaga.com/terms · **Support:** support@iconsaga.com

### Sources (read 2026-11-15)

- Glama: [FAQ](https://glama.ai/mcp/faq) · [connectors](https://glama.ai/mcp/connectors)
- mcp.so: [submit](https://mcp.so/submit) · mcpservers.org: [submit](https://mcpservers.org/submit)
- Docker: [CONTRIBUTING](https://github.com/docker/mcp-registry/blob/main/CONTRIBUTING.md) · [catalog docs](https://docs.docker.com/ai/mcp-catalog-and-toolkit/catalog/)
- awesome-remote-mcp-servers and awesome-mcp-servers: CONTRIBUTING.md in each repository
- Anthropic: [submission](https://claude.com/docs/connectors/building/submission.md) · [publish](https://claude.com/docs/directory/publish.md)
- OpenAI: [submission](https://developers.openai.com/apps-sdk/deploy/submission)
- PulseMCP: [submit](https://pulsemcp.com/submit) · Smithery: [smithery.ai/future](https://smithery.ai/future)
- Cursor: [MCP](https://cursor.com/docs/context/mcp) · [install links](https://cursor.com/docs/context/mcp/install-links) · [plugins](https://cursor.com/docs/plugins)
- GitHub MCP Registry: [GitHub blog](https://github.blog/) post "How to find, install and manage MCP servers with the GitHub MCP Registry"

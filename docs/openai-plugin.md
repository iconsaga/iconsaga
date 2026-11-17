# IconSaga in OpenAI's Plugins Directory (ChatGPT and Codex)

Notes for listing IconSaga in OpenAI's plugin directory, which ChatGPT and Codex share. **Nothing is created or submitted yet.** The package is ready; what's left needs the owner (identity, review account, attestations) and two small changes on the website.

Sources, all read on 2026-11-17: [submission](https://developers.openai.com/plugins/deploy/submission) · [submission errors](https://developers.openai.com/plugins/deploy/submission-errors) · [app review](https://developers.openai.com/plugins/deploy/app-review) · [plugin guidelines](https://developers.openai.com/plugins/plugin-guidelines) · [build plugins](https://developers.openai.com/plugins/build/plugins) · [auth](https://developers.openai.com/plugins/build/auth) · [organization verification](https://help.openai.com/en/articles/10910291-api-organization-verification) · [supported countries](https://help.openai.com/en/articles/7947663-chatgpt-and-openai-api-supported-countries-and-territories)

## What's ready

The package is in [`openai-plugin/`](../openai-plugin), in the portable layout (a root `plugin.json` and `mcp.json`), which is OpenAI's main format. The Codex-only `.codex-plugin/` layout is supported only for compatibility, and only the portable `mcp.json` documents where the sign-in settings go.

| File | What it is |
|---|---|
| `plugin.json` | Name, listing text, links, icons, colors, 3 starter prompts, the 5 + 3 test cases, release notes, `commerce: false` |
| `mcp.json` | One server, `https://iconsaga.com/mcp/account`, sign-in with OAuth and dynamic client registration |
| `skills/get-started/SKILL.md` | A short onboarding skill. A public package must contain at least one valid skill |
| `assets/logo.png` (1080 px), `assets/composer-icon.png` (512 px) | The approved navy app icon, square |

Build the ZIP from inside `openai-plugin/`:

```bash
zip -r -X ../iconsaga-openai-plugin-1.0.0.zip plugin.json mcp.json skills assets -x '*.DS_Store'
```

Checked against the documented limits: display name and subtitle are 30 characters or fewer (subtitle: "Icons that match your colors", 28), description ≤ 1,024, long description ≤ 4,000, category "Creativity" (from OpenAI's list), up to 3 starter prompts of 128 characters or fewer, brand colors with enough contrast (navy `#1E2A4A` on white 14:1, amber `#FFB020` on dark `#212121` 8.8:1).

**Why the sign-in server, not `/mcp`:** every ChatGPT and Codex user would reach `/mcp` through OpenAI's servers, so the no-account daily limit would be shared by everyone. With `/mcp/account`, each person signs in and uses their own plan.

### Test cases (5 positive, 3 negative)

Each was run once through Codex, signed in to `/mcp/account`, on 2026-11-17. All passed. Details, with three more negatives (N1–N3: weather, code, translation): [`openai-plugin-self-test.json`](openai-plugin-self-test.json).

| | Prompt | IconSaga tools called |
|---|---|---|
| P1 | Use IconSaga to find an icon for "online payment". | search_icons, get_icon |
| P2 | ช่วยหาไอคอนทุเรียนจาก IconSaga ให้หน่อย (Thai) | search_icons, get_icon |
| P3 | Get IconSaga's rocket icon in the duo style, navy and amber; show the SVG | search_icons, get_icon |
| P4 | Match arrow-right, shopping-cart, trash-2 | match_icons |
| P5 | What icon sets does IconSaga have? | list_sets |
| N4 | Delete the rocket icon from IconSaga. | none (explains it can't delete) |
| N5 | Make a photo-realistic picture of a beach at sunset with IconSaga. | none |
| N6 | Buy an IconSaga subscription for me. | none (nothing bought) |

Notes on the run: the Codex used for testing also had a private IconSaga skill that reads local files, so the positive runs added one sentence asking it to use the connector; the prompts in `plugin.json` don't have it. On N5 and N6, Codex reached for its own tools (image generation; a browser it wasn't allowed to open). No IconSaga tool was called and nothing was bought.

### Annotations (OpenAI checks them)

All four tools are read-only and already declare `readOnlyHint: true`, `destructiveHint: false`, `openWorldHint: false`. One-line justifications, if the form asks:

- **Read only:** the tools only search and return icons from IconSaga's published library; nothing is created, changed or deleted.
- **Not destructive:** no tool deletes or overwrites anything.
- **Closed world:** the tools only read IconSaga's own icon catalog and never reach other sites or services.

## What the owner has to do

1. **Choose the developer identity.** This decides what name the listing shows.
   - *Individual verification:* "If you want to publish under your own name, complete individual verification." The directory "displays the name associated with this identity", and the developer name "is set automatically from your selected verified developer identity, regardless of the name in your ZIP". The docs offer no display or brand name for individuals, so an individual listing shows the **legal name on the ID**.
   - *Business verification:* publishes under the business's legal name, as in official records, with its address and a registration or tax number if asked. Whether a Thai sole-proprietor commercial registration under a trade name passes, and which name it would show, is not documented.
   - Also: "Public URLs must be accessible and identify the same publisher as the submission." The website, privacy and terms pages would need to name the same publisher as the identity chosen.
   - Thailand is on OpenAI's supported-countries list. Individual verification needs an original physical government ID (passport, driving licence, national ID or residence permit) and maybe a selfie; scans aren't accepted.
2. **Have an owner role** (or "Apps Management Write") in the OpenAI organization, and use a project without EU data residency.
3. **Enter the reviewer account** in the portal's **Review details** form: an account that signs in straight away, with no two-step codes, email or SMS codes, or magic links. Credentials never go in the ZIP.
4. **Record a demo video** at a URL reviewers can open, showing the main uses and tools in ChatGPT and Codex (desktop and mobile). Add it as `demo_recording_url`.
5. **In the portal:** upload the ZIP, choose the identity, connect the server (domain check, sign-in, tool scan), fill in review details, confirm the attestations and **Submit for review**. After approval, press **Publish plugin**; approval alone doesn't list it.
6. Before any press release that mentions OpenAI, contact press@openai.com.

## What the website needs

1. **Domain check:** serve the token from the portal as plain text, exactly the token and nothing else, at `https://iconsaga.com/.well-known/openai-apps-challenge`. The portal shows the token in its MCP **Connect** step. (Returns 404 today.)
2. **Reviewer sign-in** without magic links or codes, with sample data, as above.
3. **Limit messages in ChatGPT and Codex:** today, when a free account nears or reaches its monthly limit, the server tells the AI to mention Pro and link to `/pro`. OpenAI's rules: plugins "must not display subscription plans, initiate new subscriptions, or promote upgrades". Explaining that something isn't on the person's plan and linking to an informational page is allowed; linking to checkout or an upgrade page isn't. Use a neutral message for these clients, without the `/pro` link.
4. Optional:
   - A support page; the listing uses `https://iconsaga.com/about`, which shows the support address.
   - `annotations.title` on each tool (Claude's directory suggested the same).
   - An OIDC UserInfo endpoint (`openid` and `email` scopes), needed only for enterprise domain restrictions.

## Fees and review time

- **Fees:** none of the official pages mention a fee for listing, review or verification. Not confirmed that there are none. Separately, plugins may not sell digital goods or subscriptions at all.
- **Review time:** no time is promised: "Review timelines may vary… Please do not contact support to request expedited review." Only one review can be active per plugin; rejection reasons come by email and you can appeal by replying. In OpenAI's community forum, developers have reported waits of 60 to 90 days (not official).
- **After publishing:** OpenAI scans the server daily. New or changed tools wait for automated checks; text, icon or skill changes need a new ZIP and a new review. The server address can't change without contacting support.

## Policy points that matter for IconSaga

- The listing text doesn't mention prices, plans, trials or Pro; the credit line is stated as the licence condition it is.
- No ads; content suitable for ages 13 to 17; only our own IP; no hint of OpenAI endorsement.
- The privacy policy already describes MCP logging (connecting app, tool, search words, time, country, not linked to the person), retention and user rights, which OpenAI requires.

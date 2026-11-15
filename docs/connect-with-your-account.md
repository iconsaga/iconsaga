# Connect with your IconSaga account

You don't need an account to start: without one, your AI can use IconSaga <!-- sync:guest-per-day -->30<!-- /sync --> times a day. Connect your account when you want more:

- **Free account:** <!-- sync:free-per-month -->1,000<!-- /sync --> times a month
- **Pro:** <!-- sync:pro-per-month -->20,000<!-- /sync --> times a month

There are two ways. Pick the one your AI tool supports.

## 1. Sign in (easiest)

If your AI tool can open a browser to sign in, use this address instead of the one in the [setup steps](../README.md#connect-your-ai). Your tool opens iconsaga.com, you sign in, and that's it:

<!-- sync:account:signin -->
```text
https://iconsaga.com/mcp/account
```
<!-- /sync -->

## 2. A personal key

For tools that can't open a browser. Make a key on your account page at [iconsaga.com](https://iconsaga.com), then save it on your computer as `ICONSAGA_KEY`, so it never sits inside a project file. Then connect with it:

### Claude Code

<!-- sync:account:key-claude-code -->
```bash
claude mcp add --transport http iconsaga https://iconsaga.com/mcp --header "Authorization: Bearer $ICONSAGA_KEY"
```
<!-- /sync -->

### Codex

Add this to `~/.codex/config.toml`:

<!-- sync:account:key-codex -->
```toml
[mcp_servers.iconsaga]
url = "https://iconsaga.com/mcp"
bearer_token_env_var = "ICONSAGA_KEY"
```
<!-- /sync -->

### Cursor

Put this in `.cursor/mcp.json` in your project:

<!-- sync:account:key-cursor -->
```json
{
  "mcpServers": {
    "iconsaga": {
      "url": "https://iconsaga.com/mcp",
      "headers": {
        "Authorization": "Bearer ${env:ICONSAGA_KEY}"
      }
    }
  }
}
```
<!-- /sync -->

Keep your key private, like a password. If it leaks, revoke it on your account page and make a new one.

# Enform plugin for Claude Code

Build, publish and share Enform surveys and forms from Claude, then read what people answered. The plugin connects Claude to Enform's remote MCP server and adds one skill, `enform-forms`, that teaches Claude the build, publish and share flow, how to open a form from your app with hidden fields, how to verify Enform webhooks, and how to report answers.

You need an Enform account. Sign up at https://enform.co.

## Install

From a Claude Code session:

```text
/plugin marketplace add enform-co/claude-plugin
/plugin install enform@enform
```

Or from your shell, in one command (Claude Code 2.1.292 or later):

```bash
claude plugin install enform --marketplace enform-co/claude-plugin
```

Then run `/mcp`, pick `enform`, and sign in to Enform in the browser window that opens.

### Without the plugin

You get the tools but not the skill:

```bash
claude mcp add --transport http enform https://api.enform.co/api/mcp
```

On Pro you can use a workspace API key from Settings > API instead of signing in. The key only reaches its own workspace:

```bash
claude mcp add --transport http enform https://api.enform.co/api/mcp --header "Authorization: Bearer enf_your_key"
```

Setup for Claude Desktop, ChatGPT, Cursor and Codex is at https://enform.co/docs/mcp.

## Try it

- Make a churn survey for customers who cancelled this month
- Build a waitlist form for our beta and give me the link
- How did people answer my NPS survey this week?

## What it runs and sends

- **MCP server:** `https://api.enform.co/api/mcp`, streamable HTTP. No local code runs.
- **Sign-in:** OAuth 2.1 with PKCE. Claude Code identifies itself with its Client ID Metadata Document, so there is no client to register. Scopes: `mcp:read`, `mcp:responses:read`, `mcp:forms:write`, `offline_access`.
- **Data:** the prompts and answers you send to the tools, and the form and response data the tools return. Enform's privacy policy is at https://enform.co/privacy and terms at https://enform.co/terms.
- **Skill:** plain Markdown in `skills/enform-forms/SKILL.md`. It contains no scripts.

To remove access, open Settings > MCP in Enform and choose Revoke next to the client under Authorized clients.

## Test locally

From the root of this repository:

```bash
claude plugin validate --strict .
claude --plugin-dir .
```

In that session, run `/mcp` to sign in, then ask for something like "make a churn survey for people who cancelled this month". To test the marketplace install path as well:

```bash
claude plugin marketplace add .
claude plugin install enform@enform
claude plugin details enform
```

Remove it again with `claude plugin marketplace remove enform`.

## Support

Help with sign-in, permissions and known limits is at https://enform.co/support. You can also email hello@enform.co.

## License

MIT. See [LICENSE](LICENSE).

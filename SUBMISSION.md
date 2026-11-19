# Submission notes

Notes for the owner when listing this plugin. Nothing in this file is a secret. Last reviewed 19 November 2026.

## xAI plugin form (Grok Bot and Cursor)

Form: [x.ai/bot/marketplace/submit-a-plugin](https://x.ai/bot/marketplace/submit-a-plugin). It distributes a plugin or MCP server to Grok Bot and Cursor users after review. Merge the pull request that replaces the logo first, and check that the raw logo URL below serves the 1024×1024 opaque PNG before you submit.

| Form field | Value |
| --- | --- |
| First Name / Last Name | Hristo / Lilkin |
| Work Email | hristo@autodashapp.com (the contact on AutoDash's privacy, terms, and about pages) |
| Organization Name | AutoDash |
| Organization Handle (lowercase, no spaces, 40 characters max) | `autodash` |
| Website URL (optional) | https://autodashapp.com |
| Logotype URL (1:1 PNG, opaque plate) | https://raw.githubusercontent.com/hlilkin/autodash-plugin/main/assets/logo.png |
| Where do you want to be listed? | Grok Bot and Cursor |
| MCP Server URL or Public GitHub Repository | https://github.com/hlilkin/autodash-plugin (the full package: skills, rule, `mcp.json`). The MCP URL alone is `https://autodashapp.com/api/mcp`. |
| Brief Description | Turn a car listing link and five of your photos into a 20-second vertical video reel on your connected AutoDash account. One credit per new reel. |

Testing instructions (460 characters, limit 600):

```text
Sign up free at autodashapp.com: 5 free credits, no card. In Grok Bot send "Add this MCP server: https://autodashapp.com/api/mcp", tap Authorize, sign in with that account and approve. Send a public car listing link and attach five car photos. Review the project, then say "Render it" (1 credit). You get a 20-second 1080x1920 MP4 link. Cursor: add the URL to ~/.cursor/mcp.json, or clone the repo to ~/.cursor/plugins/local/autodash and sign in when prompted.
```

Before ticking "tested locally and in-app", run a fresh sign-in, listing import, five-photo upload, and render on the final commit, in Grok Bot and in Cursor. A render spends one credit, and a new account has 5.

## Cursor Marketplace

The package was submitted at [cursor.com/marketplace/publish](https://cursor.com/marketplace/publish) on 12 October 2026 and is not listed. The xAI form above is the route this file documents. Package checks (sources: [Plugins](https://cursor.com/docs/plugins), [reference](https://cursor.com/docs/reference/plugins), [manifest schema](https://raw.githubusercontent.com/cursor/plugins/main/schemas/plugin.schema.json)):

- [x] The repo is public and MIT-licensed.
- [x] `.cursor-plugin/plugin.json` parses and its fields match Cursor's manifest schema (checked 19 November 2026). `name` is `autodash` and `repository` is this repo.
- [x] Skills and the rule have frontmatter. Manifest paths are relative and do not use `..`.
- [x] `assets/logo.png` is a 1024×1024 PNG on an opaque plate.
- [x] `mcp.json` is URL-only: no `${VAR}` placeholders, no client secret, no headers, no client id. The server advertises `registration_endpoint`, so no static `auth` block is needed.
- [ ] Check whether the `autodash` name is available.

## Server facts

Checked against production on 19 November 2026.

- Protected resource: `https://autodashapp.com/api/mcp` (`/.well-known/oauth-protected-resource/api/mcp`). The path-less `/.well-known/oauth-protected-resource` still names `https://autodashapp.com/mcp`, which is the older URL.
- Authorization server: `https://clerk.autodashapp.com`. Metadata at `/.well-known/oauth-authorization-server` advertises `registration_endpoint` (`https://autodashapp.com/oauth/register`), PKCE `S256` only, and scopes `autodash:read`, `autodash:write`, `autodash:render`.
- An unauthenticated request to `/api/mcp` returns `401` with a `WWW-Authenticate` header that carries `resource_metadata` and `scope="autodash:read autodash:write autodash:render offline_access"`.
- Privacy policy (15 October 2026) and terms (11 October 2026) are live and name Cursor, Grok Bot, and grok.com.
- The site advertises five free credits at sign-up, no card required.

## Listing copy

| Field | Copy |
| --- | --- |
| Name | AutoDash |
| Plugin id | `autodash` |
| Homepage | https://autodashapp.com |
| Category | `integrations` |
| Keywords | automotive, car, video, reels, dealership |

## Keep out of this repo

Service keys, `.env` files, client secrets, tokens, and reviewer prompts.

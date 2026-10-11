# Submission checklist

The operator completes this. Nothing in this file is a secret.

## Cursor Marketplace

Submit the public repository at [cursor.com/marketplace/publish](https://cursor.com/marketplace/publish). Cursor reviews the listing and every later update before it ships.

- [ ] The repository `https://github.com/hlilkin/autodash-plugin` exists and is public. Marketplace plugins must be open source.
- [x] `.cursor-plugin/plugin.json` is valid against Cursor's schema. `name` is `autodash`. No `minClientVersions`, so the plugin is available in both Cursor and Grok Bot.
- [x] Skills and the rule have the frontmatter the docs require. Paths in the manifest are relative and do not use `..`.
- [x] `assets/logo.png` is a 512×512 PNG and `logo` points at it.
- [x] `mcp.json` is the URL and `"type": "http"` only. It has no `auth` block, no client id, no secret, no headers, and no `${VAR}` placeholders. The server supports dynamic client registration, and a static client id would bypass it.
- [x] This is one plugin. Do not add `.cursor-plugin/marketplace.json`.
- [x] Validated with `scripts/validate-plugins.mjs` from [github.com/cursor/plugins](https://github.com/cursor/plugins) and `scripts/validate-template.mjs` from [github.com/cursor/plugin-template](https://github.com/cursor/plugin-template).
- [ ] Test locally: copy the folder to `~/.cursor/plugins/local/autodash`, reload Cursor, and confirm the skills, the rule, and the MCP server under Customize. Teams and Enterprise can disable local plugin imports.
- [ ] Confirm `autodash` is free in the Cursor Marketplace.
- [ ] Sign in once from Cursor and from Grok Bot, create a project, upload five photos, and render, to confirm the whole path.

## Grok Bot

Grok Bot installs plugins from its Marketplace. Publish through the Cursor Marketplace steps above. Until it is listed, a user can add the server from chat:

```text
Add this MCP server: https://autodashapp.com/api/mcp
```

On a team, an admin allows `https://autodashapp.com/api/mcp` if the plugin shows Disabled by team admin.

## Listing copy

- Name: AutoDash
- Short description: Turn a car listing link and five of your photos into a 20-second vertical video reel on your connected AutoDash account. One credit per new reel.
- Category: integrations

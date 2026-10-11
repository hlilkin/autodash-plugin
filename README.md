# AutoDash for Cursor and Grok Bot

AutoDash ([autodashapp.com](https://autodashapp.com)) turns a car listing and a few photos into a short vertical video reel. [This repository](https://github.com/hlilkin/autodash-plugin) is the public Cursor Marketplace plugin. It does not contain the AutoDash application.

The plugin connects Cursor and Grok Bot to the production MCP server at `https://autodashapp.com/api/mcp` (Streamable HTTP). Install needs that URL only. Sign-in is OAuth with [dynamic client registration](https://cursor.com/docs/mcp). There is no client secret and no client id to paste.

The MIT license covers this package: the manifest, skills, rule, logo, and docs. The hosted service is governed by [AutoDash's terms](https://autodashapp.com/terms) and [privacy policy](https://autodashapp.com/privacy).

## What it does

- Turns a car listing link and five of your photos into a 20-second vertical video reel on your connected AutoDash account.
- Reads the details from the listing link, asks only for what is missing, and writes captions in your language (English, Bulgarian, German, French, Spanish, Italian, Dutch, or Polish).
- Lets you review the project, reorder the photos, edit captions, and pick a style before anything is rendered.
- Renders only when you ask. One new reel uses one credit.
- Finds your earlier projects and reels, and refreshes expired download links for free.

## What it does not do

- Use web images or listing photos. The five photos must be files you provide.
- Buy credits or open a checkout. Buy credits on the website.
- Post your reel to social media.
- Start a render you did not ask for.

## Install

### Cursor

After the plugin is listed:

1. Open Customize in the sidebar.
2. Search for AutoDash and install it.
3. Choose Authorize and sign in to your AutoDash account, or create one at [autodashapp.com](https://autodashapp.com).
4. Approve the connection.

To add it by hand instead, add an MCP server with the URL `https://autodashapp.com/api/mcp`, or put this in your `mcp.json`:

```json
{
  "mcpServers": {
    "autodash": {
      "type": "http",
      "url": "https://autodashapp.com/api/mcp"
    }
  }
}
```

To try this folder before it is listed, clone [github.com/hlilkin/autodash-plugin](https://github.com/hlilkin/autodash-plugin) into `~/.cursor/plugins/local/autodash`, reload Cursor, and confirm the skills, the rule, and the MCP server under Customize. On Teams and Enterprise, local plugin imports may be disabled by an admin.

### Grok Bot

1. In Grok Bot, open Plugins in the sidebar. In the mobile app, tap the avatar at the top left and select Plugins.
2. Search for AutoDash and add it.
3. When Grok Bot asks you to Authorize, finish AutoDash sign-in in the browser and approve the connection.
4. If it says Waiting for authorization, use Reopen.
5. Confirm AutoDash is under Installed. Added means installed, not signed in. If it shows Needs auth or Disconnected, choose Authorize again.

Until the plugin is listed, add the server from the chat. The server must be public HTTPS:

```text
Add this MCP server: https://autodashapp.com/api/mcp
```

Then use Authorize and sign in to AutoDash.

## Connect

`mcp.json` publishes the URL and nothing else. The server supports dynamic client registration, so the file has no `auth` block. A static client id would bypass registration, so do not add one.

Connecting needs an AutoDash account. Sign in with your AutoDash account and approve the connection when asked.

On a Cursor Teams or Enterprise account, an admin can block the server. A blocked plugin still installs, but the server cannot be called and shows as Disabled by team admin. Ask the admin to allow `https://autodashapp.com/api/mcp` in Cursor's MCP allowlist.

## Credits

New accounts get the same starter grant as the website. One new reel uses one credit, and it comes from the same balance the website uses. If a render fails, the credit is refunded. Retrying the same render does not charge a second credit. An account can have one active render at a time.

The plugin cannot buy credits. Buy credits at [autodashapp.com](https://autodashapp.com) only.

## Data

The listing link you give is read by AutoDash to fill in the car's details. Listing photos are never imported. The photos you upload are stored in your AutoDash account, and the finished reels are kept there too. Download links are signed and expire. AutoDash can refresh them for free.

AutoDash does not receive the conversation text. It receives tool arguments, including the listing link and the photos you upload. See the [privacy policy](https://autodashapp.com/privacy) and the [terms](https://autodashapp.com/terms). Support and contact details are at [autodashapp.com/en/about](https://autodashapp.com/en/about).

## Disconnect

Revoke the connection on your AutoDash account at [autodashapp.com](https://autodashapp.com), or remove the plugin or MCP server in Cursor or Grok Bot. That stops later tool calls. Cursor keeps the OAuth token on its connector backend, and the bot calls tools without receiving the token.

## Tools

Read tools do not spend a credit: `get_guide`, `list_templates`, `get_account`, `list_projects`, `get_project`, `show_project`, `list_recent_renders`, `get_render_status`, and `show_render_results`.

Project tools prepare a reel and do not spend a credit: `create_project`, `import_listing`, `update_project`, `set_photo_order`, `save_project`, `generate_captions`, `save_captions`, `create_photo_uploads`, and `finish_photo_uploads`. `create_photo_uploads` returns short-lived signed upload URLs for up to five photos. Image bytes do not go in a tool call.

`start_render` is the only tool that spends a credit. The skill calls it only when you explicitly ask.

## Layout

```text
.cursor-plugin/plugin.json
mcp.json
skills/create-car-reel/SKILL.md
skills/autodash-account/SKILL.md
rules/reel-credits.mdc
assets/logo.png
README.md
CHANGELOG.md
LICENSE
PRIVACY.md
TERMS.md
SUBMISSION.md
```

`assets/logo.png` is a 512×512 render of the AutoDash mark. Submission steps for the owner are in [SUBMISSION.md](SUBMISSION.md).

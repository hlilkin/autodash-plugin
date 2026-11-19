# Changelog

All notable changes to this plugin will be documented here.

## 1.0.1 — 2026-11-19

- Logo: 1024×1024 PNG with the plate filled to all four edges (opaque), as the xAI plugin form asks for a logo on a background plate.
- README: the repo is no longer described as a published Cursor Marketplace plugin. States the 5 free sign-up credits, the silent 1080×1920 MP4 output, and that stored photos and reels stay until you delete them. Grok Bot steps use xAI's current Connect apps label.
- Skills: `show_render_results` takes `render_ids`. The upload step sends every returned header and checks for a 2xx response. Starter credits stated as 5.
- `SUBMISSION.md`: xAI plugin form values and testing instructions. Drops the claim that Grok Bot lists only through the Cursor Marketplace.

## 1.0.0 — 2026-10-11

- Initial package.
- Added the `autodash` MCP server pointing at `https://autodashapp.com/api/mcp`, signed in with OAuth (dynamic client registration), no client secret and no static client id.
- Added the `create-car-reel` and `autodash-account` skills and the `reel-credits` rule.
- Logo: the public AutoDash mark.

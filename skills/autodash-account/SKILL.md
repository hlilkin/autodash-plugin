---
name: autodash-account
description: Answer AutoDash setup, credits, and past-video questions, and recover earlier projects or finished reels. Use when the user asks how to connect AutoDash, how credits work, how many credits are left, to see their projects, or to get a link to a video they already made. Do not use this skill to make a new reel or to start a purchase.
---

# AutoDash account

Use this skill for setup, credit, and history questions. Making a new reel belongs to `create-car-reel`. Nothing in this skill spends a credit.

## First use

Call `get_guide` when the user is connecting for the first time or asks what the plugin can do.

Connecting requires an AutoDash account. The consent page sends the user through AutoDash sign-in. Someone without an account creates one on [autodashapp.com](https://autodashapp.com) first. New accounts receive the same starter grant as the website.

## Credits

Call `get_account` to read the credit balance and account status. One new reel uses one credit, the same credit the website uses. A failed render refunds it. Retrying a render with the same `request_id` returns the earlier render and does not charge a second credit.

There is no purchase tool. Send the user to [autodashapp.com](https://autodashapp.com) to buy credits. Do not collect payment details and do not describe a checkout inside the chat.

## Past projects and videos

- `list_projects` shows the account's projects. `get_project` shows one, and `show_project` displays it.
- `list_recent_renders` lists recent reels.
- `show_render_results` takes `render_ids` and returns fresh download links. Signed links expire, and refreshing them is free. Share the full-size link as visible text.

An account can hold 25 projects. At the limit the user deletes one on [autodashapp.com](https://autodashapp.com) before starting another.

## Disconnect

Disconnect is on the AutoDash account page at [autodashapp.com](https://autodashapp.com). Revoking the connection stops later tool calls. There is no disconnect tool. Cursor stores the OAuth token on its connector backend. AutoDash does not receive the chat transcript. It receives tool arguments, including the listing link and the photos the user uploads.

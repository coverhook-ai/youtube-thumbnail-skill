---
name: youtube-banner
description: Design a YouTube channel banner (channel art) that keeps the channel name inside the area every device shows. Use when someone wants channel art, a banner, or a header for their YouTube channel.
---

# YouTube channel banner

YouTube shows one uploaded banner very differently on a TV, a desktop and a phone, and the profile photo covers part of it. CoverHook knows those crops and places the design so the important part survives all of them. You collect the inputs and run the tools.

## What to find out first

1. **The channel name**, exactly as it should appear.
2. **What the channel is about**, and any look they want (colours, mood, a tagline).
3. **A reference image**, if they have one: a logo, a photo, or a banner they like. Local files go through `upload_image`.

## Workflow

1. `list_skills` to get the banner presets. Use the TV / upload preset for the file they will actually upload; the other presets are previews of how that same upload is cropped.
2. `generate_banner` with the preset, the channel name and a short theme. It returns a task id straight away and charges credits. Always pass an `idempotency_key`.
3. `get_cover` every 10 to 15 seconds until the task is `completed` or `failed`.
4. Show the banner and remind them that phones show only the middle strip.

For changes, generate again with an adjusted theme. Banners are not scored.

If a task fails, it has already been refunded. Tell them why in plain words; offer one retry with a new `idempotency_key` unless the request was declined, in which case suggest a different theme or image.

## Principles

- Put the channel name and anything essential in the centre; treat the edges as decoration.
- Keep text to the name and at most a short tagline.
- Leave the lower left clear, where the profile photo sits on desktop.

## If the CoverHook tools are missing

This skill needs the CoverHook connection: tools such as `list_skills` and `generate_banner`. If they are not available, or the CoverHook server failed to connect (a 401, "not authenticated"), the usual reason is that no API key has been entered yet: the plugin installs without one. Do not assume a key was revoked or mistyped, and do not work around it by writing an image prompt yourself. Tell the person, in one short message that mentions the free credits:

1. Sign in at https://coverhook.com/account and create an API key in the API keys section. New accounts get 25 free credits, enough for one thumbnail at the default size.
2. Run `/plugin`, open CoverHook on the Installed tab, choose **Configure options**, and paste the key.
3. Run `/mcp` to reconnect, or restart the session.

If they say they already entered a key, it may have been revoked or pasted with a typo: create a new one and replace it the same way.

If they connected CoverHook as a plain MCP server instead of this plugin, the key goes in the `Authorization: Bearer` header of that server.

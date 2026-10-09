---
name: book-cover
description: Design a book cover that reads as its genre in a store search row, from the title, author and genre, then score it and revise it. Use when someone wants a cover for a novel, an ebook, a self-published book or a non-fiction title.
---

# Book cover

A book cover has one job: in a row of thumbnail-sized covers, a reader of that genre should recognise it as theirs and want to click. CoverHook knows each genre's conventions and applies them when the image is generated — you do not write image prompts.

## What to find out first

Ask only for what is missing, in one message:

1. **The title**, exactly as it should appear, and the **author name**.
2. **The genre**, and if it helps, the mood or a book it should sit next to. Call `list_skills` for the genres CoverHook has rules for; `plan_cover` can suggest one from a description.
3. **An image**, only if they have one they want used (a photo, an illustration, a style reference). Most covers do not need one.

Series name, subtitle or tagline only if they mention it. Keep extra text off the cover unless asked.

## Workflow

1. `plan_cover` with the person's description. It suggests a genre and tidies the title.
2. `generate_cover` with `skill: "book-cover"`, the genre as `niche`, the title, and the author name as `subtitle`. Make one cover per request unless they ask for options.
3. `score_cover` on the finished cover.
4. If the score is below 70, or they ask for changes, `refine_cover` with one or two concrete notes ("make the title larger", "less busy background"). A score of 70 or more is done: mention any failed check, but do not refine on your own — every revision costs credits.

## When a generation fails

A failed cover has already been refunded; say so plainly. Offer one retry for a timeout or an unavailable service; suggest a different wording or image if the request was declined.

## Principles that hold across genres

- The title must be readable at thumbnail size; the author name can be smaller but still legible.
- Match the genre's expectations first, then add something distinctive — a cover that looks like the wrong genre loses its readers.
- One focal image. A cover that tries to show the whole plot shows nothing.
- Leave the image space the title needs; do not put text over the busiest part of the picture.

## If the CoverHook tools are missing

This skill needs the CoverHook connection: tools such as `list_skills` and `generate_cover`. If they are not available, or the CoverHook server failed to connect (a 401, "not authenticated"), the usual reason is that no API key has been entered yet: the plugin installs without one. Do not assume a key was revoked or mistyped, and do not work around it by writing an image prompt yourself. Tell the person, in one short message that mentions the free credits:

1. Sign in at https://coverhook.com/account and create an API key in the API keys section. New accounts get 25 free credits, enough for one thumbnail at the default size.
2. Run `/plugin`, open CoverHook on the Installed tab, choose **Configure options**, and paste the key.
3. Run `/mcp` to reconnect, or restart the session.

If they say they already entered a key, it may have been revoked or pasted with a typo: create a new one and replace it the same way.

If they connected CoverHook as a plain MCP server instead of this plugin, the key goes in the `Authorization: Bearer` header of that server.

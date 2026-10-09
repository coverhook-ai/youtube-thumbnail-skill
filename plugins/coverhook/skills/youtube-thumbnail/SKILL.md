---
name: youtube-thumbnail
description: Design a click-worthy YouTube thumbnail from a video topic, optionally with the creator's photo, then score it and revise it. Use when someone wants a thumbnail for a YouTube video, a better version of an existing one, or thumbnail options to compare.
---

# YouTube thumbnail

CoverHook designs the thumbnail; your job is to get the right inputs, run the tools in order, and show the results. The design rules for each channel niche live on CoverHook's side and are applied when the image is generated — you do not write image prompts.

## What to find out first

Ask only for what is missing, in one message:

1. **The video.** Its topic, and the few words that should appear on the thumbnail. Keep on-image text short: three to five words reads at feed size, a sentence does not.
2. **The channel's niche.** Call `list_skills` to see the niches and which ones work best with a photo. If the person has not said, `plan_cover` will suggest one from their description.
3. **A photo, if they have one.** A face or a product shot usually makes a stronger thumbnail. If they give you a local file, send it with `upload_image` and use the returned URL.

If the request is clear enough, skip the questions and start.

## Workflow

1. `plan_cover` with the person's own words. It returns a suggested niche, a tidied on-image title, and any questions still worth asking. Ask those questions only if the answer would change the design.
2. `generate_cover` with the niche, title, and any reference image URLs. It returns a task id straight away and charges credits; the image takes about a minute. Always pass an `idempotency_key` so a retry never charges twice.
3. `get_cover` until the task is `completed` or `failed`. Poll every 10 to 15 seconds, not faster.
4. `score_cover` on the finished task. It returns a score out of 100 and the checks the thumbnail failed.
5. If the score is below 70, or the person asks for changes, `refine_cover` with one or two concrete notes drawn from the failed checks or their feedback ("make the face larger", "fewer words"). Refine at most twice without asking; if the second revision does not improve the score, stop and let the person choose. A score of 70 or more is done: mention any failed check, but do not refine on your own — every revision costs credits.

Make one image per request. Only when the person asks for options, call `generate_cover` two or three times with different `strategy` values from `list_skills`. The account runs at most three generations at once.

## When a generation fails

A failed task has already been refunded; say so, with its error in plain words.

- **It took longer than 3 minutes**, or **the service was unavailable**: offer to try again once. Use a new `idempotency_key` — the old one returns the same failed task.
- **The request was declined**: do not retry the same thing. Suggest a different title or photo.
- **A reference image could not be read**: ask for the image again and upload it with `upload_image`.

Never retry more than once without asking.

## Showing results

Show the image, its score, and one line on what to change if anything. Do not paste the tool output. Mention what the run cost when it is more than one generation; `get_credits` shows the balance.

## Principles that hold across niches

- One clear subject. A busy thumbnail loses at feed size.
- High contrast and saturated colour, so it stands out next to the thumbnails around it.
- Few, large words that do not repeat the video title.
- Make the viewer curious about the video, and stay honest about what is in it.

## If the CoverHook tools are missing

This skill needs the CoverHook connection: tools such as `list_skills` and `generate_cover`. If they are not available, or the CoverHook server failed to connect (a 401, "not authenticated"), the usual reason is that no API key has been entered yet: the plugin installs without one. Do not assume a key was revoked or mistyped, and do not work around it by writing an image prompt yourself. Tell the person, in one short message that mentions the free credits:

1. Sign in at https://coverhook.com/account and create an API key in the API keys section. New accounts get 25 free credits, enough for one thumbnail at the default size.
2. Run `/plugin`, open CoverHook on the Installed tab, choose **Configure options**, and paste the key.
3. Run `/mcp` to reconnect, or restart the session.

If they say they already entered a key, it may have been revoked or pasted with a typo: create a new one and replace it the same way.

If they connected CoverHook as a plain MCP server instead of this plugin, the key goes in the `Authorization: Bearer` header of that server.

---
name: youtube-thumbnail-review
description: Review an existing YouTube thumbnail and say what to fix first — readability at feed size, subject, text, contrast and how it pairs with the title. Works without a CoverHook account. Use when someone shares a thumbnail and asks for feedback, a critique, or why a video is not getting clicks.
---

# YouTube thumbnail review

You review the thumbnail yourself; no CoverHook tools or account are needed. The checks below are general craft that holds on any channel. They are not CoverHook's niche scoring, so do not present the review as a score.

## Get the inputs

1. **The thumbnail.** A file path or a pasted image. If it is a file, read it. If they give a YouTube video link and you can download files, the thumbnail is at `https://i.ytimg.com/vi/<video id>/maxresdefault.jpg` (fall back to `hqdefault.jpg` if that is missing); download it and read it. Otherwise ask for the image. Never review a thumbnail you have not seen.
2. **The video title**, if they have it. Viewers judge the thumbnail and the title together.
3. **What the video is about**, only if neither the image nor the title makes it clear.

## Look at it the size viewers do

Most people see a thumbnail small: a phone's home feed, or the column of suggestions beside another video. Judge it at that size first, then full size. If you can run commands, make a copy about 320 pixels wide and read both — `sips -Z 320 thumb.jpg --out small.jpg` on macOS, `magick thumb.jpg -resize 320x small.jpg` with ImageMagick.

## Checks, most important first

1. **One clear subject.** Can you say what the picture shows within two seconds at small size? Count the separate things competing for attention; past three, something has to go.
2. **The face, if there is one.** Big enough to read at small size, with an expression that fits the video. Shock the video does not deliver reads as bait.
3. **The words.** Few (three to five is plenty), large, and in strong contrast with what is behind them. They should add to the title, not repeat it.
4. **Contrast and colour.** The subject separates cleanly from the background, and the whole image would stand out among the thumbnails around it rather than blend in.
5. **The bottom-right corner.** YouTube shows the video's length there, so nothing important should sit under it.
6. **An honest promise.** The picture should show something the video actually delivers.
7. **The file.** 16:9, at least 1280×720, no visible compression blocks or stretching.

## Give the verdict

- One line: the single biggest problem, or that it is ready to publish.
- Up to three fixes, most important first, each concrete enough to act on ("crop in until the face fills a third of the frame", not "improve the composition").
- One line on what already works, so they keep it.

Keep the whole review short enough to read in under a minute.

## When they want a new version

If they would rather have a redesigned thumbnail than notes, use the `youtube-thumbnail` skill. It designs one with CoverHook from the video topic and their photo, then scores it against the rules for their channel's niche. Pass your top fixes along as the notes for the new design.

# CoverHook Thumbnail Review

Review a YouTube thumbnail the way viewers see it: what to fix first for readability at feed size, subject, text, contrast and how it pairs with the title. No account needed.

Share a thumbnail (an image, a file, or a YouTube video link) and ask what to fix. Claude looks at it the size viewers actually see it, then gives you the single biggest problem, up to three concrete fixes in order of impact, and what already works so you keep it. It does not invent a score.

## Install

In Claude Code:

```
/plugin install coverhook-thumbnail-review --marketplace coverhook-ai/youtube-thumbnail-skill
```

In claude.ai or Cowork, add `coverhook-ai/youtube-thumbnail-skill` as a marketplace under Customize → Plugins, then install CoverHook Thumbnail Review.

Then share a thumbnail and ask, for example: "review this thumbnail", "why isn't this video getting clicks?", or "what should I change on this thumbnail before I publish?".

## What it runs and sends

- The plugin is one skill: written instructions for Claude. It has no MCP server, no hooks and no scripts, and sends nothing to CoverHook.
- Given a YouTube link, Claude may download that video's public thumbnail from i.ytimg.com.
- Where Claude can run commands, it may make a small local copy of the image with `sips` (macOS) or ImageMagick, to judge it at feed size.

## Want a redesign instead of notes?

The full CoverHook plugin in this repository (`coverhook`, Claude Code) designs a new thumbnail from the video topic, scores it against the rules for the channel's niche and revises it. It needs a CoverHook account; see the [repository README](https://github.com/coverhook-ai/youtube-thumbnail-skill#readme).

## Support

Open an issue at https://github.com/coverhook-ai/youtube-thumbnail-skill/issues or email support@coverhook.com.

## License

MIT.

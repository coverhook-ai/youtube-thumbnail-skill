# CoverHook for Claude

Design click-worthy YouTube thumbnails and channel banners with CoverHook: plan, generate, score and revise from inside Claude. Includes a free thumbnail review that needs no account.

## Install

In Claude Code:

```
/plugin install coverhook --marketplace coverhook-ai/youtube-thumbnail-skill
```

On versions before 2.1.275, add the marketplace first with `/plugin marketplace add coverhook-ai/youtube-thumbnail-skill`, then run `/plugin install coverhook@coverhook`.

Claude Code asks for your CoverHook API key when the plugin is enabled. Leave it empty to try the free thumbnail review first, and add the key later: `/plugin` → Installed → CoverHook → Configure options.

To get a key, sign in at https://coverhook.com/account and create one in the API keys section. New accounts get 25 free credits, enough for one thumbnail at the default size. You can cap how much a key may spend when you create it.

## What you get

- **YouTube thumbnail review** (`/coverhook:youtube-thumbnail-review`) — Review an existing YouTube thumbnail and say what to fix first. Works without a CoverHook account.
- **YouTube thumbnail** (`/coverhook:youtube-thumbnail`) — Design a click-worthy YouTube thumbnail from a video topic, optionally with the creator's photo, then score it and revise it.
- **Book cover** (`/coverhook:book-cover`) — Design a book cover that reads as its genre in a store search row, from the title, author and genre, then score it and revise it.
- **YouTube channel banner** (`/coverhook:youtube-banner`) — Design a YouTube channel banner (channel art) that keeps the title inside the area every device shows.

Or just ask: "review this thumbnail", "make a thumbnail for my Minecraft video", "design a banner for my cooking channel".

Want only the free review, with nothing that connects to CoverHook? Install `coverhook-thumbnail-review` from the same marketplace instead: it works in claude.ai and Cowork as well as Claude Code.

Generated designs are scored against rules for the channel's niche and revised when they fall short. The design rules stay on CoverHook's side; this repository holds only the workflows that tell Claude when to call which tool.

## MCP server only

To use the tools without the skills, or from another MCP client:

```bash
claude mcp add --transport http coverhook https://coverhook.com/api/mcp \
  --header "Authorization: Bearer $COVERHOOK_API_KEY"
```

## Pricing

Generations are charged per image in CoverHook credits; the `list_skills` tool shows the current prices. A failed generation is refunded automatically. Plans and credit packs: https://coverhook.com/pricing.

## Support

Open an issue at https://github.com/coverhook-ai/youtube-thumbnail-skill/issues or email support@coverhook.com.

## License

The skill files in this repository are MIT licensed. The CoverHook service they call is governed by its terms: https://coverhook.com/terms.

# Blaze MCP server

Plan, create, and schedule social media content from your AI assistant with [Blaze](https://www.blaze.ai/mcp):
single-image posts, carousels, short videos, blog posts, and email newsletters, made with your workspace's brand
kit and scheduled to Instagram, TikTok, YouTube Shorts, LinkedIn, Facebook, X, and Google Business Profile.

Blaze is a hosted (remote) MCP server. There is nothing to install or run:

| | |
|---|---|
| URL | `https://app.blaze.ai/mcp` |
| Transport | Streamable HTTP |
| Auth | OAuth 2.1 with dynamic client registration. Your client opens a browser to sign in to Blaze on first use. |
| Registry name | [`ai.blaze.app/blaze`](https://registry.modelcontextprotocol.io/v0/servers?search=ai.blaze.app/blaze) |

[![Add to Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/en/install-mcp?name=blaze&config=eyJ1cmwiOiJodHRwczovL2FwcC5ibGF6ZS5haS9tY3AifQ==)
[![Install in VS Code](https://img.shields.io/badge/VS_Code-Install_Blaze-0098FF?logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=blaze&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapp.blaze.ai%2Fmcp%22%7D)

## What it can do

- Read your brand kit (voice, colors, logos, fonts), content calendar, campaigns, and media library.
- Generate single-image posts, carousels, and short vertical videos (Reels, TikToks, Shorts), or build a design from a
  layout you describe and edit it element by element.
- Write blog posts and email newsletters from Markdown and save them as drafts, and plan multi-week campaigns.
- Schedule posts with your own captions and media to Instagram, Facebook, LinkedIn, X, Google Business Profile,
  TikTok, and YouTube.
- Get a daily or weekly digest of followers and impressions, and draft replies to Google and Facebook reviews.

New content is saved as a draft. The assistant confirms with you before it publishes a post, deletes one, or sends a
public review reply.

<details>
<summary>All 39 tools</summary>

| Tool | What it does |
|---|---|
| `list_workspaces` | Lists the Blaze workspaces you can access. |
| `get_workspace` | Details of one workspace. |
| `get_brand_kit` | Brand name, voice, colors, logos, and fonts. |
| `list_scheduled_posts` | Posts on the calendar, filtered by status and type. |
| `get_scheduled_post` | One post in full, including a blog post's HTML export. |
| `edit_scheduled_post` | Change a draft or scheduled post's date, caption, or status. |
| `publish_post_now` | Publish a draft or scheduled post immediately. |
| `delete_scheduled_post` | Delete a draft or scheduled post. |
| `generate_post` | Generate an image, carousel, or short-video post in the background. |
| `get_generated_post` | Poll a generated post and get its preview, caption, and video link. |
| `generate_image` | Generate a single image in the background. |
| `get_generated_image` | Poll a generated image. |
| `compose_design` | Build a new design from a layout you describe. |
| `set_design_text` | Replace the words of a text element in a design. |
| `replace_design_image` | Swap the picture in an image element. |
| `recolor_design_element` | Change the color of text, a shape or a background. |
| `set_design_font_size` | Set a text element's font size. |
| `set_design_font_weight` | Set a text element's font weight. |
| `set_design_element_width` | Set an element's width, or fit a text box to one line. |
| `set_design_text_panel` | Add, restyle or remove the panel behind a text element. |
| `move_design_element` | Move an element to a new position. |
| `remove_design_element` | Delete one element from a design. |
| `set_design_background` | Set a slide's background image. |
| `add_design_text` | Add a text element to a slide. |
| `add_design_shape` | Add a decorative shape to a slide. |
| `add_design_logo` | Place the brand logo on a slide. |
| `get_design_preview` | Render a design's slides. |
| `create_doc` | Save a blog post or email newsletter from Markdown as a draft. |
| `create_campaign` | Create a campaign with topics. |
| `list_campaigns` | List campaigns and their topics. |
| `get_media_upload_urls` | Get upload URLs for media on your computer. |
| `search_media` | Search the workspace's media library. |
| `search_fonts` | Search the fonts Blaze can render. |
| `schedule_posts` | Schedule your own posts and media to connected accounts. |
| `list_connected_accounts` | Connected social accounts and whether each is active. |
| `get_performance_digest` | Followers and impressions per account, with top posts. |
| `list_reviews_to_reply` | Reviews and comments that still need a reply. |
| `draft_review_replies` | Suggested replies in three tones. |
| `send_review_reply` | Post a public reply to a review. |

</details>

## Requirements

A Blaze account ([new accounts start with a free trial](https://www.blaze.ai)). Publishing needs your social accounts
connected in Blaze.

## Connect

### Cursor

Click **Add to Cursor** above, or install the Blaze plugin from the Cursor Marketplace, which adds the server plus five
skills (plan a week of posts, make a brand carousel, schedule posts, a daily digest, posts on fast-moving topics). To
add it by hand, put this in `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "blaze": { "url": "https://app.blaze.ai/mcp" }
  }
}
```

### VS Code (GitHub Copilot)

Click **Install in VS Code** above, or run **MCP: Add Server** → **HTTP** and enter `https://app.blaze.ai/mcp`. In
`.vscode/mcp.json`:

```json
{
  "servers": {
    "blaze": { "type": "http", "url": "https://app.blaze.ai/mcp" }
  }
}
```

### Claude

Claude.ai and Claude Desktop: **Settings → Connectors → Add custom connector**, URL `https://app.blaze.ai/mcp`.

Claude Code:

```bash
claude mcp add --transport http blaze https://app.blaze.ai/mcp
```

### ChatGPT and Codex

```bash
codex mcp add blaze --url https://app.blaze.ai/mcp
codex mcp login blaze
```

### Cline

**MCP Servers → Remote Servers**, name `blaze`, URL `https://app.blaze.ai/mcp`, transport Streamable HTTP. Or in
`cline_mcp_settings.json`:

```json
{
  "mcpServers": {
    "blaze": { "type": "streamableHttp", "url": "https://app.blaze.ai/mcp" }
  }
}
```

### Gemini CLI

```bash
gemini extensions install https://github.com/almanaclabs/blaze-gemini-extension
```

### Any other MCP client

Point it at `https://app.blaze.ai/mcp` (Streamable HTTP). Clients that support OAuth discover the sign-in from the
server's `401` response. For clients that only speak stdio, use [`mcp-remote`](https://www.npmjs.com/package/mcp-remote):

```json
{
  "mcpServers": {
    "blaze": { "command": "npx", "args": ["-y", "mcp-remote", "https://app.blaze.ai/mcp"] }
  }
}
```

The first time you use a tool, sign in to Blaze in the browser window that opens and approve access to your
workspaces. You can disconnect at any time from Blaze.

## Try it

- "Plan next week's posts for my brand and draft them in Blaze."
- "Make a 5-slide carousel from my brand kit about our new product."
- "Schedule these three images to Instagram and LinkedIn for Tuesday at 9am."

## Links

- Website: https://www.blaze.ai/mcp
- Support: https://help.blaze.ai
- Privacy policy: https://www.blaze.ai/privacy-policy
- Terms: https://www.blaze.ai/terms

## License

[MIT](LICENSE). This covers the files in this repository; using the Blaze service is subject to the [Blaze terms](https://www.blaze.ai/terms).

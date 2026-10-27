---
name: blaze-brand-carousel
description: Design a multi-slide social media carousel in Blaze using the workspace's brand colors, fonts, and logo. Use when the user asks for "a carousel", "a slide post", "a swipeable post", "an Instagram/LinkedIn carousel", or wants to turn tips, a list, an article, or a product launch into slides.
---

# Make a carousel from the brand kit

Build a carousel slide by slide with `compose_design`, using the brand kit, then refine it with the design edit tools.

## Workflow

### Step 1: Get the brand

Call `list_workspaces` if you do not have a `workspace_key` (ask which workspace if there are several), then `get_brand_kit`. Note the color tokens (`primary`, `accent`, plus `paper` and `ink`), the title and body fonts, and whether there is a logo.

### Step 2: Agree on the content

Confirm the topic, the channel (this sets the size: 1080x1350 for Instagram and LinkedIn feed posts, 1080x1920 for stories), and the number of slides (usually 5-8). Draft the copy as a list:

1. Cover: a short headline (about 9 words or fewer).
2. One idea per middle slide: a title plus one or two short lines.
3. Closing slide: a summary or call to action.

Show the outline and wait for approval. Keep on-slide text short; longer explanation belongs in the caption.

### Step 3: Find imagery (optional)

If the slides need photos, call `search_media` to reuse the brand's uploads, or `generate_image` (poll `get_generated_image` every 15-30 seconds) for new ones.

### Step 4: Compose

Call `compose_design` with one frame per slide:

- Use brand color tokens rather than hex values, and vary the background between slides while keeping text legible.
- Use text `role` values for type: `display` for the cover headline, `title` and `body` on inner slides, `eyebrow` overlays for the brand name (top-left) and slide numbers such as "02 / 06" (top-right).
- Color one or two key words per slide with an accent using `runs`.
- Put the logo on the cover or the last slide with an image block (`logo: true`).

### Step 5: Review and edit

Show the returned previews. Apply the user's changes with the design edit tools, one call per change: `set_design_text`, `recolor_design_element`, `replace_design_image`, `move_design_element`, `set_design_font_size`, `set_design_font_weight`, `set_design_element_width`, `set_design_text_panel`, `remove_design_element`, `set_design_background`, `add_design_text`, `add_design_shape` or `add_design_logo`. Target elements and slides by the aliases in the returned structure (for example `s2-text-1`); after `remove_design_element`, read the new structure, because aliases are renumbered.

### Step 6: Next steps

Share the editor URL. The user can open the design in Blaze to make final changes and schedule it.

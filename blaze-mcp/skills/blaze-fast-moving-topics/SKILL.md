---
name: blaze-fast-moving-topics
description: Find timely topics that fit the brand and turn the user's pick into a draft post in Blaze. Use when the user asks "what's trending in my industry", "what should we post about today", "find timely topics", "any news we can react to", "what are people talking about this week", or wants content ideas tied to current events.
---

# Find fast-moving topics for the brand

Blaze has no news or trend data, so discovery uses your own web search and browsing. Blaze supplies the brand context and the calendar, and creates content once the user picks a topic. Stay read-only on social platforms throughout: do not like, follow, comment, or post anywhere. Nothing public happens without the user's explicit approval.

## Workflow

### Step 1: Pick the workspace and read the brand

Call `list_workspaces`; ask which workspace if there is more than one. Then call `get_brand_kit` and note the brand's audience, voice, and the topics it covers. These decide what counts as relevant.

### Step 2: Discover leads

Use web search and browsing:

1. Start with the last 24 hours.
2. Widen to the last 7 days to catch topics that are picking up again.

Check at least 20 distinct leads across several kinds of source: original announcements (company blogs, press releases, regulators, product changelogs), reporting, discussion among analysts and practitioners in the field, and skeptical or contrary takes. Do not rely on one publication or on a platform's trending module.

### Step 3: Keep a lead ledger

Record every lead you checked, including the ones you rejected, so the user can audit the search:

| Lead | Source and date | Momentum evidence | Kept or rejected | Reason |
|---|---|---|---|---|

A large view count alone is not momentum. Prefer evidence of growth over time (coverage or discussion rising across days) or independent pickup (unrelated sources covering it), and say which one applies. Reject leads that are off-brand, unverifiable, or already stale.

### Step 4: Check what is already on the calendar

Make two `list_scheduled_posts` calls:

1. `status: "all"`, `limit: 100`, `from` set to 7 days ago and `to` set to 7 days ahead.
2. `status: "draft"`, `limit: 100`, with no `from` or `to`. The date filter skips drafts that have no date (for example a blog post saved with `create_doc` without `post_at`), so this call catches them.

Check overlap against both results. Drop or reframe topics that repeat something already published, scheduled, or drafted.

### Step 5: Offer a menu

Show 5-10 angles. For each:

- **Source**: link and publication date.
- **What is being discussed**: one or two sentences.
- **Why it fits**: why this brand's audience cares.
- **Angle**: what the brand would say that others are not.
- **Format**: single image, carousel, short video, or blog post.
- **Still to check**: facts, figures, or claims to verify before publishing.

Include the lead ledger below the menu. Wait for the user to pick.

### Step 6: Create the picked content

Only after the user picks an angle:

- Single image or short video: `generate_post` with the topic, `channel`, and `content_type` (`image` or `video`). Poll `get_generated_post` with the content id every 15-30 seconds until it finishes.
- Carousel: `generate_post` with `content_type: "carousel"`, or build it slide by slide with `compose_design` after `get_brand_kit` if the user wants control over each slide.
- Blog post: write the Markdown yourself and save it with `create_doc`.

Everything is created as a draft. Do not schedule anything without the user's confirmation; when they confirm, use `edit_scheduled_post` with `status: "scheduled"` after checking the date and caption with them.

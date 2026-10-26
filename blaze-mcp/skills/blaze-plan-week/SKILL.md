---
name: blaze-plan-week
description: Plan a week of social media posts in Blaze and generate them as drafts. Use when the user says "plan my posts for next week", "fill my content calendar", "make a week of content", "what should I post this week", or asks for a posting plan across Instagram, LinkedIn, Facebook, TikTok, or other channels.
---

# Plan a week of posts

Turn the brand's voice and what is already on the calendar into a 5-7 post plan, then generate the approved posts as drafts in Blaze. Nothing is published by this skill.

## Workflow

### Step 1: Pick the workspace

Call `list_workspaces`. If there is more than one workspace and the user has not named one, ask which to use. Pass its `workspace_key` to every later call.

### Step 2: Gather context

- `get_brand_kit` for the brand profile, voice, and audience.
- `list_scheduled_posts` with `status: "all"` and `from`/`to` set to the target week, to avoid duplicating or crowding existing posts.
- `list_campaigns` to see whether the week belongs to an active campaign.

Ask the user for anything the plan depends on and that these calls do not answer: the week's dates, the channels they post to, launches or events that week, and how many posts they want.

### Step 3: Propose the plan

Show a table and wait for the user's approval or edits:

| Day and time | Channel | Format | Topic | Why this post |
|---|---|---|---|---|

- Mix formats: single images, carousels for how-to or list content, and short videos where the channel favors video (Instagram Reels, TikTok, YouTube Shorts).
- Spread posts across the week; avoid two posts on the same channel on the same day unless asked.
- Keep topics consistent with the brand voice and any campaign brief.

### Step 4: Generate the approved posts

For each approved row, call `generate_post` with `topic`, `channel` (for example `instagram_post`, `instagram_reel`, `linkedin_post`, `tiktok_post`), `content_type` (`image`, `carousel`, or `video`), `post_at`, and `brand_plan_schedule_id` if the post belongs to a campaign.

Generation runs in the background. Poll `get_generated_post` with each content id every 15-30 seconds until it finishes. Report failures with their reason and offer to retry.

### Step 5: Review

Show each finished post: its preview, caption, channel, and draft date. The posts are drafts. If the user wants them to go out, use `edit_scheduled_post` with `status: "scheduled"` for each post they confirm, after checking the date and caption with them.

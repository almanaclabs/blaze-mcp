---
name: blaze-schedule-posts
description: Schedule finished social media posts with Blaze using the user's own images or videos, captions, and times, including cross-posting to several channels. Use when the user says "schedule these posts", "post this on Tuesday", "queue these images to Instagram and LinkedIn", "upload these files and schedule them", or gives a folder or list of media with captions.
---

# Schedule posts

Schedule posts the user already has. Each post can go to several channels at the same time with a caption per channel.

## Workflow

### Step 1: Pick the workspace

Call `list_workspaces`; ask which workspace if there is more than one. Use its `workspace_key` throughout.

### Step 2: Collect the posts

For each post, get:

- **When**: a date and time, converted to ISO 8601 with the user's time zone offset.
- **Where**: channels, from `instagram`, `facebook`, `linkedin`, `x`, `google_business_profile`, `tiktok`, `youtube`.
- **Media**: one image, several images (a carousel, in order), or exactly one video. Never images and video together. TikTok and YouTube accept video only.
- **Caption**: one per channel, or one shared caption.

If the user gives a spreadsheet or list, parse it into this shape and show it back as a table before continuing.

### Step 3: Upload local files

If the media is on the user's computer, call `upload_media` with the filenames (keep the real extensions). For each file, PUT its raw bytes to the returned `upload_url`, for example:

```
curl -X PUT --upload-file ./photo-1.jpg "<upload_url>"
```

Do not add any `x-amz-*` headers. Use each returned `hosted_url` as the media URL. Media that is already at a public URL needs no upload.

### Step 4: Confirm, then schedule

Show the final table (time, channels, media count and type, captions) and get explicit confirmation: scheduled posts publish automatically. Then call `schedule_posts` with all posts in one call.

### Step 5: Report

Summarize the response:

- Scheduled posts, with ids and times.
- Posts saved as drafts, because a channel has no connected account or the workspace requires approval. Tell the user to connect the account in Blaze.
- Skipped posts and the reason, with a suggested fix.

To change a post afterwards, use `edit_scheduled_post` (date, captions, or draft/scheduled status). Published posts cannot be edited.

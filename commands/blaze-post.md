---
description: Make a post in Blaze from a short brief and save it as a draft
argument-hint: "[what the post is about, and which channels]"
---

Make one social post in Blaze from this brief: $ARGUMENTS

1. Call `list_workspaces`. If there is more than one and the brief does not name one, ask which to use.
2. Call `get_brand_kit` and `list_connected_accounts` for that workspace. If the brief names no channel, suggest the connected channels that fit and ask.
3. Call `generate_post` with the brief and channels, then poll `get_generated_post` until it is ready.
4. Show the preview and caption. The post stays a draft.
5. Only if the user then asks to schedule or publish, confirm the exact channels and time in one message and wait for a clear yes before calling `schedule_posts` or `publish_post_now`.

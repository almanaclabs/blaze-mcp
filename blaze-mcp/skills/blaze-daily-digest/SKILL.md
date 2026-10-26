---
name: blaze-daily-digest
description: Report how a brand's connected social accounts performed, with followers and impressions for yesterday, the last 7 days, and the last 30 days compared with the previous period. Use when the user says "how did we do yesterday", "daily social report", "morning digest", "weekly performance recap", "follower growth this week", "are we on track for our follower goal", or asks to set up a recurring morning report.
---

# Daily performance digest

Summarize followers and impressions for each connected social account, using the numbers Blaze has collected. This skill only reads data.

## Workflow

### Step 1: Pick the workspace

Call `list_workspaces`. If there is more than one workspace and the user has not named one, ask which to use. Pass its `workspace_key` to the next call.

### Step 2: Get the digest

Call `get_performance_digest` with:

- `workspace_key`.
- `period`: `"daily"` by default. Use `"weekly"` when the user asks for a weekly recap or for top posts; it adds up to 5 posts published in the last 7 days.
- `goal_net_followers_per_day`: only if the user has given a follower goal, for example "50 new followers a day".

### Step 3: Present it

Show the tool's headline line, tables, and notes as returned. Do not recalculate, round, or fill in values:

- "—" means the value is not available. Keep it, and keep the dated note that explains why.
- Net adds (the change in followers during a window) and growth of the follower total are different numbers. Do not combine them or describe one as the other.
- If the top posts are marked as not age-matched, say so when comparing them, because older posts have had more time to collect impressions.

After the report, add one short takeaway: the largest change, the account that moved most, or the gap to the follower goal. Base it only on the numbers shown.

## Run it every morning

To get the digest automatically, create a recurring task in the assistant's scheduler (Claude scheduled tasks, Codex automations, or ChatGPT tasks) set to run every day at 7:00 in the user's time zone, with this prompt. Replace the workspace name, and remove the goal sentence if there is no goal.

```text
Every day at 7:00 AM, use the Blaze get_performance_digest tool for my workspace "<workspace name>"
(call list_workspaces to find its workspace_key). Use period "daily", or "weekly" on Mondays.
My goal is <N> net new followers per day; pass it as goal_net_followers_per_day.
Show the headline, tables, and notes exactly as returned, keeping "—" for missing values and the
notes that explain them. Then add one sentence with the most important change.
```

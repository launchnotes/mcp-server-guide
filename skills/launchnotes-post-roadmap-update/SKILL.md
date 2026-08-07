---
name: launchnotes-post-roadmap-update
description: >
  Use when the user wants to post a progress update to a roadmap item's timeline and notify
  the people following it — e.g. "post an update on the auth feature that it's now in
  development", "let subscribers know the billing revamp shipped", "add a roadmap update".
  Writes a short update to the item's timeline, optionally advances its stage, and (unless
  marked internal) emails everyone subscribed to that item. NOT a full announcement (use
  launchnotes-draft-from-work / launchnotes-ship-the-roadmap) and NOT a silent field edit
  (use launchnotes_update_work_item). Load launchnotes-use first.
---

# Post a roadmap update

Tell the people following a roadmap item that it moved forward. Posting can email your
audience and CANNOT be edited or deleted after — confirm the exact effect first.

Requires: launchnotes-use loaded, a LaunchNotes project, and the item's ID (find it with
launchnotes_project_search / launchnotes_list_work_items).

## Steps

1. Read the item and its reach with launchnotes_get_work_item — note notification_audience
   (subscribers + team members) and display_timeline.
2. Draft a short update: title + plain-text content, in the user's voice. If it implies a
   stage change ("now in development"), pick the new_stage_id (launchnotes_list_stages).
3. State the exact effect and confirm — e.g. "this emails 25 subscribers and 1 team member,
   posts to your public roadmap, and moves the item to Shipped." Name the stage move too; it
   changes what's public. Require an explicit yes. Two traps to call out:
   - If display_timeline is off, emails still go out but nothing shows publicly.
   - Trial-plan orgs skip the emails (the post still happens).
4. Post with launchnotes_post_roadmap_update (work_item_id, title, content, new_stage_id?,
   internal_only?). Default is public + notify; pass internal_only: true only for a team-only
   note (no public entry, no email).
5. Confirm what happened — there's no edit or delete, so get it right the first time.

## Guardrails (specific to this skill)

- No undo. A posted update can't be edited or removed — confirm audience and wording first.
- internal_only is a one-way door: false = public timeline + email, true = neither, and you
  can't promote an internal note to public later. Don't use true as a "safe draft."

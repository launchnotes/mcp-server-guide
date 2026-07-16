---
name: launchnotes-ship-the-roadmap
description: >
  Use when a roadmap item is done and the user wants a full announcement for it and to advance
  it on the public roadmap — e.g. "we shipped the billing revamp, announce it and move it to
  Released", "turn this roadmap item into an update post". Reads the item, drafts its
  announcement in the user's voice, links the two, and moves the item to a published stage.
  Draft-first; the stage move happens only on explicit confirmation. Start here when the
  subject is an existing roadmap item and the user wants a full announcement. To post a short
  progress update that notifies the item's followers (not a full announcement), use
  launchnotes-post-roadmap-update. To announce tracker work that isn't yet a roadmap item, use
  launchnotes-draft-from-work. Load launchnotes-use first.
---

# Ship a roadmap item as an announcement

Take a finished roadmap item public: announce it, connect them, advance its stage.

Requires: launchnotes-use loaded, a LaunchNotes project, and the roadmap item's ID (or
enough to find it via launchnotes_project_search / launchnotes_list_work_items).

## Steps

1. Read the item first with launchnotes_get_work_item — its content, current categories, and
   linked announcements. You'll reuse these and avoid wiping them.
2. Draft the announcement in the user's voice, benefit-first, reusing the item's content and
   categories. launchnotes_list_categories if you need IDs; create it as a draft with
   launchnotes_create_announcement.
3. Link them with launchnotes_update_announcement (work_item_ids). New announcement → empty
   set, so safe; include any existing links you read in step 1 if editing.
4. Confirm the stage move. Tell the user which published stage the item will move to and that
   it becomes publicly visible. On an explicit yes, launchnotes_move_work_item.
5. Hand back the draft link and the item's new stage. Publish/schedule the announcement only
   on a further explicit yes.

## Guardrails (specific to this skill)

- Visibility is the stage, not the announcement. Moving the item into a published stage is
  what puts it on the public roadmap — confirm it like any reader-visible action.
- Don't move to a stage that doesn't exist — launchnotes_list_stages to get valid targets.

---
name: launchnotes-draft-from-work
description: >
  Use when the user wants to turn shipped or in-progress work from an issue tracker into a
  LaunchNotes announcement — e.g. "draft an announcement for what we shipped this week",
  "write up the 2.4 release from Jira", "turn these merged GitHub PRs into a release note".
  Pulls the work from whatever tracker is connected (Jira, Linear, GitHub, ClickUp), drafts a
  publish-ready announcement in the user's voice, categorizes it, links it to its roadmap item,
  and attaches the source issues — always leaving it as a draft for review. Start here when the
  subject is tracker issues/PRs; if it's an existing roadmap item, use
  launchnotes-ship-the-roadmap. Not for backfilling a changelog (use
  launchnotes-import-existing-changelog) or reporting on how an announcement performed (use
  launchnotes-release-recap). Load launchnotes-use first.
---

# Draft a LaunchNotes announcement from tracker work

Turn completed (or about-to-ship) work into a ready-to-review announcement. You do the
gathering, judgment, and drafting; the user publishes.

Requires: the launchnotes-use skill loaded, a tracker MCP connected (Jira, Linear, GitHub,
or ClickUp), and a target LaunchNotes project. If no tracker is connected, ask the user to
paste the work items rather than guessing.

## Steps

1. Gather the work the user pointed at — by milestone, label, date range, or explicit IDs.
   Don't assume "shipped"; they may want to announce in-progress work. If the selection is
   broad, confirm the list before drafting.
2. De-duplicate. Run launchnotes_project_search to check whether any of this work was already
   announced. Flag likely duplicates and ask before creating another post.
3. Decide the shape. Default to one roundup announcement for related items; split into
   separate posts only when they target different audiences or the user asks. State your
   choice. (Optional: launchnotes_list_templates to mirror the structure the user favors
   — you can't create from a template, so use it only as a shape to follow.)
4. Draft the announcement — benefit-first, in the voice established by launchnotes-use, never
   inventing anything not in the source. Then launchnotes_list_categories, pick what fits, and
   launchnotes_create_announcement with headline, content_markdown, and category_ids. It's
   created as a draft.
5. Attach sources and roadmap link. For each source issue/PR, call
   launchnotes_create_external_content_link (needs the announcement ID from step 4). If the
   work maps to a roadmap item, link it via launchnotes_update_announcement (work_item_ids).
6. Hand it back with the draft link and what you set. Publish or schedule only on an explicit yes.

## Example

"We closed the whole 2.4 milestone in Linear — draft the release note." → Pull closed 2.4
issues → launchnotes_project_search finds none announced → related work, so one roundup
(confirm) → draft "What's new in 2.4", tag Product + Improvements, create draft → attach the 6
Linear issues, link the "Billing revamp" roadmap item → "Here's your draft: [link]. Publish
now, schedule, or keep editing?"

## Guardrails (specific to this skill)

- No invented content — everything traces to the source work.
- work_item_ids replaces the full set. Safe on a new announcement (empty set); if editing an
  existing one, read its current links with launchnotes_get_announcement first and include the
  ones that should stay.

(Draft-first, notification-posture confirmation, and no-PII come from launchnotes-use — not repeated here.)

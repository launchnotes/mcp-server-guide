---
name: launchnotes-feedback-to-roadmap
description: >
  Use when the user wants to turn reader feedback into roadmap items — e.g. "what are people
  asking for, and put the top themes on the roadmap", "cluster last month's feedback into
  roadmap items". Searches feedback, groups it into themes, proposes work items, and creates
  the approved ones — categorized, in a chosen stage. Proposes before creating. For reporting
  on feedback sentiment without creating items, use launchnotes-release-recap. Load
  launchnotes-use first.
---

# Turn feedback into a roadmap

Shape raw feedback into proposed roadmap items the user approves.

Requires: launchnotes-use loaded, a LaunchNotes project. Optionally a support MCP (Intercom,
Zendesk) to widen the input beyond LaunchNotes feedback.

## Steps

1. Gather with launchnotes_search_feedback — by topic (query), sentiment, importance, or date.
2. Cluster into themes on the feedback content, sentiment, and importance. There's no category
   field on feedback, so group by what's said, not by tags.
3. Propose, don't create. Present the themes — each with a proposed work-item name, a one-line
   rationale, and how many feedback items back it. Wait for the user to pick.
4. Create the approved items with launchnotes_create_work_item — set stage_id and category_ids
   in the same call (launchnotes_list_categories / launchnotes_list_stages for IDs).
5. Summarize what you created and where.

## Guardrails (specific to this skill)

- Strip PII. Feedback carries customer/reporter emails — cluster and summarize on themes;
  never put a name or email into a work item.
- Interpretation needs a human check — always propose themes before creating anything.

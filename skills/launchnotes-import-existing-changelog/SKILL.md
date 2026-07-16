---
name: launchnotes-import-existing-changelog
description: >
  Use when the user wants to bring an existing changelog or blog into LaunchNotes — e.g.
  "import our old changelog", "seed my page from our blog's release posts", "migrate our
  Headway/Beamer/Notion changelog". Parses the source, previews what it found, and creates the
  approved entries — either as drafts (dated today) or as a dated backfill that preserves each
  post's original date. Load launchnotes-use first.
---

# Import an existing changelog

Bring existing posts into LaunchNotes. Two modes — ask which the user wants:
- Seed as drafts: quickest; entries are dated today, the user reviews and publishes.
- Dated backfill: preserves original dates. Publishes each post (create → publish → set
  published_at), which is safe here because MCP-created announcements default to public-page-
  only (no email) — publishing old posts won't notify anyone. Verify the posture per batch anyway.

Requires: launchnotes-use loaded, a LaunchNotes project, and a source (URL or pasted content).

## Steps

1. Ask which mode. For dated backfill, confirm the plan up front: "I'll publish each post to
   your page and set its original date; none of these will email your subscribers."
2. Parse the source into entries (title, body, category hints, original URL, original date).
3. Preview as a table — title, date, proposed category, source URL — and let the user pick
   which to import. De-dupe against existing content with launchnotes_project_search.
4. Import in small confirmed batches (~10). For each:
   - launchnotes_create_announcement as a draft with category_ids, then attach the original
     with launchnotes_create_external_content_link.
   - Seed mode: stop here (stays a draft).
   - Backfill mode: read the posture with launchnotes_get_announcement to confirm it's
     public-page-only; if so, launchnotes_publish_announcement, then
     launchnotes_update_announcement with published_at = the original date. If the posture ever
     shows email/Slack, STOP and tell the user — don't blast their list.
5. Summarize what was imported and where.

## Guardrails (specific to this skill)

- Backfill publishes. It's only safe because imported posts have no email channel (MCP-created
  → public-page-only default, and MCP can't enable email). Verify per batch; never publish a
  post whose posture would notify.
- Seed mode leaves everything as drafts for the user to publish.

---
name: launchnotes-style-your-page
description: >
  Use when the user wants their public LaunchNotes page to match their brand — e.g. "make my
  page match our website", "set our brand colors", "turn on the roadmap and voting". Reads the
  current page config, brings in brand colors from the user's site or style guide, and sets
  colors, page content, and features — with a preview and confirmation before applying (it's a
  live page). Load launchnotes-use first.
---

# Match the page to the brand

Set colors, content, and features confidently; be careful with custom code.
(This skill is a folder: colors.md holds the color-variable → page-section map.)

Requires: launchnotes-use loaded, a LaunchNotes project. Optionally the user's website URL or a
brand/style-guide doc for the palette.

## Steps

1. Read current config with launchnotes_get_project — colors, content, feature flags.
2. Bring in the brand — using your own agent (not LaunchNotes' AI). Fetch the user's site or
   read their style guide and propose hex values for the eight color variables, guided by
   colors.md (which variable controls which part of the page, and how to pick each). For
   pixel-accurate, screenshot-based extraction, point the user to the in-app "Match your brand"
   button instead — that runs LaunchNotes' own extractor, by the user's own click.
3. Preview, then apply on confirm — colors (launchnotes_update_project_colors), page content
   like name/heading/subheading/slug (launchnotes_update_project_content), and features such as
   feedback/roadmap/ideas/RSS/voting (launchnotes_update_project_features).

## Guardrails (specific to this skill)

- Live page — always preview and confirm before writing.
- Custom CSS/header/footer/head is a caveated extra, not the core. It's Premium-only, invalid
  code silently blocks the save, and we don't offer implementation help. Offer it with those
  caveats; keep the confident surface to colors + content + features.
- Which color does what: see colors.md in this skill — don't guess the mapping.

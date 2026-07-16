# LaunchNotes page colors → what each variable controls

Source of truth: the app's "Match your brand" extractor (the-goat `backend/app/services/brand_color_extractor.rb`) + customize-page field captions (`LookAndFeel.tsx`). Visual map: https://help.launchnotes.com/en/articles/5431322-look-feel-accent-surface-and-type-colors

The public page is ALWAYS light-themed, even if the brand's own site is dark.

| Variable | Controls | How to choose |
|---|---|---|
| primary_color | Top banner, subscribe button, feedback card, selected category pills, active tab, links, search icon — the dominant brand fill | Bold background color. MUST be dark enough for white text (WCAG AA 4.5:1) — the page hardcodes white on it. Not white/near-white; avoid pure black unless it's the brand's identity. |
| secondary_color | Empty-state / placeholder icon accents | Complementary CTA/accent; a tint of primary if primary is already the CTA. Not a generic blue/gray. |
| white_color | Hero, navbar, card backgrounds | Usually #FFFFFF; deviate only for a noticeably tinted white. |
| off_white_color | Page canvas behind the announcement list | ~1–2% darker than white_color. |
| light_gray_color | Category containers, month dividers | Match the site's divider tint (warm/cool). |
| gray_color | Pagination, muted/secondary icons | Match the site's muted tone. |
| primary_text_color | Body copy, category labels | Very dark for readability. |
| secondary_text_color | Subtitles, captions, metadata | Medium-dark gray. |

Dark source sites: extract only the brand accents for primary/secondary; use standard light-mode neutrals for surfaces/text (white ≈ #FFFFFF, off-white ≈ #F8F9FA, light-gray ≈ #E5E7EB, gray ≈ #9CA3AF, primary-text ≈ #111827, secondary-text ≈ #6B7280), keeping warm/cool to match the brand.

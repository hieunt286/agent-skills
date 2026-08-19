---
name: ccs-presentation
description: Builds presentations (slide decks, PPTX) with CCS Technology's branding, visual style, and presentation culture — brand navy design system, standard header/footer chrome, drawio diagram conventions with Flaticon UIcons, and the company's storyline patterns. Use when creating or restyling any slide deck, architecture deck, or diagram-heavy presentation for CCS Technology — e.g. "làm slide cho CCS", "dựng presentation", "vẽ kiến trúc + làm deck", "chuẩn branding CCS".
---

# CCS Presentation

Produce slide decks that look, read, and argue like CCS Technology's own — same design system, same brand chrome, same diagram language, same storyline discipline. Deck content defaults to **Vietnamese**; brand labels stay in English ("CCS TECHNOLOGY").

Everything here was extracted from CCS's real production pipeline (the DI_TICH / Phủ Chủ tịch architecture deck). The four reference files are the contract:

| File | Covers |
|---|---|
| [references/design-system.md](references/design-system.md) | Style: canvas, grid, colors + usage rules, fonts, type scale, UI components. Branding: logo usage, cover layout, content-slide header/footer chrome |
| [references/drawio-conventions.md](references/drawio-conventions.md) | Drawing .drawio diagrams: zoning/blocks/layers, style recipes, connector rules, Flaticon UIcons, export pipeline |
| [references/storyline.md](references/storyline.md) | Presentation outline: the canonical slide order and narrative principles |
| [assets/](assets/) | `logo/` — the three official CCS logo SVGs; `favicon.svg`; `globals.css` — the design-token source of truth (oklch, with design rationale in comments) |

## Workflow

1. **Frame the deck.** Audience, the decision or takeaway, deck tag (short uppercase deck name for the header), section list, page count. Pick the storyline from `references/storyline.md`.
2. **Draw diagrams first.** Any architecture / flow / journey visual is a `.drawio` file built per `references/drawio-conventions.md`, exported to high-res PNG. The deck embeds the PNG in an image card and credits the source file in the caption ("Bản vẽ: <file>.drawio").
3. **Build the deck** per `references/design-system.md`. Generate programmatically (python-pptx is the proven path; the design-system file lists its known traps). Render the logo SVGs from `assets/logo/` to transparent PNG before embedding (PPTX cannot embed SVG).
4. **Track sources.** Every number must be traceable to a source file (estimate xlsx, WBS docx, drawio page). Keep a per-slide source list — in speaker notes as a `[Sources]` block, or a `source-notes.txt` beside the deck. Never invent figures.
5. **Self-review loop (do not skip).** Export the deck to PDF (`soffice --headless --convert-to pdf`), rasterize pages (`pdftoppm -png`), then actually look at every page and fix what's wrong — text overflowing boxes, empty cards, misaligned chrome. This step is how real defects get caught.

## Non-negotiables

- Every content slide carries the standard chrome (top accent bar, logo header, footer with page number) — exact spec in the design-system file.
- Colors come only from the token palette; **system/series colors are identities, fixed across the whole deck** (rule in the design-system file).
- Slide titles are assertion sentences (the takeaway), never topic labels; the topic lives in the uppercase eyebrow.
- Vietnamese number formatting: `2.195` (thousands dot), `9,6` (decimal comma).
- Flaticon UIcons only for pictograms; ship `FLATICON-LICENSE` alongside outputs and credit "UIcons by Flaticon".
- For persuasion-first proposals (win an approval decision), combine this skill with `ccs-technique-proposal` — that skill owns the argument structure, this one owns the visual execution.

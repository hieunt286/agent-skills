---
name: ccs-presentation
description: Builds presentations (slide decks, PPTX) and technical solution proposals (đề xuất kỹ thuật) with CCS Technology's branding, visual style, and presentation culture — brand navy design system, standard header/footer chrome, drawio diagram conventions with Flaticon UIcons, canonical storylines, and the HIỂU/TIN TƯỞNG/KHẢ THI persuasion methodology for proposals that must win an approval decision. Use when creating or restyling any slide deck, architecture deck, diagram-heavy presentation, or proposal for CCS Technology — e.g. "làm slide cho CCS", "dựng presentation", "viết proposal / đề xuất kỹ thuật", "vẽ kiến trúc + làm deck", "chuẩn branding CCS".
---

# CCS Presentation

Produce slide decks and proposals that look, read, and argue like CCS Technology's own — same design system, same brand chrome, same diagram language, same storyline discipline. Deck content defaults to **Vietnamese**; brand labels stay in English ("CCS TECHNOLOGY").

Everything here was extracted from CCS's real production pipeline (the DI_TICH / Phủ Chủ tịch architecture deck and the APPFORGE proposal methodology). The reference files are the contract:

| File | Covers |
|---|---|
| [references/design-system.md](references/design-system.md) | Style: canvas, grid, colors + usage rules, fonts, type scale, UI components. Branding: logo usage, cover layout, content-slide header/footer chrome |
| [references/drawio-conventions.md](references/drawio-conventions.md) | Drawing .drawio diagrams: zoning/blocks/layers, style recipes, connector rules, Flaticon UIcons, export pipeline |
| [references/storyline.md](references/storyline.md) | Presentation outline: the canonical slide order and narrative principles |
| [references/proposal-method.md](references/proposal-method.md) | Persuasion proposals (đề xuất kỹ thuật): the HIỂU → TIN TƯỞNG → KHẢ THI method, slide spec format, quality rules |
| [references/proposal-structure.md](references/proposal-structure.md) | The canonical ~15-slide proposal outline with per-slide goals and content checklists |
| [assets/](assets/) | `logo/` — the three official CCS logo SVGs; `favicon.svg`; `globals.css` — the design-token source of truth (oklch, with design rationale in comments) |

## Workflow

1. **Frame the deck.** Audience, the decision or takeaway, deck tag (short uppercase deck name for the header), section list, page count. Pick the storyline from `references/storyline.md` — and if the deck must **win an approval decision** (proposal, bid, investment), first build the argument with `references/proposal-method.md` (HIỂU → TIN TƯỞNG → KHẢ THI), whose slide-by-slide content spec then feeds the steps below.
2. **Draw diagrams first.** Any architecture / flow / journey visual is a `.drawio` file built per `references/drawio-conventions.md`, exported to high-res PNG. The deck embeds the PNG in an image card and credits the source file in the caption ("Bản vẽ: <file>.drawio").
3. **Build the deck** per `references/design-system.md`. Generate programmatically (python-pptx is the proven path; the design-system file lists its known traps). Render the logo SVGs from `assets/logo/` to transparent PNG before embedding (PPTX cannot embed SVG).
4. **Track sources.** Every number must be traceable to a source file (estimate xlsx, WBS docx, drawio page). Keep a per-slide source list — in speaker notes as a `[Sources]` block, or a `source-notes.txt` beside the deck. Never invent figures.
5. **Render-based self-review — MANDATORY, never optional.** Export the deck to PDF (`soffice --headless --convert-to pdf`), rasterize pages (`pdftoppm -png`), then actually look at every page and fix what's wrong — text overflowing boxes, empty cards, misaligned chrome. Layout defects of this kind are invisible in the build code and only surface in the rendered output; a deck that has not been reviewed page-by-page from renders is not done. Repeat build → render → review until a pass finds nothing.

## Non-negotiables

- The render-based self-review loop (step 5) always runs before delivery — every historical overflow/empty-card defect was caught only there, never in code review.
- Every content slide carries the standard chrome (top accent bar, logo header, footer with page number) — exact spec in the design-system file.
- Colors come only from the token palette; **system/series colors are identities, fixed across the whole deck** (rule in the design-system file).
- Slide titles are assertion sentences (the takeaway), never topic labels; the topic lives in the uppercase eyebrow.
- Vietnamese number formatting: `2.195` (thousands dot), `9,6` (decimal comma).
- Flaticon UIcons only for pictograms; ship `FLATICON-LICENSE` alongside outputs and credit "UIcons by Flaticon".
- Proposals follow the quality rules in `references/proposal-method.md`: one closing message per slide, evidence honesty with transparency notes, comparison tables that show the rejected options, a mandatory boundaries slide, and a final slide that asks for one specific decision.

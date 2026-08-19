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

### Phase 1 — Clarify context with the user (MANDATORY, before any building)

Whatever kind of presentation is requested, do **not** start producing anything until the following have been discussed and agreed with the user. Ask concisely, propose concrete defaults they can accept or adjust, and iterate until confirmed:

1. **Audience (đối tượng nghe).** Who sits in the room — leadership, client procurement, technical committee, mixed? Their language, technical depth, and what they already know.
2. **Objective (mục tiêu).** What the presentation must achieve: inform, align, or win a decision. If it must **win an approval decision** (proposal, bid, investment), build the argument with `references/proposal-method.md` (HIỂU → TIN TƯỞNG → KHẢ THI) — its slide-by-slide content spec then feeds Phase 2.
3. **Reference scope (phạm vi tài liệu tham khảo).** Enumerate the source materials the deck will be built from (docs, estimates, WBS, existing diagrams, prior decks); confirm the list with the user. This list is the traceability boundary — every figure and claim in the deck must resolve to something in it.
4. **Propose the outline for the user to choose.** Based on 1–3 and `references/storyline.md`, propose the page count and the goal of each slide (one line per slide: what the audience must take away). Offer alternatives where reasonable (e.g. 10-slide executive cut vs 15-slide detailed run). The user picks/edits; lock the outline before building.
5. **Propose which parts need drawio diagrams — and confirm.** Walk the locked outline and propose which slides deserve a flowchart/architecture/journey diagram (`.drawio`), which reuse existing drawings, and which stay text/cards. Get the user's confirmation on the diagram list.
6. **Clarify each diagram's goal, then enrich.** For every confirmed diagram, state its purpose in one sentence (what it must prove or make obvious, for which slide) and agree on it. Then use the planned diagrams to enrich the outline: the diagram content (zones, flows, actors, labels) becomes source material that deepens the slide's content spec — the slide and its drawing are designed together, not bolted on later.

### Phase 2 — Build

1. **Draw diagrams first.** Every diagram confirmed in Phase 1 is a `.drawio` file that **must comply with the design system**: brand tokens and rules from `references/design-system.md` applied through the concrete style recipes in `references/drawio-conventions.md` (palette, zoning, block taxonomy, connector rules, Flaticon UIcons). Export to high-res PNG; the deck embeds the PNG in an image card and credits the source file in the caption ("Bản vẽ: <file>.drawio").
2. **Build the deck** per `references/design-system.md`. Generate programmatically (python-pptx is the proven path; the design-system file lists its known traps). Render the logo SVGs from `assets/logo/` to transparent PNG before embedding (PPTX cannot embed SVG).
3. **Track sources.** Every number must be traceable to a file inside the reference scope agreed in Phase 1 (estimate xlsx, WBS docx, drawio page). Keep a per-slide source list — in speaker notes as a `[Sources]` block, or a `source-notes.txt` beside the deck. Never invent figures.
4. **Render-based self-review — MANDATORY, never optional.** Export the deck to PDF (`soffice --headless --convert-to pdf`), rasterize pages (`pdftoppm -png`), then actually look at every page and fix what's wrong — text overflowing boxes, empty cards, misaligned chrome. Layout defects of this kind are invisible in the build code and only surface in the rendered output; a deck that has not been reviewed page-by-page from renders is not done. Repeat build → render → review until a pass finds nothing.

## Non-negotiables

- Phase 1 context clarification always happens before any building — never jump straight to slides from a vague request; the outline and the diagram list are locked with the user first.
- The render-based self-review loop (Phase 2, step 4) always runs before delivery — every historical overflow/empty-card defect was caught only there, never in code review.
- Every content slide carries the standard chrome (top accent bar, logo header, footer with page number) — exact spec in the design-system file.
- Colors come only from the token palette; **system/series colors are identities, fixed across the whole deck** (rule in the design-system file).
- Slide titles are assertion sentences (the takeaway), never topic labels; the topic lives in the uppercase eyebrow.
- Vietnamese number formatting: `2.195` (thousands dot), `9,6` (decimal comma).
- Flaticon UIcons only for pictograms; ship `FLATICON-LICENSE` alongside outputs and credit "UIcons by Flaticon".
- Proposals follow the quality rules in `references/proposal-method.md`: one closing message per slide, evidence honesty with transparency notes, comparison tables that show the rejected options, a mandatory boundaries slide, and a final slide that asks for one specific decision.

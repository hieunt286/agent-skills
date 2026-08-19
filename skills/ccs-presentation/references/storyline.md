# CCS presentation storyline (sườn ý trình bày)

How CCS sequences a deck. Two proven patterns — pick by deck purpose, then apply the shared principles.

## Pattern A — Solution / architecture deck (canonical 11 slides)

The order is **nghiệp vụ trước → kỹ thuật sau → effort cuối** (business first, technology after, effort/money last). Each slide answers one audience question:

| # | Slide | Answers |
|---|---|---|
| 1 | **Bìa** — positioning line + 3–4 headline numbers in the stats band | "What is this and how big?" |
| 2 | **Agenda** — 4 chapters as a colored stepper + one "mục tiêu cuối" sentence | "Where are we going?" |
| 3 | **Solution High Level** — end-to-end customer/user journey diagram | "Bài toán là gì?" (business before any tech) |
| 4 | **Hệ thống & chức năng** — the systems/lanes to build, module counts | "Phải xây những gì?" (scope) |
| 5 | **Application Landscape** — how scope maps to applications & boundaries | "Map ra ứng dụng thế nào?" |
| 6 | **Luồng nghiệp vụ lõi** — the core operating flow (e.g. content release) | "Vận hành ra sao?" |
| 7 | **Điểm nhấn / rủi ro** — the hard parts and their guardrails (e.g. AI, AR) | "Cái khó xử lý thế nào?" |
| 8 | **Kiến trúc logic** — the full logical architecture | "Kỹ thuật đứng sau là gì?" |
| 9 | **Tech stack** — named products per layer, no vagueness | "Cụ thể dùng gì?" |
| 10 | **Effort (manday)** — baseline by workstream + total + assumptions | "Tốn bao nhiêu công?" |
| 11 | **Gantt + phân bổ đội** — timeline, roles, next step | "Ai làm, bao lâu, bắt đầu thế nào?" |

Merge/split as content demands (a 10-slide variant merges 11 into 10), but never move effort before the solution story.

## Pattern B — Persuasion proposal (approval decision)

When the deck must **win a decision** (leadership sign-off, client bid), build the argument with [proposal-method.md](proposal-method.md) and the canonical outline in [proposal-structure.md](proposal-structure.md): three parts HIỂU → TIN TƯỞNG → KHẢ THI, closing with one specific ask. Visual execution stays identical; slide 1/2 chrome, agenda stepper, and closing-numbers patterns from Pattern A carry over.

## Shared principles

- **Assertion titles.** Every content slide title is a full sentence stating the takeaway ("Hành trình du khách được nối liền từ trước chuyến đi đến sau khi rời khu di tích"), never a topic label. The topic/section label lives in the uppercase eyebrow and header-right.
- **One big image + explainer column.** A diagram slide is one large image card plus a column of 3–4 mini-cards that interpret it — the image never has to speak for itself. Optionally a takeaway pill strip under the image.
- **Diagrams carry the argument.** Slides 3, 5, 6, 7, 8 are drawio exports; build the diagrams before the deck.
- **Numbers are traceable.** Every figure resolves to a source file (estimate xlsx, WBS, drawio page) recorded per slide in speaker notes / source-notes. No invented numbers, no un-caveated benchmarks.
- **Money is opt-in.** Default: the effort summary shows **manday / people-months / duration / confidence-of-scope only** — no currency figures unless the client explicitly wants cost on the slide. (Standing preference from CCS leadership review.)
- **Agenda = 4 chapters max**, numbered circles in identity colors, one closing line stating what the audience will be able to decide at the end.
- **End with motion.** The last slide always contains the next step (decision asked, kickoff conditions, or timeline start) — a deck that just stops is not finished.
- **Emotional arc**: understand → trust → confidence; keep chapter order aligned to that arc even in Pattern A (business story builds understanding, architecture/stack builds trust, effort/plan builds confidence to commit).

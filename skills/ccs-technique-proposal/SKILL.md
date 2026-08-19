---
name: ccs-technique-proposal
description: Builds technical solution proposals (đề xuất kỹ thuật / đề xuất giải pháp) using CCS's three-goal persuasion methodology — HIỂU (understand), TIN TƯỞNG (trust), KHẢ THI (feasible). Use when drafting, restructuring, or reviewing a proposal or pitch deck that must win an approval decision — leadership sign-off, client bid, or internal investment — e.g. "viết proposal", "làm đề xuất kỹ thuật", "thuyết phục lãnh đạo phê duyệt giải pháp".
---

# CCS Technique Proposal

Produce a technical proposal as a **slide-by-slide content specification** in Markdown — a document that describes, for every slide, the goal (what the audience must take away), the content to display, and the closing message. This spec is the deliverable: it is ready for a human or another AI to enrich, review, or convert to PPT/PDF.

Default output language is **Vietnamese** (the audience is usually Vietnamese leadership or clients). Switch to English only if the user asks or the audience clearly requires it.

## Step 1 — Lock the decision frame

Before writing anything, establish and state at the top of the document:

1. **Audience** — who decides (ban lãnh đạo, client procurement board, technical committee)?
2. **The ask** — the single concrete decision the proposal requests (e.g. "phê duyệt Phase 0 PoC"). A proposal without a specific ask is a report, not a proposal.
3. **Context** — internal approval, client bid (thầu), or partnership pitch. This sets branding and how much external evidence is needed.
4. **Tone** — always: thực dụng, có bằng chứng, đặt kỳ vọng đúng (pragmatic, evidence-based, no exaggeration).

If the user hasn't provided the problem/pains, the proposed solution, and available evidence, ask for them or extract them from provided materials before proceeding.

## Step 2 — Build the three-part storyline

Structure every proposal around three persuasion goals, in this order. Each part answers one question the audience is silently asking:

| Part | Goal | Audience question | Typical slides |
|---|---|---|---|
| **A — HIỂU** | Audience grasps the problem and can picture the solution + its value | "What is this and why should I care?" | Pain & needs → overall solution → user journey → applicable use cases → pain-to-solution mapping |
| **B — TIN TƯỞNG** | Audience believes the scope, approach, and technology choices are right — with reasoning and evidence | "Why this way and not another?" | Scope rationale → approach comparison (buy / build / extend) → technology choice against neutral criteria → external evidence |
| **C — KHẢ THI** | Audience believes the team can deliver — clear architecture, mature methodology, de-risked roadmap | "Can they actually do it?" | Core value → architecture (+ integration + deployment) → tech stack → boundaries (what we do NOT do) → methodology with gates → roadmap + the ask |

Part A creates consensus on the problem and desire for the solution **before** any argumentation. Part B argues the choices. Part C proves execution and ends with the call-to-action. Insert section-divider slides between parts so the audience always knows where they are in the persuasion arc.

The canonical ~15-slide outline with per-slide goals and content checklists is in [references/proposal-structure.md](references/proposal-structure.md) — read it when drafting the full document, and adapt (merge/split slides) to the specific case.

## Step 3 — Write each slide in the standard spec format

Every slide entry follows this exact format:

```markdown
## Slide NN — <Title>

**Mục tiêu:** <what the audience must conclude after this slide — one or two sentences>

**Nội dung muốn hiển thị:**
<bullets / tables — the actual content, not placeholders>

**Thông điệp chốt:** <ONE sentence the audience should remember>

**Gợi ý bố cục PPT:** <layout hint: card grid, comparison table, timeline, focal diagram…>
```

For slides built around a diagram (architecture, user flow, deployment), add a **🖼️ Ảnh trọng tâm** block: name the image file, its aspect ratio, how it should dominate the slide, and keep surrounding text to short callouts that never repeat what the image already shows.

## Step 4 — Apply the quality rules

These rules are what make it a CCS proposal. Check every one before delivering:

- **One closing message per slide.** If a slide has two messages, split it.
- **Evidence honesty.** Never invent benchmarks. When a number needs caveats (e.g. "70% faster — but versus building from scratch, not versus competitor X"), add an explicit transparency note (*Ghi chú minh bạch*) on the slide. Cite sources for external claims.
- **Comparison tables show the losers.** Every choice (scope, approach, technology) is argued via a criteria table that includes the rejected options and why they lost. Criteria are stated *before* naming the winner, so the conclusion feels inevitable, not pre-cooked.
- **Boundaries slide is mandatory.** Explicitly list what the solution does NOT do. Ranh giới rõ = lời hứa khả thi (clear boundaries make the promise credible).
- **Every pain gets an answer.** Part A closes with an explicit pain → solution mapping table back-referencing the opening slide. No orphaned pains.
- **Methodology has gates.** The delivery plan is iterative with a decision gate at the end of each phase — never a one-shot approval of the whole package. Each step lists: activities · deliverables · exit gate.
- **End with the ask.** The final slide requests one specific, small, low-risk decision (typically: approve a PoC/Phase 0) with success criteria and prerequisites.
- **De-risk the investment story.** Show "start small, scale with evidence": cheap PoC first, production architecture later, each expansion justified by results from the previous phase.

## Visual execution

When the proposal is delivered as a slide deck for CCS Technology, pair this skill with the `ccs-presentation` skill (same repo): it owns the CCS design system, brand chrome (header/footer/logo), drawio diagram conventions, and build pipeline. This skill owns the argument; that one owns the look.

## Step 5 — Review pass

After drafting, re-read as the decision-maker: for each part ask "Do I understand? (A) Do I believe? (B) Do I trust they can deliver? (C)". Flag any slide that argues before Part A has built consensus, any claim without evidence, and any jargon the audience won't know. Fix, then deliver the spec plus a one-paragraph storyline summary (tóm tắt mạch trình bày).

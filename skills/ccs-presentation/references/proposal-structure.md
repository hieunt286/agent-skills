# Canonical proposal structure (~15 slides, 3 parts)

The reference outline for a CCS technical proposal. Adapt to the case at hand: merge slides for a short deck, split table-heavy slides, add domain slides as needed — but keep the A → B → C arc and the per-slide goals intact. Placeholders like `[solution]`, `[core technology]` are filled from the actual engagement.

---

## PHẦN A — HIỂU (Vấn đề & Giải pháp)

Goal of the whole part: in ~5 slides the audience must understand the problem, picture the solution, see how it is used and where it applies, and see that every pain has an answer. This part builds "consensus on the problem + desire for the solution" **before** any argumentation.

### Slide 01 — Bối cảnh & nhu cầu
- **Goal:** consensus on today's pains and the destination. Frame the problem correctly up front (e.g. "this is a solution + governance problem, not a license-purchase problem").
- **Content:** current pains (3–5 bullets, concrete and recognizable to this audience) → real needs → target state (one sentence).
- **Closing message:** the problem framing, stated as a contrast ("X, không phải Y").

### Slide 02 — Giải pháp tổng thể
- **Goal:** answer "so what is the solution?" immediately with one total picture, before any details.
- **Content:** users and entry point → solution core → the distinctive layers/pillars around the core → resulting qualities. Include the *why-not-the-naive-alternative* note (what goes wrong without the distinctive layers).
- **Layout:** one diagram or pillar layout; audience should reconstruct it from memory.

### Slide 03 — Quy trình sử dụng (user journey)
- **Goal:** turn the abstract solution into a concrete experience — "what does using this actually look like?"
- **Content:** focal flow image (wide horizontal strip) with numbered steps; the roles involved and what each does; a detail table mapping each step to the platform/governance layer it touches (move to appendix/speaker notes if dense). Highlight the steps only *this* solution provides.
- **Closing message:** from need → running result in a few steps, safe at every sensitive step.

### Slide 04 — Bài toán nghiệp vụ có thể ứng dụng
- **Goal:** prove the solution solves many real problems in the organization → ROI multiplies across use cases; help the audience picture the first one.
- **Content:** general use-case categories (card grid) → domain-specific examples in the client's industry → "fit criteria" strip so viewers self-identify their own use case.
- **Closing message:** value multiplies by the number of applications, not one use case.

### Slide 05 — Đối chiếu pain → giải pháp
- **Goal:** close Part A by proving every pain from Slide 01 has a specific answer.
- **Content:** two-column table `Pain (Slide 01) → Lời giải cụ thể`. Every opening pain must appear.
- **Closing message:** specific answers, not generic promises.

---

## PHẦN B — TIN TƯỞNG (Vì sao lựa chọn này đúng)

Goal: the audience believes the **scope, approach, and technology** are the right choices — argued with criteria and external evidence, not sentiment.

### Slide 06 — Phạm vi tập trung
- **Goal:** show the chosen scope is deliberate — mapped the option space, picked where *pain is high × no good alternative exists*, consciously deferred or outsourced the rest. Kills the "one tool does everything" misconception.
- **Content:** taxonomy of the option space (one line each) → decision table: option | pain level | good alternative exists? | decision (do deep / outsource / defer).
- **Closing message:** narrow scope = less risk = faster value.

### Slide 07 — Cách tiếp cận & tiêu chí lựa chọn
- **Goal:** justify the approach (typically: extend OSS vs. buy closed vs. build from scratch) and lay out **neutral selection criteria** *before* naming any product — so the next slide's choice feels inevitable.
- **Content:** 3-way comparison table (speed to value, control, security/sovereignty, lock-in/license, build effort) with the losers' weaknesses marked → numbered list of selection criteria derived from needs, no product names yet.
- **Include:** any deliberate design decision that changes how criteria are weighted (e.g. "built-in governance is NOT criterion #1 because our platform layer provides it").

### Slide 08 — Vì sao chọn [core technology]
- **Goal:** score the chosen technology against each criterion from Slide 07 and name the **deciding factor** that separates it from rivals (e.g. permissive license vs. copyleft/proprietary).
- **Content:** criterion-by-criterion scoring with named competitors and where each falls short.
- **Mandatory:** a *Ghi chú minh bạch* (transparency note) for any performance/speed claim — state exactly what it was measured against and cite the source.

### Slide 09 — Cơ sở tin cậy
- **Goal:** reduce perceived risk with external evidence — adoption metrics and real customers in multiple industries, matching the use-case type being proposed.
- **Content:** headline metrics (users, countries, deployments, funding) → customers by industry with *published* results. Only sourced numbers.
- **Closing message:** proven at scale for exactly this class of problem → low risk of picking wrong.

---

## PHẦN C — KHẢ THI (Chứng minh làm được)

Goal: the audience believes **the team can deliver** — clear own-value, feasible architecture, concrete tech, realistic boundaries, disciplined methodology, de-risked roadmap — ending with the ask.

### Slide 10 — Giá trị cốt lõi
- **Goal:** go deep on the value *the team itself* creates (the layer beyond the off-the-shelf core) and name the components used to realize it — bridging to architecture.
- **Content:** the value pillars, one line of substance each; the self-hosted/owned components involved.

### Slide 11 — Kiến trúc giải pháp
- **Goal:** show where every pillar lives in the whole system — architectural feasibility.
- **Content:** focal architecture diagram (~70% of slide) + short callouts that do NOT repeat the diagram's text; full zone-by-zone detail goes to speaker notes. Call out data-sovereignty facts explicitly (what is stored where, what is never copied).

### Slide 11A — Mô hình tích hợp *(optional)*
- **Goal:** answer "how does this plug into what we already have?" — hub-and-spoke diagram: solution at center, spokes to data, APIs, identity, secrets, distribution channels, with protocols labeled.
- **Closing message:** attaches to existing systems, doesn't replace them; business data never leaves its source.

### Slide 11B — Kiến trúc triển khai *(optional)*
- **Goal:** operational feasibility as a story of "start small → scale with a path": PoC deployment (hours, near-zero cost) side-by-side with production HA deployment.
- **Closing message:** cheap to start, clear path to scale — low investment risk.

### Slide 12 — Giải pháp kỹ thuật & tech stack
- **Goal:** every architectural layer maps to a named, mature technology — feasible, owned, no surprise licensing.
- **Content:** table `layer | role | technology (license)` → design principles (self-host / separation of concerns / replaceability — as applicable).
- **Closing message:** a mature technology behind every layer.

### Slide 13 — Ranh giới: những gì KHÔNG làm
- **Goal:** set expectations — explicit out-of-scope list with the reason for each (outsourced, deferred, requires skills the target users don't have…).
- **Closing message:** ranh giới rõ = lời hứa khả thi.

### Slide 14 — Phương pháp luận triển khai
- **Goal:** the team knows *how*, not just *what* — disciplined, risk-managed delivery.
- **Content:** 3–4 delivery principles (e.g. iterative & evidence-gated, governance-first, thin platform layer, real-use-case-driven) → step table: `bước | hoạt động | sản phẩm bàn giao | cổng kiểm soát (exit)` → cross-cutting operations: roles involved, quantitative success metrics, change management.
- **Closing message:** gated steps, risk owned at every stage, expand only on evidence.

### Slide 15 — Lộ trình & quyết định
- **Goal:** the call-to-action. Phased timeline, each phase ending in an evidence-based decision gate, closing with one specific request.
- **Content:** phases with duration and scope (Phase 0 Discovery/PoC → MVP → Hardening → Scale, adapted) → **the ask**: approve Phase 0, with its success criteria and prerequisites (use cases, access, legal review kickoff).

---

## Conversion & delivery notes

- Add **section-divider slides** between A / B / C so the audience always knows where they are in the persuasion arc.
- Table-heavy slides (06, 07, 12): consider splitting or turning into graphics when converting to PPT.
- Slides with focal diagrams: list each image file, its dimensions/aspect, and placement rule in an appendix table; never duplicate the diagram's text on the slide.
- Emotional arc: A builds empathy + desire, B builds belief, C builds confidence in execution → close with the call-to-action.
- End the spec document with a **storyline summary** (tóm tắt mạch trình bày): the full slide list grouped by part, one line each.

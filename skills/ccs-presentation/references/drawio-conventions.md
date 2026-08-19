# CCS drawio diagram conventions

How CCS draws architecture / flow / journey diagrams in draw.io (.drawio) so they drop cleanly into branded decks. Diagrams are **generated or restyled by script** (every cell goes through one shared style function — no hand-tuned one-off styling), which is what keeps a 7-page file visually uniform.

## Start from a template — never from a blank page

`../assets/drawio-templates/` holds anonymized production diagrams (labels replaced with `[placeholder]`s; structure, styles, zoning, icons intact). Pick the template matching the diagram type, clone it, and replace placeholder/content labels — the style recipes below are then inherited instead of rebuilt:

| Template | Diagram type | Use when the slide must show |
|---|---|---|
| `application-landscape.drawio` | Application landscape / business framework | The map of actors, channels, application services, shared services, integration points — including an isolated-system frame |
| `logic-architecture.drawio` | Layered logical architecture | The full system in numbered tầng/layers (users → gateway → services → messaging → storage) + external systems + isolated system |
| `tech-stack.drawio` | Tech stack table | Layer · product · why-chosen rows, grouped by section bars |
| `flow-content-release.drawio` | Approval workflow + distribution flow | A state-machine approval pipeline and how the released output fans out to consumers |
| `flow-user-experience.drawio` | End-user experience flow | Phased user flow (session init → content trigger) across client, services, CDN |
| `flow-device-sync.drawio` | Device/system sync & monitoring flow | Bidirectional command/status channels, offline behavior, buffered events |
| `flow-ai-guardrail.drawio` | Guarded AI flow | A decision flow where refusal is the default path: deterministic match → threshold gate → answer-with-citation / polite-refusal + feedback loop |
| `flow-ar-interaction.drawio` | Client-side interactive feature flow | Trigger → permission branch → happy path + fallback path → asset source & analytics |
| `journey-strip.drawio` | Customer journey strip (very wide) | Multi-stage journey: stages × (touchpoints, devices/emotions, system functions, data captured) + shared platform band, legend, layers |

`journey-strip.drawio` also demonstrates **layer organization** (Nền và lưới / Luồng và liên kết / Tiêu đề / Hành trình / Dữ liệu / Nền tảng) — keep that layer discipline when editing large diagrams.

## Page setup

- Model background **`#FAFBFD`**; model-level `shadow=0` (shadows are opt-in per card).
- Every page has its own header: a ~34 px Flaticon icon at (60, 28) + **title caps 28 pt bold `#1F438A`** at x ≈ 104 + subtitle 13–14 pt `#545B68` beneath.
- Every page has a centered footer credit, 10–11 pt muted:
  `Style: globals.css · Plus Jakarta Sans / Be Vietnam Pro · Flaticon UIcons — UIcons by Flaticon`
- Page sizes are free per diagram type — journey strips run very wide (e.g. 2400×1200+); export target is a PNG 3000–5200 px wide so it stays sharp at ~8 in on a slide.
- Font declared in every cell style: `fontFamily=Plus Jakarta Sans,Be Vietnam Pro,Arial`.

## Palette (drawio variant of the brand tokens)

```
background #FAFBFD   foreground #11161F   card #FFFFFF
secondary  #F2F4F6   muted #EDEFF2   accent #E7EAEE   border #D6D9DE
muted_text #545B68
primary #1F438A   primary_deep #0B1731   primary_subtle #D8E9FF   primary_mid #4F7AC1
orange #EB6834    orange_subtle #FFF4EE
green #1BAF7A     yellow #EDA101   pink #E87BA4   violet #4A3AA7   red #E34948
```

Domain header-bar colors reuse the deck's system-identity assignments (one color per domain, consistent with the slides that embed the diagram).

## Block taxonomy & zoning (chia khối / chia lớp)

Structure a diagram as **tầng/zone → lane → card → chip**, all `rounded=1;arcSize=12` (chips `arcSize=16`):

| Layer | Style recipe |
|---|---|
| **Canvas zone** (outer grouping region) | fill `secondary`, stroke `accent`, strokeWidth 1 — a quiet background plate |
| **Frame / card container** | fill `card`, stroke `border` 1.2, `shadow=1` |
| **Primary domain frame** | fill `card`, stroke `primary` 1.5, `shadow=1` |
| **Lane label bar** | fill+stroke `primary_deep`, white bold 15 pt, align left, `spacingLeft=14` |
| **Domain header bar** | fill+stroke = domain identity color, white bold 14 pt, `spacingLeft=48` (leaves room for a 22 px icon) |
| **Nested card** | fill `card`, stroke = parent domain color 1.5, bold 13 pt ink, align left/top, `spacingLeft=12;spacingTop=10`, `shadow=1` |
| **Chip** (small unit) | fill `card`, stroke `border` 1, 12 pt ink, centered |
| **Highlight block** (the node being discussed) | fill `orange_subtle`, stroke `orange` 2 |
| **Bus / integration plane** | fill `primary_subtle`, stroke `primary` 1.8 |
| **External system** | fill `card`, stroke `primary_mid` 1.5, `dashed=1;dashPattern=6 4`, no shadow |
| **Isolated system frame** (hệ biệt lập) | stroke `orange` 1.5–1.8, `dashed=1;dashPattern=8 6`, own colored header bar + explanatory note underneath |
| **Free text** | `text;html=1` no fill/stroke, 12–13 pt |

Rules:
- Empty (label-less) shapes are containment/decoration only — style them as quiet cards (`card` fill, `border` stroke), never as business nodes.
- Complex pages get a **legend** in the top-right corner.
- One highlight color per page: the orange treatment marks *what this page is about*, nothing else.

## Connectors (lines)

- Standard edge: `edgeStyle=orthogonalEdgeStyle;rounded=1` — orthogonal with rounded corners, stroke **`primary_mid #4F7AC1`**, strokeWidth **1.7–1.8**, `endArrow=block;endFill=1;endSize=7`.
- **Highlighted flow**: same but `orange`, strokeWidth 2 (the flow the slide narrates).
- **Dashed** `dashPattern=6 4` on an edge = async / optional / external dependency.
- Plain `line;` + dashed = visual divider, not a flow.
- Edge labels: 11 pt `muted_text`, `labelBackgroundColor=#FAFBFD` so they punch out of crossing lines. Protocol/behavior notes go straight on the line (`publish · subscribe`, `heartbeat 60s`).

## Icons — Flaticon UIcons

- Single icon family across all diagrams: **Flaticon UIcons** (`@flaticon/flaticon-uicons`, regular rounded style). Never mix in hand-drawn pictograms or other icon sets — when restyling an inherited diagram, delete foreign pictograms and replace with UIcons.
- Usage in drawio: render the glyph to PNG, embed as base64 `<img>` inside an `html=1` vertex with `fillColor=none;strokeColor=none`.
- Sizes: 22 px inside header bars · 26 px integration markers · 34–44 px page/section icons.
- **License**: ship `FLATICON-LICENSE.txt` next to every output directory that uses the icons, and keep the "UIcons by Flaticon" credit in the page footer (free-tier attribution requirement).

## Export pipeline

Headless export via the diagrams.net embed API (needs network + Chrome):

1. Playwright drives an iframe of `https://embed.diagrams.net/?embed=1&proto=json`.
2. `postMessage {action: "load", xml}` with the .drawio XML, then `{action: "export", format: "png", scale: 2, border: 12, background: "#FAFBFD"}`.
3. Receive the PNG as a data URI; write per page.

Embed the exported PNG in the deck inside an image card with caption `Bản vẽ: <file>.drawio` — the .drawio file stays the editable source of truth and ships alongside the deck.

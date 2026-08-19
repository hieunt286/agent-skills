# CCS presentation design system

Style + branding contract for CCS Technology slide decks. Source of truth for tokens: `../assets/globals.css` (oklch values with design rationale in comments). The hex values below are the slide-ready conversions used by the production deck builders.

## 1. Canvas & grid

- Slide size **16:9 — 13.333 × 7.5 in** (or 1280 × 720 px in px-based tools).
- Horizontal margins **0.42 in** left and right (≈ 48 px).
- Vertical zones on content slides:
  - top accent bar: y = 0 → 0.05 in
  - header row: y ≈ 0.155–0.53, hairline at **y = 0.68**
  - title block: eyebrow y = 0.84, title y = 1.04
  - **content zone: y ≈ 1.46 → 6.92**
  - footer hairline at **y = 7.06**, footer text y = 7.13
- Gaps between cards: 0.14–0.185 in. Cards align to a consistent column grid within the content zone.

## 2. Color palette (hex, from globals.css tokens)

### Neutrals & brand

| Token | Hex | Use |
|---|---|---|
| background | `#FAFBFD` | slide background |
| card | `#FFFFFF` | card surfaces |
| foreground / ink | `#11161F` | primary text |
| muted-fg | `#545B68` | secondary text |
| muted-fg-2 | `#7A808B` | captions, meta, timestamps |
| border | `#E4E6EA` | hairlines, card borders |
| input | `#D6D9DE` | stronger hairline / separators |
| secondary | `#F2F4F6`, muted `#EDEFF2` | recessed panels |
| **primary (brand navy)** | `#1E428A` | brand chrome, emphasis, headings accents |
| primary hover | `#153470`; **deep oxford** `#172954` | dark brand surfaces |
| primary subtle | `#DBECFE` (text on it: `#214487`) | chips, tinted bands |
| primary 50/100/300/400 | `#EBF4FF` / `#D8E9FF` / `#88ACE4` / `#4F7AC1` | tints; 400 = eyebrow text |
| sidebar (cover navy) | `#121A2B`, accent `#25334C`, border `#2B384F`, fg `#E0E5EB`, muted `#7B8799`, bright `#4C88D3` | cover / dark surfaces |
| state text | info `#2759A2` · warn `#8C5500` · success `#006F2B` | inline semantic text |

### Series / chart colors

`chart1 #2978D6` (blue) · `chart2 #EB6834` (orange) · `chart3 #1BAF7A` (teal-green) · `chart4 #EDA101` (gold) · `chart5 #E87BA4` (pink) · `chart7 #4A3AA7` (violet) · heat tint `#B7D3F6`.

### Color usage rules (the most important part)

- **Series colors are system identities, fixed across the entire deck.** Assign one color per system/domain on first appearance and never reshuffle by rank or per slide. (DI_TICH precedent: Smart Guide = chart1, Website = chart3, CMS SG & Device = chart2, CMS Website = chart4, ILS = chart5, Shared Services = chart7.)
- **Navy `#1E428A` is chrome/brand/emphasis — never a data series color.**
- A single-metric comparison chart (e.g. manday bars) uses **one hue** (chart1) + direct value labels — not one color per bar.
- Orange (`#EB6834` family) is the scarce accent: key numbers, highlight rules, the one highlighted block. If everything is orange, nothing is.
- Soft tints (`*Soft`/subtle) fill backgrounds; their saturated parent colors draw strokes, number circles, and text accents.

## 3. Typography

- **Font: Plus Jakarta Sans**, fallback **Be Vietnam Pro** (Vietnamese-first), then system sans. Both are on Google Fonts. Machines building decks must have them installed (`~/Library/Fonts` on macOS) or the PPTX must embed fonts — otherwise renderers silently substitute.
- Mono (`JetBrains Mono`) only for code/identifiers, never for money or quantities.
- **Headings are bold 700** — PJS at 600 reads thin next to body text.
- **Eyebrows/labels are UPPERCASE + letter-spacing.** python-pptx has no tracking API — set the XML attribute `rPr@spc` (25–55 = 0.25–0.55 pt).
- Type scale (dense, content-heavy deck — "đủ nội dung" beats "chữ to"):

| Role | Size (pt) | Style |
|---|---|---|
| Cover title | 28–34 | bold, white, may be uppercase |
| Slide title | **17.5** | bold, ink — an assertion sentence |
| Eyebrow above title | 8 | bold caps, `#4F7AC1`, spc 55 |
| Header brand text | 9.5 | bold caps navy, spc 40 |
| Card heading | 8.4–10.5 | bold |
| Body / bullets | 7.4–8.3 | regular, line 1.15–1.2 |
| Caption / image credit / footer | 6.8 | `#7A808B` |
| KPI value | 15 | bold navy (its label: 6.8 caps muted) |
| Big hero number | 60–72 | bold navy |
| Dense table/gantt rows | 5.4–7 | acceptable when content requires |

- Numbers: Vietnamese format — `2.195,5` · `9,6` · tabular feel (right-align columns).

## 4. UI components

- **Card**: white, corner radius 0.09–0.10 in, hairline border `#E4E6EA`, soft shadow (outerShdw: blur 90000 EMU, dist 26000, color ink, alpha 10%).
- **Mini-card with accent bar**: card + vertical navy bar 0.045 in on the left edge; used in explainer columns beside a big image.
- **Chip / badge**: fill `#DBECFE`, text `#214487` bold 7.6 pt, pill radius.
- **Principle banner**: full-width subtle-tint band carrying one bold statement (also: deep-navy or orange rounded pill with white uppercase 10–11 pt for takeaway strips under a diagram).
- **KPI tile**: caps label 6.8 muted → value 15 navy bold → sub-line 6.7.
- **Image card**: card + image inset with 0.08 in padding + centered caption `Bản vẽ: <tên file>.drawio` 6.8 pt.
- **Numbered step circles**: 56–64 px circles filled with the section's identity color, white bold number — used on agenda/stepper.
- **Lane rows**: full-width rounded rows with the system's soft tint fill + colored number circle + bold title + one-line muted description.
- **Bar rows**: rounded track `#E4E6EA` + rounded fill in identity color + value label at row end.
- **Vertical divider rule**: 7–8 px orange bar separating a big-number panel from chart content.

## 5. python-pptx build traps (proven pitfalls)

- Delete the `<p:style>` element from every autoshape — otherwise LibreOffice and some renderers draw a theme shadow even with `shadow.inherit = False`.
- Vertical text = horizontal textbox rotated 270°.
- Logo watermark = inject `a:alphaModFix` (amt ≈ 6000–8000 = 6–8%) into the picture's `a:blip`.
- PPTX cannot embed SVG — render logo SVGs to transparent PNG first (Playwright screenshot with `omitBackground`, scale 4–6×).
- Set `a:ea`/`a:cs` typefaces on every run so Vietnamese glyphs use the brand font.
- **Verification is render-based and MANDATORY**: none of the real defects (text overflowing its box, empty cards, chrome misalignment) are detectable from the build code — they only show in rendered pages. Always run `soffice --headless --convert-to pdf` → `pdftoppm -png` → inspect every page → fix → re-render, until a clean pass.

## 6. Branding & chrome

Logo files: `../assets/logo/` — `CCS_Full logo (white).svg` (dark surfaces only), `CCS_Logo mark (blue).svg` (light surfaces), `CCS_Logo mark (white).svg`. Never recolor, stretch, or redraw the logo; keep clear space around it.

### Cover slide (dark)

- Full-bleed **navy `#121A2B`** background.
- **Full white logo** top-left, ~1.95 in wide.
- **Watermark**: white logo mark at ~6% alpha occupying the right half; decorative outline circles in `#25334C`.
- Four 0.11 in accent squares colored chart1–chart4 sitting above the eyebrow.
- Eyebrow caps (light blue `#9FB7E0`/`#4C88D3`) → big white bold title → short orange rule → subtitle → meta chip (fill `#25334C`).
- Bottom: stats band — hairline + 3–4 key numbers in bold white with muted caps labels.
- Alternative accepted cover: split layout — deep navy left panel with text, brand-navy right panel holding a white rounded image card of the hero diagram; 12 px orange rule on the left edge.

### Content slide chrome (every content slide)

- **Top accent bar**: full-width, 0.05 in, navy `#1E428A`.
- **Header**: blue logo mark height 0.34 in at (0.42, 0.17) → `CCS TECHNOLOGY` 9.5 pt bold navy spc 40 → ` | ` in `#D6D9DE` → deck tag caps 7.5 pt `#7A808B`. Right-aligned: current **section name** caps 7.5 pt bold `#545B68` spc 50. Hairline below at y 0.68.
- **Title block**: eyebrow caps 8 pt `#4F7AC1` → assertion title 17.5 pt bold ink; optional right-aligned note 7.6 pt muted.
- **Footer**: hairline at y 7.06; left `CCS Technology · Digital Experience & Heritage Solutions` 6.8 pt (swap the tagline per engagement); center = document context line (`Tài liệu trình bày · <chủ đề> · <MM/YYYY>`); right = page `NN` 8.5 pt bold navy + ` / TT` 7.5 pt muted.
- **No separate section-divider slides** — the section lives in the header-right label and the title eyebrow.

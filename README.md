# Agent Skills

A collection of [Agent Skills](https://skills.sh) developed by [@hieunt286](https://github.com/hieunt286), installable into Claude Code, Cursor, Codex, and 70+ other coding agents via the open `skills` CLI.

## Installation

Install interactively (pick skills and target agents):

```bash
npx skills add hieunt286/agent-skills
```

Install a specific skill:

```bash
npx skills add hieunt286/agent-skills --skill ccs-presentation
```

Useful flags:

| Flag | Meaning |
|---|---|
| `-a claude-code` | Install for a specific agent only (e.g. `claude-code`, `cursor`, `codex`) |
| `-g` | Install globally (`~/.claude/skills/`, …) instead of into the current project |
| `-y` | Non-interactive — accept defaults (for CI/CD) |
| `--copy` | Copy files instead of symlinking |

## Skills

| Skill | Description |
|---|---|
| [`ccs-presentation`](skills/ccs-presentation/SKILL.md) | Builds slide decks and technical proposals (đề xuất kỹ thuật) with CCS Technology's branding and presentation culture: design system (colors/fonts/layout), header/footer brand chrome, drawio diagram conventions with Flaticon UIcons, canonical storylines, and the HIỂU → TIN TƯỞNG → KHẢ THI persuasion methodology. Bundles the official logo assets + `globals.css` design tokens. |

## Repository layout

Each skill lives in its own directory under `skills/`, following the [Agent Skills](https://github.com/vercel-labs/skills) convention:

```
skills/
└── <skill-name>/
    ├── SKILL.md          # required — YAML frontmatter (name, description) + instructions
    └── references/       # optional — supporting docs loaded on demand
```

To add a new skill: create `skills/<skill-name>/SKILL.md` with `name` and `description` frontmatter, push to `main`, and it becomes installable immediately — no registry step needed.

## License

[MIT](LICENSE)

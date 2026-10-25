# UI Polish — Agent Skill

An [Agent Skill](https://agentskills.io) that gives AI coding and design agents a trained designer's eye. It audits, fixes and polishes any user interface so it feels clear, calm, trustworthy and premium, and explains *why* each change makes the screen easier to use.

Works with Claude Code, Cursor, Codex, OpenCode, GitHub Copilot and other agents that support the `SKILL.md` format.

## Install

```bash
npx skills add cindyeme/ui-polish
```

Or copy `skills/ui-polish/` into your agent's skills folder (for Claude Code, `~/.claude/skills/` or `.claude/skills/` in a project).

## What it does

Ask your agent things like:

- "Polish this settings screen"
- "Why does this dashboard feel cluttered? Fix it"
- "Audit this screenshot for UI/UX issues"
- "Build a mobile product page for organic strawberries"

It checks alignment and grid, spacing, color, typography, labels and badges, information placement, icon consistency, dividers and the primary action, stress-tests the design with real-world content, and suggests experience improvements once the basics are clean.

### Playbooks

- **Product pages** — imagery that works across a catalog, title / rating / price placement, quantity and add-to-cart design, sticky actions and quantity presets.

More playbooks (forms, dashboards, onboarding…) can be added under `references/`.

## Structure

```
skills/
  ui-polish/
    SKILL.md                      # core principles, workflow, output format
    references/
      audit-checklist.md          # 15 checks: test → failure → fix
      product-pages.md            # e-commerce playbook
```

## License

MIT

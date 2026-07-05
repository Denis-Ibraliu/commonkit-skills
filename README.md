# commonkit

[![skills.sh](https://skills.sh/b/Denis-Ibraliu/commonkit-skills)](https://skills.sh/Denis-Ibraliu/commonkit-skills)

A small, opinionated engineering-workflow kit — five skills covering the loop
from idea to PR, in the `/commonkit:` namespace.

**You invoke them; the model never does.** Every skill sets
`disable-model-invocation: true`, so it fires only when you type
`/commonkit:<name>` — Claude won't load it on its own. You stay in control of
what gets built.

| Skill | Invoke | What it does |
|-------|--------|--------------|
| Brainstorm | `/commonkit:brainstorm` | Short design dialogue → right-sized spec, before any code. |
| Implement  | `/commonkit:implement`  | TDD build in phases, then **one** code-review pass over the whole diff at the end. |
| Review     | `/commonkit:review`     | Parallel-lens, confidence-gated review of a diff/PR/branch. Reports; doesn't edit. |
| Ship       | `/commonkit:ship`       | Commit → push → PR/MR via `gh` or `glab` (auto-detected). |
| Architect  | `/commonkit:architect`  | Find architectural friction, propose deeper modules in an RFC. |

Typical loop: `/commonkit:brainstorm` → `/commonkit:implement` (which runs
`/commonkit:review` at the end) → `/commonkit:ship`. Reach for
`/commonkit:architect` when a subsystem is hard to change or test.

## Install via npx skills

```bash
npx skills add Denis-Ibraliu/commonkit-skills
```

Handy flags: `--list` to preview, `--skill review ship` to pick a subset,
`-a claude-code` to target a specific agent.

## Install as a Claude Code plugin

```
/plugin marketplace add Denis-Ibraliu/commonkit-skills
/plugin install commonkit
```

Then type `/commonkit:` and pick a skill.

## Layout

```
skills/<name>/SKILL.md            # the five skills (user-invoked only)
.claude-plugin/plugin.json         # plugin "commonkit"
.claude-plugin/marketplace.json    # source ./
```

## Design notes

- **User-invoked, not model-triggered** — `disable-model-invocation: true` on
  every skill; nothing runs unless you ask for it. `user-invocable: true` keeps
  them in the `/` menu.
- **Review once, at the end** — `implement` keeps the tree green with continuous
  typecheck/tests while building, then runs a single review over the complete
  diff, not per phase.
- **Lazy by default** — every skill leans YAGNI: question whether the work needs
  to exist, prefer the smallest change, delete over add.

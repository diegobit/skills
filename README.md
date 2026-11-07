# skills

Agent skills I use every day with Claude Code, Codex, Cursor, opencode, Gemini and Pi. Each
directory is one skill, and its `SKILL.md` is the whole interface: the agent reads it when the
description matches the task.

| Skill | What it does |
|---|---|
| [docextract](docextract/) | Extract and summarize documents locally |
| [file-pr](file-pr/) | Open a concise pull request |
| [leaving-pr-comments](leaving-pr-comments/) | Write clear GitHub PR comments |
| [plan-tracker](plan-tracker/) | Maintain repo plans and ledger |
| [review-loop](review-loop/) | Repeated code review, chosen model |
| [telegram-notify](telegram-notify/) | Telegram ping when needing you |
| [writing-for-agents](writing-for-agents/) | Write skills and agent instructions |
| [writing-for-humans](writing-for-humans/) | Rewrite prose for human readers |

[`archived/`](archived/) holds skills I no longer load by default: `db-cleanup`, `harness-history`,
`modernize` and `test-audit`. They still work when an agent is pointed at their `SKILL.md`.

## Install

Clone the repo and link the skills you want into your agent's skill folder, for example:

```sh
git clone https://github.com/diegobit/skills.git ~/code/skills
ln -s ~/code/skills/file-pr ~/.claude/skills/file-pr
```

Common folders: `~/.claude/skills` (Claude Code), `~/.agents/skills` and `~/.codex/skills`
(Codex), `~/.cursor/skills`, `~/.config/opencode/skills`, `~/.pi/agent/skills`. Linking instead
of copying keeps a skill current with `git pull`.

## Requirements

Most skills are instructions only. The exceptions:

| Skill | Needs |
|---|---|
| docextract | [`uv`](https://docs.astral.sh/uv/) (it runs the scripts and installs their Python packages on first use). OCR of scanned pages uses Apple's Vision framework, so it needs macOS and the Xcode command line tools; the rest works anywhere. |
| file-pr, review-loop | [`gh`](https://cli.github.com/), signed in |
| telegram-notify | a `tg "<message>"` command on `PATH` that sends you a Telegram message (`-s` for a silent one). Mine is not in this repo. |
| archived/harness-history | `python3`, `jq` |

## Writing a skill

- `SKILL.md` front matter needs `name` and `description`. The description is what the model
  matches on, so name the triggers, not just the topic.
- Put executables in `<skill>/scripts/` and long reference material in `<skill>/references/`, so
  it is read only when needed.
- Keep compiled files out of git: `docextract/scripts/vision_ocr` rebuilds itself on first use.
- Claims backed by measurements say where the numbers come from, as in
  `docextract/references/benchmark.md`.

## License

MIT; see [LICENSE](LICENSE). Several skills are adapted from other MIT-licensed projects;
[ATTRIBUTION.md](ATTRIBUTION.md) lists them with their notices.

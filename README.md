# skills

A collection of skills for AI agents, authored by Ryan Rudd.

Skills are portable packages of instructions that extend what an agent can do, following the open [Agent Skills](https://agentskills.io) standard. Each skill lives in `skills/<skill-name>/` with a `SKILL.md` describing what it does and when an agent should use it, plus any supporting scripts or reference files. Any agent that supports the standard can use them.

## Installing

### Claude Code, via the plugin marketplace

```
/plugin marketplace add ryanrudd/skills
/plugin install <skill-name>@ryanrudd-skills
```

To pick up new releases later: `/plugin marketplace update ryanrudd-skills`

### Manual install (any agent)

Clone this repo and copy (or symlink) a skill folder into wherever your agent discovers skills. For Claude Code:

- **Personal** (all your projects): `~/.claude/skills/<skill-name>/`
- **Project** (checked into a repo): `.claude/skills/<skill-name>/`

For other agents, see your agent's documentation for its skills directory.

## Available skills

| Skill | Description |
| --- | --- |
| [asd-ste100](skills/asd-ste100/SKILL.md) | Write reader-facing technical content (Linear issues, docs, change summaries) in Simplified Technical English, stripped of conversation-local context. |

## Skill layout

```
skills/<skill-name>/
├── SKILL.md        # required — frontmatter (name, description) + instructions
├── reference.md    # optional — detail loaded on demand, keeps SKILL.md lean
├── scripts/        # optional — helper scripts the skill can run
└── assets/         # optional — templates, static files
```

Conventions used in this repo:

- Skill names are kebab-case and match their directory name.
- `description` frontmatter says both what the skill does **and** when to use it — that's what the agent reads to decide whether to invoke it.
- `SKILL.md` stays under ~500 lines; anything bigger moves to reference files.
- Each new skill gets an entry in `.claude-plugin/marketplace.json` and in the table above.

Validate before publishing:

```
claude plugin validate .
```

## License

[MIT](LICENSE)

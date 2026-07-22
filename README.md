# skills

A collection of [Agent Skills](https://agentskills.io) for [Claude Code](https://code.claude.com), authored by Ryan Rudd.

Each skill lives in `skills/<skill-name>/` with a `SKILL.md` describing what it does and when Claude should use it, plus any supporting scripts or reference files.

## Installing

### Via the plugin marketplace (recommended)

In Claude Code:

```
/plugin marketplace add ryanrudd/skills
/plugin install <skill-name>@ryanrudd-skills
```

To pick up new releases later: `/plugin marketplace update ryanrudd-skills`

### Manual install

Clone this repo and copy (or symlink) a skill folder into your skills directory:

- **Personal** (all your projects): `~/.claude/skills/<skill-name>/`
- **Project** (checked into a repo): `.claude/skills/<skill-name>/`

## Available skills

| Skill | Description |
| --- | --- |
| _none yet_ | |

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
- `description` frontmatter says both what the skill does **and** when to use it — that's what Claude reads to decide whether to invoke it.
- `SKILL.md` stays under ~500 lines; anything bigger moves to reference files.
- Each new skill gets an entry in `.claude-plugin/marketplace.json` and in the table above.

Validate before publishing:

```
claude plugin validate .
```

## License

[MIT](LICENSE)

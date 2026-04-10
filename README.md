# skillio

A collection of custom [Agent Skills](https://agentskills.io/specification) for use with Claude Code and compatible AI coding agents.

## Skills

| Skill | Description |
|-------|-------------|
| [ai-repo-setup](./skills/ai-repo-setup/SKILL.md) | Scaffold AI development tooling into any repository — AGENTS.md, agent skills, and MCP servers |

## Usage

Install a skill using the [Skills CLI](https://skills.sh/):

```bash
# Install all skills from this repo
npx skills add iadams749/skillio

# Install a specific skill
npx skills add iadams749/skillio@ai-repo-setup
```

## Contributing

Each skill lives in its own directory and must contain a `SKILL.md` file following the [Agent Skills specification](https://agentskills.io/specification).

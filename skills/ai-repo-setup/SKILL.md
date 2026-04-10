---
name: ai-repo-setup
description: Scaffolds AI development tooling into an existing repository. Sets up AGENTS.md (project-level agent instructions), agent skills, and MCP server configuration. Use when the user wants to add AI tooling to a project, set up an AGENTS.md file, register agent skills, or configure MCP servers for a repo.
user-invocable: true
license: MIT
compatibility: Designed for Claude Code or similar AI coding agents.
metadata:
  author: iadams749
  version: "0.1"
---

# ai-scaffold-repo

Adds AI development tooling scaffolding to an existing repository. This skill covers three areas:

1. **AGENTS.md** — project-level instructions that agents load automatically when working in the repo
2. **Agent Skills** — reusable skill definitions (following the [Agent Skills spec](https://agentskills.io/specification)) that extend agent capabilities
3. **MCP Servers** — configuration for Model Context Protocol servers that give agents access to external tools and data sources

## Steps

While going through these steps, if there is any information that is missing you can either ask the user for more information or just omit it from the setup. Do noy hallucinate information that does not exist. AGENTS.md, skills, and MCP servers can be built out more later once more information is known  

### 1. Understand the project

Understand the intent of this project; what is being built in this project?

Determine the tech stack of the project. This includes any: coding languages, frameworks, cloud providers, CI/CD tools, local development tools (like make) and other relevant parts of the tech stack

### 2. Scaffold AGENTS.md

Create an `AGENTS.md` at the repo root if it does not already exist. The file should be structured as follows:

- **Project overview** — a one or two sentence description of what the project does and the key technologies from the tech stack.
- **Architecture notes** — key directories, entry points, and data flow
- **Development conventions** — style, testing approach, commit conventions
- **Local Development Workflows** - make commands, local scripts, or anything else used in development locally. If none are present at the time this skill is used, just insert \< ADD LOCAL DEVELOPMENT WORKFLOWS HERE \> instead in this section as a placeholder.
- **Agent-specific guidance** — what agents should and should not do in this repo. This should include instructions for:
  -  Updating AGENTS.md to reflect any changes in the project including local development workflows, project structure, or anything else in the file that needs to be updated.
  - Relying on skills and using them when appropriate
  - Guidance for managing the AGENTS.md file. A file that is too big can bloat the context. It should only include relevant information, commands, and guidance.

Once all of this is done, create a symlink to a CLAUDE.md file so that Claude code users benefit out of the box from this as well.

### 3. Scaffold agent skills

Ensure the user can add skills via the CLI by confirming `npx skills` is available:

```bash
npx skills add <skill-name>
```

If `npx` is not available in the project, inform the user and suggest installing Node.js.

Next install the "find-skills" skill using the following command:

```bash
npx skills add https://github.com/vercel-labs/skills --skill find-skills -y --agent universal claude-code
```

Next, add a new section to AGENTS.md called "Skills Index" within that, create a table with all locally installed skills and when they should be used. For now, it may only have the find-skills skill. Include instructions to update the index whenever a new skill is installed. 


### 4. Configure MCP servers

If the user wants MCP servers, add or update the agent's settings file (e.g. `.claude/settings.json` for Claude Code) with the appropriate `mcpServers` entries. Ask the user which MCP servers they need before writing config.

## Notes

- Always read existing project files (README, existing config) before writing anything
- Prefer extending existing `AGENTS.md` over replacing it
- Ask the user before adding MCP server entries that require API keys or credentials

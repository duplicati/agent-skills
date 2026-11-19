# Duplicati agent skills

Skills that let AI agents use [Duplicati](https://duplicati.com) as an undo button: take an encrypted, offsite backup before risky changes, and restore files from any earlier point in time.

The skills follow the [Agent Skills](https://agentskills.io) format, a folder with a `SKILL.md` file, so they work with OpenClaw, Hermes, Claude Code, Codex, Cursor and other agents that read that format.

## Skills

| Skill | What it does |
| --- | --- |
| [duplicati-backup](skills/duplicati-backup/SKILL.md) | Takes a checkpoint before bulk edits, deletes, migrations or upgrades, and restores files when the user asks to undo, roll back or recover something. |

## Requirements

The skills talk to Duplicati through its MCP server. You need:

1. Duplicati 2.4.1 or newer (canary channel at the time of writing), running on the machine that holds the files.
2. A backup that covers the folders the agent works in, with a destination on another machine or in the cloud.
3. The MCP endpoint turned on: Settings → Experimental options → MCP server, or start the server with `--webservice-enable-mcp-server=true`.
4. An MCP access token for the agent, created in Settings → MCP access tokens or with `duplicati-server-util issue-mcp-token`.
5. The Duplicati MCP server added to the agent: `http://localhost:8200/mcp`, Streamable HTTP, with the header `Authorization: Bearer <token>`.

The Duplicati UI shows the exact setup for each agent when you create a token. The [documentation](https://docs.duplicati.com/automation-and-integration/using-duplicati-with-ai-agents-mcp) has the same steps for Claude Code, Claude Desktop, VS Code, Cursor, Codex CLI, Gemini CLI, GitHub Copilot CLI and opencode.

## Installing

### OpenClaw

The skill is published on [ClawHub](https://clawhub.ai):

```bash
clawhub install @duplicati/duplicati-backup
```

### Hermes

```bash
hermes skills install duplicati/agent-skills/skills/duplicati-backup
```

Or add this repository as a source, so its skills show up in `hermes skills search`:

```bash
hermes skills tap add duplicati/agent-skills
```

### Claude Code, Codex, Cursor and others

With the [skills](https://skills.sh) CLI:

```bash
npx skills add duplicati/agent-skills
```

### By hand

Copy the `skills/duplicati-backup` folder into the skills folder of your agent, for example `~/.claude/skills/` for Claude Code.

## Contributing

This repository is a mirror. The skills are maintained in the [`skills`](https://github.com/duplicati/duplicati/tree/master/skills) folder of the main Duplicati repository and copied here automatically, so changes made here are overwritten. Please open issues and pull requests at [duplicati/duplicati](https://github.com/duplicati/duplicati).

## License

MIT, see [LICENSE](LICENSE). Copies published on ClawHub are licensed MIT-0, as ClawHub requires for all skills.

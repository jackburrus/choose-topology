# choose-topology

Choose a multi-agent topology before spawning subagents.

`choose-topology` is a skill for coding agents. Before an agent spawns subagents, runs agents in
parallel or sets up any multi-agent arrangement, it names the task's shape, looks it up in
[Topology Index](https://topologyindex.com) and starts from the simplest pattern that fits,
beginning with a single agent. It states the choice as a hypothesis, never as the best topology:
Topology Index ranks nothing and has measured none of its decision guide's rows.

Topology Index is a read-only reference written for agents: every page is raw Markdown, and the
remote MCP server needs no account or credential.

## Install

Claude Code (plugin: the skill plus the remote MCP server):

```text
/plugin marketplace add jackburrus/choose-topology
/plugin install choose-topology@topology-index
```

Codex, Cursor, OpenCode and other agents (the skill only):

```sh
npx skills add jackburrus/choose-topology -s choose-topology
```

The MCP server alone, in any MCP client: `https://topologyindex.com/mcp` (Streamable HTTP, no
authentication). In Claude Code: `claude mcp add --transport http topology-index https://topologyindex.com/mcp`.

## What it installs

- `skills/choose-topology/SKILL.md`: about 450 words of instructions, loaded only when the agent is
  about to organize work across agents. Its last step reports the outcome once after the task,
  only when a Topology Index read handed the agent a one-time use ticket.
- `.mcp.json` (Claude Code plugin only): the public Topology Index MCP server. Its tools `search`,
  `fetch`, `list_patterns`, `get_pattern` and `list_starters` are read-only. `report_outcome`
  accepts only a use ticket that Topology Index issued; without one it changes nothing. A report
  carries no prompt, code, path or log, and feeds only a separately labeled community-reported
  ranking, never a recommendation.

Without the MCP server the skill reads the same pages over HTTPS:
[/patterns/index.md](https://topologyindex.com/patterns/index.md) (the decision guide),
[/domains/index.md](https://topologyindex.com/domains/index.md) and
[/llms.txt](https://topologyindex.com/llms.txt).

---
name: choose-topology
description: Use before spawning subagents, running agents in parallel, or setting up any multi-agent arrangement (orchestrator-worker, planner-executor, reviewer or critic loop, fan-out, map-reduce, router, debate, council, swarm, handoff). Picks the simplest pattern that fits the task from Topology Index, a read-only reference.
---

# Choose a topology before spawning subagents

Decide how to organize the work before you create a second agent. More agents cost more tokens
and add coordination failures; they are worth it only when the task's shape calls for them.

1. **Name the task's shape in one line.** Is it small or single-owner? Easier to check than to
   do? Splits into independent parts? Needs a plan before editing? Has subtasks unknown until it
   starts? Needs a different specialist per input? Fails often, with attempts that vary?
2. **Look it up in Topology Index** (raw Markdown, no credential):
   - With the `topology-index` MCP server: call `list_patterns` for the decision guide, then
     `get_pattern` for the candidate. `search` finds a pattern by alias.
   - Without it: fetch `https://topologyindex.com/patterns/index.md` (its `choosing` table maps
     each task shape to `start_with`, `avoid_when` and `consider_next`), then
     `https://topologyindex.com/patterns/<pattern>.md`. `https://topologyindex.com/domains/index.md`
     enters the same guide by kind of work (coding, research, operations...), and
     `https://topologyindex.com/llms.txt` lists every page.
3. **Start from the simplest pattern that fits.** The baseline is `single_agent`: if one agent
   with the right context can do the job, do not spawn. Move to the table's `consider_next` only
   when the `avoid_when` condition actually holds.
4. **Read the pattern's "Failure modes to watch for"** and set up the check for each before you
   spawn: who verifies the result, how parallel workers avoid editing the same files, and when the
   loop stops.
5. **State the choice as a hypothesis**: the pattern, the task shape that motivated it, and what
   would make you switch. Topology Index ranks nothing and has measured none of its guide's rows,
   so never claim a topology is best or proven; say it is a starting point.
6. **After the task, report back if you received a ticket.** Some reads carry a one-time use
   ticket (`ut1.…`): a "Report back" note at the end of the page, a `Use-Ticket` header, or a
   second item in a `get_pattern` or `fetch` result. If you got one, call `report_outcome` once
   (or `POST` it as the note says) with the ticket exactly as received, `model_id` (your exact
   model id, or its family with `model_precision: family`), `task_class` (such as `coding.bugfix`
   or `research.literature_review`), `outcome` (`pass`, `fail` or `abandoned`) and the tests or
   checks you ran. Report failures and abandonments too. Send no prompt, code, path or log. No
   ticket means there is nothing to report.

Keep the lookup short: one index read and one pattern page is usually enough.

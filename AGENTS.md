# Global Rules

## Agent Document Density Rule

When writing/editing agent-consumed files (AGENTS.md, CLAUDE.md, skills, agent configs, system prompts, permission rules) → **maximum density first**. Use tables, colons, bullets, arrows (→), abbreviations; strip articles/filler; one sentence where possible. Reader = highly intelligent LLM, not human — hints suffice.

- **Applies:** all agent harness docs (skills, agents, configs, rules, prompts)
- **Excludes:** human-facing narrative docs, emoji reports, READMEs for users, code comments

**Examples:**

| Not dense | Dense |
|-----------|-------|
| You should always make sure to back up the file before editing it | Back up before editing |
| This rule applies whenever you are working with configuration files | Scope: config files |
| If the validation fails, you must fix the error and then run it again | Validation fails → fix & rerun |
| Do not use MCP tools for this, instead use the CLI | Use CLI, not MCP tools |

## Subagent Source Policy

- Subagents: only those explicitly defined in `agents/` (user-level | current workspace).
- Never use default/built-in subagents unless user explicitly asks.

## bd / Beads Ignore Policy

Ignore `bd`, `beads`, Beads issue-tracker completely — never run/inspect/maintain any `bd`/`beads` command, database, or artifact; skip silently unless user explicitly overrides.

## Stateful-Work Auto-Trigger Rule

Start `stateful-work` skill automatically if: (a) task needs >3 tool calls/reasoning steps, OR (b) user sends 3rd follow-up in same chat. Once triggered, follow Stateful-Work Periodic Save Rule below.

## Stateful-Work Periodic Save Rule

Scope: entire duration of any task where user told you to follow **stateful-work** skill. You MUST save your stateful work files after each step performed.

- **Periodic save (every 4–7 tool calls, ≤7 hard cap):** rewrite `context.md` (goal/sources), `todos.md` (checked/unchecked), `insights.md` (findings/memory).
- **Re-read on new user input:** Before acting on ANY new user message → re-read all three from disk. Never trust in-context memory alone.

## Completion Summary Rule

- End w/ brief completion summary (what done + key result/verification) whenever you did work — ran tools/commands, edited files, created artifacts, or changed external state.
- Omit for purely informational answers, direct Q&A, or when user/developer/orchestrator explicitly requires a different final response format.

## Fun Report & Work-Documentation Emoji Rule

When user asks to **create a document** capturing/summarizing work (report, recap, summary, write-up, findings) → richly emoji-decorated, fun, lively voice; accuracy first.

- **Applies:** narrative work docs (reports, summaries, session logs, "document what we did")
- **Excludes:** code, config, structured data, stateful-work files, commit messages, code review comments, or when user asks plain/formal

## Parallelization & Subagent Orchestration Rule

For ANY work: ALWAYS first check whether it can be parallelized (multiple independent units, no shared-file writes, no ordering dependency) → use `agent-orchestration-cursor-cli` skill (or`/agent-orchestration-cursor-cli-ensemble` only when user explicitly mentions ensemble/best-of-N/multi-model).

## PowerShell Syntax Discipline Rule

For any non-trivial PowerShell command (variable interpolation, multi-line, native exe w/ multiple flags) → refer to `powershell-syntax-gotchas` skill first.

## CLI Over MCP Rule

Prefer CLI tools over MCP tools for external services — CLIs don't consume context until invoked; MCP tool schemas load upfront every session.

## GitHub Access Rule

For any GitHub operation beyond the local repo (PRs, issues, reviews, comments, threads, remote branches, Actions, releases, etc.) → use `gh` CLI, not MCP tools.

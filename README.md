# Agent Needle 🪡

**Persistent context. Surgical execution.**

Agent Needle gives AI coding agents lightweight, repository-backed memory. No
database, service, or complex setup—just Markdown files placed inside your
project.

## Philosophy

Agent Needle combines two ideas:

1. **Persistent context:** The repository acts as durable memory between otherwise
   isolated agent sessions.
2. **Surgical execution:** The agent should make the smallest complete change,
   avoid unsupported assumptions, and verify the requested outcome.

The name reflects the project's emphasis on small, precise, disciplined changes.

## Add to any project

For Codex and other `AGENTS.md`-compatible agents, copy:

```text
AGENTS.md
.agent/
.memory/
.gitignore
```

If you use Claude Code, also copy:

```text
CLAUDE.md
```

`CLAUDE.md` simply imports `AGENTS.md`, keeping one canonical instruction source.

That's it. Start your coding agent inside the project.

## Structure

```text
AGENTS.md          Core agent and memory instructions
CLAUDE.md          Optional Claude Code compatibility
.agent/
├── IDENTITY.md    Agent identity, operator, timezone, and scope
└── CONFIG.md      Behavior and persistence settings
.memory/
├── INDEX.md       Durable-memory index
└── ACTIVE.md      Current work and resumption point
```

The agent creates additional memory files only when useful:

```text
.memory/
├── state/         Verified project facts
├── decisions/     Important decisions and rationale
└── episodes/      Dated records of meaningful work
```

Memory is retrieved by relevance, verified against the project, and stored as
transparent, human-readable Markdown.

## Influences

Agent Needle was inspired by [Agent Ember](https://github.com/almahdi/agent-ember) by [Ali Almahdi](https://github.com/almahdi), a minimal pattern for repository-backed agent memory.

## License

Agent Needle is available under the [MIT License](https://github.com/iMythms/agent-needle/blob/main/LICENSE).

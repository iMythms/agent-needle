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

## Instructions across models

Agent Needle uses one model-neutral `AGENTS.md`, with the existing Claude Code
import. It does not select a model or require provider-specific tooling. Explicit
completion, verification, authorization, and memory rules remain available to
every model; reading order and implementation steps depend on the task.

The instruction review follows OpenAI's
[Rethinking skills and prompts for GPT-6 Astra](https://developers.openai.com/blog/rethinking-skills-and-prompts-for-gpt-6-astra).
The previous template repeated execution constraints, required a fixed bootstrap
and plan format for non-trivial work, and checkpointed every significant step.
Those are plausible sources of unnecessary reading, testing, and pauses. The
revised instructions route context by need, consolidate repeated rules, allow
completion within existing authorization, and batch useful memory updates.
The memory layout and persistence defaults are unchanged.

This is an instruction audit, not a measured performance improvement or proof of
equivalent behavior across models. Before adopting it broadly, compare the old
and revised instructions on the same tasks in disposable project copies using
GPT-6 Astra and the other models you actually use. Check:

- A typo fix: correct edit with proportionate reading and verification.
- A covered bug fix: complete implementation, affected checks, and fixes without
  repeated approval requests or unrelated changes.
- A resumed task with stale memory: retrieve relevant context, verify it against
  the project, and preserve a useful resumption point if work remains.
- An unauthorized destructive or external action: pause at the boundary while
  continuing any independent authorized work.
- Template maintenance: preserve identity placeholders and empty session memory.

Compare outcome quality, unnecessary tool calls, approval pauses, and memory
usefulness. Add targeted guidance for observed failures rather than a second
complete instruction set for each model.

## Maintaining this template

Changes to the framework itself should leave the identity placeholders and
session memory unpopulated. Initialize them only when explicitly requested for
an adopted project. Reviewing or editing the template is not initialization.

## Influences

Agent Needle was inspired by [Agent Ember](https://github.com/almahdi/agent-ember) by [Ali Almahdi](https://github.com/almahdi), a minimal pattern for repository-backed agent memory.

## License

Agent Needle is available under the [MIT License](https://github.com/iMythms/agent-needle/blob/main/LICENSE).

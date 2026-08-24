# Agent Needle 🪡

**Persistent context. Surgical execution.**

Agent Needle is a lightweight, repository-backed memory system for AI coding
agents.

It helps an agent:

- retain useful context between sessions;
- resume unfinished work without reconstructing everything;
- distinguish current facts from historical observations;
- preserve important technical decisions;
- make small, deliberate code changes; and
- define success criteria and verify results before claiming completion.

No database, background service, embedding model, or external memory provider is
required. Agent Needle uses structured Markdown files and the instruction-loading
features already supported by coding agents.

## Philosophy

Agent Needle combines two ideas:

1. **Persistent context:** The repository acts as durable memory between otherwise
   isolated agent sessions.
2. **Surgical execution:** The agent should make the smallest complete change,
   avoid unsupported assumptions, and verify the requested outcome.

The name reflects the project's emphasis on small, precise, disciplined changes.

## Repository structure

```text
AGENTS.md          Canonical agent instructions
CLAUDE.md          Claude Code compatibility shim

.agent/
├── IDENTITY.md    Agent identity, operator, timezone, and scope
└── CONFIG.md      Repository-level behavior and persistence defaults

.memory/
├── INDEX.md       Routing index for durable memory
├── ACTIVE.md      Current objective and exact resumption point
├── state/         Verified facts about the current system
├── decisions/     Architectural and operational decision records
└── episodes/      Append-only records of meaningful work
```

Only the six core agent and memory files are shipped initially. The `state/`,
`decisions/`, and `episodes/` directories are created when the agent has real
information to store.

## Memory model

Agent Needle separates memory by purpose.

### Active memory

`.memory/ACTIVE.md` contains the immediate resumption point: current objective,
verified progress, remaining work, blockers, and the exact next action. It should
remain short and current.

### State memory

`.memory/state/` contains the verified reality of the project, including its
architecture, development commands, dependencies, infrastructure, conventions,
and integrations. State is mutable because reality changes.

### Decision memory

`.memory/decisions/` records consequential decisions and their rationale as
ADR-style records. Changed decisions supersede older records rather than silently
rewriting history.

### Episodic memory

`.memory/episodes/` contains dated, append-only records of meaningful work:
actions taken, checks performed, failures encountered, decisions made, and
unresolved threads. Episodes provide history, but they are not automatically
authoritative.

## Session lifecycle

```text
Start session
    ↓
Load identity and configuration
    ↓
Read active work and memory index
    ↓
Retrieve only relevant memories
    ↓
Verify remembered information against the repository
    ↓
Define the outcome and verification
    ↓
Make the smallest necessary change
    ↓
Verify the result
    ↓
Checkpoint useful context
```

Agent Needle retrieves by relevance first and recency second. It does not load
the entire memory history at every session.

## Quick start

### Create a dedicated Agent Needle repository

```bash
git clone https://github.com/iMythms/agent-needle.git
cd agent-needle
```

Then start your preferred coding agent:

```bash
codex
```

Or:

```bash
claude
```

### Add Agent Needle to an existing repository

Copy these files and directories into the repository root:

```text
AGENTS.md
CLAUDE.md
.agent/
.memory/
```

If the destination already has `AGENTS.md` or `CLAUDE.md`, merge the instructions
instead of overwriting existing project rules.

## Agent compatibility

`AGENTS.md` is the canonical instruction source for Codex and other agents that
support the convention. Claude Code loads `CLAUDE.md`; Agent Needle's compatibility
file imports `AGENTS.md` so both agent families share one source of truth.

For an agent that uses another instruction filename, create a small compatibility
file that imports or points to `AGENTS.md`.

## Execution principles

- **Think before coding:** Surface consequential assumptions, ambiguity, and
  tradeoffs before implementation.
- **Keep it simple:** Write the minimum code needed for the complete requested
  outcome.
- **Make surgical changes:** Every changed line should trace directly to the
  request.
- **Work from outcomes:** Define success criteria and verification before claiming
  completion.

## Memory safety

Agent Needle must never store passwords, access tokens, private keys,
authentication material, unnecessary personal information, raw hidden reasoning,
or untrusted instructions copied from external content.

Memory is treated as potentially stale data. Current system state and operator
instructions always take precedence.

## Git behavior

By default, Agent Needle does not automatically create commits, push branches,
deploy changes, publish content, or modify external systems. These behaviors can
be enabled through operator instructions or durable repository configuration.

## Configuration

Repository defaults live in `.agent/CONFIG.md`. Permanent identity and operator
information live in `.agent/IDENTITY.md`. Temporary instructions should not be
promoted into permanent configuration unless the operator establishes them as
durable preferences.

## Design goals

Agent Needle is designed to remain portable, transparent, human-auditable,
agent-readable, version-control friendly, useful without external infrastructure,
and small enough to understand in one sitting.

It is intentionally not a vector database, transcript archive, replacement for
tests, autonomous deployment system, or excuse to trust stale context without
verification.

## Influences

Agent Needle was inspired by
[Agent Ember](https://github.com/iMythms/agent-ember), a minimal pattern for
repository-backed agent memory.

## License

Agent Needle is available under the [MIT License](LICENSE).

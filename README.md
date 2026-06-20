# CHARACTER.md

AI agents forget who they are. Memory tools like Mem0, Zep, and LangMem help agents recall past conversations — but none of them answer a more basic question: *who is this agent?* How should it behave, what does it know, and how do those things relate to what it's been through?

CHARACTER.md gives your agent a structured identity. Three sections — dispositions, knowledges, and experiences — each handle a different kind of memory that changes at a different rate. One file, plain Markdown, no runtime dependency.

## Getting started

The fastest way to understand the format is to look at one. Here's a work assistant that manages clients and tracks project status across sessions:

[`examples/agent/CHARACTER.md`](examples/agent/CHARACTER.md)

Copy it into a conversation with any AI, and the AI will know how to behave, what projects are active, and what happened in the last few sessions. Edit it, and you have your own agent.

For a simpler starting point, see the [minimal example](examples/minimal/CHARACTER.md) — a single-file character you can read in 30 seconds.

## What you can build with it

**A persistent AI assistant.** Define how your agent should behave, write down what it needs to know about you and your work, and let it accumulate experiences over time. The next conversation picks up where the last one left off — not because the platform remembers, but because the file does. The format marks which parts are stable, which parts update, and which parts only grow — an AI consuming the file can write changes back to the right place automatically.

**A multi-agent team.** Each agent is a self-contained file. Load several into the same conversation and they each bring their own dispositions, knowledge, and history. A team of AI assistants can cover different specialties without stepping on each other. The file is the boundary.

**A stateful NPC or game character.** Define starting traits and knowledge, then let the experience layer fill in as players interact. The format already separates what changes from what doesn't, so you don't need to build that logic yourself.

## How it works

A CHARACTER.md file has three sections, each handling a different kind of memory:

**Dispositions** — how the agent behaves and what it can do. Rules, tendencies, skills, and boundaries that stay mostly stable. Think of them as the agent's operating system: personality, tone, areas of competence, how it responds under specific conditions.

**Knowledges** — what the agent knows. Some are facts that rarely change; others are current state that gets updated as things happen. Domain knowledge, situational awareness, and working context live here.

**Experiences** — what the agent has been through. A record of events, decisions, and interactions. This section only grows — nothing is deleted, but older entries can settle into deeper storage, the way long-term memory works.

```
CHARACTER.md
├── Dispositions      — how it behaves
├── Knowledges        — what it knows
└── Experiences       — what it's been through
```

This three-way split isn't arbitrary — it mirrors the procedural / semantic / episodic memory model from cognitive science, specifically the [CoALA framework](https://arxiv.org/abs/2309.02427) (Cognitive Architectures for Language Agents). Dispositions map to procedural memory, Knowledges to semantic memory, Experiences to episodic memory. The format inherits a structure that cognitive science and AI research have already validated, rather than inventing its own.

The spec defines a semantic structure, not a file format. Markdown is the simplest implementation — plain text, no tooling, works everywhere — but the same three sections work in any document your AI can read.

## How is this different from existing memory solutions?

**Different layer, not a competing product.** Agent memory frameworks — Mem0, Zep, LangMem, Letta — are runtime infrastructure. They handle storage, indexing, and retrieval while your agent runs. CHARACTER.md operates one layer above: it defines who the agent *is* before it starts running. You can use both together — CHARACTER.md for identity, your preferred memory framework for retrieval.

**Structure that prevents drift.** Memory, custom instructions, and system prompts tend to become flat lists where personality traits, domain facts, and yesterday's events all blend together. Over time, the AI can't tell which parts are stable and which are outdated. CHARACTER.md separates them by design — dispositions that rarely change, knowledge that updates in place, experiences that only accumulate — so the structure itself prevents drift.

**Portable.** CLAUDE.md and AGENTS.md solve a similar problem for coding agents — persistent instructions and learned behaviors across sessions. They handle procedural and semantic memory well but lack a structured episodic layer. CHARACTER.md adds that third layer, formalizes the boundaries between all three, and works across any AI platform, not just one vendor's toolchain.

## Where to go from here

To understand why the format is designed this way — why three sections, why natural language, why not YAML — read the [design rationale](RATIONALE.md).

If you're building a tool or platform that consumes character files, the [spec](SPEC.md) has the precise definitions, conformance rules, and lifecycle semantics.

For a working example of a CHARACTER.md served over MCP, see [book-mcp](https://github.com/liheng-personal/book-mcp).

## License

This specification is released under [CC BY 4.0](LICENSE). Use it, build on it, adapt it — just give credit.

## Credits

CHARACTER.md is created and maintained by [Narrativesaw](https://narrativesaw.com).

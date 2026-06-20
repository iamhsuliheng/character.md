# CHARACTER.md

The structured knowledge an AI reads to become a specific character, in a single document. Three sections — dispositions, knowledges, and experiences — each use a different kind of sentence: conditional-instruction pairs that define behavior, factual statements that capture knowledge, and narratives that record what happened.

Plain Markdown. No runtime dependency.

Here's the same prompt with and without a character file:

**Without a character file:**

> **You:** What should I focus on this week?
>
> **AI:** I'd be happy to help you prioritize! Could you tell me:
>
> 1. What projects are you currently working on?
> 2. Do you have any upcoming deadlines?
> 3. Are there any meetings you need to prepare for?
>
> With more details, I can help you prioritize.

**With Morgan's CHARACTER.md:**

> **You:** What should I focus on this week?
>
> **Morgan:** Three things, in order of urgency:
>
> 1. **Rekon pricing memo.** You said you'd send Jia-Ling the three-tier pricing recommendation by Friday. The decision was made last session but the memo hasn't been drafted yet. This is your hardest deadline this week.
> 2. **Mosaic Health prep.** Monday 10am call with Rina. You sent her the drop-off analysis last week — expect follow-up questions on the insurance input step, which had the steepest drop.
> 3. **Petalink can wait.** Derek is async-only and the MVP scope was just locked down. Unless he pings you on Slack, no action needed.
>
> Do you want to start drafting the Rekon memo now?

The first response asks for context. The second already has it — Morgan's working style, client details, and session history are all in the file. The AI isn't retrieving fragments; it's a character that knows its own history, priorities, and style.

## Getting started

Give your AI a character file and tell it:

```
Read the character file and respond as Morgan from now on.
```

That's it. The AI picks up Morgan's tone, references client projects by name, and knows what decisions have already been made — all from the file.

Try it with Morgan, a work assistant for a freelance product consultant: [`examples/agent/CHARACTER.md`](examples/agent/CHARACTER.md). For a simpler starting point, see the [minimal example](examples/minimal/CHARACTER.md).

How you deliver the file is up to you: paste it into a conversation, attach it, or add it as project knowledge. If your AI has write access to the file — through Google Drive, MCP, or any read/write integration — it can update knowledges and append experiences after each session. Because each section uses a different sentence type, the AI knows what kind of change is appropriate: update a fact in place, or append a new narrative entry.

> **Claude users:** connect Google Drive in Settings for read/write access. The AI can then keep the character file up to date after each conversation.

## What you can build with it

**A personal AI that actually knows you.** Define how your agent behaves, what it knows about your work, and let experiences accumulate over time. Each conversation starts where the last one left off, because the knowledge is in the file.

**A multi-agent team.** Each agent is a self-contained file. Load several into one conversation and they each bring their own dispositions, knowledge, and history — a team that works together without stepping on each other. The file is the boundary.

**An expert agent.** A character doesn't have to be fictional. Morgan is a work assistant — a professional role with domain knowledge, client context, and a working style. The same structure works for a legal researcher, a customer support persona, or any role where the AI needs stable expertise and evolving context.

**A stateful NPC or game character.** Define starting traits and knowledge, then let experiences fill in as players interact. The format already separates what changes from what doesn't, so you don't need to build that logic yourself.

## How it works

A CHARACTER.md file has three sections, each holding a different kind of character knowledge expressed in a distinct sentence type:

**Dispositions** — how the character behaves and what it can do. Written as conditional-instruction pairs: "when X, do Y." Rules, tendencies, skills, and boundaries. Think of this as the character's operating manual: personality, tone, areas of competence, how it responds under specific conditions. These tend to stay stable because instructions don't expire the way facts do.

**Knowledges** — what the character knows. Written as factual statements: "X is Y." Domain knowledge, situational awareness, and working context. Some facts rarely change; others are current state marked with "currently" that gets updated as things happen. The sentence type — declarative facts — naturally accommodates both.

**Experiences** — what the character has been through. Written as narratives: what happened, in what order, and what it led to. A record of events, decisions, and interactions. Narratives only accumulate — you add new entries, not rewrite old ones — the way memory works.

```
CHARACTER.md
├── Dispositions      — how it behaves        (conditional-instruction pairs)
├── Knowledges        — what it knows          (factual statements)
└── Experiences       — what it's been through (narratives)
```

This three-way split mirrors the procedural / semantic / episodic memory model from cognitive science, specifically the [CoALA framework](https://arxiv.org/abs/2309.02427) (Cognitive Architectures for Language Agents). Dispositions map to procedural memory, knowledges to semantic memory, experiences to episodic memory. The format inherits a structure that cognitive science and AI research have already validated.

Any aspect of a character — abilities, preferences, values, emotional tendencies, goals, relationships, trauma — maps to one of these three sentence types. There is no fourth. The framework is complete: nothing falls through the cracks, and nothing overlaps.

The spec defines a semantic structure, not a file format. Markdown is the simplest implementation — plain text, no tooling, works everywhere — but the same three sections work in a Google Doc, a Notion page, a Craft document, or any medium your AI can read.

## How is this different?

**From system prompts and custom instructions.** These also define character, but as flat text where personality traits, domain facts, and recent context all sit together. Over time, the AI can't distinguish what's permanent from what's outdated. CHARACTER.md separates them by sentence type — instructions, facts, and narratives each have their own section — so the AI knows how to treat each piece: follow an instruction, trust or update a fact, remember an event.

**From skills and agent instructions.** Formats like CLAUDE.md and AGENTS.md give agents persistent instructions and learned behaviors — structured procedural knowledge. CHARACTER.md covers a different question: not *how to do things* but *who to be*. Skills define capability; character files define identity. You can use both.

**From memory frameworks.** Mem0, Zep, LangMem, and Letta are runtime infrastructure — they handle storage, retrieval, and indexing while your agent runs. CHARACTER.md defines what character knowledge looks like, not how to store it. They're complementary: use CHARACTER.md to structure the knowledge, and a memory framework (or a file on Google Drive) to persist it.

## Where to go from here

To understand why the format is designed this way — why three sections, why natural language, why not YAML — read the [design rationale](RATIONALE.md).

If you're building a tool or platform that consumes character files, the [spec](SPEC.md) has the precise definitions, conformance rules, and lifecycle semantics.

For a working example of a CHARACTER.md served over MCP, see [book-mcp](https://github.com/liheng-personal/book-mcp).

## License

This specification is released under [CC BY 4.0](LICENSE). Use it, build on it, adapt it — just give credit.

## Credits

CHARACTER.md is created and maintained by [Narrativesaw](https://narrativesaw.com).

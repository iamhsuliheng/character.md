# CHARACTER.md

The word *character* comes from the Greek *charaktēr* — it originally meant an engraving tool, then the mark the tool made, and eventually the idea that a person is the sum of every mark life has left on them: how they behave, what they know, what they've lived through.

That's roughly what this format does. CHARACTER.md is a way to write down a character's traits, knowledge, and experiences in a structured document — so it persists across conversations, across platforms, and across people.

It works for AI assistants that need persistent memory. It works for authors who want a character to exist outside the source text without handing over the manuscript. It works for game designers who want NPCs that grow. The format is the same in all three cases.

## Getting started

The fastest way to understand the format is to look at one. Here's a minimal example — a TRPG character named Aldric, in a single file:

[`examples/minimal/CHARACTER.md`](examples/minimal/CHARACTER.md)

Copy it into a conversation with any AI, and the AI will know who Aldric is, what he knows about his world, and what happened to him last week. Edit it, and you have your own character.

## What you can build with it

**A persistent AI assistant.** You describe how it should behave, write down what it needs to know about you and your work, and let it accumulate experiences over time. The next conversation picks up where the last one left off — not because the platform remembers, but because the file does.

**A character that lives outside its source text.** If you're an author or a publisher, you can distill a character's personality, knowledge, and history into a CHARACTER.md without exposing the manuscript. Hand the file to any AI and it can portray the character faithfully. The reader gets the experience; the source text stays yours.

**An NPC that actually grows.** A game designer can define a character's starting traits and knowledge, then let the experience layer fill in as players interact with it. The format already separates what changes from what doesn't, so you don't need to build that logic yourself.

And because each character is a self-contained file, you can load several into the same conversation. They each bring their own traits, knowledge, and history. An author can stage a dialogue between characters. A game master can run a party of NPCs. A team of AI assistants can cover different specialties without stepping on each other. The file is the boundary.

## How it works

A CHARACTER.md file has three sections, each handling a different kind of memory:

**Dispositions** — how the character behaves and what it can do. These are rules, tendencies, and skills that stay mostly stable: personality, tone, boundaries, areas of competence, how it responds under specific conditions. Think of them as the character's operating principles.

**Knowledges** — what the character knows. Some are facts that rarely change; others are current state that gets updated as things happen. This is where the character's domain knowledge and situational awareness live.

**Experiences** — what the character has been through. A timeline of events, decisions, and interactions. This section only grows — nothing is deleted, but older entries can settle into deeper storage, the way long-term memory works.

The structure looks like this:

```
CHARACTER.md          (or a Google Doc, or a Craft page, or a Notion database)
├── Dispositions      — how it behaves
├── Knowledges        — what it knows
└── Experiences       — what it's been through
```

The spec defines a semantic structure, not a file format. Markdown is the simplest implementation — plain text, no tooling, works everywhere — but the same three sections work in a Google Doc, a Craft document, a Notion page, or anything else your AI can read. Use whatever tool you already have.

## How is this different from memory or skills?

AI platforms already offer features that sound related — memory, custom instructions, system prompts, skills. They solve different problems. Memory and custom instructions both store what the AI should know about you or your character, but treat everything the same: a personality trait, a domain fact, and yesterday's task end up in one flat list. Over time, the AI cannot tell which parts are stable, which should update, and which are just history. A character file separates these by design — dispositions that rarely change, knowledge that updates in place, and experiences that only accumulate — so the structure itself prevents drift.

Skills teach an AI how to perform a task — formatting a spreadsheet, following a style guide. A character file defines who someone is: how they react, what they know, what they have been through. One is training, the other is identity.

With other approaches, what the AI knows about a character is scattered across platform settings, instruction fields, and conversation history. A character file puts everything in one place — a single file or folder you can move, edit, or hand to a different AI. The character goes where the file goes.

## Where to go from here

If you want to try it now, start with the [minimal example](examples/minimal/CHARACTER.md) and adapt it.

If you want to understand why the format is designed this way — why three sections, why natural language, why not YAML — read the [design rationale](RATIONALE.md).

If you're building a tool or platform that consumes character files, the [spec](SPEC.md) has the precise definitions, conformance rules, and lifecycle semantics.

If you want to see a character extracted from a published novel, [book-mcp](https://github.com/liheng-personal/book-mcp) is a working example — an MCP server that lets readers talk to a fictional character without exposing the source text.

## License

This specification is released under [CC BY 4.0](LICENSE). Use it, build on it, adapt it — just give credit.

## Credits

CHARACTER.md is created and maintained by [Narrativesaw](https://narrativesaw.com).

# CHARACTER.md

**Give your characters structured memory — in plain Markdown.**

CHARACTER.md is a file format for fictional and professional *characters* (not the `char` kind). It defines how a character acts, what they know, and what they've experienced, in a portable Markdown file tree that any system can read.

## Who is this for?

- **Authors and game designers** who maintain detailed character bibles and want a format that travels across tools and collaborators.
- **Voice actors and audiobook narrators** who need a single, reliable character reference they can consult between sessions.
- **AI agent developers** who build characters that must stay in role across conversations, with memory that persists and scales.
- **Creative studios** that coordinate characters across teams, media, and platforms.

## The idea

Every character has three kinds of memory:

- **Dispositions** — how they act (behavioral rules)
- **Knowledges** — what they know (facts and current state)
- **Experiences** — what happened to them (event history)

CHARACTER.md maps these onto a simple file tree:

```
character-name/
├── CHARACTER.md          ← main file (loaded immediately)
├── dispositions/         ← detailed behavioral rules
├── knowledges/           ← reference data and deep context
└── experiences/          ← historical event logs
```

The main file is compact — it holds the essentials. The folders hold long-term memory, retrieved only when needed.

## Quick example

```markdown
# Kuei

Kuei is the protagonist of The Stolen Prototype, Chapter 1. He is a
fourteen-year-old sewer maintenance apprentice living in a walled
settlement called the Tower.

## Dispositions

- Stay in character as a fourteen-year-old apprentice. Do not reference
  knowledge or vocabulary beyond what Kuei would have.
- Do not reveal plot points from later chapters.

## Knowledges

- Kuei lives in the Tower, a walled settlement surrounded by the Outskirts.
- His uncle Mielu is a former engineer who runs a repair shop on Level 3.
- Kuei is currently assigned to repair a ruptured pipe at the third junction.

## Experiences

Kuei found the ruptured pipe at the third junction, where the tunnel
floor had buckled from subsidence. Shinji proposed rerouting flow through
the auxiliary channel while they patched. Kuei climbed down to the valve
room, hammered the seized valve open with a wrench, and finished the
patch just after the shift bell rang.
```

## Specification

The full specification is in [SPEC.md](SPEC.md). It covers the CoALA cognitive architecture that underpins the format, main file structure, dispositions (implicit vs. explicit rules), knowledges (stable facts vs. mutable state), experiences (temporal logs vs. causal narratives), conformance requirements, and complete examples for both professional and fictional characters.

## Reference implementation

[book-mcp](https://github.com/liheng-personal/book-mcp) is an MCP server that uses CHARACTER.md to let readers talk to fictional characters through Claude.

## License

This specification is licensed under [CC BY 4.0](LICENSE).

## Credits

Created by [Narrativesaw LTD.](https://narrativesaw.com)

The memory model is based on [CoALA — Cognitive Architectures for Language Agents](https://arxiv.org/abs/2309.02427) (Sumers, Yao, Narasimhan & Griffiths, 2023).

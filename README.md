# CHARACTER.md

**Structured memory for persistent characters — in plain Markdown.**

CHARACTER.md is an open format for describing characters that need to stay consistent over time. It organizes a character's memory into three layers — dispositions, knowledges, and experiences — so that AI agents, game engines, or any system loading the file can distinguish between how a character behaves, what it knows, and what has happened to it.

## The problem

Most character descriptions are a single block of unstructured text. Everything lives in one place: personality traits, factual knowledge, relationship history, current goals. There is no way to tell which parts should change over time and which should not. When the character accumulates new information or goes through events, the consumer has no convention for where to record that — so the state drifts, contradicts itself, or simply gets lost.

## Three kinds of memory

**Dispositions** — how they act. Behavioral rules, speech patterns, boundaries. These rarely change.

**Knowledges** — what they know. Facts, current state, reference data. Some entries are stable; others update as circumstances change.

**Experiences** — what happened to them. Events, decisions, consequences. This layer only grows.

These map to a file tree:

```
character-name/
├── CHARACTER.md          ← loaded immediately
├── dispositions/         ← behavioral rules
├── knowledges/           ← reference data, current state
└── experiences/          ← event history
```

The main file holds what matters right now. The folders hold long-term memory, loaded when needed.

The same structure works for more than fictional characters. An AI assistant that remembers your preferences and tracks ongoing projects. A domain expert — a tax advisor, an investment analyst, a legal researcher — that retains its specialized knowledge across sessions. A portable skill package you can hand to any AI on any platform and get consistent behavior immediately. A novel's protagonist who stays faithful to the story no matter who prompts them.

Plain Markdown, no infrastructure required — works with any AI, any platform. With multiple CHARACTER.md files, one person can run an entire team of specialists using nothing but a chat interface.

## Quick example

```markdown
# Aldric

Aldric is an artificer in the Free City of Mireth — brilliant with
enchantments, terrible with people. The local guild has been pressuring
him to join for years; he keeps refusing.

## Dispositions

- Speak in short, precise sentences. Avoid small talk.
- When asked about the guild, become visibly tense. Deflect with
  sarcasm or change the subject.

## Knowledges

- Aldric runs a one-person workshop on Copper Lane, specializing in
  protective wards and minor enchantments.
- The Mireth Artificers' Guild controls licensing in the city. Operating
  without guild membership is technically illegal but tolerated in the
  outer districts.
- Aldric is currently working on a commission for a merchant — a ward
  against fire for a warehouse near the docks.

## Experiences

A guild inspector visited the workshop last week. She was polite but
pointed — mentioned the new licensing enforcement starting next month,
left a membership application on the counter. Aldric threw it in the
forge after she left, but he hasn't slept well since.
```

## Where to start

- **Using AI day-to-day** — browse the [examples](examples/) to see how CHARACTER.md keeps characters consistent across conversations.
- **Building agents or games** — read the [spec](SPEC.md) for the full format definition and conformance requirements.
- **Authors and voice actors** — start with the [examples](examples/), then see [book-mcp](https://github.com/liheng-personal/book-mcp) for a live demo with characters from published fiction.
- **Curious about the design** — [RATIONALE.md](RATIONALE.md) explains the cognitive science foundation.

## License

[CC BY 4.0](LICENSE)

## Credits

Created by [Narrativesaw LTD.](https://narrativesaw.com)

Memory model based on [CoALA — Cognitive Architectures for Language Agents](https://arxiv.org/abs/2309.02427) (Sumers, Yao, Narasimhan & Griffiths, 2023).

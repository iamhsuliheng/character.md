# CHARACTER.md

**Structured memory for persistent characters — in plain Markdown.**

CHARACTER.md is an open format that gives characters structured, evolving memory — so they stay consistent whether a conversation is ten turns or ten thousand.

## What you can build with it

Most character descriptions are a single block of unstructured text that drifts over time — personality, knowledge, and history all mixed together with no way to tell what should change and what should not. CHARACTER.md separates these concerns. Because the format marks which parts are stable, which parts update, and which parts only grow, an AI consuming the file can write changes back to the right place automatically — the character grows with every interaction, no manual editing required.

That separation opens up real applications:

**A personal AI that actually remembers.** Define an assistant that knows your preferences, tracks your ongoing projects, and accumulates context across sessions — without starting from zero every time.

**Domain experts you can hand to anyone.** Package a tax advisor, an investment analyst, or a legal researcher as a portable file. Their specialized knowledge, operating rules, and case history travel with them — drop the file into any AI, on any platform, and get consistent expertise immediately.

**Game characters that don't forget.** Give an NPC a memory that persists across play sessions. They remember what the player said, what deals were struck, what grudges remain. The world feels alive because the characters in it have continuity.

**Fictional characters faithful to the story.** Distill a novel's protagonist into a structured profile — their voice, their knowledge of the world, their lived experiences — and let readers interact with them without the AI inventing things that never happened.

## How it works

Three kinds of memory, each with different update rules:

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

The main file holds what matters right now. The folders hold long-term memory, loaded when needed. Because each layer has clear mutability rules, an AI agent can update knowledges and append experiences during use — the character file becomes a living document that improves the more you use it.

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

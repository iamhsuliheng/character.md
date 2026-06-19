# CHARACTER.md

**Structured memory for persistent characters — in plain Markdown.**

You give an AI a character to play. It's great for a while. Then it starts forgetting things. It contradicts itself. It loses track of what it knows and what happened to it.

Sound familiar?

- You spend more time correcting your AI assistant than actually working with it.
- Your game character meets the player a second time and has no memory of the first.
- You ask an AI to play a character from your novel, and it invents things that never happened.

CHARACTER.md fixes this by giving characters structured memory — three kinds, matching how memory actually works:

**Dispositions** — how they act. Behavioral rules, speech patterns, boundaries.

**Knowledges** — what they know. Facts, current state, reference data.

**Experiences** — what happened to them. Events, decisions, consequences.

These map to a file tree:

```
character-name/
├── CHARACTER.md          ← loaded immediately
├── dispositions/         ← behavioral rules
├── knowledges/           ← reference data, current state
└── experiences/          ← event history
```

The main file holds what matters right now. The folders hold long-term memory, loaded when needed. Knowledge updates as things change, experiences grow as events unfold, and the character stays coherent — whether the conversation is ten turns or ten thousand.

It's plain Markdown. Use it with any AI, any platform, no infrastructure required. Each character is a self-contained file — so with multiple CHARACTER.md files, one person can run an entire team of AI specialists, each with its own expertise, memory, and personality, using nothing but a chat interface.

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

- **Using AI tools day-to-day** — browse the [examples](examples/) to see how CHARACTER.md keeps characters consistent across conversations.
- **Building agents or game characters** — read the [spec](SPEC.md) for the full format specification and conformance requirements.
- **Authors and voice actors** — start with the [examples](examples/) to see how characters are structured. For a live demo of characters from published fiction, see [book-mcp](https://github.com/liheng-personal/book-mcp).
- **Curious about the design?** — [RATIONALE.md](RATIONALE.md) explains the cognitive science foundation.

## License

[CC BY 4.0](LICENSE)

## Credits

Created by [Narrativesaw LTD.](https://narrativesaw.com)

Memory model based on [CoALA — Cognitive Architectures for Language Agents](https://arxiv.org/abs/2309.02427) (Sumers, Yao, Narasimhan & Griffiths, 2023).

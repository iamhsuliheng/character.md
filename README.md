# CHARACTER.md

CHARACTER.md is the whole data required for an agent to become a character who knows you, in a single file or a package. Memories, skills, instructions, knowledges… CHARACTER.md has it all. 

Getting an agent to know you is cumbersome. You need to setup instructions, find memory solutions, install skills, and maintain all of them continuously, or they will soon start to contradict themselves. Worst of all? They are all different configs and services, so you need to travel back and forth just for fixing a wrong fact.

That's because every platform organizes your setup by mechanism — one bucket for memory, another for instructions, another for skills. Each platform's buckets are different, so the same knowledge ends up in different places depending on the platform. The structure only works where it was built.

CHARACTER.md organizes by meaning instead — specifically, by sentence type. Everything you'd put into an AI setup is one of three things:

**Dispositions** — rules. Written as conditional-instruction pairs: "When X, do Y." Behavior, skills, boundaries, preferences. The AI reads an instruction and follows it.

**Knowledges** — facts. Written as statements: "X is Y." Domain expertise, personal context, current status. The AI reads a fact and trusts it — or updates it when the fact changes.

**Experiences** — stories. Written as narratives: what happened, in what order, what it led to. The AI reads a story and remembers it.

```
CHARACTER.md
├── Dispositions      (rules — conditional-instruction pairs)
├── Knowledges        (facts — statements)
└── Experiences       (stories — narratives)
```

That's it. Every aspect of an AI setup — behavior, knowledge, context, history, skills, preferences — maps to one of these three. There is no fourth.

No special syntax. No metadata. Your entire AI setup — memory, instructions, project knowledge, skills — maps into these three sections with nothing left over. The only thing your platform needs to do is read the file.

Here's what that looks like. Same prompt, with and without a character file:

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
> 1. **Rekon pricing memo.** You said you'd send the three-tier recommendation by Friday. Decision's made — memo isn't drafted yet.
> 2. **Mosaic Health prep.** Monday 10am call with Rina. Expect follow-ups on the insurance input step.
> 3. **Petalink can wait.** MVP scope just locked down. No action unless Derek pings.

Morgan doesn't need a memory system or a skills framework. Its working style, client details, and session history are all in one file — rules in Dispositions, facts in Knowledges, events in Experiences. That's why it works on any platform: the structure is in the language, not in the tooling.

When you organize rules, facts, and stories into one file, what you get isn't just a configuration — it's a character. Morgan is one. A legal researcher could be another. So could a game NPC that grows with every player interaction.

That's why the format is called CHARACTER.md. Not because it starts with a character concept, but because the structure produces one.

## Getting started

Give your AI a character file and tell it:

```
Read the character file and respond as Morgan from now on.
```

That's it. Try it with [Morgan](examples/agent/CHARACTER.md), a work assistant for a freelance product consultant. For a simpler starting point, see the [minimal example](examples/minimal/CHARACTER.md).

How you deliver the file depends on your platform: paste it into a conversation, attach it, or add it as project knowledge. If your AI can write back to the file — through Google Drive, MCP, or any read/write integration — the character updates its own knowledge and appends new experiences after each session. The file grows with use.

> **Claude users:** connect Google Drive in Settings to give the AI read/write access to the character file.

## What you can build with it

**A multi-agent team.** Each agent is a self-contained file. Load several into one conversation and they each bring their own knowledge, rules, and history. The file is the boundary.

**An expert agent.** A character doesn't have to be fictional. The same structure works for a legal researcher, a customer support persona, or any role where the AI needs stable expertise and evolving context.

**A game character that grows.** Define starting traits and knowledge, then let experiences fill in as players interact. The format already separates what changes from what doesn't.

## Where to go from here

The three sentence types map to the procedural / semantic / episodic memory model from cognitive science, specifically the [CoALA framework](https://arxiv.org/abs/2309.02427). The spec defines a semantic structure, not a file format — the same three sections work in Markdown, a Google Doc, a Notion page, or any medium your AI can read. For the full design rationale, see [RATIONALE.md](RATIONALE.md).

If you're building a tool or platform that consumes character files, the [spec](SPEC.md) has precise definitions, conformance rules, and lifecycle semantics. For a working example served over MCP, see [book-mcp](https://github.com/liheng-personal/book-mcp).

## License

This specification is released under [CC BY 4.0](LICENSE).

## Credits

CHARACTER.md is created and maintained by [Narrativesaw](https://narrativesaw.com).

---
Annotations: 0,5794 SHA-256 5878716e0d152943ce09  
&Claude <claude.ai>: 537,5257  
@Li-Heng Hsu <lihenghsu.com>: 0,537  
...

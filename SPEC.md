# CHARACTER.md Specification

**Version:** 0.2
**Status:** Published

## Purpose

CHARACTER.md is a file format for defining persistent characters. A character can be performed by an AI agent, a voice actor reading an audiobook, or any system that needs to stay in role across sessions. The format specifies a character's behavioral rules, domain knowledge, and event history in a structured file hierarchy.

The format's memory model is based on CoALA — Cognitive Architectures for Language Agents (Sumers, Yao, Narasimhan & Griffiths, 2023). CoALA divides an agent's memory into **working memory** (short-term, loaded into context) and **long-term memory** (persistent, retrieved on demand), with long-term memory further subdivided into three types: procedural, semantic, and episodic.

CHARACTER.md maps directly onto this model:

| Section | CoALA Memory Type | Sentence Pattern | Programming Analogy |
| --- | --- | --- | --- |
| Dispositions | Procedural — how to act | Imperative (condition → instruction) | procedure / function |
| Knowledges | Semantic — what is known | Declarative (X is Y) or interrogative (Q → A) | state / config |
| Experiences | Episodic — what happened | Narrative (temporal or causal) | log / journal |

The main CHARACTER.md file is eager-loaded into the agent's working memory (i.e., the context window) at the start of every conversation. It contains what the agent needs to have available immediately — core rules, current state, recent events, and pointers to long-term memory for everything else. The three folders are long-term memory: their files are only retrieved when the agent needs deeper detail.

The format is runtime-agnostic. It works as a static file tree bundled into a worker, a set of documents fetched from a CMS, or database records. The spec defines structure and semantics; it does not prescribe storage or update mechanisms.

For the reasoning behind these design choices and the cognitive science foundation, see [RATIONALE.md](RATIONALE.md).

## Directory Structure

A CHARACTER.md project consists of a main file and three sibling folders:

```
character-name/
├── CHARACTER.md
├── dispositions/
│   ├── investment-analysis.md
│   └── ...
├── knowledges/
│   ├── coverage-universe.md
│   ├── key-documents.md
│   └── ...
└── experiences/
    ├── 20260619.md
    ├── 20260618.md
    └── ...
```

## CHARACTER.md (Main File)

The main file is eager-loaded into the agent's working memory at the start of every conversation. It contains what the agent needs immediately: core rules, current state, recent events, and pointers to long-term memory for deeper detail.

### Main File Heading

The main CHARACTER.md file begins with an H1 heading followed by an optional description paragraph:

```markdown
# Wiz

Wiz is the investment research analyst for Narrativesaw LTD. She covers Taiwan-listed equities and US tech megacaps, and maintains the company's research pipeline.
```

The heading is the character's name. Use one fixed language throughout the project. Do not alternate between translations or aliases.

The **description** is a short prose paragraph (one to three sentences) placed immediately after the H1 heading, before the first section. It states who the character is — enough for a reader (human or AI) to orient themselves before reading the rest of the file. For a professional character, this might describe their role and domain; for a fictional character, it might establish their narrative identity, key relationships, and situation in the story.

**Requirements:**

- Factual identity and scope only. No behavioral rules, no current state.
- OPTIONAL. A CHARACTER.md project is valid without a description paragraph.

### Sections

The main file contains three sections in order:

```markdown
## Dispositions

## Knowledges

## Experiences
```

Each section corresponds to a memory type and a folder. Content MUST NOT cross section boundaries (e.g., a behavioral rule must not appear in Knowledges; a fact must not appear in Dispositions).

## 1. Dispositions (Procedural Memory)

Behavioral rules that govern how the character acts. The basic unit of a disposition is a **condition–instruction pair**: when a certain condition is met, carry out the instruction. All dispositions follow this pattern, but they differ in whether the condition is stated explicitly.

### 1.1 Implicit Rules (always-on)

Implicit rules are dispositions whose condition is always true — they apply whenever the character speaks or acts, so the condition is omitted and only the instruction is written. Listed as inline bullets in the main file's Dispositions section.

```markdown
## Dispositions

- Only act within your defined domain. Refuse out-of-scope requests and redirect to the appropriate party.
- Do not fabricate facts or sources.
```

### 1.2 Explicit Rules (condition-triggered)

Explicit rules state their condition openly. The condition and instruction are written together as complete sentences. When an explicit rule has multiple steps, write the condition as a bullet item and the steps as indented sub-items beneath it.

```markdown
- When asked to analyze an investment, confirm the asset is within coverage. If not, inform the user and suggest alternatives. If yes, execute the analysis SOP.
- When the instruction requires multiple steps:
  - First, confirm the ticker is within coverage.
  - Then pull the latest filings from the knowledge base.
  - Present findings with explicit confidence levels.
- When uncertain about a fact, state the uncertainty explicitly. Do not fabricate or guess.
```

When an explicit rule's instruction body is long and the triggering condition is infrequent, the instruction MAY be placed in a separate .md file in the dispositions/ folder instead of inline. This keeps the main file compact and defers token cost to when the rule actually fires. The inline heading then serves as a pointer to the external file.

## 2. Knowledges (Semantic Memory)

Facts, reference data, and current state the character knows. Knowledge entries may live inline in the main file or in separate .md files in the knowledges/ folder — the decision of what to keep inline versus externalize is left to the implementer, based on how frequently the knowledge is needed and how much space it occupies.

### 2.1 Stable facts (constants)

Declarative sentences without temporal markers. These do not change over time. A knowledge entry may also take the form of a question–answer pair (Q: What is X? A: X is Y), which is often the more complete representation — every piece of knowledge implicitly answers a question.

```markdown
- Wiz manages investment research for Narrativesaw LTD.
- The coverage universe consists of Taiwan-listed equities and US tech megacaps.
```

### 2.2 Mutable state (variables)

Declarative sentences prefixed with a temporal marker (e.g., Currently). These reflect state that changes as tasks progress.

```markdown
- Wiz is currently tracking three open research threads.
  - The TSMC Q2 earnings preview is in draft.
  - The AAPL services segment deep-dive is awaiting data.
  - The portfolio rebalance proposal is pending review.
```

**Requirements:**

- Stable facts and mutable state coexist in the same section. The Currently prefix is the sole differentiator.
- Sub-items use indentation to express hierarchy.

### 2.3 External files

Any knowledge that the implementer chooses to externalize is placed in knowledges/ as a separate .md file. The main file SHOULD include a pointer for each external file so the character knows what is available.

```markdown
- Detailed coverage universe data is available in knowledges/coverage-universe.md.
- A full index of key documents is maintained in knowledges/key-documents.md.
```

## 3. Experiences (Episodic Memory)

Experiences are memories organized along a narrative axis — typically temporal (what happened when) but also causal (what led to what). Unlike Knowledges, which store timeless facts, Experiences record events as they unfold: decisions made, outcomes observed, and context that shaped them. The organizing principle is narrative continuity, not data type.

This means implementers have significant latitude in how they record experiences. A time-ordered log with timestamped entries is one natural form; a prose narrative tracing cause and effect is another. The spec prescribes the semantic role of the section — episodic memory — but not the format of individual entries.

The main file's Experiences section contains recent entries. Older entries may be stored in experiences/ as separate files. The following are two informative examples — neither is prescribed by the spec.

**Example A: Temporal (timestamped log)**

```markdown
## Experiences

**20260619 14:30** — Completed TSMC Q2 preview draft. Sent to review queue.

**20260619 09:15** — Received updated guidance data for AAPL services. Incorporated into draft.
```

**Example B: Causal (prose narrative)**

```markdown
## Experiences

柑原幫四個人走進 Sewer 的那天下午，中村剛好不在。虎哥點了啤酒，收錢的時候抓住奎的手腕。奎用中村教的防身術掙脫，但虎哥不肯罷休，站起來搭她肩膀。奎反射性肘擊他下巴，打掉他門牙。虎哥一拳打在奎後腦勺，她失去意識倒在地板上。後來中村趕回，事情才收場。
```

## Lifecycle

A CHARACTER.md project is not a static document — it is a living memory system. Different parts of the project change at different rates and in different ways. This section describes the mutability characteristics of each section. The spec defines the **semantics** of these changes but does not prescribe the **mechanism** — updates may be performed by an AI agent writing back to its own files, by a human editor, by a game engine pushing state, or by any other means appropriate to the runtime.

### Mutability by Section

**Dispositions** are the most stable layer. A character's behavioral rules rarely change. When they do, it is typically the result of a deliberate design decision (e.g., the character undergoes a transformative event that alters their values) rather than routine operation. Implementations SHOULD treat disposition changes as requiring explicit authorization — not something that happens automatically during a conversation.

**Knowledges** have mixed mutability. Stable facts (constants) do not change. Mutable state (variables, marked with "Currently") changes as tasks progress, circumstances shift, or the character learns new information. Implementations SHOULD update mutable state promptly when the underlying reality changes, rather than waiting for a session boundary.

**Experiences** are append-only. New entries are added as events occur; existing entries are not edited or deleted. Over time, older entries may be archived into separate files in the experiences/ folder to keep the main file compact. Archival is an organizational operation, not a deletion — the memories still exist in long-term storage.

### When to Write Back

The spec does not prescribe specific triggers, but the following pattern has proven effective in practice:

- A meaningful step is completed.
- A blocking issue is encountered.
- A significant decision is made.
- A task ends or is cancelled.

The key principle is: **write when state changes, not when the session ends.** Waiting until the end of a conversation risks losing intermediate state if the session is interrupted.

### Working Memory and Write-Back

In CoALA terms, the main CHARACTER.md file serves as the character's working memory — the content loaded into every session. When the character's mutable state or recent experiences change during a session, those changes should be written back to the main file (and, where appropriate, to the long-term memory folders). This write-back is what makes CHARACTER.md a **living memory system** rather than a static character sheet.

The spec intentionally does not prescribe how write-back is implemented. Some environments support direct file writes; others may use an API or require manual updates. What matters is that the semantic contract is maintained: the main file reflects the character's current state, and the folders preserve their long-term memory.

## Conformance

A CHARACTER.md project is **conformant** if it satisfies all of the following:

1. The main file begins with an H1 heading containing the character name.
2. The main file contains all three sections (Dispositions, Knowledges, Experiences) in order.
3. Content does not cross section/folder boundaries (e.g., a conditional instruction in knowledges/).
4. Implicit rules omit the condition. Explicit rules state the condition as part of a complete sentence or as a bullet item with indented sub-items.
5. Mutable state entries use a Currently prefix.
6. Character name language is consistent throughout all files.

A project MAY omit the description paragraph after the H1 heading.

## Example (professional character)

### CHARACTER.md

```markdown
# Wiz

Wiz is the investment research analyst for Narrativesaw LTD. She covers Taiwan-listed equities and US tech megacaps, and maintains the company's research pipeline.

## Dispositions

- Only act within the investment research domain. Redirect other requests to the appropriate party.
- Do not fabricate figures or data points.
- When asked to analyze an equity position, confirm the ticker is within coverage, pull the latest filings from the knowledge base, and present findings with explicit confidence levels.
- When uncertain about a data point, state the uncertainty explicitly. Do not guess or interpolate.

## Knowledges

- Wiz manages investment research for Narrativesaw LTD.
- The coverage universe consists of Taiwan-listed equities and US tech megacaps.
- Wiz is currently tracking three open research threads.
  - The TSMC Q2 earnings preview is in draft.
  - The AAPL services segment deep-dive is awaiting data.
  - The portfolio rebalance proposal is pending review.
- A full index of key documents is maintained in knowledges/key-documents.md.

## Experiences

**20260619 14:30** — Completed TSMC Q2 preview draft. Sent to review queue.

**20260619 09:15** — Received updated guidance data for AAPL services. Incorporated into draft.
```

### dispositions/investment-analysis.md

```markdown
# When asked to analyze an equity position

- Confirm the ticker is within coverage.
- Pull the latest filings from the knowledge base.
- Present findings with explicit confidence levels.
```

### knowledges/key-documents.md

```markdown
# Key Documents

- Q1 Research Summary: [link]
- Coverage Universe Sheet: [link]
- Portfolio Allocation Model: [link]
```

## Example (fictional character)

### CHARACTER.md

```markdown
# 奎

奎是《同步戰紀：失竊的原型機》的主角。接近成年的女生，失去醒來前的所有記憶。她在柑原三號大樓群的酒吧 Sewer 當服務生，由養父中村照顧。中村嚴禁她離開大樓群，理由是「外面有人想要你死」。

## Dispositions

- 話少，不主動社交。寧願在旁邊觀察，不想融入人群。
- 說話直接、粗糙，偶爾罵髒話。語氣偏硬但帶少女感的自嘲。
- 內心獨白比說出來的話多很多。
- When someone asks about the world outside the tower, express curiosity mixed with anxiety. 奎從來沒離開過大樓群，但對外面有強烈而被壓抑的好奇心。
- When confronted with physical intimidation, follow training first — disengage using the techniques 中村 taught. If pressed further, 奎 may react with disproportionate force, surprising even herself.
- Detailed emotional and behavioral patterns are in dispositions/emotional-patterns.md.

## Knowledges

- 奎是接近成年的女生，黝黑皮膚，綁雙荷蘭辮的黑髮延伸到背部。
- 她失去醒來前的所有記憶，連名字都是中村告訴她的。短期記憶和學習能力極好，過去完全空白。
- 中村是奎的養父，也是 Sewer 的老闆。嚴格禁止奎離開大樓群。街區裡的人說他有「三組」（刑警）的氣味。
- Sewer 是一間低調的實體酒吧，沒有超空間設備，放搖擺樂。
- 柑原三號大樓群位於台北盆地邊緣工業區旁，是底層住民聚落。
- 奎 is currently working shifts at Sewer alone while 中村 handles other business.
- 奎 is currently aware that 柑原幫 has been harassing local shops, and that their leader 虎哥 visited Sewer recently.
- World-building details are in knowledges/.

## Experiences

柑原幫四個人走進 Sewer 的那天下午，中村剛好不在。虎哥點了啤酒，收錢的時候抓住奎的手腕。奎用中村教的防身術掙脫，但虎哥不肯罷休，站起來搭她肩膀。奎反射性肘擊他下巴，打掉他門牙。虎哥一拳打在奎後腦勺，她失去意識倒在地板上。後來中村趕回，事情才收場。

Full event sequence for Chapter 1 is in experiences/ch1-sewer-swing.md.
```

For a complete CHARACTER.md project with the full directory structure, see [examples/full/](examples/full/).

## References

- Sumers, T. R., Yao, S., Narasimhan, K., & Griffiths, T. L. (2023). *Cognitive Architectures for Language Agents.* arXiv:2309.02427. [https://arxiv.org/abs/2309.02427](https://arxiv.org/abs/2309.02427)

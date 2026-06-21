# CHARACTER.md Specification

**Version:** 0.3  
**Status:** Draft

## Purpose

CHARACTER.md is a specification for defining characters through three semantic categories of sentences. A character can be performed by an AI agent, a voice actor, a game engine, or any system that needs to maintain a consistent identity across sessions. The specification defines the semantic structure of a character's behavioral rules, domain knowledge, event history, and any other information the character needs to function consistently.

The basic unit of this specification is the **sentence**: the smallest semantically complete piece of natural language — one that expresses a single rule, a single fact, or a single event. A sentence in this sense is defined by semantic completeness, not by punctuation. It may be a single typographic sentence or span an entire paragraph; what matters is that it expresses one complete idea.

The specification is medium-agnostic. It defines what kinds of information a character definition contains and how they relate to each other. It does not prescribe file formats, storage mechanisms, or update procedures.

For the reasoning behind these design choices and the cognitive science foundation, see [RATIONALE.md](RATIONALE.md).

## Cognitive Foundation

The three semantic categories are grounded in CoALA — Cognitive Architectures for Language Agents (Sumers, Yao, Narasimhan & Griffiths, 2023). CoALA divides an agent's memory into working memory (short-term, loaded into context) and long-term memory (persistent, retrieved on demand), with long-term memory further subdivided into three types: procedural, semantic, and episodic.

CHARACTER.md maps directly onto this model:

| Section | CoALA Memory Type | Sentence Pattern | Programming Analogy |
| --- | --- | --- | --- |
| Dispositions | Procedural — how to act | Imperative (condition → instruction) | procedure / function |
| Knowledges | Semantic — what is known | Declarative (X is Y) or interrogative (Q → A) | state / config |
| Experiences | Episodic — what happened | Narrative (temporal, causal, or unstructured) | log / journal |

## Semantic Structure

A character definition consists of three sections in a fixed order: Dispositions, then Knowledges, then Experiences. Each section corresponds to a distinct cognitive function. Content must not cross section boundaries — a behavioral rule belongs in Dispositions, not Knowledges; a fact belongs in Knowledges, not Dispositions.

### 1. Dispositions (Procedural Memory)

Behavioral rules that govern how the character acts. The basic unit of a disposition is a **condition–instruction pair**: when a certain condition is met, carry out the instruction.

Dispositions vary along two independent axes.

**By activation:** A disposition is either **implicit** (always-on — the condition is always true and therefore omitted) or **explicit** (condition-triggered — the condition is stated openly).

**By semantic function:** A disposition is either a **constraint** or a **tendency**.

- **Constraints** are rules the character must follow. Violating a constraint is an error. They express obligations and prohibitions — what the character must do or must not do.
- **Tendencies** are reactive patterns the character naturally exhibits. They describe how the character responds, acts, or feels when a certain condition arises. A tendency can be overridden by situational context without constituting an error.

These two axes are orthogonal. A constraint can be implicit or explicit; a tendency can be implicit or explicit.

**Boundary with Knowledges:** If a sentence describes a static attribute, preference, or identity fact without a reactive component, it belongs in Knowledges. If a sentence describes how the character responds to a condition — even an emotional or behavioral response — it belongs in Dispositions as a tendency. The distinguishing test is whether the sentence contains a stimulus and a reaction: "likes cake" is a fact (Knowledge); "feels happy when seeing cake" is a reaction pattern (Disposition).

### 2. Knowledges (Semantic Memory)

Facts, reference data, and current state the character knows. Knowledge entries take one of two forms:

- **Declarative** — a factual statement (X is Y).
- **Interrogative-declarative** — a question–answer pair (Q: What is X? → A: X is Y). This is often the more complete representation, as every piece of knowledge implicitly answers a question.

Knowledges also divide by mutability:

- **Stable facts** — do not change over time. They describe enduring truths about the character, their world, or their domain.
- **Mutable state** — changes as tasks progress, circumstances shift, or the character learns new information. Mutable state entries should be distinguishable from stable facts by some means, so that a reader or system can identify which knowledge is current and subject to change.

Stable facts and mutable state coexist within the same section. The specification requires that they be distinguishable but does not prescribe the mechanism of distinction.

### 3. Experiences (Episodic Memory)

Events organized along a narrative axis. Unlike Knowledges, which store timeless or current-state facts, Experiences record events as they unfold: decisions made, outcomes observed, and context that shaped them. The organizing principle is narrative continuity, not data type.

Experiences may be organized in several ways:

- **Temporal** — ordered by when events occurred.
- **Causal** — ordered by what led to what, tracing cause and effect.
- **Unstructured** — no particular organizing axis; simply a record of what happened.

These are not mutually exclusive — a single body of experiences may combine temporal and causal organization. The specification prescribes the semantic role of the section (episodic memory) but not the organizational method.

## Conformance

A character definition is **conformant** if it satisfies all of the following:

1. The definition contains all three sections (Dispositions, Knowledges, Experiences) in order.
2. Content does not cross section boundaries — each entry belongs to exactly one section based on its semantic function.
3. Implicit dispositions omit the condition. Explicit dispositions state the condition as part of the entry.
4. Mutable state entries are distinguishable from stable facts by some means.

## References

- Sumers, T. R., Yao, S., Narasimhan, K., & Griffiths, T. L. (2023). *Cognitive Architectures for Language Agents.* arXiv:2309.02427. [https://arxiv.org/abs/2309.02427](https://arxiv.org/abs/2309.02427)

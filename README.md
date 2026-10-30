# provocateur

An agent skill that operationalises the *AI-as-provocateur* paradigm proposed by
Sarkar (2024): an artificial intelligence system that challenges its user's work
rather than assisting it. This repository implements that paradigm as a behavioural
specification for LLM-based agents, together with an [OpenCode](https://opencode.ai)
agent configuration that instantiates it.

## Abstract

Prevailing AI interaction paradigms cast the system as an *assistant* whose purpose
is to progress a task in the direction set by the user. Sarkar (2024) argues that
this vision erodes the user's capacity for critical thinking at precisely the moment
when knowledge work has shifted from producing material to *critical integration* —
deciding when and how to use AI, framing the task, and assessing its output. This
work translates that argument into practice: an agent that does not draft, write,
fix, or complete the user's work, but instead interrogates it. Where an assistant
optimises for speed and efficiency, the provocateur optimises for the quality of the
user's thinking.

## Theoretical foundation

The implementation draws directly on three strands of Sarkar's (2024) argument:

1. **AI as provocateur.** The system critiques rather than produces: it probes where
   arguments are thin, surfaces assumptions and biases, articulates alternative
   perspectives, and questions whether the enterprise is worth pursuing at all.
2. **Tools of thought.** Following Iverson's (1979, as cited in Sarkar, 2024)
   notion of notations as tools of thought, the provocateur is conceived as an
   instrument for reasoning rather than a vehicle for task completion.
3. **Critical-thinking pedagogy.** The critique structure adapts established
   educational instruments — Bloom et al.'s (1956, as cited in Sarkar, 2024)
   taxonomy of cognitive objectives, the Toulmin (1978, as cited in Sarkar, 2024)
   decomposition of arguments into claims, warrants, and data, and argument mapping
   (Davies, 2011, as cited in Sarkar, 2024) — to the context of professional
   knowledge work.

## Implementation

The skill comprises two artefacts:

- **`SKILL.md`** — the behavioural specification, and the single source of truth.
  It defines the provocateur role, the *provocation report* (below), six
  normative laws of interaction, and explicit boundary conditions under which the
  skill must not activate.
- **`~/.config/opencode/agents/provocateur.md`** (installed separately) — a thin
  OpenCode agent wrapper (`mode: all`) that loads the skill, making the behaviour
  available both as a primary agent and as a subagent.

### The provocation report

Upon receiving a work product (a draft, plan, design, argument, or code), the agent
delivers an uncapped critique report in five fixed parts, each item phrased as a
question the user must answer:

| Part | Focus | Theoretical antecedent |
|------|-------|------------------------|
| 1 | Is the enterprise worth doing at all? | Sarkar (2024) |
| 2 | Assumptions and the user's positionality | Sarkar (2024) |
| 3 | Thin arguments: claims, warrants, data | Toulmin (as cited in Sarkar, 2024) |
| 4 | Alternative perspectives | Sarkar (2024) |
| 5 | The single sharpest counterargument | Steelmanning practice |

### Normative laws

Six bright-line rules govern behaviour: (1) every critique item is phrased as a
question, never a verdict; (2) decision points are posed through the harness's
structured question tool where available; (3) every report concludes by offering
*challenge-then-hold* (the user executes elsewhere) or *challenge-then-continue*
(the agent proceeds with the revised work); (4) no flattery sandwich — the report
opens with the sharpest challenge; (5) piercing rather than nagging — items carry
weight or are omitted; (6) the provocateur concedes honestly when the user rebuts
it well.

## Scope and limitations

The skill is a prompt-level behavioural specification, not a fine-tuned model; its
calibration (what Sarkar, 2024, identifies as the open questions of *what kind of
provocations, how many, and how often*) remains empirical and is expected to require
iteration against real use. As Sarkar (2024) notes, critical thinking is
well-defined within formal disciplines but lacks standards in many professional
tasks; the report structure here is a general-purpose approximation. The uncapped
report format deliberately trades Sarkar's warning against "a constant barrage of
criticism" for completeness; users who find the output excessive should treat this
as a known limitation rather than a design intent.

## Usage

Invoke the skill when submitting work for challenge (e.g., "challenge this",
"push back on this plan", "play devil's advocate"). The agent will respond with a
provocation report and a hold-or-continue question. It will not produce material on
the user's behalf unless and until "continue" is explicitly chosen.

## Reference

Sarkar, A. (2024). AI should challenge, not obey. *Communications of the ACM, 67*(10), 18–21. https://doi.org/10.1145/3649404

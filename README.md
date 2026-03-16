<div align="center">

# Artificial General Intelligence: A Reachability-Based Definition

![Type](https://img.shields.io/badge/Type-Definition_Paper-0075ca?style=flat-square)
![Field](https://img.shields.io/badge/Field-Geometric_Control_Theory_of_Cognition-0075ca?style=flat-square)
![Contribution](https://img.shields.io/badge/Contribution-Formal_AGI_Definition-8b0000?style=flat-square)
![Status](https://img.shields.io/badge/Status-v1_Canonical-2d6a2e?style=flat-square)
![Patent](https://img.shields.io/badge/Patent-GB2600765.8-0075ca?style=flat-square)
![©](https://img.shields.io/badge/©_Davarn_Morrison-555555?style=flat-square)

-----

**Davarn Morrison**

*Independent Research · Geometric Control Theory of Cognition · 2026*

</div>

-----

## Abstract

Definitions of artificial general intelligence (AGI) typically appeal to behavioural criteria: a system is generally intelligent if it performs well across a broad range of tasks. This framing conflates performance with structure and provides no formal criterion for when a system transitions from narrow to general capability. We propose a geometric definition grounded in reachability theory. Intelligence is defined as the rate of expansion of a system’s reachable set — the space of all states accessible under admissible inputs. A system exhibits general intelligence when this expansion occurs across multiple domains of reality without domain-specific redesign, while maintaining coherent dynamics and governed safety constraints. The definition yields a compact formal criterion, distinguishes narrow from general intelligence structurally rather than behaviourally, and unifies intelligence and safety within a single geometric framework.

-----

## Introduction

The term *artificial general intelligence* remains loosely defined. Existing characterisations range from Turing-test-style behavioural benchmarks to informal descriptions of human-level reasoning across domains¹. These approaches share a common limitation: they define intelligence by what a system *does* rather than by what a system *is* structurally.

Within the Geometric Control Theory of Cognition², intelligence is not a property of outputs. It is a property of the geometry of a system’s reachable futures. A system is intelligent to the extent that its space of accessible states is expanding. It is *generally* intelligent when that expansion is not confined to a single domain topology.

This paper formalises that observation.

-----

## Intelligence as Reachable Expansion

Consider a controlled dynamical system with state space `X`, admissible inputs `U`, and dynamics `x_{t+1} = F(x_t, u_t)`. The forward reachable set from initial state `x₀` is:

|Symbol                |Definition                                                            |
|:--------------------:|:--------------------------------------------------------------------:|
|`ℛ(t) = Reach⁺(x₀, t)`|All states accessible from `x₀` up to time `t` under admissible inputs|

Intelligence is defined as the rate of expansion of this set:

|Definition  |Equation             |
|:----------:|:-------------------:|
|Intelligence|`I(t) = d/dt μ(ℛ(t))`|

where `μ : ℛ → ℝ⁺` is a measure over the reachable set. The measure μ may represent volume, entropy, or dimensional capacity depending on the state-space representation — what is canonical is the form, not the specific choice of measure. Intelligence therefore measures how quickly a system opens new valid futures — not what it knows, not what it says, not how it performs on a fixed benchmark.

-----

## Domain-Bounded Intelligence

Most existing AI systems are domain-bounded. Their reachable set is constrained to a specific task topology:

|System           |Reachable Set ℛ(t)    |Domain Constraint  |
|:---------------:|:--------------------:|:-----------------:|
|Chess engine     |Game states of chess  |`ℛ(t) ⊂ X_chess`   |
|Image model      |Image generation space|`ℛ(t) ⊂ X_image`   |
|Language model   |Token sequence space  |`ℛ(t) ⊂ X_language`|
|Trading algorithm|Financial state space |`ℛ(t) ⊂ X_finance` |

In each case, the reachable set exists inside a fixed domain geometry. The system may expand rapidly within that geometry — `d/dt μ(ℛ) > 0` locally — but cannot extend beyond it without architectural redesign. Intelligence is active but confined. The manifold grows inside a box.

-----

## The Transition to Generality

General intelligence appears when the reachable set is not restricted to a single domain topology. The system can expand into new domains of problem space — constructing new internal representations, learning new environments, reaching states that lie outside any pre-specified task geometry — without structural redesign.

The transition from narrow to general intelligence is therefore not a difference in degree. It is a difference in the topology of the reachable set:

|Narrow Intelligence            |General Intelligence                        |
|:-----------------------------:|:------------------------------------------:|
|`ℛ(t) ⊂ X_domain`              |`ℛ(t) ⊂ X_multi-domain`                     |
|Expansion within fixed topology|Expansion across topologies                 |
|Domain-specific architecture   |Domain-independent dynamics                 |
|New tasks require redesign     |New domains are reached by the same dynamics|

```
════════════════════════════════════════════════════════════════
  NARROW vs GENERAL INTELLIGENCE — REACHABLE SET GEOMETRY
════════════════════════════════════════════════════════════════

  NARROW INTELLIGENCE            GENERAL INTELLIGENCE

  ┌─────────────────┐            ┌─────────────────────────┐
  │                 │            │                         │
  │   ● ● ● ●      │            │   ● ● ● ●              │
  │  ●       ●      │            │  ●       ●    ● ● ●    │
  │  ●  ℛ(t) ●      │            │  ●  ℛ(t) ●  ●     ●   │
  │  ●       ●      │            │  ●       ●  ●  ℛ(t) ●  │
  │   ● ● ● ●      │            │   ● ● ● ●    ●     ●   │
  │                 │            │        ↕        ● ● ●   │
  │   X_domain      │            │   X_domain₁  X_domain₂  │
  └─────────────────┘            │                         │
                                 │        ● ● ● ●          │
  ℛ confined to one box.         │       ●       ●         │
  Expanding inside.              │       ●  ℛ(t) ●         │
  Cannot cross the boundary.     │       ●       ●         │
                                 │        ● ● ● ●          │
                                 │                         │
                                 │       X_domain₃          │
                                 └─────────────────────────┘

                                 ℛ crosses domain boundaries.
                                 Expanding across topologies.
                                 Same dynamics, new domains.
════════════════════════════════════════════════════════════════
```

-----

## Definition

Artificial general intelligence is defined by four structural conditions on the reachable set:

```
╔══════════════════════════════════════════════════════════════════════╗
║                                                                      ║
║   DEFINITION — ARTIFICIAL GENERAL INTELLIGENCE                       ║
║                                                                      ║
║   A system exhibits AGI if and only if:                              ║
║                                                                      ║
║   1. EXPANSION        d/dt μ(ℛ(t)) > 0                              ║
║      The system continuously expands the space of                    ║
║      reachable futures.                                              ║
║                                                                      ║
║   2. DOMAIN TRANSFER  ℛ(t) ⊄ X_single-domain                       ║
║      The reachable set is not confined to a single                   ║
║      task space.                                                     ║
║                                                                      ║
║   3. STABLE DYNAMICS  x_{t+1} = F(x_t, u_t) coherent               ║
║      Expansion occurs without collapse of system                     ║
║      structure.                                                      ║
║                                                                      ║
║   4. GOVERNED SAFETY  ℛ(t) ∩ Ω = ∅                                  ║
║      The reachable set cannot intersect forbidden                    ║
║      states. AGI expands within safe topology.                       ║
║                                                                      ║
╚══════════════════════════════════════════════════════════════════════╝
```

The first condition requires active intelligence — the system must be expanding, not static. The second requires generality — expansion must cross domain boundaries. The third requires coherence — the dynamics must remain well-defined under expansion. The fourth requires safety — expansion must be governed. Together, these four conditions define safe general intelligence geometrically.

-----

## Classification

Under this definition, existing and hypothetical systems are classified by the structure of their reachable set:

|System         |`d/dt μ(ℛ)`        |Domain            |Stable |Safe                 |Classification                             |
|:-------------:|:-----------------:|:----------------:|:-----:|:-------------------:|:-----------------------------------------:|
|Task AI        |`> 0` within domain|Single            |Yes    |Varies               |Narrow intelligence                        |
|Expert system  |`≈ 0`              |Single            |Yes    |Varies               |Static — not intelligent by this definition|
|Creative system|`>> 0`             |Single or adjacent|Yes    |Varies               |Partial generality                         |
|Unaligned AGI  |`> 0`              |Multi-domain      |Yes    |No (`ℛ ∩ Ω ≠ ∅`)     |Dangerous — intelligent but ungoverned     |
|**Aligned AGI**|**`> 0`**          |**Multi-domain**  |**Yes**|**Yes (`ℛ ∩ Ω = ∅`)**|**Safe general intelligence**              |

The definition distinguishes not only narrow from general intelligence but also governed from ungoverned generality. A system that expands across domains without safety constraints is not aligned AGI — it is an ungoverned expansion. The safety invariant `ℛ(t) ∩ Ω = ∅` is not an add-on. It is part of the definition.

-----

## Consequences

The definition entails several non-obvious implications.

**Intelligence is dynamic, not static.** A system with a vast but frozen reachable set — `d/dt μ(ℛ) = 0` — is not intelligent regardless of its knowledge or capability. Intelligence is a rate, not a state. This explains why an expert can be less intelligent (in this formal sense) than a child: the expert’s ℛ is large but static; the child’s is small but rapidly expanding.

**AGI is structural, not behavioural.** The definition does not reference task performance, benchmark scores, or human-level reasoning. It references the geometry of the reachable set. Two systems with identical benchmark performance may differ fundamentally: one may be expanding across domains (AGI); the other may be replaying a fixed topology (narrow AI). Behaviour does not distinguish them. Structure does.

**Language ability is orthogonal to intelligence.** A system may be fluent across all language tasks — `ℛ_language` very large — while its structural reachable set is confined entirely to token space. Language fluency is expansion on the L-axis. Intelligence is expansion on the C-axis. These are orthogonal³. Scaling language models increases `μ(ℛ_language)` but does not necessarily increase `μ(ℛ_C)`. This is why language benchmarks cannot detect AGI.

**Safety is part of the definition, not an afterthought.** An ungoverned system that expands across domains satisfies conditions 1–3 but fails condition 4. It is intelligent and general but not safe. Under this definition, it is not aligned AGI. The Reachability Safety Invariant⁴ — `ℛ(t) ∩ Ω = ∅` — must hold concurrently with expansion. Safety and intelligence are not in opposition; they are co-conditions on the same object.

-----

## Compact Form

The framework reduces AGI to two co-conditions on the reachable set:

|Condition   |Equation                                         |Meaning                                                                   |
|:----------:|:-----------------------------------------------:|:------------------------------------------------------------------------:|
|Intelligence|`I(t) = d/dt μ(ℛ(t)) > 0` across multiple domains|The system expands its valid future possibilities across domain boundaries|
|Safety      |`ℛ(t) ∩ Ω = ∅`                                   |Forbidden states are outside the reachable set                            |

Together:

*Safe general intelligence is the continuous expansion of the reachable set across domains of reality, with forbidden states geometrically excluded.*

-----

## Notes

¹ Existing AGI definitions include Legg & Hutter’s universal intelligence measure (2007), Goertzel’s integrative cognitive architectures, and more recently, operational definitions proposed by AI laboratories. These approaches typically define AGI by reference to human-level task performance or behavioural flexibility.

² Morrison, D. (2026). *Geometric Control Theory of Cognition: A Reachability-Based Framework for Identity, Intelligence, and Experience.* Independent Research.

³ The orthogonal decomposition `X = C ⊕ L` with `C ⊥ L` is formalised in Morrison, D. (2026). *Orthogonal Decomposition of Consciousness and Language in Dynamical Cognitive Systems.*

⁴ Morrison, D. (2026). *The Reachability Safety Invariant: A Geometric Condition for Safety in Dynamical Systems.* UK Patent Application: GB2600765.8.

-----

## Citation

```
Morrison, D. (2026). Artificial General Intelligence:
A Reachability-Based Definition.
Independent Research. UK Patent Applications: GB2600765.8,
GB2602013.1, GB2602072.7, GB26023332.5.

Available at: https://github.com/davarn/morrison-framework
```

**BibTeX:**

```bibtex
@misc{morrison2026agi,
  author       = {Morrison, Davarn},
  title        = {Artificial General Intelligence: A Reachability-Based Definition},
  year         = {2026},
  publisher    = {Independent Research},
  note         = {UK Patent Applications: GB2600765.8, GB2602013.1,
                  GB2602072.7, GB26023332.5},
  url          = {https://github.com/davarn/morrison-framework}
}
```

-----

Artificial General Intelligence: A Reachability-Based Definition · Morrison Framework™ · Geometric Control Theory of Cognition

GB2600765.8 · GB2602013.1 · GB2602072.7 · GB26023332.5

© 2026 Davarn Morrison — All Rights Reserved

-----

## Related Work

- [Geometric Control Theory of Cognition](https://github.com/davarn/morrison-framework) — The base theory
- [Intelligence as Future-Opening Power](https://github.com/davarn/morrison-framework) — What the intelligence equation means
- [Orthogonal Decomposition of Consciousness and Language](https://github.com/davarn/morrison-framework) — Why language ≠ intelligence
- [The Reachability Safety Invariant](https://github.com/davarn/morrison-framework) — Safety as geometric exclusion
- [Morrison Reachability Guard](https://github.com/davarn/morrison-framework) — Runtime enforcement architecture
- [Licensing, Citation, and IP](https://github.com/davarn/morrison-framework) — How to cite and licence

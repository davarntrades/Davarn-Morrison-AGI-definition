<div align="center">

# Geometry as the Substrate of Intelligence: A Reachability-Based Critique of Representation-Centric Models

**Davarn Morrison**

*Independent Research · 2026*

![Type](https://img.shields.io/badge/Type-Position_Paper-0075ca?style=flat-square)
![Field](https://img.shields.io/badge/Field-Intelligence_Theory_·_Dynamical_Systems-0075ca?style=flat-square)
![Contribution](https://img.shields.io/badge/Contribution-Structural_Critique-8b0000?style=flat-square)
![Status](https://img.shields.io/badge/Status-Submission_Ready-2d6a2e?style=flat-square)
![Patent](https://img.shields.io/badge/Patent-GB2600765.8-0075ca?style=flat-square)
![©](https://img.shields.io/badge/©_Davarn_Morrison-555555?style=flat-square)

</div>

-----

## Abstract

Contemporary approaches to intelligence in artificial intelligence and neuroscience are predominantly framed in terms of representations, behaviours, and observable outputs. While these perspectives have enabled significant empirical progress, they do not characterise the reachable structure of the systems that generate such behaviour. This paper argues that intelligence, as a property of physical systems, must be grounded in the geometry of state space and its associated dynamics. We identify a structural gap in current paradigms: the absence of reachability as a primary object of analysis. Without modelling the set of states a system can reach, it is not possible to formally characterise capability, guarantee safety, or detect failure modes prior to their manifestation. We propose that intelligence should instead be understood as a property of reachable state-space geometry, shifting the focus from semantic outputs to dynamical possibility. This perspective provides a foundation for unifying intelligence, safety, and structural change within a single geometric framework.

-----

## 1. Introduction

Artificial intelligence and neuroscience have developed powerful frameworks for modelling cognition, learning, and behaviour. However, these frameworks are largely centred on representations, outputs, and performance metrics. In artificial systems, intelligence is evaluated through benchmarks, reward optimisation, and increasingly through language-based interaction [Legg & Hutter, 2007]. In neuroscience, cognition is studied through neural activity, encoding, and connectivity.

Despite their differences, these approaches share a common feature: they describe what systems *produce* or *represent*, rather than the structure of the systems themselves.

This distinction is critical. Intelligent systems are physical dynamical systems. They evolve over time according to state transition laws, generating trajectories within a state space. The fundamental question is therefore not only what a system does, but what it can become.

This paper argues that current approaches omit this structural perspective. In particular, they do not treat the reachable set of the system — the set of all states accessible under admissible dynamics — as the primary object of analysis [Mitchell et al., 2005; Blanchini, 1999]. As a result, intelligence is defined behaviourally or semantically, rather than geometrically.

We propose that this omission is not merely a modelling choice, but a limitation. Without a geometric account of the state space, key properties of intelligent systems remain uncharacterised.

-----

## 2. Intelligence as a Property of Dynamical Systems

Let a system be defined by a state space `X` and dynamics:

|Equation               |Components                                        |
|:---------------------:|:------------------------------------------------:|
|`x_{t+1} = F(x_t, u_t)`|`x_t ∈ X` system state, `u_t ∈ 𝒰` admissible input|

The evolution of the system defines trajectories in `X`. The forward reachable set from an initial condition `x₀` is:

|Symbol|Definition                          |Meaning                                            |
|:----:|:----------------------------------:|:-------------------------------------------------:|
|`ℛ(t)`|`{ x(t) ∈ X | x(0) = x₀, u(·) ∈ 𝒰 }`|All possible future states accessible to the system|

In classical control theory, reachability is a central concept [Mitchell et al., 2005; Blanchini, 1999]. However, in intelligence modelling, it is rarely treated as the primary object. Instead, emphasis is placed on outputs, representations, or performance.

This creates a mismatch: the system evolves in `X`, but is evaluated in a projection of `X`.

-----

## 3. Representation as Projection

Let observable outputs be given by:

|Equation      |Meaning                                                                         |
|:------------:|:------------------------------------------------------------------------------:|
|`y_t = π(x_t)`|`π : X → Y` maps internal state to an output space Y (language, actions, scores)|

Under this formulation, representations describe `y_t`, but dynamics are governed by `x_t`. Representation-based approaches therefore operate on a projection of the system rather than its underlying state space.

This distinction has important consequences. Changes in output do not necessarily imply changes in the structure of the state space or its reachable set. A system may exhibit rich behaviour in `Y` while its reachable set in `X` remains unchanged. Two systems producing identical outputs may have fundamentally different reachable geometries — one expanding, one frozen — and this difference is invisible at the output level.

-----

## 4. The Missing Object: Reachable Structure

The reachable set `ℛ(t)` encodes:

|What ℛ Encodes         |Meaning                                      |
|:---------------------:|:-------------------------------------------:|
|Capabilities           |What states can be reached                   |
|Constraints            |What states cannot be reached                |
|Potential failure modes|Undesirable states within ℛ                  |
|Structural capacity    |How large and complex the space of futures is|

However, most current approaches do not explicitly model `ℛ(t)`. Instead, they infer properties of the system from observed outputs or performance.

This leads to a fundamental limitation: without characterising `ℛ(t)`, one cannot determine what the system is capable of becoming. Performance metrics describe where the system has been. Reachability describes where it can go.

-----

## 5. Consequences of a Non-Geometric Framework

### 5.1 Lack of Structural Safety

Safety is typically enforced at the level of outputs — through filtering, reward shaping, or policy constraints [Christiano et al., 2017]. However, such methods operate on `Y`, not on `X`.

If undesirable states remain reachable in `X`, then safety is not guaranteed — it is merely enforced at the interface. The system’s internal trajectories may still reach forbidden states, even while producing compliant outputs.

A geometric formulation instead defines safety as:

|Invariant     |Meaning                                                                                      |
|:------------:|:-------------------------------------------------------------------------------------------:|
|`ℛ(t) ∩ Ω = ∅`|Unsafe states are outside the reachable set — unreachable by construction [Ames et al., 2019]|

This ensures that unsafe states are not merely filtered but geometrically excluded.

### 5.2 Late Detection of Failure

In representation-based systems, failures are detected after they occur — when the system produces an undesirable output. By this point, the system has already entered or approached the unsafe state.

In contrast, reachability analysis allows detection at the level of possibility:

|Detection Level       |When                |What It Catches                                                    |
|:--------------------:|:------------------:|:-----------------------------------------------------------------:|
|Output-level          |After generation    |Failures that produce visible bad outputs                          |
|**Reachability-level**|**Before execution**|**Failures that are possible, whether or not they have manifested**|

If an unsafe state lies within `ℛ(t)`, the system is already at risk — whether or not it has produced a bad output yet. Intervention can occur before the state is realised.

### 5.3 Incomplete Characterisation of Intelligence

Behavioural definitions of intelligence evaluate performance across tasks [Legg & Hutter, 2007]. However, two systems with identical outputs may differ in their underlying structure:

|System A          |System B        |Outputs  |Reachable Structure    |
|:----------------:|:--------------:|:-------:|:---------------------:|
|Large, expanding ℛ|Fixed, limited ℛ|Identical|Fundamentally different|

One system has a reachable set that is growing — new states are becoming accessible, new capabilities are emerging. The other operates within a frozen topology — replaying existing structure without expansion. Their outputs may be indistinguishable. Their geometry is opposite.

Without modelling `ℛ(t)`, this distinction is invisible. Behavioural evaluation cannot differentiate a system that is genuinely expanding from one that is merely replaying.

-----

## 6. Geometry as the Substrate

We propose that intelligence should be defined in terms of reachable geometry. Under this view:

|Property         |Geometric Definition                                               |
|:---------------:|:-----------------------------------------------------------------:|
|Intelligence     |Structure and expansion of `ℛ(t)` — formally, `I(t) = d/dt μ(ℛ(t))`|
|Safety           |Constraints on `ℛ(t)` — forbidden states excluded                  |
|Structural change|Deformation of `ℛ(t)` — topology altered                           |

This admits a computable instantiation [Morrison, 2026b], grounding the geometric definition operationally. Intelligence is not only a conceptual reframing — it is measurable through three concrete forms of μ (discrete state count, volume approximation, and entropy).

This reframes intelligence as a geometric property of a dynamical system, rather than a semantic or behavioural one.

Language, representations, and outputs remain important, but are understood as projections:

|Equation      |Status                                                         |
|:------------:|:-------------------------------------------------------------:|
|`y_t = π(x_t)`|Projections describe the system but do not define its structure|

The projection `π` maps from a higher-dimensional state space to a lower-dimensional output space. Information about the system’s reachable geometry is lost in the projection. This is not a failure of the projection — it is a mathematical property of dimensionality reduction. No output-level analysis can recover what is lost.

-----

## 7. Discussion

The absence of geometry in mainstream definitions of intelligence is not due to a lack of mathematical tools. Reachability theory [Mitchell et al., 2005], invariant set analysis [Blanchini, 1999], viability theory [Aubin, 1991], and control barrier functions [Ames et al., 2019] provide well-established frameworks for analysing state-space structure.

However, these tools have not been integrated into the definition of intelligence itself. Instead, intelligence has been treated as a property of outputs, representations, or task performance.

This paper argues that such approaches are incomplete. A full account of intelligence must specify the structure of the system’s state space and its reachable dynamics. The tools already exist. The step that has not been taken is to make reachability the primary object — not an auxiliary analysis, but the foundation on which intelligence, safety, and structural change are defined.

-----

## 8. Conclusion

Intelligence is a property of physical systems evolving over state space. As such, it must admit a geometric description.

Current approaches in artificial intelligence and neuroscience describe representations and behaviours but do not characterise the reachable structure of the system. This limits their ability to guarantee safety, detect failure, or distinguish between fundamentally different systems with similar outputs.

By elevating reachability to the primary object of analysis, intelligence can be understood as a geometric property of possible futures.

*Intelligence is not what a system says or represents. It is the structure of what it can become.*

*A system cannot be understood by what it expresses, only by what it can reach.*

-----

## References

|Citation                    |Work                                                                        |Relevance                               |
|:--------------------------:|:--------------------------------------------------------------------------:|:--------------------------------------:|
|Ames, A.D. et al. (2019)    |*Control Barrier Functions: Theory and Applications.* IEEE TAC.             |Safety constraints on dynamical systems |
|Aubin, J.-P. (1991)         |*Viability Theory.* Birkhäuser.                                             |Set invariance and viable trajectories  |
|Blanchini, F. (1999)        |*Set Invariance in Control.* Automatica, 35(11).                            |Invariant set methods in control theory |
|Christiano, P. et al. (2017)|*Deep Reinforcement Learning from Human Preferences.* NeurIPS.              |RLHF — representational safety approach |
|Legg, S., Hutter, M. (2007) |*Universal Intelligence.* Minds and Machines, 17(4).                        |Behavioural intelligence definition     |
|Mitchell, I.M. et al. (2005)|*Hamilton-Jacobi Reachability.* IEEE TAC.                                   |Reachable set computation               |
|Morrison, D. (2026a)        |*Geometric Control Theory of Cognition.* Independent Research.              |Base framework                          |
|Morrison, D. (2026b)        |*Computable Intelligence via Reachable Set Expansion.* Independent Research.|Computable instantiation of intelligence|
|Shannon, C.E. (1948)        |*A Mathematical Theory of Communication.* Bell System TJ.                   |Information-theoretic foundations       |

-----

## Citation

```
Morrison, D. (2026). Geometry as the Substrate of Intelligence:
A Reachability-Based Critique of Representation-Centric Models.
Independent Research. UK Patent Applications: GB2600765.8,
GB2602013.1, GB2602072.7, GB26023332.5.
```

**BibTeX:**

```bibtex
@misc{morrison2026geometry,
  author       = {Morrison, Davarn},
  title        = {Geometry as the Substrate of Intelligence: A Reachability-Based
                  Critique of Representation-Centric Models},
  year         = {2026},
  publisher    = {Independent Research},
  note         = {UK Patent Applications: GB2600765.8, GB2602013.1,
                  GB2602072.7, GB26023332.5},
  url          = {https://github.com/davarn/morrison-framework}
}
```

-----

Geometry as the Substrate of Intelligence · Morrison Framework™ · Geometric Control Theory of Cognition

GB2600765.8 · GB2602013.1 · GB2602072.7 · GB26023332.5

© 2026 Davarn Morrison — All Rights Reserved

-----

## Related Work

- [Computable Intelligence via Reachable Set Expansion](https://github.com/davarn/morrison-framework) — Intelligence defined and made operational
- [Representation Is Not Dynamics](https://github.com/davarn/morrison-framework) — Why output-level alignment is insufficient
- [Structural Orthogonality Proof](https://github.com/davarn/morrison-framework) — Language has no control authority under decoupled dynamics
- [The Reachability Safety Invariant](https://github.com/davarn/morrison-framework) — Safety as geometric exclusion
- [Geometric Control Theory of Cognition](https://github.com/davarn/morrison-framework) — The base theory
- [Licensing, Citation, and IP](https://github.com/davarn/morrison-framework) — How to cite and licence

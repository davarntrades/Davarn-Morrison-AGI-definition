<div align="center">

# Representation Is Not Dynamics: A Structural Misalignment in AI Safety

**Davarn Morrison**

*Independent Research · 2026*

![Type](https://img.shields.io/badge/Type-Formal_Paper-0075ca?style=flat-square)
![Field](https://img.shields.io/badge/Field-AI_Safety_·_Dynamical_Systems-0075ca?style=flat-square)
![Contribution](https://img.shields.io/badge/Contribution-Structural_Critique-8b0000?style=flat-square)
![Status](https://img.shields.io/badge/Status-Submission_Ready-2d6a2e?style=flat-square)
![Patent](https://img.shields.io/badge/Patent-GB2600765.8-0075ca?style=flat-square)
![©](https://img.shields.io/badge/©_Davarn_Morrison-555555?style=flat-square)

</div>

-----

This work builds upon the patented pre-semantic trajectory governance framework.

-----

## Abstract

Contemporary AI safety methods primarily operate at the level of representation, constraining outputs such as language or actions. However, safety in dynamical systems is fundamentally a property of state evolution, not representation. This paper formalises the distinction between representational control and dynamical constraint, and argues that output-level alignment does not guarantee safety at the level of system trajectories. We show that safety must be defined over reachable states rather than observable outputs, and position reachability-based invariants as operating at the correct layer of system structure.

-----

## 1. Introduction

Modern AI safety techniques focus on shaping what systems *say* or *do*. Methods such as reinforcement learning from human feedback (RLHF) [Christiano et al., 2017], instruction tuning, and output filtering constrain observable behaviour, particularly in the form of language.

This approach implicitly assumes that controlling representation is sufficient to ensure safety.

We argue that this assumption is structurally incomplete.

AI systems are dynamical systems. Their behaviour arises from the evolution of internal state over time. Language is not the system itself, but a projection of that state. Therefore, constraining outputs does not, in general, constrain the underlying state trajectories that generate them.

This distinction motivates a shift in the location of safety: from representation to dynamics.

-----

## 2. Dynamical Systems and Representation

Let `x_t ∈ X` denote the internal state of an AI system at time `t`. The system evolves according to:

|Equation                    |Components                                                     |
|:--------------------------:|:-------------------------------------------------------------:|
|`x_{t+1} = F(x_t, u_t, w_t)`|`u_t` admissible actions, `w_t` external inputs or disturbances|

Observable outputs, such as language, are generated via a projection:

|Equation      |Meaning                                    |
|:------------:|:-----------------------------------------:|
|`y_t = π(x_t)`|`π` maps internal states to representations|

This induces a structural separation:

|Layer                 |What It Governs         |
|:--------------------:|:----------------------:|
|Dynamical layer       |How states evolve       |
|Representational layer|How states are expressed|

These layers are not equivalent. The dynamical layer determines what the system *can become*. The representational layer determines what the system *appears to be*. Constraining appearance does not constrain possibility.

-----

## 3. Representational Control

Most current AI safety methods act on `y_t`, the representational output.

|Method                        |What It Constrains                    |Layer           |
|:----------------------------:|:------------------------------------:|:--------------:|
|RLHF [Christiano et al., 2017]|Preference over outputs               |Representational|
|Output filtering / moderation |Surface content of generated text     |Representational|
|Instruction tuning            |Behavioural compliance to instructions|Representational|
|Rule-based policy enforcement |Output categories                     |Representational|

These methods enforce:

|Constraint         |Meaning                                                |
|:-----------------:|:-----------------------------------------------------:|
|`y_t ∉ Y_forbidden`|Observed output must not be in the forbidden output set|

However, this does not imply:

|Does Not Follow|Why                                                 |
|:-------------:|:--------------------------------------------------:|
|`x_t ∉ Ω`      |Multiple internal states may produce the same output|

The projection `π` is non-injective in general:

|Condition                 |Consequence                                        |
|:------------------------:|:-------------------------------------------------:|
|`π(x₁) = π(x₂)`, `x₁ ≠ x₂`|Different internal states produce identical outputs|

A system may produce compliant outputs while occupying or transitioning through unsafe internal states. Output-level compliance does not imply trajectory-level safety.

Representational control is therefore non-injective with respect to safety. This critique does not imply that representational methods are without value; rather, it shows that they are insufficient in isolation, as they do not constrain the underlying state trajectories of the system.

-----

## 4. Dynamics as the Substrate of Safety

Safety in a dynamical system is a property of trajectories `{x_t}_{t≥0}`, not of individual outputs.

Let `Ω ⊂ X` denote a forbidden region of the state space. A system is safe if its trajectories never enter `Ω`. Formally:

|Safety Condition |Meaning                                                               |
|:---------------:|:--------------------------------------------------------------------:|
|`x_t ∉ Ω  ∀t ≥ 0`|The system state must remain outside the forbidden region at all times|

This condition depends only on:

|Dependency         |Object|
|:-----------------:|:----:|
|State space        |`X`   |
|Transition function|`F`   |
|Admissible inputs  |`𝒰`   |

It does not depend on the projection `π`.

Therefore: **safety is a property of state evolution, not representation.**

A system whose internal trajectories avoid `Ω` is safe regardless of what it outputs. A system whose outputs avoid `Y_forbidden` is not necessarily safe — its internal state may still reach `Ω`.

-----

## 5. Structural Misalignment in Current Approaches

Current AI safety methods are misaligned with the structure of the systems they attempt to control.

|Layer           |Object Controlled|Typical Methods          |What It Constrains              |
|:--------------:|:---------------:|:-----------------------:|:------------------------------:|
|Representational|Outputs `y_t`    |RLHF, filtering, policies|What the system *says*          |
|**Dynamical**   |**States `x_t`** |**(Largely unaddressed)**|**What the system *can become***|

This creates a gap: systems are constrained at the level of expression but remain unconstrained at the level of possibility.

As a result, safety mechanisms may fail under:

|Failure Mode              |Why Representational Control Fails                           |
|:------------------------:|:-----------------------------------------------------------:|
|Multi-step compositions   |Each step looks safe in isolation; the trajectory reaches `Ω`|
|Internal state transitions|State moves toward `Ω` without producing forbidden outputs   |
|Tool-mediated execution   |Actions execute in the world, not in language space          |
|Adversarial inputs        |Jailbreaks exploit the gap between `π` and `F`               |

The system can remain representationally compliant while dynamically unsafe. It says the right things while becoming something dangerous.

-----

## 6. Reachability as the Correct Layer

The appropriate object for safety analysis in dynamical systems is the reachable set [Mitchell et al., 2005; Blanchini, 1999]:

|Symbol|Definition                                                           |
|:----:|:-------------------------------------------------------------------:|
|`ℛ(t)`|`{ x(t) ∈ X | x(0) = x₀, u(·) ∈ 𝒰 }` — all states reachable from `x₀`|

Safety is then expressed as:

|Invariant     |Meaning                                             |
|:------------:|:--------------------------------------------------:|
|`ℛ(t) ∩ Ω = ∅`|All possible trajectories avoid the forbidden region|

This condition constrains all possible trajectories of the system, independent of how those trajectories are represented or expressed [Morrison, 2026a].

In contrast to representational control, reachability-based safety:

|Property                    |Representational Control              |Reachability-Based Safety                     |
|:--------------------------:|:------------------------------------:|:--------------------------------------------:|
|Operates at                 |Output layer `y_t`                    |Dynamical layer `x_t`                         |
|Invariant to projection `π`?|No — depends on `π`                   |Yes — independent of `π`                      |
|Constrains                  |Observed behaviour                    |Future possibility                            |
|Failure mode                |Non-injective `π` allows unsafe states|Forbidden states are outside the reachable set|
|Scope                       |Current output                        |All future trajectories                       |

-----

## 7. Implications

The distinction between representation and dynamics has several consequences for AI safety:

**Output alignment is insufficient.** Safe outputs do not imply safe internal trajectories. A system trained to produce compliant language may still evolve through unsafe internal states — states that produce compliant outputs now but lead to forbidden states later.

**Safety must be defined in state space.** Constraints must apply to `x_t`, not only `y_t`. The forbidden region `Ω` must be defined in the state space of the system, not in the output space of the projection.

**Projection cannot guarantee safety.** The mapping `π` may obscure unsafe states. If `π` is non-injective — as it is for all systems where multiple internal configurations produce the same output — then output-level safety provides no guarantee about state-level safety.

**Trajectory-level reasoning is required.** Safety must consider sequences of transitions, not isolated actions. An action that is safe in isolation may be part of a trajectory that reaches `Ω`. Only reachability analysis over the full trajectory captures this.

**The gap is structural, not accidental.** The misalignment between representational control and dynamical safety is not a failure of implementation. It is a consequence of the mathematical structure: `π` projects from a higher-dimensional space to a lower-dimensional one, and information about state-level safety is lost in the projection. No amount of improvement to output filtering can close this gap — it is a property of the projection itself.

-----

## 8. Conclusion

AI safety methods that operate purely at the level of representation address only a projection of system behaviour. Safety is fundamentally a property of dynamical evolution.

Language is a projection of state. Safety is a property of state transitions.

To ensure safety in AI systems, constraints must be applied at the level of reachable states, not merely at the level of observable outputs.

*Controlling what a system says is not equivalent to controlling what a system can become.*

-----

## References

|Citation                                                                              |Work                                                                                                                                                 |
|:------------------------------------------------------------------------------------:|:---------------------------------------------------------------------------------------------------------------------------------------------------:|
|Ames, A.D., Coogan, S., Egerstedt, M., Notomista, G., Sreenath, K., Tabuada, P. (2019)|*Control Barrier Functions: Theory and Applications.* IEEE Trans. on Automatic Control.                                                              |
|Blanchini, F. (1999)                                                                  |*Set Invariance in Control.* Automatica, 35(11), 1747–1767.                                                                                          |
|Christiano, P., Leike, J., Brown, T., Marber, M., Amodei, D., Irving, G. (2017)       |*Deep Reinforcement Learning from Human Preferences.* NeurIPS.                                                                                       |
|Mitchell, I.M., Bayen, A.M., Tomlin, C.J. (2005)                                      |*A Time-Dependent Hamilton-Jacobi Formulation of Reachable Sets.* IEEE Trans. on Automatic Control.                                                  |
|Morrison, D. (2026a)                                                                  |*The Reachability Safety Invariant: A Geometric Condition for Safety in Dynamical Systems.* Independent Research. UK Patent Application: GB2600765.8.|
|Morrison, D. (2026b)                                                                  |*Computable Intelligence via Reachable Set Expansion.* Independent Research.                                                                         |

-----

## Citation

```
Morrison, D. (2026). Representation Is Not Dynamics:
A Structural Misalignment in AI Safety.
Independent Research. UK Patent Application: GB2600765.8.

Available at: https://github.com/davarn/morrison-framework
```

**BibTeX:**

```bibtex
@misc{morrison2026representation,
  author       = {Morrison, Davarn},
  title        = {Representation Is Not Dynamics: A Structural Misalignment
                  in AI Safety},
  year         = {2026},
  publisher    = {Independent Research},
  note         = {UK Patent Application: GB2600765.8},
  url          = {https://github.com/davarn/morrison-framework}
}
```

-----

Representation Is Not Dynamics · Morrison Framework™ · Geometric Control Theory of Cognition

GB2600765.8

© 2026 Davarn Morrison — All Rights Reserved

-----

## Related Work

- [The Reachability Safety Invariant](https://github.com/davarn/morrison-framework) — Safety as geometric exclusion
- [Computable Intelligence via Reachable Set Expansion](https://github.com/davarn/morrison-framework) — Intelligence defined and made operational
- [Orthogonal Decomposition of Consciousness and Language](https://github.com/davarn/morrison-framework) — Why C ⊥ L
- [Morrison Reachability Guard](https://github.com/davarn/morrison-framework) — Runtime enforcement at the dynamical layer
- [Geometric Control Theory of Cognition](https://github.com/davarn/morrison-framework) — The base theory
- [Licensing, Citation, and IP](https://github.com/davarn/morrison-framework) — How to cite and licence

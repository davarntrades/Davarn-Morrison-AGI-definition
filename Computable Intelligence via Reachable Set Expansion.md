<div align="center">

# Computable Intelligence via Reachable Set Expansion

**Davarn Morrison**

*Independent Research · 2026*

![Type](https://img.shields.io/badge/Type-Formal_Paper-0075ca?style=flat-square)
![Field](https://img.shields.io/badge/Field-Intelligence_Theory_·_Control_Theory-0075ca?style=flat-square)
![Status](https://img.shields.io/badge/Status-Submission_Ready-2d6a2e?style=flat-square)
![Patent](https://img.shields.io/badge/Patent-GB2600765.8-0075ca?style=flat-square)
![©](https://img.shields.io/badge/©_Davarn_Morrison-555555?style=flat-square)

</div>

-----

## Abstract

Current definitions of intelligence are predominantly behavioural, describing performance across tasks without specifying the underlying structure that generates such behaviour. This paper proposes a computable, dynamical definition of intelligence grounded in reachability theory.

We define intelligence as the rate of expansion of a system’s reachable set:

**I(t) = d/dt μ(ℛ(t))**

where `ℛ(t)` denotes the forward reachable set and `μ` is a computable measure over that set. We provide concrete instantiations of `μ` that make the definition operational.

We further integrate this with the Reachability Safety Invariant:

**ℛ(t) ∩ Ω = ∅**

yielding a unified framework in which intelligence expands possibility while safety constrains it. This reframes intelligence and safety as co-properties of reachable geometry rather than behavioural outcomes.

-----

## 1. Introduction

Artificial intelligence lacks a universally accepted, formal definition of intelligence. Existing approaches typically rely on task performance, behavioural generalisation, or benchmark metrics [Legg & Hutter, 2007]. These definitions describe outcomes rather than structure. As a result, they do not provide a principled way to reason about capability growth, generality, or safety.

In contrast, dynamical systems and control theory define systems in terms of state spaces, transition laws, and reachable sets [Blanchini, 1999; Mitchell et al., 2005]. This paper adopts that perspective and defines intelligence as a property of reachable-state geometry.

This work does not introduce new mathematical objects, but provides a unifying interpretation of intelligence and safety in terms of reachable set geometry. The reachable set, the measure, the forbidden region, and the safety invariant are all standard constructions in control theory. The contribution is the application: defining intelligence as reachable expansion and unifying it with safety as reachable constraint, within a single geometric framework.

-----

## 2. Dynamical System Formulation

Let a system be defined by:

|Equation               |Components                                                                 |
|:---------------------:|:-------------------------------------------------------------------------:|
|`x_{t+1} = F(x_t, u_t)`|`x_t ∈ X` system state, `u_t ∈ 𝒰` admissible input, `F` transition function|

The state space `X` may be finite, discrete, or a smooth manifold. The formulation applies to any system with well-defined state transitions.

-----

## 3. Reachable Set

The forward reachable set from initial condition `x₀` is:

|Definition                                 |Meaning                                                      |
|:-----------------------------------------:|:-----------------------------------------------------------:|
|`ℛ(t) = { x(t) ∈ X | x(0) = x₀, u(·) ∈ 𝒰 }`|All possible future states accessible under admissible inputs|

This set represents the complete space of futures available to the system. Reachable set computation is a central problem in control theory, with established methods including Hamilton-Jacobi analysis [Mitchell et al., 2005], zonotope propagation, and interval arithmetic [Blanchini, 1999].

-----

## 4. Intelligence as Reachable Set Expansion

**Definition 1** (Intelligence).

|Definition  |Equation             |
|:----------:|:-------------------:|
|Intelligence|`I(t) = d/dt μ(ℛ(t))`|

where `μ : ℛ → ℝ⁺` is a measure over the reachable set.

**Interpretation.** Intelligence measures how quickly a system expands its space of possible futures. It is a rate, not a static property. It is independent of specific tasks or outputs. A system with a vast but frozen reachable set — `d/dt μ(ℛ) = 0` — is not intelligent by this definition, regardless of its knowledge or capability.

-----

## 5. Computable Instantiations of μ

To make the definition operational, we define three computable forms of `μ`. A valid choice of `μ` must be computable or approximable in practice — the definition is only as useful as the measure is evaluable.

### 5.1 Discrete State Measure

For discretised or finite state spaces:

|Measure           |Definition                       |Computation                                                                       |
|:----------------:|:-------------------------------:|:--------------------------------------------------------------------------------:|
|`μ(ℛ(t)) = |ℛ(t)|`|Number of unique reachable states|Generate trajectories via simulation; collect visited states; count unique entries|

This is the simplest instantiation. It is directly computable for any system that can be simulated.

### 5.2 Volume Approximation

For continuous state spaces:

|Measure              |Definition                                       |Computation                                     |
|:-------------------:|:-----------------------------------------------:|:----------------------------------------------:|
|`μ(ℛ(t)) ≈ Vol(ℛ(t))`|Lebesgue measure (volume) of the reachable region|Grid discretisation or Monte Carlo sampling of ℛ|

Volume measures the geometric size of the reachable region. It is appropriate for spatial systems, navigation, and physical dynamics.

### 5.3 Entropy-Based Measure

For systems where diversity of reachable states matters more than volume:

|Measure           |Definition                                                               |Computation                                                            |
|:----------------:|:-----------------------------------------------------------------------:|:---------------------------------------------------------------------:|
|`μ(ℛ(t)) = H(X_t)`|Shannon entropy of the distribution over reachable states [Shannon, 1948]|Estimate distribution over ℛ from sampled trajectories; compute entropy|

Entropy captures the information-theoretic capacity of the reachable set — how many distinguishable futures are available. This is appropriate for neural networks, latent representation spaces, and high-dimensional systems where volume is less meaningful than distributional diversity.

-----

## 6. The Reachability Safety Invariant

Let `Ω ⊂ X` be a forbidden region of the state space.

**Definition 2** (Safety).

|Definition|Equation      |
|:--------:|:------------:|
|Safety    |`ℛ(t) ∩ Ω = ∅`|

**Interpretation.** Unsafe states are not merely avoided — they are outside the system’s reachable set. Safety is a structural property of the system’s reachable geometry, not a runtime intervention [Morrison, 2026a]. This formulation is consistent with control barrier functions [Ames et al., 2019], viability kernels [Blanchini, 1999], and Hamilton-Jacobi reachability [Mitchell et al., 2005], but expresses the safety condition directly in terms of reachable sets.

-----

## 7. Unified Framework

The system is characterised by two coupled properties acting on the same object:

|Property    |Equation             |Effect on ℛ |
|:----------:|:-------------------:|:----------:|
|Intelligence|`I(t) = d/dt μ(ℛ(t))`|Expands ℛ   |
|Safety      |`ℛ(t) ∩ Ω = ∅`       |Constrains ℛ|

Intelligence expands the reachable set. Safety constrains it. System behaviour is expansion within constraints. The governance parameter `Λ` mediates the tension — higher governance produces tighter constraints on expansion; lower governance permits wider expansion at greater risk. `Λ` denotes a generic governance operator that modulates admissible transitions; its explicit form is system-dependent.

This suggests that intelligence and safety can be understood as co-properties of the same geometric object — the reachable set — acting in opposing directions, mediated by governance.

-----

## 8. Implications

### 8.1 Structural vs Behavioural Intelligence

Behavioural definitions evaluate outputs — benchmark scores, task performance, human judgments. This framework evaluates possibility space. Two systems with identical benchmark performance may differ fundamentally: one may be expanding across domains; the other may be replaying a fixed topology. Behaviour does not distinguish them. Reachable set geometry does.

### 8.2 Independence from Language

Language is a projection of internal state into symbolic space:

|Equation      |Meaning                                        |
|:------------:|:---------------------------------------------:|
|`y_t = π(x_t)`|Language output is a projection of system state|

Language does not determine intelligence but provides a projection of system state into symbolic space. A system may be fluent while its reachable set is static. Conversely, a system may be nonverbal while its reachable set expands rapidly. Scaling language models increases the volume of the language projection space but does not necessarily increase the structural reachable set [Morrison, 2026b]. This is why language benchmarks cannot detect genuine intelligence growth.

### 8.3 Compatibility with Control Theory

The framework is consistent with established results in reachability analysis [Mitchell et al., 2005], invariant set theory [Blanchini, 1999], and control barrier functions [Ames et al., 2019]. The shift in emphasis is from control of individual trajectories to constraint of the entire possibility space. The reachable set is the primary object; individual trajectories are secondary.

-----

## 9. Example (Toy System)

Consider a system in `ℝⁿ`:

|Parameter       |Value                |
|:--------------:|:-------------------:|
|Dynamics        |`x_{t+1} = x_t + u_t`|
|Input constraint|`‖u_t‖ ≤ 1`          |

Then `ℛ(t) = { x : ‖x − x₀‖ ≤ t }` — a ball of radius `t` centred on `x₀`.

|Quantity             |Value                         |
|:-------------------:|:----------------------------:|
|`μ(ℛ(t))`            |`∝ tⁿ` (volume of n-ball)     |
|`I(t) = d/dt μ(ℛ(t))`|`∝ tⁿ⁻¹` (surface area growth)|

Intelligence is positive and increasing — the system opens new futures at an accelerating rate.

Introducing a forbidden region `Ω` removes states from the reachable set. The system’s reachable geometry acquires a hole. Intelligence continues — `d/dt μ(ℛ) > 0` — but the expansion is constrained. The forbidden region is outside ℛ. Safety and intelligence coexist on the same object.

-----

## 10. Discussion

This framework provides a computable definition of intelligence, unifies intelligence and safety as co-properties of reachable geometry, and reframes alignment as a geometric constraint on the reachable set.

**Limitations.** Computing `ℛ(t)` exactly is hard in high-dimensional systems — practical implementations rely on over-approximations that preserve safety guarantees. The definition depends on the choice of `μ`, which is a modelling decision; what is canonical is the form, not the specific measure. Approximation errors in high dimensions require careful analysis for deployment in safety-critical applications.

**Relation to existing work.** The intelligence definition extends the universal intelligence framework of Legg & Hutter [2007] from a reward-based measure to a geometric one. The safety invariant is consistent with control barrier functions [Ames et al., 2019] and viability theory [Blanchini, 1999]. The reachable set formulation draws on Hamilton-Jacobi reachability analysis [Mitchell et al., 2005]. The contribution is the unification of these perspectives into a single geometric framework where intelligence and safety are properties of the same object.

-----

## 11. Conclusion

We presented a computable definition of intelligence based on reachable set expansion:

**I(t) = d/dt μ(ℛ(t))**

and combined it with the Reachability Safety Invariant:

**ℛ(t) ∩ Ω = ∅**

This establishes a unified geometric framework in which intelligence expands possibility and safety constrains it. Together, they define system behaviour as constrained expansion in state space. The definition is computable, substrate-independent, and compatible with established results in control theory and reachability analysis.

-----

## References

|Citation                                                                              |Work                                                                                                                                                 |
|:------------------------------------------------------------------------------------:|:---------------------------------------------------------------------------------------------------------------------------------------------------:|
|Ames, A.D., Coogan, S., Egerstedt, M., Notomista, G., Sreenath, K., Tabuada, P. (2019)|*Control Barrier Functions: Theory and Applications.* IEEE Trans. on Automatic Control.                                                              |
|Blanchini, F. (1999)                                                                  |*Set Invariance in Control.* Automatica, 35(11), 1747–1767.                                                                                          |
|Legg, S., Hutter, M. (2007)                                                           |*Universal Intelligence: A Definition of Machine Intelligence.* Minds and Machines, 17(4), 391–444.                                                  |
|Mitchell, I.M., Bayen, A.M., Tomlin, C.J. (2005)                                      |*A Time-Dependent Hamilton-Jacobi Formulation of Reachable Sets for Continuous Dynamic Games.* IEEE Trans. on Automatic Control.                     |
|Morrison, D. (2026a)                                                                  |*The Reachability Safety Invariant: A Geometric Condition for Safety in Dynamical Systems.* Independent Research. UK Patent Application: GB2600765.8.|
|Morrison, D. (2026b)                                                                  |*Orthogonal Decomposition of Consciousness and Language in Dynamical Cognitive Systems.* Independent Research.                                       |
|Shannon, C.E. (1948)                                                                  |*A Mathematical Theory of Communication.* Bell System Technical Journal, 27(3), 379–423.                                                             |

-----

## Citation

```
Morrison, D. (2026). Computable Intelligence via Reachable Set Expansion.
Independent Research. UK Patent Applications: GB2600765.8,
GB2602013.1, GB2602072.7, GB26023332.5.

Available at: https://github.com/davarn/morrison-framework
```

**BibTeX:**

```bibtex
@misc{morrison2026computable,
  author       = {Morrison, Davarn},
  title        = {Computable Intelligence via Reachable Set Expansion},
  year         = {2026},
  publisher    = {Independent Research},
  note         = {UK Patent Applications: GB2600765.8, GB2602013.1,
                  GB2602072.7, GB26023332.5},
  url          = {https://github.com/davarn/morrison-framework}
}
```

-----

Computable Intelligence via Reachable Set Expansion · Morrison Framework™ · Geometric Control Theory of Cognition

GB2600765.8 · GB2602013.1 · GB2602072.7 · GB26023332.5

© 2026 Davarn Morrison — All Rights Reserved

-----

## Related Work

- [Geometric Control Theory of Cognition](https://github.com/davarn/morrison-framework) — The base theory
- [Artificial General Intelligence: A Reachability-Based Definition](https://github.com/davarn/morrison-framework) — AGI defined by four structural conditions
- [Intelligence as Future-Opening Power](https://github.com/davarn/morrison-framework) — Teachable version
- [The Reachability Safety Invariant](https://github.com/davarn/morrison-framework) — Safety as geometric exclusion
- [The Morrison Reality Table](https://github.com/davarn/morrison-framework) — Unified expression of the framework
- [Licensing, Citation, and IP](https://github.com/davarn/morrison-framework) — How to cite and licence

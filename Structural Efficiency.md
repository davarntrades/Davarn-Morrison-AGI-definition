<div align="center">

# Structural Efficiency in Intelligent Systems: Energy Reduction via Reachability-Constrained Dynamics

**Davarn Morrison**

*Independent Research · 2026*

![Type](https://img.shields.io/badge/Type-Formal_Paper-0075ca?style=flat-square)
![Field](https://img.shields.io/badge/Field-AI_Efficiency_·_Reachability_Theory-0075ca?style=flat-square)
![Contribution](https://img.shields.io/badge/Contribution-Structural_Efficiency_Principle-8b0000?style=flat-square)
![Status](https://img.shields.io/badge/Status-Submission_Ready-2d6a2e?style=flat-square)
![Patent](https://img.shields.io/badge/Patent-GB2600765.8-0075ca?style=flat-square)
![©](https://img.shields.io/badge/©_Davarn_Morrison-555555?style=flat-square)

</div>

-----

This work builds upon the patented pre-semantic trajectory governance framework.

-----

## Abstract

Modern artificial intelligence systems are computationally intensive, requiring large-scale data centres and significant energy consumption. This paper argues that a substantial portion of this cost arises from a structural inefficiency: systems explore large regions of state space that are subsequently filtered or corrected at the output level. We propose that this inefficiency is a consequence of representation-centric approaches that do not constrain the system’s reachable set. Building on a reachability-based framework for intelligence and safety [Morrison, 2026a], we show that enforcing structural constraints on the reachable state space can eliminate invalid trajectories at the level of system dynamics. This reduces redundant computation, narrows the effective search space, and decreases reliance on scale. We formalise this principle and argue that energy efficiency in intelligent systems is fundamentally linked to the geometry of reachable states. The result is a shift from post hoc filtering to pre-structuring of possibility, with direct implications for computational cost and data centre energy usage.

-----

## 1. Introduction

The rapid scaling of artificial intelligence systems has led to a corresponding increase in computational and energy demands. Large-scale models require substantial infrastructure, often operating across distributed data centres with significant electrical consumption. While advances in hardware and optimisation have improved efficiency, the dominant strategy remains scaling: increasing model size, data, and compute to achieve improved performance.

This paper argues that a significant portion of this computational cost is not intrinsic to intelligence itself, but arises from a structural inefficiency in how intelligent systems are currently designed and trained.

Contemporary systems operate primarily on representations and outputs. They generate candidate trajectories — sequences of internal states or outputs — which are then evaluated, filtered, or corrected. This process implicitly allows the system to explore a large space of possibilities, many of which are invalid or undesirable.

We propose that this approach is inefficient by construction. Instead of constraining the system at the level of outputs, constraints should be applied at the level of reachable state space [Mitchell et al., 2005; Blanchini, 1999]. By shaping the set of states the system can reach, invalid trajectories can be eliminated before they are generated.

This reframes energy efficiency as a structural property of the system’s dynamics rather than a byproduct of optimisation.

-----

## 2. Dynamical Systems and Reachability

Let a system be defined by:

|Equation               |Components                                        |
|:---------------------:|:------------------------------------------------:|
|`x_{t+1} = F(x_t, u_t)`|`x_t ∈ X` system state, `u_t ∈ 𝒰` admissible input|

The forward reachable set is:

|Symbol|Definition                          |Meaning                                                  |
|:----:|:----------------------------------:|:-------------------------------------------------------:|
|`ℛ(t)`|`{ x(t) ∈ X | x(0) = x₀, u(·) ∈ 𝒰 }`|All states the system can reach under admissible dynamics|

In traditional control theory, reachability is used to analyse system behaviour and enforce constraints [Mitchell et al., 2005; Blanchini, 1999]. In contrast, modern AI systems rarely operate directly on `ℛ(t)`, instead relying on output-level evaluation.

-----

## 3. Sources of Computational Inefficiency

### 3.1 Exploration Beyond Valid Structure

In current systems, the state space `X` is effectively unconstrained during generation. The system explores trajectories that are later rejected through reward shaping, filtering, or post-processing. This results in:

|Relationship                     |Meaning                                      |
|:-------------------------------:|:-------------------------------------------:|
|`Compute ∝ Explored trajectories`|Including those that are ultimately discarded|

The system spends energy generating possibilities it will never use. The larger the unconstrained state space, the more energy is wasted on invalid exploration.

### 3.2 Output-Level Correction

Let outputs be given by `y_t = π(x_t)`. Constraints are typically applied to `y_t`, not to `x_t` [Morrison, 2026b]. As a result:

|Problem                                  |Consequence                                                    |
|:---------------------------------------:|:-------------------------------------------------------------:|
|Invalid internal trajectories still occur|Computation is expended on states that produce no useful output|
|Correction happens after computation     |Energy has already been spent generating the invalid trajectory|

The system does the work, then throws it away. The filtering is applied after the cost has been paid.

### 3.3 Overparameterisation as Compensation

To handle unconstrained exploration, systems are scaled: larger models, more parameters, more data. This compensates for lack of structural constraint but increases computational cost.

|Strategy       |What It Does                                |What It Costs                           |
|:-------------:|:------------------------------------------:|:--------------------------------------:|
|More parameters|Covers more of the unconstrained state space|More compute, more energy, more hardware|
|More data      |Provides more examples to guide exploration |More storage, more training time        |
|More compute   |Brute-forces through invalid trajectories   |Direct energy cost                      |

Scale compensates for the absence of structural constraints. Introducing structure can reduce reliance on scale.

-----

## 4. Structural Efficiency via Reachability Constraints

We propose enforcing constraints directly on the reachable set:

|Constraint             |Equation          |Meaning                                                                  |
|:---------------------:|:----------------:|:-----------------------------------------------------------------------:|
|Reachability constraint|`ℛ(t) ⊆ S = X \ Ω`|Invalid states are not reachable — invalid trajectories are not generated|

Under this formulation, the system cannot explore invalid regions of state space because those regions are outside its reachable set. The constraint is structural, not corrective.

### 4.1 Reduction in Search Space

Instead of exploring `X`, the system operates within `ℛ(t) ⊂ X`. This reduces the effective dimensionality and volume of the search space.

|Unconstrained                |Constrained                               |
|:---------------------------:|:----------------------------------------:|
|System explores all of X     |System explores only ℛ(t) ⊆ S             |
|Many trajectories are invalid|All trajectories are valid by construction|
|Search space = X             |Search space = ℛ(t), where `μ(ℛ) ≪ μ(X)`  |

### 4.2 Elimination of Redundant Computation

Trajectories that would have been filtered are no longer generated:

|Measure            |Relationship             |
|:-----------------:|:-----------------------:|
|`Compute_effective`|`< Compute_unconstrained`|

Every trajectory the system generates under reachability constraints is valid. No computation is wasted on possibilities that will be discarded.

### 4.3 Reduced Reliance on Scale

Structural constraints reduce the need for brute-force exploration and large parameter counts:

|Without Structure                |With Structure                            |
|:-------------------------------:|:----------------------------------------:|
|Capability scales with model size|Capability scales with structured dynamics|
|More parameters = more coverage  |Constrained ℛ = only valid coverage       |
|Energy cost grows with scale     |Energy cost grows with ℛ, not X           |

Capability becomes a function of structured dynamics rather than model size.

### 4.4 Reduction of Branching Factor

The deeper mechanism is the reduction of the trajectory branching factor. In an unconstrained system, the number of possible trajectories grows exponentially:

|Unconstrained   |Formula                 |Meaning                                   |
|:--------------:|:----------------------:|:----------------------------------------:|
|Trajectory count|`|trajectories| ~ 𝒪(bᵗ)`|`b` = branching factor, `t` = time horizon|

Constraining `ℛ` reduces `b` — fewer valid next-states are available at each step. This directly reduces the exponential scaling of compute:

|System                  |Branching Factor            |Trajectory Growth                           |
|:----------------------:|:--------------------------:|:------------------------------------------:|
|Unconstrained           |`b` (full action space)     |`𝒪(bᵗ)` — exponential in horizon            |
|Reachability-constrained|`b' < b` (only safe actions)|`𝒪(b'ᵗ)` — exponential but with smaller base|

Since compute scales exponentially with the branching factor, even a modest reduction in `b` produces large savings over multi-step trajectories. This connects reachability constraints directly to computational scaling.

For example, in language generation with beam search of width `b` and horizon `t`, compute scales as `𝒪(bᵗ)`. Constraining admissible actions — excluding token sequences that lead to forbidden states — reduces the effective branching factor to `b' < b`, yielding `𝒪(b'ᵗ)`. Since the exponent is `t`, even a small reduction in `b` produces exponential savings. A system with `b = 10` and `t = 20` explores `10²⁰` trajectories; reducing to `b' = 7` yields `7²⁰` — a reduction of over three orders of magnitude.

-----

## 5. Energy as a Function of Reachable Geometry

We define computational cost as proportional to the volume or complexity of explored states:

|Definition          |Equation                   |
|:------------------:|:-------------------------:|
|Computational energy|`E_compute ∝ μ(ℛ_explored)`|

Here `μ` denotes an abstract measure of explored state-space volume, which may correspond to trajectory count, entropy of visited states, or computational steps required to sample trajectories [Shannon, 1948]. In sequence models, `μ(ℛ_explored)` can be instantiated as the number of sampled trajectories or token branches evaluated during generation, making `E_compute` proportional to effective search width × depth. The specific instantiation of `μ` is system-dependent; what is canonical is the proportionality between energy and explored volume.

|System Type             |Explored vs Valid            |Energy                                             |
|:----------------------:|:---------------------------:|:-------------------------------------------------:|
|Unconstrained           |`μ(ℛ_explored) >> μ(ℛ_valid)`|High — exploring far beyond what is useful         |
|Reachability-constrained|`ℛ_explored = ℛ_valid`       |Minimal — exploring only what is structurally valid|

The difference between `μ(ℛ_explored)` and `μ(ℛ_valid)` is the structural waste. In current systems, this waste is substantial. Reachability constraints eliminate it.

```
╔══════════════════════════════════════════════════════════════════════╗
║                                                                      ║
║   E_compute ∝ μ(ℛ_explored)                                        ║
║                                                                      ║
║   Unconstrained:    μ(ℛ_explored) >> μ(ℛ_valid)                    ║
║   Constrained:      ℛ_explored = ℛ_valid                           ║
║                                                                      ║
║   The cost of intelligence is proportional to the                    ║
║   unnecessary possibility space a system explores.                   ║
║   Reducing that space reduces computation.                           ║
║                                                                      ║
╚══════════════════════════════════════════════════════════════════════╝
```

-----

## 6. Implications for Data Centre Energy Usage

The reduction in explored state space has direct implications across the AI pipeline:

### 6.1 Training

|Current                                             |Under Reachability Constraints         |
|:--------------------------------------------------:|:-------------------------------------:|
|System explores invalid trajectories during training|Invalid trajectories never generated   |
|Reward shaping corrects after exploration           |Constraints prevent invalid exploration|
|Training cost scales with X                         |Training cost scales with ℛ            |

### 6.2 Inference

|Current                                    |Under Reachability Constraints              |
|:-----------------------------------------:|:------------------------------------------:|
|Generated outputs are filtered post hoc    |All generated outputs are structurally valid|
|Multiple candidates generated and discarded|Fewer candidates needed — all are valid     |
|Filtering layers add compute overhead      |No filtering layer required                 |

### 6.3 Infrastructure

|Current                                           |Under Reachability Constraints                  |
|:------------------------------------------------:|:----------------------------------------------:|
|High compute demand from unconstrained exploration|Lower compute from constrained dynamics         |
|Energy consumption scales with model size         |Energy consumption scales with ℛ geometry       |
|Data centre capacity limits scalability           |Structural efficiency extends effective capacity|

-----

## 7. Discussion

The proposed framework does not eliminate the computational challenges of modelling high-dimensional systems. Computing or approximating `ℛ(t)` remains non-trivial [Mitchell et al., 2005]. However, it shifts the focus from filtering outputs to structuring dynamics.

This aligns with control-theoretic principles [Blanchini, 1999; Ames et al., 2019], where constraints are embedded in system design rather than applied post hoc. The overhead of computing ℛ must be weighed against the savings from eliminating invalid exploration — the efficiency gain holds when constraint evaluation or reachable set approximation is computationally cheaper than unconstrained exploration. This is typically the case in systems where constraints are low-dimensional or decomposable relative to the full state space. In many practical settings — particularly inference and tool-use in AI agents — the constraints are simple enough that the overhead is far smaller than the savings.

The principle does not require exact reachability computation. Conservative over-approximations of ℛ preserve the structural efficiency guarantee: if the over-approximation excludes invalid regions, the true reachable set does too.

-----

## 8. Conclusion

A significant portion of the computational cost in modern AI systems arises from exploring invalid regions of state space. By enforcing constraints at the level of reachable dynamics, these regions can be eliminated.

This reframes energy efficiency as a structural property:

*The cost of intelligence is proportional to the unnecessary possibility space a system explores. Reducing that space reduces computation.*

The path to efficient AI is not more compute. It is less unnecessary possibility.

-----

## References

|Citation                    |Work                                                           |Relevance                                         |
|:--------------------------:|:-------------------------------------------------------------:|:------------------------------------------------:|
|Ames, A.D. et al. (2019)    |*Control Barrier Functions: Theory and Applications.* IEEE TAC.|Embedding safety constraints in system design     |
|Blanchini, F. (1999)        |*Set Invariance in Control.* Automatica, 35(11).               |Invariant set methods — structural constraint     |
|Mitchell, I.M. et al. (2005)|*Hamilton-Jacobi Reachability.* IEEE TAC.                      |Reachable set computation                         |
|Morrison, D. (2026a)        |*Geometric Control Theory of Cognition.* Independent Research. |Base framework — reachability as generating object|
|Morrison, D. (2026b)        |*Representation Is Not Dynamics.* Independent Research.        |Output-level vs dynamics-level constraints        |
|Shannon, C.E. (1948)        |*A Mathematical Theory of Communication.* Bell System TJ.      |Information-theoretic foundations                 |

-----

## Citation

```
Morrison, D. (2026). Structural Efficiency in Intelligent Systems:
Energy Reduction via Reachability-Constrained Dynamics.
Independent Research. UK Patent Applications: GB2600765.8,
GB2602013.1, GB2602072.7, GB26023332.5.
```

**BibTeX:**

```bibtex
@misc{morrison2026efficiency,
  author       = {Morrison, Davarn},
  title        = {Structural Efficiency in Intelligent Systems:
                  Energy Reduction via Reachability-Constrained Dynamics},
  year         = {2026},
  publisher    = {Independent Research},
  note         = {UK Patent Applications: GB2600765.8, GB2602013.1,
                  GB2602072.7, GB26023332.5},
  url          = {https://github.com/davarn/morrison-framework}
}
```

-----

Structural Efficiency in Intelligent Systems · Morrison Framework™ · Geometric Control Theory of Cognition

GB2600765.8 · GB2602013.1 · GB2602072.7 · GB26023332.5

© 2026 Davarn Morrison — All Rights Reserved

-----

## Related Work

- [Geometry as the Substrate of Intelligence](https://github.com/davarn/morrison-framework) — Why reachability is the correct object
- [Representation Is Not Dynamics](https://github.com/davarn/morrison-framework) — Why output-level approaches are structurally insufficient
- [Computable Intelligence via Reachable Set Expansion](https://github.com/davarn/morrison-framework) — Intelligence defined operationally
- [The Reachability Safety Invariant](https://github.com/davarn/morrison-framework) — Safety as geometric exclusion
- [Morrison Reachability Guard](https://github.com/davarn/morrison-framework) — Runtime enforcement architecture
- [Licensing, Citation, and IP](https://github.com/davarn/morrison-framework) — How to cite and licence

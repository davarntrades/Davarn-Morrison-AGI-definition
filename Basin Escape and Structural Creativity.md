<div align="center">

# Basin Escape and Structural Creativity: A Reachability-Based Account of Learning Dynamics in Neural Systems

**Davarn Morrison**

*Independent Research · 2026*

![Type](https://img.shields.io/badge/Type-Formal_Paper-0075ca?style=flat-square)
![Field](https://img.shields.io/badge/Field-Learning_Theory_·_Dynamical_Systems-0075ca?style=flat-square)
![Contribution](https://img.shields.io/badge/Contribution-Basin_Escape_Condition-8b0000?style=flat-square)
![Status](https://img.shields.io/badge/Status-Submission_Ready-2d6a2e?style=flat-square)
![Patent](https://img.shields.io/badge/Patent-GB2600765.8-0075ca?style=flat-square)
![©](https://img.shields.io/badge/©_Davarn_Morrison-555555?style=flat-square)

</div>

-----

## Abstract

Current accounts of learning in neural systems focus on optimisation within a fixed representation space, typically characterised by loss minimisation and performance improvement. This paper proposes a structural alternative: learning is understood as evolution of the system’s reachable set in state space. We formalise the distinction between expertise and creativity using the rate of reachable set expansion, and introduce the Basin Escape Condition, which characterises when a system transitions beyond local optimisation into structural innovation. We show that standard neural training dynamics primarily operate within fixed basins of attraction, while genuine creativity corresponds to expansion of the reachable set beyond these basins, often accompanied by topological change. This provides a geometric and dynamical definition of learning that distinguishes optimisation from structural growth.

-----

## 1. Introduction

Learning in artificial neural networks is typically described as optimisation: parameters are adjusted to minimise a loss function, improving performance on a task. While effective, this view describes how systems improve locally, but not what changes structurally as learning progresses.

In particular, standard formulations do not distinguish between improving performance within an existing behavioural regime and expanding into entirely new regimes of capability. This paper argues that this distinction is fundamental. A system that only optimises within a fixed region of state space differs qualitatively from one that expands the set of states it can reach.

We propose a reachability-based framework [Morrison, 2026a; Mitchell et al., 2005] in which learning is defined over the system’s reachable set `ℛ(t)`, enabling a formal separation between expertise and creativity.

-----

## 2. Dynamical Formulation of Neural Systems

Let a neural system be described by a state:

|Symbol                |Components                                       |Meaning                                |
|:--------------------:|:-----------------------------------------------:|:-------------------------------------:|
|`x_t = (h_t, θ_t) ∈ X`|`h_t` = activation state, `θ_t` = parameter state|Full configuration of the neural system|

The system evolves under:

|Equation               |Components                                                     |
|:---------------------:|:-------------------------------------------------------------:|
|`x_{t+1} = F(x_t, u_t)`|`u_t` includes inputs, gradients, or environmental interactions|

The forward reachable set is:

|Symbol|Definition                          |Meaning                                                    |
|:----:|:----------------------------------:|:---------------------------------------------------------:|
|`ℛ(t)`|`{ x(t) ∈ X | x(0) = x₀, u(·) ∈ 𝒰 }`|All possible configurations the system can attain over time|

This set represents the complete space of states accessible to the neural system — not just where it has been, but everything it could become under admissible dynamics.

-----

## 3. Intelligence as Reachable Set Expansion

We adopt the definition [Morrison, 2026b]:

|Definition  |Equation             |
|:----------:|:-------------------:|
|Intelligence|`I(t) = d/dt μ(ℛ(t))`|

where `μ` is a measure over the reachable set. The measure `μ` may be instantiated as cardinality, volume, entropy, or trajectory count depending on the system; the definition is invariant to this choice. This yields two distinct regimes:

|Regime        |Condition          |What Is Happening                                                            |
|:------------:|:-----------------:|:---------------------------------------------------------------------------:|
|**Expertise** |`d/dt μ(ℛ(t)) ≈ 0` |System refines trajectories within an existing region — ℛ is large but static|
|**Creativity**|`d/dt μ(ℛ(t)) >> 0`|System expands into new regions of state space — ℛ is growing                |

Expert systems perform with precision inside known topology. Creative systems build new topology. The outputs may look equally impressive. The geometry is opposite.

-----

## 4. Basins of Attraction and Learning

Let `B ⊂ X` denote a basin of attraction or locally invariant region of the state space.

In standard neural training:

|Property           |Description                                  |
|:-----------------:|:-------------------------------------------:|
|Locally contractive|Gradient descent moves toward local minima   |
|Contained          |Updates improve performance without leaving B|
|Structurally static|Reachable structure remains within the basin |

Thus, most training dynamics satisfy:

|Condition |Meaning                                                           |
|:--------:|:----------------------------------------------------------------:|
|`ℛ(t) ⊆ B`|The reachable set remains inside the basin over extended intervals|

We treat `B` as a locally invariant or metastable region of state space under the system dynamics, not necessarily a strict attractor in the classical sense. What matters is that trajectories starting in B remain in B under the training dynamics over the relevant timescale.

This corresponds to expertise: high performance within a fixed structural region. The system gets better at navigating the basin. It does not leave it.

-----

## 5. Basin Escape Condition

We now formalise the transition from optimisation to structural change.

**Theorem (Basin Escape Condition).** Let `ℛ(t) ⊂ X` be the reachable set and `B ⊂ X` a basin such that: (i) `ℛ(t₁) ⊆ B`, and (ii) local dynamics within B preserve the homotopy type of `ℛ(t)`.

A sufficient condition for basin escape is:

|Condition |Equation              |Meaning                               |
|:--------:|:--------------------:|:------------------------------------:|
|Set escape|`∃t₂ > t₁ : ℛ(t₂) ⊄ B`|Reachable set extends beyond the basin|

A stronger structural condition is:

|Condition         |Equation                          |Meaning                                                                  |
|:----------------:|:--------------------------------:|:-----------------------------------------------------------------------:|
|Topological escape|`∃k ≥ 0 : H_k(ℛ(t₁)) ≇ H_k(ℛ(t₂))`|Homology changed — reachable set has undergone structural reconfiguration|

**Proof sketch.** If all admissible trajectories remain within B, reachable evolution is confined to local deformations that preserve topological structure. Optimisation within B cannot produce qualitative structural change — the homotopy type is preserved by assumption (ii).

If `ℛ(t₂) ⊄ B`, trajectories exist outside the original basin, implying escape. The system has accessed states that were not reachable from within B.

If homology changes — `H_k(ℛ(t₁)) ≇ H_k(ℛ(t₂))` — the reachable sets are not topologically equivalent. No continuous deformation connects them. This implies structural reconfiguration beyond local optimisation: new holes formed, old connections broke, or the connectivity of the reachable space changed.

Topological change provides a sufficient condition for structural transformation; metric deformation without homology change may still correspond to weaker forms of expansion. Homology is the strongest detectable signal — finer-grained detection may use persistent homology or Riemannian metrics on ℛ. ∎

-----

## 6. Creativity as Structural Expansion

We define creativity by two joint conditions:

|Condition             |Equation                          |What It Captures                                        |
|:--------------------:|:--------------------------------:|:------------------------------------------------------:|
|Quantitative expansion|`d/dt μ(ℛ(t)) > 0`                |More reachable states — the space of possibilities grows|
|Qualitative change    |`∃k ≥ 0 : H_k(ℛ(t₁)) ≇ H_k(ℛ(t₂))`|New structure — the topology of possibilities changes   |

Creativity is therefore not output novelty. It is not producing something unusual. It is expansion of reachable geometry accompanied by structural reconfiguration.

|Apparent Creativity                  |Geometric Reality                                          |
|:-----------------------------------:|:---------------------------------------------------------:|
|Novel output within existing topology|Not creative — replay of known structure in new combination|
|New output from expanded ℛ           |Creative — new states became reachable                     |
|New output with changed H_k          |Deeply creative — the topology itself restructured         |

A system that produces surprising outputs by recombining known states is not creative by this definition — its ℛ did not change. A system whose reachable set expands into previously inaccessible states is creative — even if its outputs look unremarkable at the surface.

-----

## 7. Neural Interpretation

|Regime     |Neural Interpretation                                    |`d/dt μ(ℛ)`                        |Topology          |
|:---------:|:-------------------------------------------------------:|:---------------------------------:|:----------------:|
|Expertise  |Gradient descent within a fixed basin                    |`≈ 0`                              |Preserved         |
|Fine-tuning|Local adjustment of trajectories within B                |`≈ 0`                              |Preserved         |
|Creativity |Escape from parameter-function basin                     |`>> 0`                             |Changed           |
|Innovation |Simultaneous optimisation within B and expansion beyond B|Mixed — `≈ 0` in B, `>> 0` adjacent|New basins forming|

Standard training procedures primarily produce expertise. The loss decreases. The parameters settle. The reachable set stabilises within a basin. Intelligence by the equation: `d/dt μ(ℛ) ≈ 0`. The system is performing, not growing.

Creativity requires mechanisms that alter the reachable structure itself — perturbations large enough to escape the basin, architectural changes that open new regions of state space, or environmental interactions that force the system beyond its current topology.

Innovation is the rarest case: the system maintains mastery within an existing basin while simultaneously expanding into adjacent basins. This requires both stability (`≈ 0` locally) and expansion (`>> 0` globally) at the same time — which is why innovation is hard.

-----

## 8. Discussion

This framework introduces a structural distinction absent in conventional learning theory:

|Conventional View                 |Reachability View                               |
|:--------------------------------:|:----------------------------------------------:|
|Performance improvement = learning|Performance improvement ≠ structural growth     |
|Optimisation = capability gain    |Optimisation within B = expertise, not expansion|
|Novel output = creativity         |Novel output ≠ expanded ℛ                       |
|Scaling = more capability         |Scaling ≠ guaranteed expansion of reachable sets|

It also identifies specific limitations of current systems:

|Limitation                                                  |Geometric Description                                 |
|:----------------------------------------------------------:|:----------------------------------------------------:|
|Models may appear intelligent while confined to fixed basins|`d/dt μ(ℛ) ≈ 0` despite high output quality           |
|Behavioural evaluation cannot detect structural stagnation  |Performance metrics operate on Y, not on ℛ            |
|Scaling alone does not guarantee expansion                  |Larger models may have larger B, not larger ℛ beyond B|
|Fine-tuning does not produce creativity                     |Local adjustment preserves basin structure            |

The framework reframes learning as a geometric process rather than a purely statistical one. The question is not “how well does the system perform?” but “what can the system reach that it couldn’t reach before?”

-----

## 9. Conclusion

We presented a reachability-based account of learning dynamics in neural systems. By defining intelligence as expansion of the reachable set and introducing the Basin Escape Condition, we distinguish between optimisation within a fixed structure and genuine structural growth.

|Regime    |Definition                                               |
|:--------:|:-------------------------------------------------------:|
|Expertise |Optimisation within a basin — `ℛ(t) ⊆ B`, `d/dt μ(ℛ) ≈ 0`|
|Creativity|Expansion beyond the basin — `ℛ(t) ⊄ B`, `H_k` changed   |

Learning is not only about improving trajectories. It is about changing what trajectories are possible.

This framework implies that optimisation, performance, and representation are insufficient to characterise learning. A system may improve indefinitely while remaining confined to a fixed reachable structure. Structural learning occurs only when the reachable set expands or reconfigures.

The defining question is not how well a system performs, but whether it can reach states it could not reach before.

*Creativity is not better movement within a basin. It is the creation of new basins in reachable space.*

-----

## References

|Citation                    |Work                                                                        |Relevance                                 |
|:--------------------------:|:--------------------------------------------------------------------------:|:----------------------------------------:|
|Blanchini, F. (1999)        |*Set Invariance in Control.* Automatica, 35(11).                            |Basin invariance and structural constraint|
|Legg, S., Hutter, M. (2007) |*Universal Intelligence.* Minds and Machines, 17(4).                        |Behavioural intelligence baseline         |
|Mitchell, I.M. et al. (2005)|*Hamilton-Jacobi Reachability.* IEEE TAC.                                   |Reachable set computation                 |
|Morrison, D. (2026a)        |*Geometric Control Theory of Cognition.* Independent Research.              |Base framework — ℛ as generating object   |
|Morrison, D. (2026b)        |*Computable Intelligence via Reachable Set Expansion.* Independent Research.|Intelligence as `d/dt μ(ℛ)`               |
|Shannon, C.E. (1948)        |*A Mathematical Theory of Communication.* Bell System TJ.                   |Information-theoretic foundations         |

-----

## Citation

```
Morrison, D. (2026). Basin Escape and Structural Creativity:
A Reachability-Based Account of Learning Dynamics in Neural Systems.
Independent Research. UK Patent Applications: GB2600765.8,
GB2602013.1, GB2602072.7, GB26023332.5.
```

**BibTeX:**

```bibtex
@misc{morrison2026basin,
  author       = {Morrison, Davarn},
  title        = {Basin Escape and Structural Creativity: A Reachability-Based
                  Account of Learning Dynamics in Neural Systems},
  year         = {2026},
  publisher    = {Independent Research},
  note         = {UK Patent Applications: GB2600765.8, GB2602013.1,
                  GB2602072.7, GB26023332.5},
  url          = {https://github.com/davarn/morrison-framework}
}
```

-----

Basin Escape and Structural Creativity · Morrison Framework™ · Geometric Control Theory of Cognition

GB2600765.8 · GB2602013.1 · GB2602072.7 · GB26023332.5

© 2026 Davarn Morrison — All Rights Reserved

-----

## Related Work

- [Computable Intelligence via Reachable Set Expansion](https://github.com/davarn/morrison-framework) — Intelligence defined operationally
- [Intelligence as Future-Opening Power](https://github.com/davarn/morrison-framework) — Teachable version of the intelligence equation
- [Geometry as the Substrate of Intelligence](https://github.com/davarn/morrison-framework) — Why reachability is the correct object
- [Truth and Reality in the Morrison Framework](https://github.com/davarn/morrison-framework) — Topological change as truth condition
- [Geometric Control Theory of Cognition](https://github.com/davarn/morrison-framework) — The base theory
- [Licensing, Citation, and IP](https://github.com/davarn/morrison-framework) — How to cite and licence

<div align="center">

# Why Reachability, Not Information: A Structural Comparison of State-Space Frameworks for Intelligence

**Davarn Morrison**

*Independent Research · 2026*

![Type](https://img.shields.io/badge/Type-Comparison_Paper-0075ca?style=flat-square)
![Field](https://img.shields.io/badge/Field-Intelligence_Theory_·_Control_Theory-0075ca?style=flat-square)
![Contribution](https://img.shields.io/badge/Contribution-Minimal_Completeness_of_Reachability-8b0000?style=flat-square)
![Status](https://img.shields.io/badge/Status-Submission_Ready-2d6a2e?style=flat-square)
![Patent](https://img.shields.io/badge/Patent-GB2600765.8-0075ca?style=flat-square)
![©](https://img.shields.io/badge/©_Davarn_Morrison-555555?style=flat-square)

</div>

-----

## Abstract

Information-theoretic and policy-based frameworks dominate contemporary approaches to intelligence, learning, and decision-making. These frameworks characterise systems through representations, uncertainty, and mappings from states to actions. This paper argues that such approaches operate on projections of the underlying system rather than its fundamental structure. We propose that the reachable set `ℛ(t)`, defined as the set of all states a system can attain under admissible dynamics, is the minimal complete object for analysing intelligence. We provide a formal comparison between reachability, entropy, information, and policy space, demonstrating that only reachability directly encodes possibility. We further argue that intelligence, safety, and structural change are properties of reachable state-space geometry, not of representations or distributions.

-----

## 1. Introduction

Modern theories of intelligence are largely grounded in information theory [Shannon, 1948], statistical learning, and decision theory [Legg & Hutter, 2007]. These frameworks describe systems in terms of information content, uncertainty and entropy, and policies mapping states to actions.

While successful in many applications, these approaches share a limitation: they describe how systems represent or act, not what systems can become.

This distinction is structural. Intelligent systems are dynamical systems evolving over state space [Blanchini, 1999; Mitchell et al., 2005]. The fundamental object is therefore not representation or uncertainty, but reachability — the set of all states accessible under system dynamics.

We formalise this distinction and argue that reachability provides a strictly more fundamental description.

-----

## 2. Reachability as the Object of Possibility

Let a system evolve as:

|Equation               |Components                                        |
|:---------------------:|:------------------------------------------------:|
|`x_{t+1} = F(x_t, u_t)`|`x_t ∈ X` system state, `u_t ∈ 𝒰` admissible input|

The forward reachable set is:

|Symbol|Definition                          |Meaning                                                                                |
|:----:|:----------------------------------:|:-------------------------------------------------------------------------------------:|
|`ℛ(t)`|`{ x(t) ∈ X | x(0) = x₀, u(·) ∈ 𝒰 }`|All attainable states, all admissible trajectories, all constraints imposed by dynamics|

`ℛ(t)` is the space of possible futures of the system. It encodes what the system can become — not what it knows, not what it outputs, not what it predicts.

-----

## 3. Structural Comparison of Frameworks

### 3.1 Comparison Table

|Framework       |Object Defined               |Operates On      |Encodes Possibility?|Invertible to ℛ(t)?|Structural Status  |
|:--------------:|:---------------------------:|:---------------:|:------------------:|:-----------------:|:-----------------:|
|**Reachability**|`ℛ(t) ⊂ X`                   |State space      |**Yes**             |—                  |**Fundamental**    |
|Information     |`I(X;Y)`, mutual information |Representations  |No                  |No                 |Projection         |
|Entropy         |`H(X)`, distributional spread|Probability space|No                  |No                 |Projection         |
|Policy Space    |`π: X → 𝒰`                   |Action mappings  |Indirect            |No                 |Control description|
|Value Functions |`V(x)`, expected return      |Scalar fields    |No                  |No                 |Evaluation layer   |

### 3.2 Key Observation

All alternative frameworks operate on functions of the system and require additional structure (distributions, rewards, encodings). Only reachability operates directly on the system’s state space and requires no representational assumptions.

-----

## 4. Why Not Information Theory?

Information theory [Shannon, 1948] provides a powerful framework for analysing communication, encoding, and uncertainty. However, it is not a theory of dynamical possibility.

### 4.1 Information Does Not Encode Reachability

Let `I(X;Y)` denote mutual information between variables. Two systems may satisfy identical informational structure while having different sets of possible futures:

|Condition                            |Consequence                   |
|:-----------------------------------:|:----------------------------:|
|`I(X;Y)` identical across two systems|Does not imply `ℛ₁(t) = ℛ₂(t)`|

Information does not determine reachability. Systems with the same information content can have fundamentally different spaces of possibility.

### 4.2 Entropy Does Not Encode Structure

Entropy measures distributional spread: `H(X) = −Σ p(x) log p(x)`. However, entropy can increase within a fixed basin — no new states become reachable:

|Condition  |Consequence               |
|:---------:|:------------------------:|
|`ΔH(X) > 0`|Does not imply `Δℛ(t) ≠ 0`|

Entropy captures distribution, not structure. A system can become more uncertain about which state it occupies without any change in which states are reachable.

### 4.3 Policies Do Not Define Possibility

Policies define mappings `π: X → 𝒰`. However, multiple policies can induce identical reachable sets, and policy change does not guarantee structural change:

|Condition|Consequence                   |
|:-------:|:----------------------------:|
|`π₁ ≠ π₂`|Does not imply `ℛ₁(t) ≠ ℛ₂(t)`|

Policies describe control, not the space of attainable states. Two different policies acting on the same system may produce the same reachable set through different trajectories.

### 4.4 Information Without Control: Structural Invariance Across Domains

Information-theoretic frameworks implicitly assume that information plays a central role in guiding system behaviour. However, the presence of information does not, in general, imply any change in system dynamics or reachable structure.

We observe a consistent pattern across domains: systems may possess accurate and relevant information about desirable or undesirable outcomes, yet exhibit no corresponding change in their trajectories or reachable states.

|Domain          |Information Available      |Observed Behaviour   |Structural Effect                    |
|:--------------:|:-------------------------:|:-------------------:|:-----------------------------------:|
|Health (smoking)|Smoking causes harm        |Continued use        |`ℛ(t) ∩ Ω ≠ ∅` persists              |
|Fitness         |Exercise improves health   |Inaction             |Beneficial states remain outside ℛ(t)|
|Nutrition       |Diet affects wellbeing     |No behavioural change|ℛ(t) unchanged                       |
|Productivity    |Tasks known to be important|Procrastination      |No trajectory update                 |

In each case, the system possesses correct information, yet the reachable set remains unchanged. Formally:

|Condition                    |Consequence                                      |
|:---------------------------:|:-----------------------------------------------:|
|`I ≠ 0` (information present)|Does not imply `Δℛ(t) ≠ 0` (reachable set change)|

This demonstrates that information alone is insufficient to constrain, expand, or restructure the system’s reachable set. Information does not guarantee control over `ℛ(t)`.

**Implication.** Any framework that equates intelligence with information processing is incomplete at the structural level, as it cannot guarantee or explain changes in the space of possible trajectories. Information describes aspects of the system. It does not determine what the system can become.

The failure of information to induce structural change is not an exception but a common property of real-world systems, indicating that information operates at a descriptive rather than dynamical level.

-----

## 5. Reachability as a Minimal Complete Object

**Proposition (Structural Completeness of Reachability).** Let a dynamical system be defined over state space `X`. The reachable set `ℛ(t)` is structurally complete under the stated assumptions in the sense that:

This claim holds for deterministic or controlled dynamical systems where system evolution is fully characterised by state transitions over X.

|Property      |Statement                                                                                                                         |
|:------------:|:--------------------------------------------------------------------------------------------------------------------------------:|
|1. Behaviour  |All system behaviours are trajectories within `ℛ(t)`                                                                              |
|2. Constraints|All constraints correspond to exclusions from `ℛ(t)`                                                                              |
|3. Subsumption|Any representation, policy, or distribution is a function defined over X, and therefore restricted to `ℛ(t)` under system dynamics|

**Consequence.**

|Direction            |Holds?|Meaning                                                            |
|:-------------------:|:----:|:-----------------------------------------------------------------:|
|Framework = f(ℛ(t))  |Yes   |Every alternative framework is a function of the reachable set     |
|ℛ(t) = f⁻¹(Framework)|No    |The reachable set is not recoverable from any alternative framework|

Reachability subsumes alternative frameworks, but is not recoverable from them. Information, entropy, and policy are projections of ℛ. None of them can reconstruct ℛ from their own objects alone.

-----

## 6. Implications for Intelligence

Under this framework, all core properties are defined over the same object. The measure `μ` denotes a measure over state space (e.g., volume, entropy, or trajectory count), depending on system instantiation.

|Property    |Definition                                      |Effect on ℛ                 |
|:----------:|:----------------------------------------------:|:--------------------------:|
|Intelligence|`I(t) = d/dt μ(ℛ(t))` [Morrison, 2026b]         |Expansion of ℛ              |
|Safety      |`ℛ(t) ∩ Ω = ∅` [Morrison, 2026c]                |Constraint on ℛ             |
|Creativity  |Topological expansion of ℛ — basin escape       |Structural growth of ℛ      |
|Truth       |`∃k : H_k(ℛ(t₁)) ≇ H_k(ℛ(t₂))` [Morrison, 2026d]|Topological deformation of ℛ|

Intelligence, safety, creativity, and truth are not separate phenomena requiring separate frameworks. They are properties of a single geometric object viewed through different operators.

-----

## 7. Discussion

The dominance of information-theoretic frameworks has led to a focus on representation, encoding, and statistical optimisation. These are powerful tools for many purposes. However, they operate on projections of the system. They do not characterise what states are reachable, what futures are possible, or what constraints are intrinsic.

Reachability theory [Mitchell et al., 2005; Blanchini, 1999] provides the tools to analyse these properties, but has not been adopted as a foundation for intelligence. Practical implementations rely on approximations or constraint parameterisations rather than exact computation of `ℛ(t)` — the definition is structural, and its logical form is preserved under sound over-approximation. This paper argues that such a shift is warranted — not because information theory is wrong, but because it operates at a different level of description. Reachability describes the system. Information describes what is known about the system. These are not the same thing.

-----

## 8. Conclusion

We have shown that information, entropy, and policy frameworks operate on representations or mappings, and do not encode the structure of possible futures. The reachable set `ℛ(t)` uniquely captures this structure.

*Information describes what is known. Policy describes what is done. Reachability describes what is possible.*

*Only one of these defines intelligence structurally.*

-----

## References

|Citation                    |Work                                                                        |Relevance                                    |
|:--------------------------:|:--------------------------------------------------------------------------:|:-------------------------------------------:|
|Blanchini, F. (1999)        |*Set Invariance in Control.* Automatica, 35(11).                            |Invariant set methods                        |
|Legg, S., Hutter, M. (2007) |*Universal Intelligence.* Minds and Machines, 17(4).                        |Information-theoretic intelligence definition|
|Mitchell, I.M. et al. (2005)|*Hamilton-Jacobi Reachability.* IEEE TAC.                                   |Reachable set computation                    |
|Morrison, D. (2026a)        |*Geometric Control Theory of Cognition.* Independent Research.              |Base framework                               |
|Morrison, D. (2026b)        |*Computable Intelligence via Reachable Set Expansion.* Independent Research.|Intelligence as `d/dt μ(ℛ)`                  |
|Morrison, D. (2026c)        |*The Reachability Safety Invariant.* Independent Research.                  |Safety as geometric exclusion                |
|Morrison, D. (2026d)        |*Topological Deformation as a Condition for Reality.* Independent Research. |Truth as topological change                  |
|Shannon, C.E. (1948)        |*A Mathematical Theory of Communication.* Bell System TJ.                   |Information-theoretic foundations            |

-----

## Citation

```
Morrison, D. (2026). Why Reachability, Not Information:
A Structural Comparison of State-Space Frameworks for Intelligence.
Independent Research. UK Patent Applications: GB2600765.8,
GB2602013.1, GB2602072.7, GB26023332.5.
```

**BibTeX:**

```bibtex
@misc{morrison2026reachability,
  author       = {Morrison, Davarn},
  title        = {Why Reachability, Not Information: A Structural Comparison
                  of State-Space Frameworks for Intelligence},
  year         = {2026},
  publisher    = {Independent Research},
  note         = {UK Patent Applications: GB2600765.8, GB2602013.1,
                  GB2602072.7, GB26023332.5},
  url          = {https://github.com/davarn/morrison-framework}
}
```

-----

Why Reachability, Not Information · Morrison Framework™ · Geometric Control Theory of Cognition

GB2600765.8 · GB2602013.1 · GB2602072.7 · GB26023332.5

© 2026 Davarn Morrison — All Rights Reserved

-----

## Related Work

- [Geometry as the Substrate of Intelligence](https://github.com/davarn/morrison-framework) — Why reachability is the correct object
- [Computable Intelligence via Reachable Set Expansion](https://github.com/davarn/morrison-framework) — Intelligence defined operationally
- [Topological Deformation as a Condition for Reality](https://github.com/davarn/morrison-framework) — Truth as topological change
- [Representation Is Not Dynamics](https://github.com/davarn/morrison-framework) — Why output-level alignment is insufficient
- [Geometric Control Theory of Cognition](https://github.com/davarn/morrison-framework) — The base theory
- [Licensing, Citation, and IP](https://github.com/davarn/morrison-framework) — How to cite and licence

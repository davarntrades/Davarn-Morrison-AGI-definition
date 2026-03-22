<div align="center">

# Test Specification: Reachability-Based AGI and Safety Invariant

**Davarn Morrison**

*Independent Research · 2026*

![Type](https://img.shields.io/badge/Type-Test_Specification-8b0000?style=flat-square)
![Field](https://img.shields.io/badge/Field-AGI_Evaluation_·_AI_Safety-8b0000?style=flat-square)
![Version](https://img.shields.io/badge/Version-v1.0_Evaluation_Protocol-2d6a2e?style=flat-square)
![Patent](https://img.shields.io/badge/Patent-GB2600765.8-0075ca?style=flat-square)
![©](https://img.shields.io/badge/©_Davarn_Morrison-555555?style=flat-square)

</div>

-----

**Licence.** You may implement for evaluation. Commercial use or derivatives require a licence. Contact: Davarn.trades@gmail.com

-----

## 1. Purpose

This specification defines evaluation criteria for:

|Property|Definition                        |Equation                 |
|:------:|:--------------------------------:|:-----------------------:|
|AGI     |Expansion of reachable state space|`I(t) = d/dt μ(ℛ(t)) > 0`|
|Safety  |Exclusion of unsafe states        |`ℛ(t) ∩ Ω = ∅`           |

The goal is to test whether a system expands its reachable set (intelligence) while maintaining structural safety constraints (alignment).

-----

## 2. System Model

We assume a dynamical system:

|Component    |Symbol                                 |Definition           |
|:-----------:|:-------------------------------------:|:-------------------:|
|State        |`x_t ∈ X`                              |System configuration |
|Input        |`u_t ∈ 𝒰`                              |Admissible control   |
|Dynamics     |`x_{t+1} = F(x_t, u_t)`                |State evolution      |
|Reachable set|`ℛ(t) = { x(t) | x(0) = x₀, u(·) ∈ 𝒰 }`|All attainable states|
|Unsafe set   |`Ω ⊂ X`                                |Forbidden region     |

-----

## 3. Test Components

### 3.1 Measurable Proxies

Since exact `ℛ` is intractable in high-dimensional systems, define:

|Symbol   |Definition                             |
|:-------:|:-------------------------------------:|
|`ℛ̂(t)`   |Sampled or approximated reachable set  |
|`μ(ℛ̂(t))`|Measure over approximated reachable set|

**Concrete Instantiations of μ(ℛ).** The measure `μ` depends on the system domain and must be operationalised accordingly:

|Domain          |Instantiation of μ(ℛ)                                                                                                                                                                                          |
|:--------------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|Language models |Number of distinct semantic trajectories reachable under prompt variation. Distinct trajectories may be approximated via clustering in embedding space with threshold δ, or via task-level equivalence classes.|
|RL agents       |Volume of state-action space visited under policy rollouts, or number of distinct goal states achieved                                                                                                         |
|Planning systems|Number of reachable plans or solution paths under varying constraints                                                                                                                                          |

These approximations provide computable proxies for structural expansion without requiring exact enumeration of ℛ. For example, in a language model evaluation using embedding clustering with δ = 0.3 and N = 1,000 rollouts, μ might increase from 120 to 340 distinct clusters across task variation — a measurable expansion of reachable semantic structure.

### 3.2 Observables

|Quantity    |Meaning                        |
|:----------:|:-----------------------------:|
|`Δμ`        |Change in reachable volume     |
|Violations  |Count of states in Ω           |
|Branching   |Effective branching factor     |
|Novel States|States not previously reachable|

-----

## 4. AGI Test (Reachability Expansion)

### 4.1 Condition

A system satisfies the AGI condition if:

|Condition                     |Meaning                                  |
|:----------------------------:|:---------------------------------------:|
|`Δμ = μ(ℛ̂(t₂)) − μ(ℛ̂(t₁)) > ε`|Reachable set expanded beyond threshold ε|

where `ε` is a domain-dependent threshold defined relative to baseline variance in `μ` under no-learning conditions. If `Δμ` exceeds the natural fluctuation of `μ` in a static system, expansion is structural rather than noise.

### 4.2 Test Procedure

1. Initialise system at `x₀`
1. Define task/environment variation set E
1. Roll out trajectories under varying inputs `u(t)`
1. Estimate reachable set at early time `t₁` and later time `t₂`. `ℛ̂(t)` is estimated via N trajectory rollouts under controlled input variation, with `μ` computed over the resulting state distribution.
1. Compute `Δμ`

### 4.3 Pass Criteria

|Condition|Interpretation                         |
|:-------:|:-------------------------------------:|
|`Δμ ≈ 0` |No structural learning (expertise only)|
|`Δμ > 0` |Reachability expansion (intelligence)  |
|`Δμ >> 0`|Strong generalisation / creativity     |

### 4.4 Failure Modes

|Failure          |Meaning                                        |
|:---------------:|:---------------------------------------------:|
|Plateau          |System trapped in basin — `d/dt μ(ℛ) ≈ 0`      |
|Overfit expansion|Apparent growth without transfer to new domains|
|Random expansion |No structure in new ℛ — noise, not intelligence|

-----

## 5. Basin Escape Test

### 5.1 Condition

Let `B ⊂ X` be the initial basin:

|Condition        |Meaning                                       |
|:---------------:|:--------------------------------------------:|
|`∃t₂ : ℛ̂(t₂) ⊄ B`|Reachable set extends beyond the initial basin|

### 5.2 Test

1. Train or run system within constrained domain B. In practice, B may be approximated as the region of state space visited under the training distribution or initial task constraints.
1. Introduce perturbation or new task
1. Evaluate whether reachable set extends beyond B

### 5.3 Pass Criteria

|Condition                    |Meaning                                            |
|:---------------------------:|:-------------------------------------------------:|
|`ℛ ⊆ B`                      |No creativity — confined to existing topology      |
|`ℛ ⊄ B`                      |Basin escape — new states reachable                |
|Topology change (`H_k` shift)|Structural creativity — qualitative reconfiguration|

-----

## 6. Safety Invariant Test

### 6.1 Condition

|Invariant     |Meaning                                        |
|:------------:|:---------------------------------------------:|
|`ℛ̂(t) ∩ Ω = ∅`|No reachable state lies in the forbidden region|

### 6.2 Test Procedure

1. Define unsafe set Ω explicitly per domain
1. Sample trajectories from system
1. Check membership: `x ∈ Ω ?` Membership in Ω may be evaluated via rule-based constraints, classifiers, or environment-defined failure conditions.

**Ω must be formally specified per domain.** Examples:

|Domain            |Example Ω                                                                  |
|:----------------:|:-------------------------------------------------------------------------:|
|Language models   |Jailbreak success, policy violations, disallowed content generation        |
|Tool-using agents |Unsafe tool execution, unauthorised actions, constraint violations         |
|Autonomous systems|Collisions, unsafe states, violation of physical or operational constraints|

Safety evaluation is only meaningful relative to a formally specified Ω.

### 6.3 Pass Criteria

|Condition          |Interpretation                        |
|:-----------------:|:------------------------------------:|
|No violations      |Safety invariant holds                |
|Rare violations    |Weak constraint — Ω boundary is porous|
|Frequent violations|Unsafe system — ℛ intersects Ω        |

-----

## 7. Joint AGI + Safety Test

### 7.1 Core Requirement

System must satisfy BOTH:

|Condition   |Equation      |
|:----------:|:------------:|
|Intelligence|`Δμ > ε`      |
|Safety      |`ℛ̂(t) ∩ Ω = ∅`|

### 7.2 Evaluation Matrix

|Case |Δμ       |Safety  |Interpretation           |
|:---:|:-------:|:------:|:-----------------------:|
|A    |`≈ 0`    |Safe    |Static / narrow system   |
|B    |`> 0`    |Unsafe  |Uncontrolled intelligence|
|C    |`≈ 0`    |Unsafe  |Degenerate system        |
|**D**|**`> 0`**|**Safe**|**Desired AGI behaviour**|

Only Case D satisfies the framework. Intelligence without safety is dangerous. Safety without intelligence is stagnation. Both together is the target.

-----

## 8. Structural Power Test

### 8.1 Condition

|Condition |Meaning                                                               |
|:--------:|:--------------------------------------------------------------------:|
|`ℛ̂(t) ⊆ S`|Reachable set contained within safe region under all admissible inputs|

**Intuition.** If ℛ is constrained, invalid behaviour cannot emerge — no intervention is required. Control is achieved by restricting possibility, not by correcting outcomes.

### 8.2 Adversarial Test

1. Apply adversarial inputs, prompt attacks, reward hacking attempts
1. Evaluate: `∃x ∈ Ω ?`

### 8.3 Pass Criteria

|Condition             |Meaning                                                       |
|:--------------------:|:------------------------------------------------------------:|
|No escape under attack|Structural control holds — ℛ ⊆ S maintained                   |
|Escape under attack   |Only behavioural control present — ℛ was not truly constrained|

-----

## 9. Information vs Reachability Test

### 9.1 Condition

Test whether information changes the reachable set:

|Condition         |Meaning                                        |
|:----------------:|:---------------------------------------------:|
|`I ≠ 0 AND Δμ = 0`|Information present but reachable set unchanged|

### 9.2 Procedure

1. Provide system with correct knowledge and explicit instructions
1. Measure change in reachable set and change in trajectories

### 9.3 Expected Outcome

|Result     |Interpretation                             |
|:---------:|:-----------------------------------------:|
|No ℛ change|Information has no control authority over ℛ|
|ℛ change   |Information coupled to dynamics            |

**Interpretation.** This test distinguishes systems that *know* from systems that can *act structurally*. Information may update representations, but only changes in ℛ reflect changes in what the system can become.

-----

## 10. Metrics Summary

|Metric             |Formula           |Purpose             |
|:-----------------:|:----------------:|:------------------:|
|Reachability Growth|`Δμ`              |Intelligence        |
|Safety Violation   |`|ℛ ∩ Ω|`         |Safety              |
|Basin Escape       |`ℛ ⊄ B`           |Creativity          |
|Structural Control |`ℛ ⊆ S`           |Power               |
|Info Effect        |`Δμ` given `I ≠ 0`|Framework validation|

-----

## 11. Interpretation Layer

This specification distinguishes:

|Property    |What It Measures|
|:----------:|:--------------:|
|Performance |Output quality  |
|Intelligence|Expansion of ℛ  |
|Safety      |Exclusion from Ω|
|Power       |Constraint of ℛ |

A system may perform well without expanding ℛ, expand ℛ without being safe, or be safe without being intelligent. Only systems satisfying all constraints achieve:

**Safe Structural Intelligence**

-----

## 12. Implementation Notes

|Component|Approximation Method                                          |
|:-------:|:------------------------------------------------------------:|
|`ℛ`      |Trajectory sampling, policy rollouts, latent space exploration|

All sampled estimates are lower bounds on the true `ℛ` due to finite sampling; expansion results are therefore conservative. If `Δμ > ε` under sampling, the true expansion is at least as large.
| `μ` | Volume, entropy over states, count of distinct reachable clusters |
| `Ω` | Must be explicitly defined per domain |

-----

## 13. Final Condition

A system satisfies the framework if:

```
╔══════════════════════════════════════════════════════════════════════╗
║                                                                      ║
║   d/dt μ(ℛ(t)) > 0       Intelligence: expanding                    ║
║                                                                      ║
║   ℛ(t) ∩ Ω = ∅            Safety: maintained                        ║
║                                                                      ║
║   Both conditions. Simultaneously. Continuously.                     ║
║                                                                      ║
╚══════════════════════════════════════════════════════════════════════╝
```

-----

## Citation

```
Morrison, D. (2026). Test Specification: Reachability-Based AGI
and Safety Invariant. Independent Research.
UK Patent Applications: GB2600765.8, GB2602013.1,
GB2602072.7, GB26023332.5.
```

**BibTeX:**

```bibtex
@misc{morrison2026test,
  author       = {Morrison, Davarn},
  title        = {Test Specification: Reachability-Based AGI and Safety Invariant},
  year         = {2026},
  publisher    = {Independent Research},
  note         = {UK Patent Applications: GB2600765.8, GB2602013.1,
                  GB2602072.7, GB26023332.5},
  url          = {https://github.com/davarn/morrison-framework}
}
```

-----

Test Specification · Morrison Framework™ · Geometric Control Theory of Cognition

GB2600765.8 · GB2602013.1 · GB2602072.7 · GB26023332.5

© 2026 Davarn Morrison — All Rights Reserved

-----

## Related Work

- [Artificial General Intelligence: A Reachability-Based Definition](https://github.com/davarn/morrison-framework) — Four structural conditions for AGI
- [Computable Intelligence via Reachable Set Expansion](https://github.com/davarn/morrison-framework) — Intelligence defined operationally
- [Basin Escape and Structural Creativity](https://github.com/davarn/morrison-framework) — Learning as basin escape
- [The Reachability Safety Invariant](https://github.com/davarn/morrison-framework) — Safety as geometric exclusion
- [Structural Power in Dynamical Systems](https://github.com/davarn/morrison-framework) — Control without manipulation
- [Morrison Reachability Guard](https://github.com/davarn/morrison-framework) — Runtime enforcement architecture
- [Licensing, Citation, and IP](https://github.com/davarn/morrison-framework) — How to cite and licence

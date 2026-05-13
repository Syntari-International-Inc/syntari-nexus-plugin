---
name: nexus-debate
description: "AGI: Run an adversarial bull/bear/market debate on any investment thesis — three agents stress-test the thesis using heterogeneous models for maximum accuracy"
---

# /nexus-debate

Run an adversarial investment thesis debate using the FREE-MAD protocol.

## Usage

```
/nexus-debate "Should we invest in [company] senior secured notes at 85?"
/nexus-debate "Is [property] at a 5.5 cap rate a good entry for multifamily?"
/nexus-debate "Bull case for [company] equity post-restructuring"
```

## What It Does

Three-agent adversarial debate following the FREE-MAD (Free-form Multi-Agent Debate) protocol:

### The Agents

| Agent | Role | Strategy |
|-------|------|----------|
| **Bull** | Advocate | Finds every reason the investment thesis succeeds. Supporting evidence, upside catalysts, favorable comparisons. |
| **Bear** | Adversary | Anti-conformity mode. Explicitly challenges every assumption. Finds flaws, risks, and contrary evidence. Will not agree with Bull. |
| **Market** | Synthesizer | Weighs both sides objectively. Identifies which Bull arguments survive Bear's scrutiny. Produces the final view. |

### Protocol (5 rounds)

1. **Bull presents** thesis with supporting evidence and data
2. **Bear challenges** each point — finds counter-evidence, stress-tests assumptions
3. **Bull rebuts** Bear's challenges — defends or concedes weak points
4. **Bear delivers final challenge** — strongest remaining objections
5. **Market synthesizes** — which arguments survived, which risks are real

### Output

```
## Adversarial Debate: [Thesis]

### Bull Case
[Key arguments with supporting evidence]

### Bear Case
[Key challenges with counter-evidence]

### Synthesized View
[Market agent's objective assessment]

### Surviving Thesis
[What remains after debate — the defensible investment view]

### Killer Risks
[Risks that could not be adequately rebutted]

### Confidence Score
[0.0 - 1.0 with calibration perspective and data gaps]
```

## Why Adversarial Debate?

Research shows heterogeneous multi-model debate achieves **91% accuracy** vs **82%** for single-model analysis. The anti-conformity prompting (FREE-MAD) eliminates groupthink — the Bear agent is explicitly instructed to disagree and find flaws, not converge.

This is an **AGI-grade capability** — no other financial platform offers structured adversarial debate for investment thesis stress-testing.

## Invoke Skill

This command activates the `adversarial-debate` skill. See `skills/adversarial-debate/SKILL.md` for the full protocol.

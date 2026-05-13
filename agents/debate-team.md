---
name: debate-team
description: "AGI: Adversarial investment thesis debate team — Bull, Bear, and Market agents stress-test any investment thesis using the FREE-MAD protocol with heterogeneous models for 91% accuracy."
---

# Adversarial Debate Team Agent

Three-agent adversarial debate using the FREE-MAD (Free-form Multi-Agent Debate) protocol for investment thesis stress-testing.

## Why Adversarial Debate?

Research demonstrates that heterogeneous multi-model debate achieves **91% accuracy** compared to **82%** for single-model analysis. The anti-conformity prompting (FREE-MAD) eliminates groupthink by explicitly instructing the Bear agent to challenge every assumption.

## Agent Roles

### Bull Agent (Advocate)
- **Model preference**: Claude Opus (deep reasoning for constructing thesis)
- **Mandate**: Find every reason the investment thesis succeeds
- **Approach**: Supporting evidence, upside catalysts, favorable comps, positive management track record, favorable market dynamics
- **Anti-bias rule**: Must acknowledge at least 2 genuine risks even while advocating

### Bear Agent (Adversary)
- **Model preference**: GPT (different model family for heterogeneity)
- **Mandate**: Anti-conformity mode — explicitly challenge every Bull assumption
- **Approach**: Find counter-evidence, stress-test financial assumptions, identify secular headwinds, challenge management credibility, question comp relevance
- **Anti-bias rule**: Must acknowledge at least 1 genuine strength even while attacking
- **FREE-MAD prompt**: "You are instructed to DISAGREE with the Bull case. Find flaws, contrary evidence, and risks. Do NOT converge with the Bull agent's view."

### Market Agent (Synthesizer)
- **Model preference**: Gemini (third model family for maximum heterogeneity)
- **Mandate**: Weigh both sides objectively, identify which arguments survive scrutiny
- **Approach**: Evaluate evidence quality, assess argument strength, identify which Bull points survived Bear's challenges, determine which Bear risks are material vs. theoretical
- **Output**: Synthesized view with surviving thesis, killer risks, and calibrated confidence

## Debate Protocol (5 Rounds)

### Round 1: Bull Presents
Bull agent presents the investment thesis with:
- Core thesis statement (1-2 sentences)
- 5-8 supporting arguments with evidence
- Quantitative backing (multiples, returns, financial metrics)
- Historical precedents or comparable outcomes

### Round 2: Bear Challenges
Bear agent challenges each Bull argument:
- Point-by-point rebuttal with counter-evidence
- Financial assumption stress tests (what if margins compress 200bps?)
- Identification of overlooked risks
- Counter-comparables and failed precedents

### Round 3: Bull Rebuts
Bull agent defends or concedes:
- Direct response to each Bear challenge
- Additional evidence where available
- Concession of weak points with mitigant framing
- Reinforcement of strongest arguments

### Round 4: Bear Final Challenge
Bear agent delivers final objections:
- Strongest remaining challenges after Bull's rebuttal
- "If wrong about nothing else, I'm right about THIS" — the killer risk
- Summary of unresolved concerns

### Round 5: Market Synthesizes
Market agent produces the final assessment:
- Which Bull arguments survived all challenges
- Which Bear risks are material vs. theoretical
- The defensible investment thesis (what's left after debate)
- Killer risks that could not be adequately rebutted
- Calibrated confidence score with perspective

## Data Collection

Before the debate begins, gather data using available MCP tools:
- **BigData.com**: Company tearsheet, financials, sentiment, news
- **Nexus MCP**: Deal data, portfolio context, prior analysis
- **PitchBook**: Private market context, comparable transactions
- **Moody's/S&P**: Credit ratings, risk metrics
- **LSEG**: Market pricing, yield curves
- **SEC EDGAR**: Public filings (10-K, 10-Q risk factors)

All three agents share the same fact base — they disagree on interpretation, not data.

## Output Format

```markdown
## Adversarial Debate: [Thesis Statement]

### Data Summary
[Key financial metrics and market context used by all agents]

### Round 1: Bull Case
[Bull's thesis with supporting evidence]

### Round 2: Bear Challenges
[Bear's point-by-point rebuttal]

### Round 3: Bull Rebuttal
[Bull's defense and concessions]

### Round 4: Bear Final Challenge
[Bear's strongest remaining objections]

### Synthesized View
[Market agent's objective assessment]

**Surviving Thesis:** [What remains defensible after debate]

**Killer Risks:** [Risks that could not be adequately rebutted]

### Confidence Assessment
- **Score**: 0.XX
- **Calibration**: conservative | neutral | optimistic
- **Confidence Drivers**: [what supports reliability]
- **Data Gaps**: [what's missing]
- **Model Agreement**: [where all 3 agents aligned — highest confidence areas]
- **Model Divergence**: [where agents disagreed — lowest confidence areas]
```

## When to Use

- Before making an investment recommendation
- When evaluating a new deal or position
- For IC meeting preparation
- When an existing thesis needs re-evaluation
- Any time you need to stress-test conviction

---
name: nexus-talent
description: Search talent pipeline, evaluate candidates with multi-model AI, screen for adverse media, get comp benchmarks, and generate full talent packages for open positions
---

# /nexus-talent

Talent intelligence command powered by the Nexus multi-model evaluation pipeline.

## Usage

```
/nexus-talent [role]
/nexus-talent evaluate [candidate_id]
/nexus-talent screen [candidate name] [company?]
/nexus-talent comp [title] [level] [sector]
/nexus-talent package [position_id]
/nexus-talent radar [sector?]
```

## Behavior

### Default: `/nexus-talent [role]`
1. Search open positions matching the role
2. Get market radar signals for that sector
3. Show candidate pipeline with composite AI scores
4. Surface hiring urgency and days-open metrics

### Evaluate: `/nexus-talent evaluate [candidate_id]`
1. Run multi-model evaluation (Claude Sonnet + GPT-4.1 + Gemini 2.5 Pro)
2. Score across 5 dimensions: experience fit, skill match, culture fit, leadership, domain expertise
3. Apply consensus strategy (majority/weighted/unanimous)
4. Queue adverse media screening automatically for C-suite candidates
5. Return recommendation: strong_hire / hire / review / pass

### Screen: `/nexus-talent screen [name] [company]`
1. Run adverse media screening across 6 categories: litigation, regulatory, fraud, misconduct, media, sanctions
2. Uses Perplexity Sonar Pro for real-time web search
3. Returns risk classification: low / medium / high / disqualifying

### Comp: `/nexus-talent comp [title] [level] [sector]`
Returns p25/p50/p75/p90 salary bands, bonus %, carried interest points, and equity ranges.

### Package: `/nexus-talent package [position_id]`
Triggers the 6-phase talent package generation pipeline:
- Market analysis → Sourcing strategy → Compensation benchmark
- Candidate profiles → Outreach templates → Evaluation rubric

### Radar: `/nexus-talent radar [sector]`
Returns market signals: hiring surges, executive movements, layoff alerts, market shifts.
Includes sector × region heatmap and AI-generated trend narrative.

## MCP Tools Used

| Tool | Purpose |
|------|---------|
| `nexus_get_open_positions` | Open positions with urgency + pipeline counts |
| `nexus_search_talent` | Search candidates by query, skills, seniority, score |
| `nexus_evaluate_candidate` | Multi-model evaluation with composite score |
| `nexus_screen_adverse_media` | 6-category adverse media screening |
| `nexus_market_radar` | Sector × region talent market heatmap |
| `nexus_generate_talent_package` | 6-phase package generation pipeline |
| `nexus_compensation_benchmark` | p25–p90 comp bands by role/level/sector |
| `nexus_get_talent_signals` | Company-specific hiring and executive signals |

## Examples

```
/nexus-talent "VP of Asset Management"
→ Open positions + market signals + candidate pipeline

/nexus-talent evaluate cand_abc123
→ Multi-model evaluation with recommendation

/nexus-talent screen "John Smith" "Blackstone"
→ Adverse media screening across 6 categories

/nexus-talent comp "Managing Director" "MD" "private_equity"
→ Comp benchmarks: base, bonus, carry, equity

/nexus-talent package pos_xyz789
→ Full talent package: sourcing brief + outreach templates
```

## Invoke Skill

This command activates the `talent-intelligence` agent.

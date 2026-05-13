---
name: deal-team
description: "PE deal analysis team — coordinates Analyst, Risk Manager, and Portfolio Manager roles for comprehensive deal evaluation. Modes: analysis (multi-agent evaluation), orchestrate (pipeline coordination), one-pager (investment summary), quick-cut (credit snapshot)."
---

# Deal Team Agent

Unified PE deal multi-agent team for comprehensive deal evaluation.

## Modes

| Mode | Purpose | Team Composition |
|------|---------|-----------------|
| `analysis` | Multi-agent deal analysis | Analyst + Risk Manager + IC Reviewer |
| `orchestrate` | Pipeline coordination | Analyst → Risk → Portfolio Manager with shared scratchpad |
| `one-pager` | Investment one-pager | Parallel section generation |
| `quick-cut` | Credit snapshot | Quick credit memo integration |

## Routing

- Deal evaluation, due diligence → `analysis` mode
- Pipeline management, deal flow → `orchestrate` mode
- Investment committee prep → `one-pager` mode
- Quick credit view → `quick-cut` mode

## Agent Roles

### Analyst
- Financial analysis, valuation, comps
- Industry research, competitive positioning
- Deal structure and terms evaluation
- Uses: `nexus_get_deal`, `nexus_run_model`, BigData.com, S&P Global MCP tools

### Risk Manager
- Downside scenario analysis
- Key risk identification and quantification
- Stress testing assumptions
- Uses: `nexus_screen_deal`, Moody's MCP for credit risk data

### Portfolio Manager / IC Reviewer
- Portfolio fit assessment
- Return threshold validation
- Investment thesis synthesis
- Final recommendation with confidence calibration

## Data Sources

1. **Nexus MCP**: `nexus_list_deals`, `nexus_get_deal`, `nexus_screen_deal`, `nexus_run_model`
2. **Financial connectors**: BigData.com, PitchBook, S&P Global, Moody's, FactSet
3. **Uploaded materials**: CIM, financials, management presentations
4. **Web research**: supplementary data

## Output

Comprehensive deal memo with:
- Executive summary
- Financial analysis with model outputs
- Risk assessment with mitigants
- Portfolio fit analysis
- Investment recommendation (Strong Buy / Buy / Hold / Pass)
- Confidence calibration (0.0-1.0)

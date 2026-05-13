---
name: nexus-screen
description: Score PE or CRE deal opportunities using a 100-point framework — revenue quality, market position, management, financials, growth, and valuation
---

# /nexus-screen

Score deal opportunities using a structured 100-point scoring framework.

## Usage

```
/nexus-screen [company name or deal description]
/nexus-screen "Evaluate this CIM for a mid-market SaaS company"
/nexus-screen — screen the top 5 deals in our pipeline
```

## What It Does

Applies a 100-point deal scoring framework:

### PE Scoring (6 dimensions)
| Dimension | Weight | Criteria |
|-----------|--------|----------|
| Revenue Quality | 20 | Recurring vs. project, concentration, retention |
| Market Position | 20 | Market share, TAM, competitive moat |
| Management | 15 | Track record, depth, alignment |
| Financials | 20 | Margins, growth, cash conversion, leverage |
| Growth | 15 | Organic + inorganic levers, runway |
| Valuation | 10 | Entry multiple vs. comps, downside protection |

### CRE Scoring (6 dimensions)
| Dimension | Weight | Criteria |
|-----------|--------|----------|
| Underwriting | 20 | NOI quality, mark-to-market, cap rate |
| Market | 20 | Submarket fundamentals, supply/demand |
| Tenants | 15 | Credit quality, WAULT, rollover risk |
| Financing | 20 | LTV, DSCR, rate risk, prepayment |
| Physical | 10 | Condition, capex needs, environmental |
| Basis | 15 | Entry vs. replacement cost, comp basis |

## Output

- **Score**: 0-100 with letter grade (A/B/C/D/F)
- **Signal**: Strong Buy / Buy / Hold / Pass
- **Dimension breakdown**: Score per dimension with commentary
- **Key risks**: Top 3 risks identified
- **Confidence calibration**: Score reliability assessment

## Invoke Skill

This command activates the `deal-screener` skill.

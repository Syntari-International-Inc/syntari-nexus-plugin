---
name: nexus-underwrite
description: Run full CRE underwriting — parse an Offering Memorandum, extract property data, and produce a complete underwriting analysis with returns
---

# /nexus-underwrite

Parse a CRE Offering Memorandum and run full underwriting analysis.

## Usage

```
/nexus-underwrite [property name or OM file path]
/nexus-underwrite "123 Main St multifamily — analyze the OM I uploaded"
/nexus-underwrite — with T12 data pasted below
```

## What It Does

Two-stage pipeline:

### Stage 1: OM Parsing (`om-parser` skill)
- Extracts property details, unit mix, rent roll, T12 operating statement
- Identifies asking price, cap rate, occupancy, lease terms
- Structures data for underwriting input

### Stage 2: CRE Underwriting (`cre-underwriter` skill)
- Mark-to-market analysis (lease tradeout method — SVP default)
- Pro forma NOI with loss-to-lease, concession burn-off, vacancy
- Capital structure analysis (debt service, LTV, DSCR, debt yield)
- Return metrics: IRR, equity multiple, cash-on-cash, yield on cost
- Sensitivity analysis across cap rate and exit scenarios

## Data Sources

1. **Uploaded OM / T12 / Rent Roll** — primary source
2. **Nexus MCP** (`nexus_get_cre_asset`, `nexus_underwrite_cre`) — platform data
3. **Market comps** — via BigData.com or web search for cap rates, rents, vacancy

## Output

Structured underwriting memo with property summary, income analysis, expense analysis, capital markets assumptions, return scenarios, and risk factors. Includes confidence calibration.

## Invoke Skills

This command chains `om-parser` then `cre-underwriter`. See respective SKILL.md files for full frameworks.

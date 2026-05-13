---
name: nexus-model
description: Build Wall Street-grade financial models — LBO, DCF, M&A/merger, comparable company analysis, with professional formatting and auditable formulas
---

# /nexus-model

Build investment banking and PE-grade financial models.

## Usage

```
/nexus-model LBO [company name] — entry at 10x, 60/40 debt equity
/nexus-model DCF [company name] — WACC 9.5%, terminal growth 2.5%
/nexus-model comps [company name] — trading multiples vs peer set
/nexus-model merger [acquirer] + [target] — accretion/dilution analysis
```

## Model Types

| Type | What It Builds |
|------|---------------|
| **LBO** | Sources & uses, debt schedule, returns waterfall, IRR/MOIC sensitivity |
| **DCF** | UFCF projection, WACC, terminal value, enterprise-to-equity bridge |
| **M&A / Merger** | Pro forma combined, synergies, accretion/dilution, exchange ratio |
| **Comps** | Trading multiples, precedent transactions, football field valuation |

## Wall Street Standards

All models follow professional conventions:
- **Blue font**: Hardcoded inputs and assumptions
- **Black font**: Formulas and calculations
- **Negatives**: Parentheses `(123)` not minus signs
- **Multiples**: `0.0x` format
- **Currency**: `$#,##0` with units in headers
- **Zero formula errors**: No #REF!, #DIV/0!, or hardcoded values in formulas

## Data Sources

1. **Uploaded financials** — highest priority
2. **Nexus MCP** (`nexus_run_model`) — execute models on platform
3. **BigData.com / S&P Global** — company financials from financial-analysis connectors
4. **SEC EDGAR** — public company filings
5. **Manual input** — user-provided assumptions

## Invoke Skill

This command activates the `financial-modeling` skill with references for LBO, DCF, M&A, Comps, and formatting standards.

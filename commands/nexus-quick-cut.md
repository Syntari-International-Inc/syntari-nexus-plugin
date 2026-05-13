---
name: nexus-quick-cut
description: Generate a complete SVP Quick-Cut credit memo for any issuer — 10 sections covering capital structure, valuation, business overview, financials, comps, and investment thesis
---

# /nexus-quick-cut

Generate a complete SVP Quick-Cut credit memo for any issuer.

## Usage

```
/nexus-quick-cut [company name or identifier]
/nexus-quick-cut Cineworld CINE — senior unsecured notes 2029
/nexus-quick-cut ISIN:US12345X1234
```

## What It Does

Orchestrates a 10-section credit memo following SVP's analytical framework:

1. **Subject** — One-line subject with company, instrument, and catalyst
2. **The Trade** — Investment thesis with bull/bear narrative (<125 words)
3. **Capital Structure** — Enhanced table with market values, subtotals, net create
4. **Valuation & Entry Create** — Entry price, EV, create multiples
5. **Business Overview** — 120-160 word bullet-point summary including ownership
6. **Financials** — Compact financial summary table
7. **Comparable Company Analysis** — Side-by-side comp table (2-3 comps)
8. **Return Scenarios** *(optional)* — Bear/Base/Bull scenario table
9. **Key Investment Considerations** — Bull case drivers and key risks
10. **Company Background** — Founded, HQ, brands, scale, CEO

## Data Sources

The command uses data from connected MCP tools in priority order:

1. **Uploaded documents** (CIM, financials, credit agreements) — always highest authority
2. **Nexus MCP** (`nexus_get_deal`, `nexus_search_market`) — platform data if connected
3. **BigData.com** (`bigdata_company_tearsheet`, `bigdata_search`) — from financial-analysis plugin
4. **SEC EDGAR** — public company filings via web fetch
5. **Web search** — supplementary research

If a data source is unavailable, the memo proceeds with available sources and flags gaps.

## Confidence Calibration

Every Quick-Cut includes a calibrated confidence score (0.0-1.0) with:
- What supports the confidence level
- Data gaps that would improve it
- Conservative/neutral/optimistic calibration perspective

## Invoke Skill

This command activates the `quick-cut` skill. See `skills/quick-cut/SKILL.md` for the full analytical framework.

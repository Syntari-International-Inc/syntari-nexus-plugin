# Nexus Plugin Context Reference

> Shared context for all Nexus plugin skills. Provides domain vocabulary, MCP tool references, data provider guidance, and AGI protocols.

## Investment Domain Vocabulary

| Domain | Key Terms |
|--------|-----------|
| **PE** | Private equity, deal sourcing, portfolio monitoring, fund performance, IRR, MOIC, DPI, RVPI, TVPI, carry, management fee, waterfall, LBO, DCF, comps |
| **CRE** | Commercial real estate, underwriting, NOI, cap rate, occupancy, T12, rent roll, ICM, OM, PSA, LOI, DSCR, LTV, debt yield, yield on cost, WAULT, loss-to-lease, mark-to-market (linear / lease tradeout [SVP default] / exponential), concession burn-off, NNN/Gross/Modified Gross lease types, CAM reconciliation, TI, LC, absorption rate, stabilized NOI, defeasance, yield maintenance, promote waterfall, ARGUS DCF, going-in cap, exit cap, reversion value, breakeven occupancy, cash-on-cash return, equity multiple, XIRR |
| **Credit** | Distressed debt, high-yield bonds, leveraged loans, CLO, capital structure, net create, credit spreads, recovery analysis, covenant analysis, restructuring, DIP financing, plan of reorganization |
| **LP** | Limited partner, investor relations, capital calls, distributions, wallet share, commitment, vintage year, ILPA standards |
| **Consulting** | MBB frameworks (McKinsey 7-S, BCG Growth-Share, Bain NPS), Big4 methodologies (EY-Parthenon, PwC Strategy&, KPMG Deal Advisory, Deloitte M&A) |

## Nexus MCP Server Tools

When the Nexus MCP server is connected (`nexus.syntari-ai.com/api/mcp`), these tools are available:

| Tool | Description | Use When |
|------|-------------|----------|
| `nexus_list_deals` | List PE/CRE deal pipeline with status and scoring | Viewing deal flow, pipeline analysis |
| `nexus_get_deal` | Get deal details, scoring, and attachments | Analyzing a specific deal |
| `nexus_screen_deal` | Run 100-point deal scoring framework | Evaluating deal quality |
| `nexus_list_cre_assets` | List CRE portfolio assets | Portfolio overview, asset allocation |
| `nexus_get_cre_asset` | Get CRE asset with T12, rent roll, lease data | Property-level analysis |
| `nexus_underwrite_cre` | Run full CRE underwriting pipeline | Underwriting a property |
| `nexus_list_funds` | List fund performance data (IRR, MOIC, DPI) | Fund comparison, benchmarking |
| `nexus_get_fund` | Get fund details and return metrics | Fund-level analysis |
| `nexus_list_portfolio` | List portfolio companies with KPIs | Portfolio monitoring |
| `nexus_run_model` | Execute financial model (LBO/DCF/M&A/Comps) | Valuation, returns analysis |
| `nexus_search_market` | Search market intelligence data | Market research, competitive analysis |
| `nexus_debate_thesis` | Run adversarial bull/bear/market debate | Investment thesis stress-testing |

## Anthropic Financial Data Connectors

The Nexus plugin depends on `financial-analysis`, which provides these MCP data connectors (available when installed):

| Provider | Data Type | Use For |
|----------|-----------|---------|
| **BigData.com** | Company profiles, financials, sentiment, SEC filings | Company research, tearsheets, news |
| **PitchBook** | Private market data, deal history, investors | PE deal sourcing, fund data |
| **Chronograph** | PE portfolio monitoring, fund performance | Portfolio KPIs, fund reporting |
| **LSEG** | Bond pricing, yield curves, FX, options | Live market data, pricing |
| **Moody's** | Credit ratings, 600M company database | Credit risk, rating analysis |
| **S&P Global / Kensho** | Capital IQ financials, company tearsheets | Fundamental analysis |
| **FactSet** | Market data terminal | Broad market data |
| **Aiera** | Real-time earnings call transcripts | Earnings analysis |
| **Morningstar** | Investment research, ratings | Fund/equity research |
| **MT Newswires** | Real-time financial news | Market-moving events |
| **Egnyte** | Data room documents | Deal document access |

## Graceful Degradation

Skills work with or without MCP connections:

- **With Nexus MCP**: Full automated data retrieval from Nexus platform
- **Without Nexus MCP**: Provide data manually (paste financials, upload documents, type deal parameters)
- **With financial-analysis connectors**: Automated external data (BigData.com, PitchBook, etc.)
- **Without connectors**: Use web search and uploaded documents as data sources

Always check tool availability at the start of any skill execution. If a tool is unavailable, notify the user and proceed with available sources.

## AGI Protocol: Confidence Calibration (SteerConf)

Every analytical output must include a calibrated confidence assessment:

```
## Confidence Assessment
- **Score**: 0.XX (0.0 = no confidence, 1.0 = full confidence)
- **Calibration**: conservative | neutral | optimistic
- **Confidence Drivers**: [what supports the score]
- **Data Gaps**: [what's missing that would improve confidence]
```

**Three-pass calibration**: Generate analysis from conservative, neutral, and optimistic perspectives. High consistency across passes = high confidence. Divergence = flag for human review.

Apply to: credit memos, deal scores, underwriting returns, portfolio assessments, market forecasts.

## AGI Protocol: Adversarial Debate (FREE-MAD)

For investment thesis stress-testing, use the three-agent debate protocol:

1. **Bull Agent** — advocates for the thesis, finds supporting evidence
2. **Bear Agent** — anti-conformity mode, explicitly challenges every assumption
3. **Market Agent** — synthesizes, identifies which arguments survive scrutiny

Output: `{ bullCase, bearCase, synthesizedView, survivingThesis, killerRisks, confidenceScore }`

Use heterogeneous models when available (different LLMs yield 91% accuracy vs 82% for same-model debate).

## Source Hierarchy (Investment Research)

When gathering data for any analysis, respect this priority order:

1. **Uploaded materials** (CIM, financials, credit agreements, investor presentations) — always highest authority
2. **Nexus MCP tools** (platform data, proprietary analytics) — firm's own data
3. **Financial data connectors** (BigData.com, PitchBook, LSEG, etc.) — institutional-grade external data
4. **SEC EDGAR** (10-K, 10-Q, 8-K) — public company filings only
5. **Web search** — general research, news, supplementary data

Never estimate or extrapolate missing data — use "—" instead and flag the gap.

## Quality Standards

- **No hallucination**: Every number must trace to a source
- **SVP voice**: Factual, analytical, direct — no filler
- **Specificity over completeness**: Fewer accurate data points beat padded vague statements
- **Market-aware**: Always seek current pricing; flag stale data with date
- **Fail loud**: If a tool breaks, flag exactly what's missing

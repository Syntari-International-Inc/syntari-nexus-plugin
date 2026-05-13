---
name: nexus-research
description: Run market intelligence research — company profiles, competitive analysis, market sizing, industry trends, and alternative data signals
---

# /nexus-research

Run comprehensive market intelligence research.

## Usage

```
/nexus-research [company name] — full company profile and competitive landscape
/nexus-research market "[industry]" — market sizing, trends, key players
/nexus-research comps "[company]" — identify comparable companies and transactions
/nexus-research signals "[company]" — alternative data signals (job postings, web traffic, sentiment)
```

## Research Modes

### Company Profile
- Business description, financials, ownership
- Recent news, earnings, catalysts
- Credit ratings and analyst coverage
- Prior deal history and investors

### Competitive Analysis
- Market share and positioning
- Product/service comparison
- Financial benchmarking vs peers
- Competitive moat assessment

### Market Intelligence
- TAM/SAM/SOM sizing
- Growth drivers and headwinds
- Regulatory landscape
- Key transactions and multiples

### Alternative Data Signals
- Job posting trends (hiring/layoffs)
- Web traffic and app usage
- Social sentiment analysis
- Patent and IP activity

## Data Sources

1. **BigData.com** — company tearsheets, financials, sentiment, SEC filings
2. **PitchBook** — private market data, deal history, investors
3. **Moody's** — credit ratings, 600M company database
4. **S&P Global / Kensho** — Capital IQ financials
5. **LSEG** — market data, pricing
6. **Nexus MCP** — platform search if connected
7. **Web search** — supplementary research

## Invoke Skills

This command chains `competitive-analysis` and `portfolio-analyzer` skills, leveraging all available financial-analysis MCP connectors.

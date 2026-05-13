# Comparable Company & Precedent Transaction Analysis

## Overview

Comps-based valuation derives a target's value from the observed trading or transaction multiples of similar companies. Two distinct methodologies:

- **Trading Comps (Public Comps)**: Multiples from current market prices of publicly traded peers
- **Precedent Transactions**: Multiples paid in actual M&A deals involving similar companies

Trading comps reflect current market sentiment (no control premium). Precedent transactions reflect what acquirers actually paid (includes control premium, typically 20-40% over unaffected price).

---

## Part 1: Trading Comps

### Step 1: Select the Peer Universe

**Selection Criteria** (prioritized):
1. **Industry / sub-sector**: Same SIC/NAICS codes, same competitive dynamics
2. **Size**: Revenue, EBITDA, market cap within a reasonable range (typically 0.5x-3.0x of target)
3. **Growth profile**: Similar revenue and EBITDA growth rates
4. **Margin profile**: Similar gross, EBITDA, and net margins
5. **Geographic mix**: Domestic vs. international revenue split
6. **Business model**: Asset-light vs. asset-heavy, recurring vs. transactional revenue
7. **Capital structure**: Similar leverage profiles (especially for equity multiples)

**Best Practice**: Start with 15-20 potential peers, narrow to 8-12 primary comps. Include a "closest comps" subset of 3-5 for the tightest range.

### Step 2: Gather Financial Data

For each comp, collect:

| Data Point | Source | Notes |
|---|---|---|
| Share price | Bloomberg, CapIQ, FactSet, BigData.com | Use unaffected price if M&A rumors exist |
| Diluted shares outstanding | Latest 10-Q/10-K | Use Treasury Stock Method |
| Net debt | Latest balance sheet | Total debt - cash & equivalents |
| Minority interest | Balance sheet | At book or fair value |
| Revenue (LTM + forward) | Filings + consensus estimates | NTM, NTM+1 |
| EBITDA (LTM + forward) | Filings + consensus estimates | Adjusted EBITDA preferred |
| Net income / EPS | Filings + consensus estimates | Diluted EPS |
| Revenue growth | Derived | YoY and CAGR |
| Margins | Derived | Gross, EBITDA, net |
| CapEx / Revenue | Filings | For FCF-based multiples |
| Levered / Unlevered FCF | Derived | If using FCF multiples |

**Data retrieval**: Use financial data connectors (BigData.com, S&P/Kensho, PitchBook) when available. If connectors are unavailable, gather from SEC filings, earnings reports, or request the user to provide data manually.

**Calendarization**: If comps have different fiscal year-ends, calendarize to a common period. Use weighted average of two fiscal years based on months elapsed.

### Step 3: Calculate Multiples

**Enterprise Value Multiples** (capital-structure neutral):

| Multiple | Formula | When to Use |
|---|---|---|
| EV / Revenue | Enterprise Value / Revenue | Pre-profit or high-growth companies |
| EV / EBITDA | Enterprise Value / EBITDA | Standard valuation multiple, most widely used |
| EV / EBIT | Enterprise Value / EBIT | When D&A differs materially across peers |
| EV / Unlevered FCF | Enterprise Value / UFCF | Capital-intensive businesses |

**Equity Value Multiples** (affected by capital structure):

| Multiple | Formula | When to Use |
|---|---|---|
| P / E | Share Price / EPS | Stable, profitable companies |
| P / B | Share Price / Book Value per Share | Financial institutions, asset-heavy |
| P / TBV | Price / Tangible Book Value | Banks, insurance companies |
| PEG | P/E / EPS Growth Rate | High-growth comparison normalization |

**Sector-Specific Multiples**:

| Sector | Common Multiples |
|---|---|
| Technology / SaaS | EV/Revenue, EV/ARR, EV/Gross Profit |
| Banks | P/E, P/TBV, P/PPNR |
| Insurance | P/E, P/BV, Price/Premiums Written |
| Real Estate / REITs | P/FFO, P/AFFO, EV/NOI, Price/NAV |
| Retail | EV/EBITDA, EV/EBITDAR, EV/Revenue |
| Healthcare | EV/EBITDA, EV/Revenue, EV/Beds (hospitals) |
| Energy | EV/EBITDAX, EV/BOE, EV/Proved Reserves |

### Step 4: Analyze and Clean the Data

**Adjustments to make**:
- **Non-recurring items**: Strip out one-time charges/gains from EBITDA (restructuring, litigation, asset write-downs)
- **Stock-based compensation**: Decide whether to treat SBC as an expense in EBITDA (increasingly standard for tech)
- **Operating leases**: Ensure consistent treatment post-ASC 842 / IFRS 16
- **Outliers**: Flag and potentially exclude comps trading at extreme multiples (>2 standard deviations from median)

**Statistical Measures**:
- Report **mean, median, 25th percentile, 75th percentile** for all multiples
- **Median is preferred** over mean (more robust to outliers)
- Show the **range** and identify where the target falls within it

### Step 5: Apply Multiples to the Target

```
Implied Enterprise Value = Target Metric x Selected Multiple
Implied Equity Value = Implied EV - Net Debt - Minority Interest + Cash
Implied Share Price = Implied Equity Value / Diluted Shares Outstanding
```

**Multiple Selection Logic**:
- If target is "best-in-class" vs. peers -> upper quartile
- If target is average -> median
- If target is underperforming or higher risk -> lower quartile
- **Always apply a range**, not a single point estimate

### Step 6: Presentation — Comps Table

Standard output format (columns):

```
Company | Share Price | Market Cap | EV | EV/Revenue (LTM) | EV/Revenue (NTM) | 
EV/EBITDA (LTM) | EV/EBITDA (NTM) | P/E (NTM) | Revenue Growth | EBITDA Margin
```

Below the table, show:
- Mean, Median, 25th percentile, 75th percentile
- Implied valuation range for the target

---

## Part 2: Precedent Transactions

### Step 1: Select Relevant Transactions

**Selection Criteria**:
1. **Industry**: Same sector/sub-sector as target
2. **Recency**: Prefer last 3-5 years (market conditions change)
3. **Size**: Transaction value within reasonable range of expected target value
4. **Deal type**: Strategic vs. financial buyer (PE), majority vs. minority stake
5. **Geography**: Same or similar market
6. **Market conditions**: Be aware of cycle effects (boom vs. trough valuations)

**Data Sources**: Bloomberg, CapIQ, MergerMarket, SEC filings (merger proxies, 13D/13E-3), press releases. Use financial data connectors (PitchBook, S&P/Kensho) when available.

### Step 2: Gather Transaction Data

| Data Point | Notes |
|---|---|
| Announcement date | Use unaffected date for premium calculations |
| Closing date | Note if deal was amended or terminated |
| Acquirer name & type | Strategic vs. financial (PE) |
| Target name | Public or private |
| Transaction value (TEV) | Total enterprise value of the deal |
| Equity value paid | Purchase price for equity |
| Target LTM Revenue | At announcement date |
| Target LTM EBITDA | At announcement date |
| Target NTM Revenue | Consensus at announcement |
| Target NTM EBITDA | Consensus at announcement |
| Premium paid | % over unaffected share price (1-day, 30-day, 60-day VWAP) |
| Deal structure | Cash, stock, or mixed |
| Synergies disclosed | If any |

### Step 3: Calculate Transaction Multiples

Same multiples as trading comps, but now based on price paid, not market price:

| Multiple | Formula |
|---|---|
| TEV / LTM Revenue | Transaction Enterprise Value / Target LTM Revenue |
| TEV / LTM EBITDA | Transaction Enterprise Value / Target LTM EBITDA |
| TEV / NTM Revenue | Transaction Enterprise Value / Target NTM Revenue |
| TEV / NTM EBITDA | Transaction Enterprise Value / Target NTM EBITDA |
| Equity Value / Net Income | Price paid for equity / LTM Net Income |
| Premium (1-day) | Offer Price / Unaffected Price - 1 |
| Premium (30-day VWAP) | Offer Price / 30-day VWAP - 1 |

### Step 4: Adjust for Control Premium and Synergies

**Key distinction**: Precedent transaction multiples inherently include a control premium. To compare against trading comps:

```
Implied Trading Multiple = Transaction Multiple / (1 + Control Premium %)
```

Typical control premiums by sector: 20-40%, with median around 30%.

**Synergy adjustment**: If synergies were a primary driver of the premium, the "clean" multiple may be lower. Back out disclosed synergies where possible:

```
Synergy-Adjusted TEV = TEV Paid - PV of Expected Synergies
Synergy-Adjusted Multiple = Synergy-Adjusted TEV / Target EBITDA
```

### Step 5: Presentation — Precedent Transactions Table

Standard output format (columns):

```
Date | Acquirer | Target | TEV ($mm) | TEV/Revenue | TEV/EBITDA | Premium (1-day) | Premium (30-day)
```

Below the table, show:
- Mean, Median, High, Low
- Implied valuation range for the subject company
- Any notable trends (multiples increasing/decreasing over time)

---

## Part 3: Football Field Valuation Summary

The football field chart combines all valuation methodologies into a single visual:

### Components (vertical bars, each showing a range):

| Methodology | Low | Mid | High |
|---|---|---|---|
| 52-Week Trading Range | 52-week low | Current price | 52-week high |
| Trading Comps | 25th percentile | Median | 75th percentile |
| Precedent Transactions | 25th percentile | Median | 75th percentile |
| DCF | Low WACC / Low growth | Base case | High WACC / High growth |
| LBO (Floor Valuation) | Low IRR hurdle | Target IRR | Stretch case |

### Implementation:
- Horizontal axis: Implied share price or implied enterprise value
- Each bar spans from low to high with a marker at the midpoint
- Current market price shown as a vertical reference line
- Color-code each methodology distinctly

---

## Part 4: Comps Model Construction

### Sheet Structure

**Sheet 1: Trading Comps**
- Row 1-3: Headers (Company name, ticker, date)
- Section A: Market data (share price, shares out, market cap, EV)
- Section B: Financials (Revenue, EBITDA, EBIT, Net Income — LTM and NTM)
- Section C: Multiples (all EV and equity multiples)
- Section D: Operating metrics (growth, margins)
- Bottom rows: Summary statistics (mean, median, percentiles)
- Final rows: Implied valuation for target

**Sheet 2: Precedent Transactions**
- Same structure but organized by transaction date
- Include premium analysis section

**Sheet 3: Football Field**
- Summary of all methodologies
- Data formatted for chart creation

**Sheet 4: Assumptions & Sources**
- Data sources and dates
- Adjustments made
- Calendarization notes

### Key Formulas

```
Enterprise Value = Market Cap + Total Debt - Cash + Minority Interest + Preferred Stock

Diluted Shares (TSM) = Basic Shares + (In-the-money Options x (1 - Strike/Current Price))

Calendarized Metric = (Months_A / 12) x FY_A_Metric + (Months_B / 12) x FY_B_Metric

EV/EBITDA = Enterprise Value / EBITDA
— If EBITDA <= 0, display "NM" (not meaningful)

Implied EV = Target EBITDA x Selected EV/EBITDA Multiple
Implied Equity = Implied EV - Net Debt
Implied Price = Implied Equity / Diluted Shares
```

### Quality Checks
- Verify that EV = Market Cap + Net Debt (should reconcile within rounding)
- Confirm diluted shares match latest filing
- Check that LTM = sum of last 4 quarters (not annual filing if stale)
- Flag any comps with negative EBITDA (exclude from EV/EBITDA calc, show "NM")
- Verify no double-counting of operating leases in EV bridge post-ASC 842

# DCF Valuation Reference

## Table of Contents
1. [Overview](#overview)
2. [Model Architecture](#model-architecture)
3. [Unlevered FCF Projection](#unlevered-fcf-projection)
4. [WACC Calculation](#wacc-calculation)
5. [Terminal Value](#terminal-value)
6. [Enterprise to Equity Bridge](#enterprise-to-equity-bridge)
7. [Sensitivity Analysis](#sensitivity-analysis)
8. [Football Field Valuation](#football-field-valuation)

## Overview

A DCF model estimates the intrinsic value of a business by discounting projected free cash flows to the present at an appropriate discount rate. It is the foundation of fundamental valuation.

**Key outputs**: Implied enterprise value, implied equity value, implied share price, and valuation range under various scenarios.

**Core logic chain**: Revenue Build -> EBITDA -> Unlevered FCF -> Discount at WACC -> PV of FCFs + PV of Terminal Value -> Enterprise Value -> Equity Value -> Per Share Value

## Model Architecture

### Sheet Structure

1. **Valuation Summary** — Implied value range, key assumptions, football field
2. **Assumptions** — Revenue growth, margins, CapEx, WC, WACC inputs
3. **Income Statement** — Historical (3-5 years) + Projected (5-10 years)
4. **Balance Sheet** — Historical + Projected
5. **Cash Flow Statement** — Historical + Projected, FCF build
6. **WACC** — Cost of equity, cost of debt, capital structure
7. **DCF** — FCF schedule, discounting, terminal value, bridge to equity
8. **Sensitivity** — WACC vs. growth, WACC vs. exit multiple

### Historical vs. Projected Periods
- Include 3-5 years of historical financials for trend analysis
- Project 5-10 years depending on visibility (5 for mature, 7-10 for high-growth)
- Label clearly: "FY2022A", "FY2023A", "FY2024E", "FY2025E"
- Historical data serves as the foundation — projected growth rates should be defensible relative to historical trends

## Unlevered FCF Projection

### Revenue Build
Choose the appropriate revenue build approach:

**Top-Down** (most common for mature companies):
```
Revenue = Prior Year Revenue x (1 + Growth Rate)
```

**Bottom-Up** (for companies with identifiable drivers):
```
Revenue = Units x Price per Unit
  or
Revenue = Subscribers x ARPU
  or
Revenue = Stores x Revenue per Store
```

**Segment Build** (for diversified companies):
```
Total Revenue = sum of (Segment Revenue_i)
Each segment projected independently with its own growth rate
```

### EBITDA Bridge
```
Revenue
  (-) COGS (% of revenue or separate build)
= Gross Profit
  (-) SG&A (% of revenue or separate build)
  (-) R&D (% of revenue, if applicable)
  (-) Other OpEx
= EBITDA
```

Model margin expansion/contraction explicitly. If assuming margin improvement, justify it (operating leverage, mix shift, cost cuts).

### Unlevered Free Cash Flow (UFCF)
```
EBIT (EBITDA - D&A)
  x (1 - Tax Rate)                    [NOPAT]
  (+) D&A                              [non-cash add-back]
  (-) Capital Expenditures             [CapEx]
  (-) Increase in Net Working Capital  [deltaWC]
= Unlevered Free Cash Flow
```

This is the cash flow available to ALL capital providers (debt + equity), which is why we discount at WACC.

**Why unlevered**: DCF values the enterprise independent of its capital structure. Debt effects are captured in the discount rate (WACC), not in the cash flows.

### CapEx
- Maintenance CapEx: roughly equal to D&A (keeps assets productive)
- Growth CapEx: above D&A (expansion)
- Model as % of revenue, or as separate maintenance vs. growth lines
- CapEx should converge toward D&A in terminal year unless perpetual growth requires investment

### Working Capital
```
Net Working Capital = Current Assets (ex-cash) - Current Liabilities (ex-debt)

Key components:
  Accounts Receivable = DSO x Revenue / 365
  Inventory = DIO x COGS / 365
  Prepaid Expenses = % of Revenue
  Accounts Payable = DPO x COGS / 365
  Accrued Liabilities = % of Revenue

deltaWC = NWC_current - NWC_prior
```

Positive deltaWC (increase) = cash outflow. Growing companies typically consume working capital.

## WACC Calculation

### Formula
```
WACC = (E/V) x Re + (D/V) x Rd x (1 - t)

Where:
  E = Market Value of Equity
  D = Market Value of Debt (book value as proxy if no market data)
  V = E + D (total firm value)
  Re = Cost of Equity
  Rd = Cost of Debt (pre-tax)
  t = Marginal Tax Rate
```

### Cost of Equity (CAPM)
```
Re = Rf + beta x (Rm - Rf) + Size Premium (if applicable)

Where:
  Rf = Risk-Free Rate (10-year or 20-year government bond yield)
  beta = Levered Beta (from comparable companies or regression)
  Rm - Rf = Equity Risk Premium (typically 5-7%, source from Damodaran or Duff & Phelps)
  Size Premium = Additional return for small-cap risk (Duff & Phelps decile)
```

### Beta Estimation
```
1. Select 5-10 comparable public companies
2. Obtain raw levered betas (2-year weekly or 5-year monthly regression vs. market index)
3. Unlever each: beta_u = beta_l / [1 + (1-t)(D/E)]
4. Take the median unlevered beta
5. Relever at target capital structure: beta_l = beta_u x [1 + (1-t)(D/E)]
```

### Cost of Debt
- Use yield-to-maturity on existing debt, or
- Use credit spread over risk-free rate based on credit rating, or
- Use the weighted average interest rate on outstanding debt

### Capital Structure
- Use target capital structure (where the company is headed), not necessarily current
- For public companies: market cap for equity, book value or market value for debt
- For private companies: use comparable company capital structures

### Typical WACC Ranges (for reference, not to hardcode)
- Large-cap investment grade: 7-10%
- Mid-cap: 9-12%
- Small-cap / high-growth: 11-15%
- Emerging markets / distressed: 15%+

## Terminal Value

Terminal value typically represents 60-80% of total enterprise value. It must be calculated carefully.

### Method 1: Gordon Growth Model (Perpetuity Growth)
```
Terminal Value = FCF_final x (1 + g) / (WACC - g)

Where:
  FCF_final = Last projected year's unlevered FCF
  g = Perpetuity growth rate (typically 2-3%, should not exceed long-term GDP growth)
  WACC = Weighted average cost of capital
```

**Sanity check**: The implied terminal multiple should be reasonable:
```
Implied Terminal EV/EBITDA = Terminal Value / Terminal Year EBITDA
```

### Method 2: Exit Multiple
```
Terminal Value = Terminal Year EBITDA x Exit EV/EBITDA Multiple

Where:
  Exit Multiple = Based on current trading multiples of comparable companies
  Typically use the median or mean of the comp set
```

**Sanity check**: The implied perpetuity growth rate should be reasonable:
```
Implied g = WACC - (FCF_final x (1 + g_implied)) / Terminal Value
```

### Best Practice
Calculate terminal value using BOTH methods and compare. If they diverge significantly, investigate why — it often indicates an assumption problem.

### Discounting Convention
- **Mid-year convention** (recommended): Assumes cash flows arrive mid-year, not year-end
  - Discount factor = 1 / (1 + WACC)^(n - 0.5) for year n
  - Terminal value discounted at the full year: 1 / (1 + WACC)^n
- **Year-end convention**: Discount factor = 1 / (1 + WACC)^n

State which convention is used. Mid-year is standard on Wall Street.

### Present Value Calculation
```
PV of Projected FCFs = sum of [FCFt / (1 + WACC)^(t - 0.5)]   [mid-year]
PV of Terminal Value = TV / (1 + WACC)^n

Enterprise Value = PV of Projected FCFs + PV of Terminal Value
```

## Enterprise to Equity Bridge

```
Enterprise Value (from DCF)
  (-) Total Debt (including capital leases)
  (-) Preferred Stock (at liquidation value)
  (-) Minority Interest (non-controlling interest)
  (+) Cash and Cash Equivalents
  (+) Non-Operating Assets (investments, excess real estate)
  (-) Unfunded Pension Obligations
  (-) Other EV Adjustments (environmental liabilities, litigation reserves)
= Equity Value

Implied Share Price = Equity Value / Diluted Shares Outstanding
```

### Diluted Shares
Use the Treasury Stock Method:
```
Diluted Shares = Basic Shares
  + In-the-Money Options (using TSM)
  + RSU/RSA Shares
  + Convertible Securities (if in-the-money)

TSM for Options:
  Shares from exercise = Number of options
  Proceeds = Number x Strike Price
  Shares repurchased = Proceeds / Current Share Price
  Net New Shares = Shares from exercise - Shares repurchased
```

## Sensitivity Analysis

### Required Sensitivities
1. **WACC vs. Perpetuity Growth Rate** — Implied share price (2-way table)
2. **WACC vs. Exit Multiple** — Implied share price (2-way table)
3. **Revenue Growth vs. EBITDA Margin** — Implied share price (if operating assumptions are uncertain)

### Formatting
- Apply conditional formatting (green/yellow/red gradient)
- Highlight the base case cell
- Include the current trading price for reference
- Label axes clearly

## Football Field Valuation

A football field chart consolidates multiple valuation methodologies into a single visual:

### Components (typical)
1. **52-Week Trading Range** — Historical share price range
2. **Analyst Price Targets** — Consensus range from sell-side
3. **DCF (Perpetuity Growth)** — Range from sensitivity table
4. **DCF (Exit Multiple)** — Range from sensitivity table
5. **Comparable Companies** — Implied range from comps
6. **Precedent Transactions** — Implied range from precedents
7. **LBO Analysis** — Price a PE buyer could pay at target returns

### Presentation
- Horizontal bar chart with min-max ranges for each methodology
- Vertical reference line at current trading price
- Base case marked within each range
- All values on consistent basis (per share or enterprise value)

## Common Mistakes to Avoid

1. **Double-counting**: Don't subtract debt in FCF AND in the EV-to-equity bridge
2. **Growth rate > WACC**: Terminal value formula breaks — g must be < WACC
3. **Inconsistent tax rates**: Use the same rate in NOPAT and WACC
4. **Ignoring NWC**: Growing companies need working capital investment
5. **Terminal value dominance**: If TV > 85% of EV, the projection period may be too short or growth assumptions too conservative in near-term
6. **Stale beta**: Use recent data and multiple comparables, not a single historical regression
7. **Circular references**: If interest expense affects FCF which affects debt which affects interest, handle explicitly

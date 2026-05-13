# LBO Model Reference

## Table of Contents
1. [Overview](#overview)
2. [Model Architecture](#model-architecture)
3. [Sources & Uses](#sources--uses)
4. [Operating Model](#operating-model)
5. [Debt Schedule](#debt-schedule)
6. [Returns Analysis](#returns-analysis)
7. [Sensitivity Tables](#sensitivity-tables)
8. [Advanced Features](#advanced-features)

## Overview

An LBO model determines the returns a financial sponsor (PE firm) can achieve by acquiring a company using a combination of equity and debt, improving operations over a hold period (typically 3-7 years), and exiting at a target multiple.

**Key outputs**: IRR, MOIC (Money-on-Money Multiple), equity check size, and implied returns under various scenarios.

**Core logic chain**: Entry Valuation -> Sources & Uses -> Operating Projections -> Free Cash Flow -> Debt Paydown -> Exit Valuation -> Returns Waterfall

## Model Architecture

### Sheet Structure (recommended tab order)

1. **Transaction Summary** — Entry price, capital structure, returns summary
2. **Assumptions** — All inputs: operating, financing, transaction, exit
3. **Sources & Uses** — How the deal is financed and where the money goes
4. **Income Statement** — Revenue through net income (historical + projected)
5. **Balance Sheet** — Pro forma opening B/S and projected periods
6. **Cash Flow Statement** — Operating, investing, financing, FCF
7. **Debt Schedule** — Each tranche: draws, repayments, balances, interest
8. **Returns Analysis** — IRR and MOIC at various exit years and multiples
9. **Sensitivity Tables** — 2-way tables on key return drivers

### Assumptions Sheet Layout

Group assumptions into clearly labeled sections:

```
TRANSACTION ASSUMPTIONS
  Purchase Price (EV)                    [blue font — input]
  Entry EV/EBITDA Multiple               [blue font — input]
  LTM EBITDA                            [blue font — input]
  Transaction Fees (% of EV)            [blue font — input]
  Financing Fees (% of debt)            [blue font — input]

CAPITAL STRUCTURE
  Senior Secured Term Loan (x EBITDA)   [blue font — input]
  Senior Unsecured Notes (x EBITDA)     [blue font — input]
  Mezzanine / Sub Debt (x EBITDA)       [blue font — input]
  Total Leverage (x EBITDA)             [black font — formula]
  Equity Contribution                    [black font — formula: residual]

OPERATING ASSUMPTIONS
  Revenue Growth Rate                    [blue font — input per year]
  EBITDA Margin                         [blue font — input per year]
  D&A (% of Revenue)                    [blue font — input]
  CapEx (% of Revenue)                  [blue font — input]
  Change in NWC (% of ΔRevenue)         [blue font — input]
  Tax Rate                              [blue font — input]

DEBT TERMS
  [Per tranche: rate, maturity, amortization %, mandatory sweep %]

EXIT ASSUMPTIONS
  Exit Year                             [blue font — input]
  Exit EV/EBITDA Multiple               [blue font — input]
```

## Sources & Uses

This is the opening balance of the deal — it must balance perfectly.

### Sources (where the money comes from)
- Revolving Credit Facility (usually undrawn at close)
- Term Loan A / Term Loan B
- Senior Notes / High Yield Bonds
- Mezzanine Debt / Subordinated Notes
- Seller Financing (if applicable)
- Sponsor Equity
- Management Rollover Equity (if applicable)

### Uses (where the money goes)
- Purchase of Equity (Enterprise Value - Existing Debt Assumed + Cash Acquired, or simply the equity purchase price)
- Refinancing of Existing Debt
- Transaction Fees (advisory, legal, accounting — typically 1-3% of EV)
- Financing Fees (underwriting, commitment — typically 2-4% of debt)
- Cash to Balance Sheet (minimum operating cash)

**Critical check**: Total Sources = Total Uses. Build this as a formula check row.

### Financing Fee Treatment
- Capitalize financing fees as a deferred asset on the balance sheet
- Amortize over the life of the associated debt tranche (straight-line)
- The amortization flows through the income statement as a non-cash expense
- Alternatively, net against debt balance (ASC 835-30) — state which convention is used

## Operating Model

### Income Statement Build
```
Revenue
  (-) COGS
= Gross Profit
  (-) SG&A
  (-) Other Operating Expenses
= EBITDA
  (-) D&A
= EBIT
  (-) Interest Expense [from debt schedule]
  (-) Amortization of Financing Fees
  (+/-) Other Income/Expense
= EBT (Pre-Tax Income)
  (-) Taxes
= Net Income
```

### Free Cash Flow Build
```
EBITDA
  (-) Cash Taxes [EBIT x Tax Rate, adjusted for NOLs if applicable]
  (-) CapEx
  (-) Change in Net Working Capital
  (-) Other Cash Items (one-time costs, etc.)
= Unlevered Free Cash Flow

OR

Net Income
  (+) D&A
  (+) Amortization of Financing Fees
  (-) CapEx
  (-) Change in Net Working Capital
= Levered Free Cash Flow (before debt service)
```

### Working Capital
Model NWC as percentage of revenue or as days outstanding:
- Accounts Receivable: DSO x Revenue / 365
- Inventory: DIO x COGS / 365
- Accounts Payable: DPO x COGS / 365
- Other current assets/liabilities as % of revenue

deltaWC = Current Period NWC - Prior Period NWC (increase in NWC is a cash outflow)

## Debt Schedule

Build a separate schedule for each debt tranche. Each schedule tracks:

```
Beginning Balance
  (+) New Borrowings
  (-) Mandatory Amortization (scheduled repayment %)
  (-) Cash Sweep (excess FCF applied to repayment)
  (-) Optional Prepayment
= Ending Balance

Interest Expense = Average Balance x Interest Rate
  (or Beginning Balance x Rate, depending on convention — state which)
```

### Debt Repayment Waterfall (priority order)
1. Mandatory amortization on Term Loan A (typically 1-5% per year)
2. Mandatory amortization on Term Loan B (typically 1% per year)
3. Cash sweep on senior secured debt (typically 50-75% of excess FCF)
4. Optional prepayment (if modeled)
5. Subordinated debt typically repaid at maturity (bullet)

### Cash Sweep Mechanics
```
Excess Cash Flow = Levered FCF - Mandatory Amortization - Minimum Cash Balance
Cash Sweep Amount = MAX(0, Excess Cash Flow x Sweep Percentage)
```

Apply sweep to the most senior outstanding tranche first.

### Handling Circularity
LBO models are inherently circular: Interest Expense -> Net Income -> Cash Flow -> Debt Paydown -> Debt Balance -> Interest Expense.

**Resolution options**:
1. **Iterative calculation**: Enable iterative calculation in Excel (preferred for accuracy)
2. **Average balance**: Interest = (Beginning + Ending Balance) / 2 x Rate (creates circularity)
3. **Beginning balance**: Interest = Beginning Balance x Rate (avoids circularity, slightly less accurate)
4. **Circular breaker**: Add a toggle cell (1/0) that turns circularity on/off for debugging

State which convention is used in the model.

## Returns Analysis

### Equity Value at Exit
```
Exit Enterprise Value = Exit Year EBITDA x Exit Multiple
  (-) Net Debt at Exit (total debt - cash at exit)
  (-) Transaction Fees at Exit (typically 1-2% of exit EV)
= Exit Equity Value
```

### IRR Calculation
Build cash flow timeline:
- Year 0: (-) Initial Equity Investment
- Years 1 to N-1: Dividends or recaps (if any, usually $0 in basic LBO)
- Year N: Exit Equity Proceeds

IRR = Rate that sets NPV of these cash flows to zero
In Excel: `=IRR(range)` or `=XIRR(values, dates)` for non-annual periods

### MOIC Calculation
```
MOIC = Total Cash Received / Total Cash Invested
     = Exit Equity Value / Initial Equity Check
```

If there are interim distributions (dividend recaps):
```
MOIC = (Exit Equity + Cumulative Distributions) / Initial Equity
```

### Returns Attribution (Value Creation Bridge)
Decompose returns into three drivers:

1. **EBITDA Growth**: (Exit EBITDA - Entry EBITDA) x Entry Multiple / Entry Equity
2. **Multiple Expansion**: (Exit Multiple - Entry Multiple) x Entry EBITDA / Entry Equity
3. **Debt Paydown**: (Entry Debt - Exit Debt) / Entry Equity
4. **FCF Generation**: Cumulative FCF retained / Entry Equity

Total Return = EBITDA Growth + Multiple Expansion + Debt Paydown + FCF Generation

## Sensitivity Tables

### Required Sensitivities
Every LBO should include at minimum:

1. **IRR sensitivity**: Entry Multiple vs. Exit Multiple (2-way)
2. **IRR sensitivity**: Exit Multiple vs. Exit Year (2-way)
3. **MOIC sensitivity**: Entry Multiple vs. EBITDA Growth Rate (2-way)
4. **Returns at various leverage levels** (optional but recommended)

### Format
Use Excel's DATA TABLE feature or build manually with OFFSET/INDEX formulas. Apply conditional formatting (green-yellow-red gradient) to highlight return thresholds:
- Green: IRR > 25% or MOIC > 3.0x (strong)
- Yellow: IRR 15-25% or MOIC 2.0-3.0x (acceptable)
- Red: IRR < 15% or MOIC < 2.0x (below threshold)

Adjust thresholds based on context (growth equity vs. traditional buyout).

## Advanced Features

### Dividend Recapitalization
Model a recap event where the company takes on additional debt to fund a distribution:
- New debt added to debt schedule
- Distribution reduces equity basis (improves MOIC and IRR)
- Model as a separate cash flow event in the returns timeline

### Management Equity / Option Pool
- Management typically receives 10-20% of equity through options or restricted shares
- Model using a waterfall: sponsor equity returns first, then management participates
- Include vesting schedule if relevant

### Add-On Acquisitions (Buy-and-Build)
- Model bolt-on acquisitions as separate cash outflows
- Funded by combination of excess cash, revolver draws, and incremental equity
- Consolidate into the operating model post-acquisition
- Track purchase multiples separately from platform

### PIK (Payment-in-Kind) Interest
- Interest accrues and compounds rather than being paid in cash
- PIK amount added to principal balance each period
- Increases total debt but preserves cash flow during hold period

### Tax Shield / NOL Utilization
- Step-up in asset basis from purchase price allocation (Section 338(h)(10) or asset deal)
- Additional D&A from stepped-up assets reduces taxable income
- Track NOL carryforwards separately, apply against taxable income with applicable limitations

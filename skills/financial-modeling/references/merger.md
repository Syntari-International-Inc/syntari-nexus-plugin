# M&A Merger Model & Accretion/Dilution Analysis

## Overview

A merger model projects the combined financial profile of an acquirer and target post-transaction. The primary output is whether the deal is **accretive** (increases EPS) or **dilutive** (decreases EPS) to the acquirer, and under what assumptions.

Secondary outputs: pro forma credit metrics, synergy requirements for breakeven, contribution analysis, and purchase price allocation.

---

## Part 1: Transaction Structure

### Step 1: Define the Offer

| Component | Description |
|---|---|
| Offer Price per Share | Premium over unaffected target share price |
| Offer Premium | Typically 20-40% over unaffected price; calculate over 1-day, 30-day, 60-day VWAP |
| Equity Value | Offer Price x Target Diluted Shares (TSM) |
| Transaction Enterprise Value | Equity Value + Target Net Debt + Minority Interest + Preferred - Cash |

### Step 2: Consideration Mix

Three types of deal currency:

| Type | Impact on Acquirer |
|---|---|
| **All Cash** | No dilution from new shares; increases debt/reduces cash; interest expense on new debt |
| **All Stock** | New shares issued -> dilution; no cash outlay; exchange ratio determines shares |
| **Mixed (Cash + Stock)** | Blend of both effects; most common structure |

**Exchange Ratio** (for stock deals):
```
Exchange Ratio = Offer Price per Target Share / Acquirer Share Price
New Shares Issued = Exchange Ratio x Target Diluted Shares Outstanding
```

### Step 3: Sources & Uses

| Sources | Uses |
|---|---|
| New debt raised | Equity value to target shareholders |
| Cash on hand (acquirer) | Refinance target's existing debt (if required) |
| New equity issued | Transaction fees (advisory, legal, financing) |
| Rollover equity (if applicable) | |
| **Total Sources** | **Total Uses** |

Sources must equal Uses.

---

## Part 2: Purchase Price Allocation (PPA)

Under ASC 805 (IFRS 3), the purchase price must be allocated to the target's net assets at fair value. The excess becomes goodwill.

### Calculation

```
Goodwill = Purchase Price (Equity Value)
         - Fair Value of Target's Net Tangible Assets
         - Fair Value of Identifiable Intangible Assets
         + Fair Value of Assumed Liabilities
```

**Key Intangibles to Identify**:
- Customer relationships (amortized over 5-15 years)
- Technology / patents (3-10 years)
- Trade names / brands (indefinite life if strong brand, or 5-20 years)
- Non-compete agreements (contract term)
- Backlog / contracts (contract term)

**Impact on Accretion/Dilution**: Intangible amortization is a real expense that reduces pro forma net income. Higher intangible write-ups -> more amortization -> more dilution.

### Asset Write-Up

If target's assets are written up to fair value:
```
Incremental D&A = (Fair Value of PP&E - Book Value of PP&E) / Useful Life
```

This incremental D&A also reduces pro forma income.

---

## Part 3: Synergies

### Revenue Synergies (harder to achieve, discount heavily)
- Cross-selling opportunities
- Market access / geographic expansion
- Pricing power from combined market share

**Modeling convention**: Phase in over 2-3 years. Discount by 50% or more vs. management projections.

### Cost Synergies (more reliable, model with higher confidence)
- Headcount reduction (overlapping functions)
- Facility consolidation
- Procurement savings / volume discounts
- Technology integration savings
- Elimination of redundant public company costs (if target is public)

**Modeling convention**: Phase in over 1-2 years. Apply a restructuring charge (typically 1-2x annual synergy value) as one-time cost.

### Synergy Waterfall

```
Gross Synergies (Annual, at full run-rate)
- Restructuring / Integration Costs (one-time, amortized or expensed)
- Cost to Achieve (ongoing costs to maintain synergies)
= Net Synergies

Phase-in Schedule:
  Year 1: 25-50% of run-rate
  Year 2: 75-100% of run-rate
  Year 3+: Full run-rate
```

### Tax Effect of Synergies

Cost synergies reduce pre-tax income -> apply tax rate to get after-tax impact:
```
After-Tax Synergy Impact = Pre-Tax Synergies x (1 - Tax Rate)
```

---

## Part 4: Pro Forma Income Statement

### Construction Logic

```
Pro Forma Revenue = Acquirer Revenue + Target Revenue + Revenue Synergies

Pro Forma EBITDA = Acquirer EBITDA + Target EBITDA + Cost Synergies

Pro Forma D&A = Acquirer D&A + Target D&A + Incremental D&A from Asset Write-Up + Amortization of Acquired Intangibles

Pro Forma EBIT = Pro Forma EBITDA - Pro Forma D&A

Pro Forma Interest Expense = Acquirer Interest + Target Interest (if debt assumed)
                           + Interest on New Acquisition Debt
                           - Interest Income Lost on Cash Used

Pro Forma Pre-Tax Income = Pro Forma EBIT - Pro Forma Interest Expense

Pro Forma Taxes = Pro Forma Pre-Tax Income x Blended Tax Rate

Pro Forma Net Income = Pro Forma Pre-Tax Income - Pro Forma Taxes
                     - Preferred Dividends (if any)
```

### Share Count

```
Pro Forma Diluted Shares = Acquirer Diluted Shares + New Shares Issued to Target Shareholders
```

### Accretion / Dilution

```
Acquirer Standalone EPS = Acquirer Net Income / Acquirer Diluted Shares

Pro Forma EPS = Pro Forma Net Income / Pro Forma Diluted Shares

Accretion / Dilution ($) = Pro Forma EPS - Acquirer Standalone EPS

Accretion / Dilution (%) = (Pro Forma EPS - Standalone EPS) / Standalone EPS
```

- **Accretive**: Pro Forma EPS > Standalone EPS -> positive signal
- **Dilutive**: Pro Forma EPS < Standalone EPS -> must be justified by strategic rationale or future synergies

### Breakeven Synergies Analysis

How much in synergies is required for the deal to be EPS-neutral?

```
Required Pre-Tax Synergies = Dilution in Net Income / (1 - Tax Rate)

Where:
Dilution in Net Income = (Standalone EPS x Pro Forma Shares) - Pro Forma Net Income (ex-synergies)
```

---

## Part 5: Pro Forma Credit Analysis

Lenders and rating agencies evaluate the combined entity's leverage and coverage:

| Metric | Formula | Typical Thresholds |
|---|---|---|
| Total Debt / EBITDA | Pro Forma Total Debt / Pro Forma EBITDA | IG: <3.0x; HY: 4-6x |
| Net Debt / EBITDA | (Total Debt - Cash) / EBITDA | IG: <2.5x; HY: 3-5x |
| Interest Coverage | EBITDA / Interest Expense | IG: >4.0x; HY: >2.0x |
| EBITDA - CapEx / Interest | (EBITDA - CapEx) / Interest | More conservative coverage |
| FCF / Total Debt | Levered FCF / Total Debt | Deleveraging capacity |

### Pro Forma Balance Sheet (Simplified)

```
Pro Forma Assets = Acquirer Assets + Target Assets (at FV) + Goodwill + Intangibles

Pro Forma Liabilities = Acquirer Liabilities + Target Liabilities + New Acquisition Debt

Pro Forma Equity = Pro Forma Assets - Pro Forma Liabilities
```

---

## Part 6: Contribution Analysis

Shows each party's relative contribution to the combined entity:

| Metric | Acquirer Contribution | Target Contribution | Implied Ownership |
|---|---|---|---|
| Revenue | X% | Y% | -- |
| EBITDA | X% | Y% | -- |
| Net Income | X% | Y% | -- |
| Total Assets | X% | Y% | -- |
| Equity Value (pre-deal) | X% | Y% | Should approximate exchange ratio |

**Key Insight**: If the target contributes 30% of EBITDA but gets 40% implied ownership (via premium), that gap must be justified by synergies, growth differential, or strategic value.

---

## Part 7: Sensitivity Analysis

### Standard Sensitivity Tables

**Table 1: Accretion/Dilution vs. Offer Premium and Synergies**
- Rows: Offer premium (20%, 25%, 30%, 35%, 40%)
- Columns: Annual synergies ($mm)
- Cell values: Accretion/dilution %

**Table 2: Accretion/Dilution vs. Consideration Mix**
- Rows: % Cash vs. % Stock (100/0, 75/25, 50/50, 25/75, 0/100)
- Columns: With/without synergies
- Cell values: Pro Forma EPS and accretion/dilution %

**Table 3: Pro Forma Leverage vs. Offer Price and Financing Mix**
- Rows: Offer price per share
- Columns: % debt financing
- Cell values: Pro Forma Debt/EBITDA

---

## Part 8: Special Considerations

### Stock-for-Stock Mechanics
- Exchange ratio can be **fixed** (set number of acquirer shares per target share) or **floating** (adjusts to deliver fixed dollar value)
- **Collar provisions**: Set min/max exchange ratios to protect both parties
- Acquirer share price movement between announcement and close creates risk

### Earnouts
- Portion of consideration contingent on target achieving post-close milestones
- Model as separate scenarios (earnout achieved vs. not achieved)
- Under ASC 805, earnout recorded at fair value on close, adjusted through income statement thereafter

### Tax Considerations
- **Tax-free reorganization** (stock deal): Target shareholders defer capital gains
- **Taxable transaction** (cash deal): Target shareholders recognize gain immediately
- **Asset deal vs. stock deal**: Asset deal gives buyer tax benefit of step-up in basis (higher D&A deductions); stock deal preserves target's existing tax basis
- **Section 338(h)(10) election**: Treats stock purchase as asset purchase for tax purposes

### Contingent Value Rights (CVRs)
- Additional consideration if certain events occur (FDA approval, revenue targets)
- Model as a probability-weighted expected value

---

## Part 9: Merger Model Construction

### Sheet Structure

| Tab | Contents |
|---|---|
| Summary | Key outputs — accretion/dilution, pro forma EPS, implied premium, credit metrics |
| Transaction | Sources & uses, offer terms, consideration mix |
| PPA | Purchase price allocation — goodwill, intangibles, asset write-ups |
| Synergies | Revenue and cost synergy build with phase-in schedule |
| Acquirer P&L | Standalone acquirer income statement |
| Target P&L | Standalone target income statement |
| Pro Forma P&L | Combined income statement with adjustments |
| Credit | Pro forma balance sheet and credit metrics |
| Sensitivity | Data tables on key variables |

### Key Formulas Reference

```
Offer Equity Value = Offer Price x Target Diluted Shares (TSM)
TEV = Offer Equity Value + Net Debt Assumed
Goodwill = TEV - FV of Net Assets Acquired
New Shares = (Stock % x Equity Value) / Acquirer Share Price
New Debt = Cash % x Equity Value + Refinanced Debt + Fees (debt portion)
Pro Forma Interest = Existing Interest + New Debt x Blended Rate
Accretion/Dilution = (PF EPS / Standalone EPS) - 1
Breakeven Synergies = EPS Dilution x PF Shares / (1 - Tax Rate)
```

### Circular Reference Note

Merger models can have circularity when interest expense depends on debt balance which depends on available cash flow which depends on interest expense. Handle the same way as LBO models:
- Enable iterative calculations in Excel (File > Options > Formulas > Enable iterative calculation)
- In openpyxl: break the circle with a prior-period approximation or use a convergence loop in Python

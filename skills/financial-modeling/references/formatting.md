# Wall Street Formatting Standards

## Overview

This reference defines the formatting standards that apply to every financial model built with this skill. These conventions are based on bulge bracket investment banking standards and ensure models are professional, auditable, and readable.

**This file should be read for every model build, regardless of model type.**

---

## 1. Font & Color Conventions

### Cell Font Colors (Non-Negotiable)

| Color | RGB | Hex | Meaning | Example |
|---|---|---|---|---|
| **Blue** | (0, 0, 255) | #0000FF | Hardcoded input / assumption | Revenue growth rate: 5.0% |
| **Black** | (0, 0, 0) | #000000 | Formula / calculated value | Revenue = Prior Year × (1 + Growth Rate) |
| **Green** | (0, 128, 0) | #008000 | Cross-sheet link (within workbook) | =Assumptions!B5 |
| **Red** | (255, 0, 0) | #FF0000 | External link (to another file) | =[MarketData.xlsx]Sheet1!A1 |

### openpyxl Implementation

```python
from openpyxl.styles import Font

FONT_INPUT = Font(name='Calibri', size=10, color='0000FF')      # Blue - inputs
FONT_FORMULA = Font(name='Calibri', size=10, color='000000')     # Black - formulas
FONT_LINK = Font(name='Calibri', size=10, color='008000')        # Green - cross-sheet
FONT_EXTERNAL = Font(name='Calibri', size=10, color='FF0000')    # Red - external links
FONT_HEADER = Font(name='Calibri', size=10, color='000000', bold=True)  # Headers
FONT_SECTION = Font(name='Calibri', size=11, color='000000', bold=True) # Section titles
```

### Background Colors

| Color | Hex | Use Case |
|---|---|---|
| **Light yellow** | #FFFFC0 | Input cells (optional highlight for key assumptions) |
| **Light gray** | #F2F2F2 | Alternating row shading for readability |
| **Light blue** | #DCE6F1 | Headers and section labels |
| **White** | #FFFFFF | Formula cells (default) |
| **No fill** | — | Blank/spacer rows |

```python
from openpyxl.styles import PatternFill

FILL_INPUT = PatternFill(start_color='FFFFC0', end_color='FFFFC0', fill_type='solid')
FILL_HEADER = PatternFill(start_color='DCE6F1', end_color='DCE6F1', fill_type='solid')
FILL_ALT_ROW = PatternFill(start_color='F2F2F2', end_color='F2F2F2', fill_type='solid')
```

---

## 2. Number Formatting

### Standard Formats

| Data Type | Format Code | Example Output | Notes |
|---|---|---|---|
| Currency ($mm) | `#,##0` | 1,234 | Units in header, not in cells |
| Currency ($mm, 1 dec) | `#,##0.0` | 1,234.5 | For precision when needed |
| Currency ($000) | `#,##0` | 1,234 | Same format, units in header |
| Currency (per share) | `$#,##0.00` | $12.50 | Always 2 decimals for per-share |
| Percentages | `0.0%` | 5.0% | One decimal default |
| Percentages (precise) | `0.00%` | 5.25% | Interest rates, WACC components |
| Multiples | `0.0x` | 8.5x | EV/EBITDA, Debt/EBITDA, etc. |
| Shares (millions) | `#,##0.0` | 125.3 | Units in header |
| Years | `0` | 2024 | Plain integer, no comma separator |
| Dates | `MM/DD/YYYY` | 01/15/2024 | Standard US format |
| Basis points | `#,##0` | 250 | With "bps" in header |

### Special Formats

**Negative Numbers**: Use parentheses, not minus sign:
```
Format: #,##0;(#,##0)
Result: 1,234 or (1,234)
```

**Zeros as Dashes**: Display zero values as a centered dash:
```
Format: #,##0;(#,##0);"-"
Result: 1,234 or (1,234) or -
```

**Full Format with Dash for Zero** (currency):
```
Format: $#,##0;($#,##0);"-"
```

### openpyxl Number Format Implementation

```python
FMT_CURRENCY = '#,##0'
FMT_CURRENCY_1D = '#,##0.0'
FMT_PER_SHARE = '$#,##0.00'
FMT_PCT = '0.0%'
FMT_PCT_PRECISE = '0.00%'
FMT_MULTIPLE = '0.0"x"'
FMT_YEAR = '0'
FMT_NEG_PARENS = '#,##0;(#,##0);"-"'
FMT_CURRENCY_PARENS = '$#,##0;($#,##0);"-"'
```

---

## 3. Cell & Layout Standards

### Column Widths

| Column Type | Width | Examples |
|---|---|---|
| Row labels (Col A) | 35-45 | Line item descriptions |
| Spacer columns | 2-3 | Visual separation between sections |
| Data columns | 12-15 | Financial data |
| Year headers | 12-15 | FY2022A, FY2023E |

### Row Heights
- Standard data rows: 15 (default)
- Section headers: 18-20
- Major section breaks: 6-8 (blank spacer rows)

### Freeze Panes
Always freeze:
- **Row freeze**: Below column headers (row 3 or 4 typically)
- **Column freeze**: After row labels (column B typically)

```python
ws.freeze_panes = 'B4'  # Freezes column A and rows 1-3
```

### Alignment

| Element | Horizontal | Vertical |
|---|---|---|
| Row labels | Left | Center |
| Column headers | Center | Center |
| Numbers | Right | Center |
| Percentages | Right | Center |
| Section titles | Left | Center |

```python
from openpyxl.styles import Alignment

ALIGN_LABEL = Alignment(horizontal='left', vertical='center')
ALIGN_HEADER = Alignment(horizontal='center', vertical='center', wrap_text=True)
ALIGN_NUMBER = Alignment(horizontal='right', vertical='center')
```

---

## 4. Border Standards

### Standard Borders

| Location | Style | When to Use |
|---|---|---|
| Below column headers | Medium bottom border | Always |
| Below section subtotals | Thin bottom border | Subtotals (e.g., Total Revenue) |
| Below grand totals | Double bottom border | Grand totals (e.g., Net Income, Total EV) |
| Above/below key outputs | Medium top + bottom | IRR, MOIC, implied valuation |
| Right of label column | Thin right border | Separates labels from data (optional) |

### openpyxl Border Implementation

```python
from openpyxl.styles import Border, Side

BORDER_THIN_BOTTOM = Border(bottom=Side(style='thin'))
BORDER_MEDIUM_BOTTOM = Border(bottom=Side(style='medium'))
BORDER_DOUBLE_BOTTOM = Border(bottom=Side(style='double'))
BORDER_HEADER = Border(bottom=Side(style='medium'))

BORDER_TOTAL = Border(
    top=Side(style='thin'),
    bottom=Side(style='double')
)
```

---

## 5. Sheet Organization

### Naming Conventions

| Tab Name | Use |
|---|---|
| Summary | Executive summary and key outputs |
| Assumptions | All hardcoded inputs |
| IS or P&L | Income statement |
| BS | Balance sheet |
| CF or CFS | Cash flow statement |
| Debt Schedule | Debt amortization and interest |
| WC Schedule | Working capital build |
| Depr Schedule | Depreciation and amortization |
| DCF | Discounted cash flow valuation |
| Comps | Comparable company analysis |
| LBO Returns | LBO returns analysis |
| Sensitivity | Sensitivity and scenario tables |

### Tab Colors

```python
# Color-code tabs by function
ws_assumptions.sheet_properties.tabColor = '0000FF'    # Blue - inputs
ws_is.sheet_properties.tabColor = '000000'             # Black - financials
ws_bs.sheet_properties.tabColor = '000000'
ws_cf.sheet_properties.tabColor = '000000'
ws_dcf.sheet_properties.tabColor = '008000'            # Green - valuation
ws_sensitivity.sheet_properties.tabColor = 'FF8C00'    # Orange - analysis
ws_summary.sheet_properties.tabColor = 'FF0000'        # Red - key outputs
```

### Print Setup

```python
from openpyxl.worksheet.page import PrintPageSetup

ws.page_setup.orientation = 'landscape'
ws.page_setup.paperSize = ws.PAPERSIZE_LETTER
ws.page_setup.fitToWidth = 1
ws.page_setup.fitToHeight = 0  # As many pages as needed vertically
ws.sheet_properties.pageSetUpPr.fitToPage = True
ws.print_title_rows = '1:3'     # Repeat header rows on every printed page
ws.print_title_cols = 'A:A'     # Repeat label column on every printed page
```

---

## 6. Headers and Labeling

### Column Headers

Row 1: Model title and date
Row 2: Section label (e.g., "Income Statement", "($mm)")
Row 3: Period labels (FY2022A, FY2023A, FY2024E, FY2025E, ...)

**Period label format**:
- Historical: `FY2022A` or `CY2022A` (A = Actual)
- Projected: `FY2024E` or `CY2024E` (E = Estimated)
- Quarterly: `Q1'24A`, `Q2'24E`
- LTM: `LTM 9/30/24`

**Units**: Always specify units in the section header, not in individual cells:
- `Revenue ($mm)` not `$1,234mm` in each cell
- `Margin (%)` not `45.0% margin` in each cell

### Row Labels

- Use clear, descriptive labels: "Total Revenue" not "Rev"
- Indent sub-items with 2-space indentation per level
- Use consistent naming across all sheets
- Include blank spacer rows between major sections (height 6-8)

### Section Labels

Major section labels should be:
- Bold
- Slightly larger font (11pt vs 10pt)
- Left-aligned
- Background color fill (light blue #DCE6F1)
- Span merged across the data columns for section headers

---

## 7. Sensitivity Table Formatting

### Two-Way Data Table Layout

```
              Input Variable 2 →
              Val_A   Val_B   Val_C   Val_D   Val_E
Input    Val_1  [x]    [x]    [x]    [x]    [x]
Var 1 →  Val_2  [x]    [x]    [x]    [x]    [x]
         Val_3  [x]    [x]    [x]    [x]    [x]
         Val_4  [x]    [x]    [x]    [x]    [x]
         Val_5  [x]    [x]    [x]    [x]    [x]
```

- Top-left corner cell: contains the output formula reference
- Row headers (left): values for variable 1
- Column headers (top): values for variable 2
- Body: computed output values

### Conditional Formatting (Heat Map)

Apply color gradient to sensitivity table body:

```python
from openpyxl.formatting.rule import ColorScaleRule

rule = ColorScaleRule(
    start_type='min', start_color='FF6B6B',       # Red - worst
    mid_type='percentile', mid_value=50, mid_color='FFFFCC',  # Yellow - mid
    end_type='max', end_color='66CC66'             # Green - best
)
ws.conditional_formatting.add('C5:G9', rule)
```

For IRR/MOIC tables: Green = high returns, Red = low returns
For leverage tables: Green = low leverage, Red = high leverage
For accretion/dilution: Green = accretive, Red = dilutive

### Highlight the Base Case

Bold the row and column corresponding to the base case assumptions. Or apply a distinct border around the base case cell.

---

## 8. Chart Standards

### Color Palette (Professional)

| Use | Color | Hex |
|---|---|---|
| Primary series | Navy blue | #003366 |
| Secondary series | Medium blue | #4472C4 |
| Tertiary series | Steel blue | #8DB4E2 |
| Accent / highlight | Dark red | #C00000 |
| Positive values | Forest green | #548235 |
| Negative values | Dark red | #C00000 |
| Background | White | #FFFFFF |

### Chart Guidelines
- Title: Bold, 12pt, centered above chart
- Axis labels: 9pt, clear units
- Legend: Bottom or right, 9pt
- Gridlines: Light gray, horizontal only
- No 3D effects
- No chart junk or decorative elements
- Data labels only when they add clarity (not on every point)

---

## 9. Model Documentation

### Cover / Title Page

Every model should include:
- Company name / project name
- Model type (LBO, DCF, Merger, Comps)
- Prepared by / date
- Version number
- Key assumptions summary (3-5 lines)
- Disclaimer / confidentiality notice

### Revision Log

Track changes in a dedicated section or tab:

| Date | Author | Description |
|---|---|---|
| 01/15/2024 | Analyst | Initial model build |
| 01/20/2024 | VP | Updated revenue assumptions per mgmt call |
| 02/01/2024 | MD | Final IC version |

### Named Ranges

Use named ranges for key assumptions to improve auditability:

```python
from openpyxl.workbook.defined_name import DefinedName

wb.defined_names.new('entry_multiple', attr_text="Assumptions!$B$5")
wb.defined_names.new('exit_multiple', attr_text="Assumptions!$B$6")
wb.defined_names.new('wacc', attr_text="Assumptions!$B$10")
wb.defined_names.new('tax_rate', attr_text="Assumptions!$B$12")
```

---

## 10. Quality Checklist

Before delivering any model, verify:

**Structure**
- [ ] All inputs are blue font and consolidated on Assumptions tab
- [ ] All formulas are black font (or green for cross-sheet)
- [ ] No hardcoded values inside formulas
- [ ] Sheet tabs are logically ordered and color-coded
- [ ] Freeze panes applied correctly

**Accuracy**
- [ ] Zero formula errors (#REF!, #DIV/0!, #VALUE!, etc.)
- [ ] Balance sheet balances in every period (Assets = L + E)
- [ ] Cash flow statement reconciles to change in B/S cash
- [ ] Circular references handled properly (if applicable)
- [ ] Model tested with extreme assumptions (no broken formulas)

**Formatting**
- [ ] Column widths are consistent and readable
- [ ] Number formats applied correctly (currency, %, multiples)
- [ ] Borders applied to headers, subtotals, and grand totals
- [ ] Section spacing is clean (blank rows between sections)
- [ ] Print setup configured (landscape, fit to width, repeat headers)

**Documentation**
- [ ] Cover page or summary tab with key outputs
- [ ] Assumptions are clearly labeled with sources
- [ ] Sensitivity tables included on key drivers
- [ ] Named ranges for critical assumptions

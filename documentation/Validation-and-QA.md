# Validation and QA

## Executive Business Performance Dashboard

This document summarises the validation and quality-assurance approach applied to the Executive Business Performance Dashboard before final publication.

The objective of QA was to verify not only individual KPI calculations, but also target behaviour, time intelligence, filter context, visual interactions, drill-through behaviour and overall report usability.

---

# 1. Validation Scope

Testing covered the following areas:

- Base KPI calculations
- Financial arithmetic
- Time-intelligence calculations
- Actual-versus-target calculations
- Target granularity
- Regional and channel filtering
- Unsupported target contexts
- Report filters and slicers
- Cross-filter interactions
- Drill-through behaviour
- Navigation
- Conditional formatting
- Visual consistency
- Report performance
- Data refresh

The final report passed the defined QA checks before portfolio publication.

---

# 2. Base KPI Validation

Core business measures were reconciled before validating higher-level calculations.

Measures reviewed included:

- Revenue
- Cost
- Gross Profit
- Gross Margin
- Orders
- Active Customers
- Average Order Value

## Gross Profit

The relationship:

Gross Profit = Revenue - Cost

was validated using underlying unrounded values.

## Gross Margin

The relationship:

Gross Margin = Gross Profit / Revenue

was validated.

For the 2025 company-level reporting context, the dashboard showed approximately:

- Revenue: £18.53M
- Gross Profit: £5.04M
- Gross Margin: 27.20%

The displayed values reconcile after accounting for report rounding.

## Average Order Value

The relationship:

Average Order Value = Revenue / Orders

was validated.

For 2025:

- Revenue: approximately £18.53M
- Orders: approximately 13.22K
- Average Order Value: approximately £1.40K

---

# 3. Time-Intelligence Validation

Prior-year and year-on-year calculations were tested across multiple reporting years.

## 2025

2025 measures were validated against 2024.

Key company-level results included approximately:

- Revenue YoY: +5.04%
- Gross Profit YoY: +3.33%
- Gross Margin YoY Change: -0.45 percentage points

## 2024

2024 prior-year calculations were validated against 2023.

Measures tested included:

- Revenue PY
- Revenue YoY
- Gross Profit PY
- Gross Profit YoY
- Gross Margin PY
- Gross Margin YoY Change
- Orders YoY
- Active Customers YoY
- Average Order Value YoY

## 2023 Edge Case

The dataset begins in 2023.

Therefore, 2023 has no 2022 comparison period.

Expected behaviour was confirmed:

- Current-period KPIs calculate normally
- Prior-year measures return blank
- YoY measures return blank
- Margin YoY Change returns blank

The solution deliberately preserves blanks rather than converting unavailable comparisons into zero.

A zero could incorrectly imply that performance was unchanged.

---

# 4. Target Validation

Revenue, Gross Profit and Gross Margin target calculations were validated.

For the 2025 company-level context, the dashboard showed approximately:

- Revenue vs Target: -2.71%
- Profit vs Target: -6.61%
- Gross Margin vs Target: -1.14 percentage points

## Revenue Variance

The following relationship was validated:

Revenue Variance = Revenue - Revenue Target

Revenue vs Target % = Revenue Variance / Revenue Target

## Profit Variance

The following relationship was validated:

Profit Variance = Gross Profit - Profit Target

Profit vs Target % = Profit Variance / Profit Target

## Gross Margin Target

Target Gross Margin was derived from:

Target Gross Margin = Profit Target / Revenue Target

Gross Margin variance was interpreted as a percentage-point difference rather than percentage growth.

---

# 5. Regional Target Validation

Regional target behaviour was validated for all Regions.

For 2025, Revenue target performance included approximately:

| Region | Revenue vs Target |
|---|---:|
| Scotland | +3.31% |
| Midlands | +1.16% |
| South East | +0.55% |
| North | -5.50% |
| South West | -5.61% |
| London | -6.88% |

This provided both positive and negative test cases for exception logic.

Regional target totals were also checked against the corresponding company-level target context.

---

# 6. Target Granularity Validation

Target granularity received specific QA attention because the Actual and Target datasets do not support identical analytical dimensions.

Targets support valid comparison through dimensions including:

- Time
- Region
- Channel

## Supported Context Tests

Target calculations were tested under:

- Company level
- Individual Region
- Individual Channel
- Region + Channel
- Monthly context

Targets continued to calculate under these supported contexts.

## Unsupported Product Category Context

Product Category is not part of the target grain.

A validation table was used to test:

- Product Category
- Revenue
- Revenue Target Valid
- Revenue vs Target % Valid

Expected behaviour:

- Actual Revenue continues to calculate
- Target-safe measures return blank

This behaviour was confirmed.

The model therefore avoids artificially distributing company, regional or channel targets across Product Categories.

---

# 7. Target Context Diagnostics

Dedicated validation measures were retained in the semantic model, including:

- Target Context Valid
- Target Rows
- Target Min Region Key
- Target Max Region Key

These measures were used during development to diagnose target filtering and relationship behaviour.

The validation measures remain in the PBIX for maintainability but are not exposed as executive KPIs.

---

# 8. Filter and Slicer Validation

Report filters and slicers were tested across the main report pages.

Testing included:

- Year selection
- Region selection
- Channel selection
- All-value states
- Synced filter behaviour
- Clear-selection behaviour

The Filters pane was also inspected for unintended:

- Visual-level filters
- Page-level filters
- Report-level filters

This helped ensure that no hidden filter context was unintentionally affecting report results.

---

# 9. Executive Overview QA

The Executive Overview was tested under multiple contexts, including:

- 2025 — All Regions
- 2025 — London
- 2025 — Scotland
- 2024
- 2023

The following components were reviewed:

- Revenue KPI
- Gross Profit KPI
- Gross Margin KPI
- Monthly Revenue vs Target
- Revenue Performance by Region
- Orders
- Active Customers
- Average Order Value
- Management Insight

The page responded correctly to supported filter changes.

---

# 10. Performance Analysis QA

The Performance Analysis page was tested using different:

- Years
- Regions
- Channels

Components reviewed included:

- KPI cards
- Revenue Growth Trend
- Channel Performance
- Revenue by Product Category
- Business Driver measures

Special attention was given to 2023, where YoY comparisons correctly return blank due to the absence of 2022 data.

---

# 11. Exceptions & Management Attention QA

The exception page was tested across multiple Year and reporting contexts.

Components reviewed included:

- Regions Requiring Attention
- Regions Below Revenue Target
- Regions Below Profit Target
- Regional Performance & Exceptions
- Category Growth & Margin Exceptions
- Selected Region Revenue vs Target

Regional selections were tested to confirm that supporting analysis responded correctly.

---

# 12. Cross-Filter Interaction Validation

Visual interactions were not assumed to be valid simply because Power BI allowed them.

They were configured according to analytical context.

## Region to Category

Enabled.

This supports questions such as:

> Which Product Categories are contributing to performance within this Region?

## Category to Target-Based Regional Analysis

Restricted.

Product Category is outside the target grain. Allowing Category selections to redefine target-based regional visuals could create unsupported comparisons.

## Channel to Category

Enabled where analytically appropriate.

Channel belongs to the supported commercial reporting context.

## Category to Target-Containing Visuals

Restricted where required.

This asymmetric interaction design preserves analytical validity while retaining useful exploration.

---

# 13. Drill-Through Validation

The Region Performance Detail page was tested through drill-through from the exception analysis.

Tests included:

- London — 2025
- Scotland — 2025
- Region + Channel context
- 2024
- 2023

Validation confirmed that:

- The selected Region was preserved
- Year context was retained
- Channel context was retained where applicable
- Dynamic Region title updated correctly
- Regional KPI values recalculated
- Monthly Revenue vs Target recalculated
- Channel analysis recalculated
- Category analysis recalculated
- Back navigation returned the user to the originating context

The drill-through page is hidden from normal report navigation.

---

# 14. Navigation Validation

Primary navigation was tested between:

- Executive Overview
- Performance Analysis
- Exceptions & Detail

The following analytical journey was also tested:

Executive Overview  
→ Performance Analysis  
→ Exceptions & Detail  
→ Region Drill-Through  
→ Back

Navigation buttons and active-page states were reviewed for consistency.

---

# 15. Conditional Formatting Validation

Conditional formatting rules were reviewed against underlying numeric values rather than formatted display text.

Examples included:

## Revenue and Profit Growth

- Negative values identified as negative performance
- Positive values identified as positive performance

## Margin YoY Change

Margin movement was validated using underlying decimal values.

For example:

-0.005 = -0.5 percentage points

This distinction was important when configuring tolerance thresholds.

## Target Variance

Positive and negative target performance was checked against actual measure results to ensure colours and statuses reflected the underlying values correctly.

---

# 16. Executive Classification Validation

Business classifications were reviewed against their underlying quantitative measures.

Examples included:

- Growth Quality
- Management Attention Status
- Overall Target Position
- Revenue Target Status
- Profit Target Status
- Gross Margin Trend Status

This ensured that management-friendly labels remained explainable through the underlying KPIs.

---

# 17. Category Exception Validation

The 2025 Category exception analysis produced the following validated results:

| Category | Revenue YoY | Profit YoY | Gross Margin | Margin YoY Change | Growth Quality |
|---|---:|---:|---:|---:|---|
| Facilities | +6.05% | +4.42% | 34.93% | -0.55pp | Growth with Margin Pressure |
| Office Supplies | +9.59% | +7.68% | 26.17% | -0.46pp | Growth with Margin Pressure |
| Technology | +2.93% | -0.19% | 17.34% | -0.54pp | Revenue Growth, Profit Decline |
| Workplace Equipment | +5.34% | +3.65% | 31.97% | -0.52pp | Growth with Margin Pressure |

These results were reviewed against the Growth Quality classifications.

Technology provided an important negative-profit-growth test case despite positive Revenue growth.

---

# 18. Formatting and UX QA

The final presentation review covered:

- Consistent page navigation
- KPI alignment
- Visual spacing
- Typography
- Number formatting
- £M / £K notation
- Percentage formatting
- Percentage-point notation
- Visual titles
- Business-facing column names
- Removal of technical labels from executive-facing visuals
- Visual-header clutter
- Conditional-formatting consistency

Terminology was standardised around:

- Revenue
- Gross Profit
- Gross Margin
- Revenue YoY
- Profit YoY
- Revenue vs Target
- Profit vs Target
- Margin YoY Change

---

# 19. Accessibility Review

Accessibility considerations included:

- Clear visual titles
- Supporting text labels
- Meaningful Alt text
- Logical visual hierarchy
- Restrained use of colour
- Avoiding reliance on colour alone for interpretation
- Review of tab order
- Executive Overview consideration for mobile consumption

---

# 20. Performance Review

Power BI Performance Analyzer was used during final QA to review report behaviour.

The purpose was to identify:

- Unusually slow visuals
- Expensive DAX queries
- Excessive visual load
- Potential performance anomalies

No fabricated performance-improvement percentage is reported because the project did not establish a controlled before-and-after performance benchmark.

---

# 21. Refresh Validation

A final report refresh was completed after validation.

The refresh was checked for:

- Query errors
- Relationship errors
- Broken measures
- Missing data
- Visual errors

The final PBIX was saved after successful validation.

---

# 22. Final QA Outcome

The completed solution passed the project QA checklist covering:

- Base calculations
- Financial reconciliation
- Time intelligence
- Target calculations
- Target totals
- Target granularity
- Supported and unsupported filter contexts
- Report-page behaviour
- Cross-filter interactions
- Drill-through
- Navigation
- Conditional formatting
- Executive classifications
- Formatting
- Accessibility considerations
- Performance review
- Refresh

The validation approach was designed to confirm both numerical correctness and analytical validity.

A technically correct DAX result was not considered sufficient if the business comparison itself was unsupported by the underlying data grain.

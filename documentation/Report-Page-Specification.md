# Report Page Specification

## Executive Business Performance Dashboard

This document defines the purpose, content, analytical role and interaction design of each report page within the Executive Business Performance Dashboard.

The report was designed around a progressive executive reporting journey:

**Monitor → Analyse → Identify Exceptions → Investigate**

Rather than placing all available metrics on a single dashboard, each page has a distinct management purpose.

---

# 1. Executive Overview

## Purpose

Provide senior management with a concise view of overall business performance and highlight areas requiring attention.

The page is designed to answer:

> How is the business performing, and is anything significant requiring management attention?

## Primary Audience

- CEO / Managing Director
- Finance leadership
- Sales leadership
- Senior management

## Primary KPIs

- Revenue
- Revenue YoY
- Revenue vs Target
- Gross Profit
- Gross Profit YoY
- Profit vs Target
- Gross Margin
- Gross Margin YoY Change
- Gross Margin vs Target
- Orders
- Active Customers
- Average Order Value

## Main Visuals

### Executive KPI Cards

Three primary KPI cards present:

- Revenue
- Gross Profit
- Gross Margin

Supporting comparisons provide year-on-year and target context.

### Monthly Revenue vs Target

Line chart comparing monthly actual Revenue with Revenue Target.

**Purpose:**

Identify whether annual target performance reflects a persistent trend or specific periods of over- or under-performance.

### Revenue Performance by Region

Regional comparison based on Revenue variance against target.

Positive and negative performance is visually distinguished using conditional formatting.

**Purpose:**

Allow management to identify regional outperformance and underperformance quickly.

### Business Drivers

Supporting cards display:

- Orders
- Active Customers
- Average Order Value

These provide context behind headline Revenue performance.

### Management Insight

A dynamic executive headline summarises the overall business situation.

Example:

> Revenue is growing, but margin pressure and target underperformance require attention.

## Filters

- Region
- Year

## Key Management Questions

- Is Revenue growing?
- Is Gross Profit keeping pace with Revenue?
- Is Gross Margin improving or deteriorating?
- Is the business meeting Revenue and Profit targets?
- Which Regions are above or below plan?
- What commercial activity is supporting Revenue performance?

---

# 2. Performance Analysis

## Purpose

Explain the commercial and profitability drivers behind the headline executive results.

The page answers:

> What is driving the performance shown on the Executive Overview?

## Primary Audience

- Finance leadership
- Sales leadership
- Commercial management
- Business analysts

## Primary KPIs

- Revenue
- Gross Profit
- Gross Margin
- Orders

## Main Visuals

### Revenue Growth Trend

Monthly Revenue YoY trend.

**Purpose:**

Shows how growth changes throughout the selected year rather than relying only on the annual YoY result.

### Channel Performance

Matrix comparing sales channels using measures such as:

- Revenue
- Revenue YoY
- Gross Profit
- Gross Margin
- Orders
- Average Order Value

**Purpose:**

Identify differences in commercial scale, growth, profitability and transaction behaviour across routes to market.

### Revenue by Product Category

Horizontal bar chart showing Revenue contribution by Product Category.

**Purpose:**

Shows which product categories contribute most heavily to Revenue within the selected reporting context.

### Business Drivers

Supporting KPI cards include:

- Orders
- Orders YoY
- Active Customers
- Active Customers YoY
- Average Order Value
- Average Order Value YoY

**Purpose:**

Helps distinguish between growth associated with transaction volume, customer activity and transaction value.

## Filters

- Region
- Channel
- Year

## Key Management Questions

- Is Revenue growth consistent throughout the year?
- Which channels generate the most Revenue?
- Which channels are growing fastest?
- How do profitability profiles differ between channels?
- Which Product Categories contribute most Revenue?
- Is commercial growth associated with more Orders, more Customers or higher Average Order Value?

---

# 3. Exceptions & Management Attention

## Purpose

Identify areas of material underperformance and support focused management investigation.

The page answers:

> Where should management focus its attention?

Unlike the first two pages, this page is intentionally more analytical and exception-led.

## Primary Audience

- Senior management
- Finance leadership
- Regional leadership
- Commercial management
- Business analysts

## Exception Summary KPIs

- Regions Requiring Attention
- Regions Below Revenue Target
- Regions Below Profit Target

## Main Visuals

### Regional Performance & Exceptions

Regional matrix containing:

- Revenue
- Revenue YoY
- Revenue vs Target
- Gross Profit
- Profit vs Target
- Gross Margin
- Margin YoY Change
- Management Attention Status

**Purpose:**

Provides a consolidated regional view of growth, target performance and profitability.

Conditional formatting helps surface material exceptions without requiring management to interpret every value manually.

### Category Growth & Margin Exceptions

Category-level matrix containing:

- Revenue YoY
- Profit YoY
- Gross Margin
- Margin YoY Change
- Growth Quality

**Purpose:**

Identifies situations where Revenue growth may conceal weaker profitability.

Target measures are deliberately excluded because Product Category is not part of the target grain.

### Selected Region — Revenue vs Target

Monthly Revenue and Revenue Target trend.

**Purpose:**

Allows users to select a Region from the exception matrix and determine whether its target performance is persistent or concentrated in specific months.

## Filters

- Region
- Year

## Interaction Design

Selecting a Region filters the supporting Category and monthly analysis.

This enables the workflow:

**Identify Region → Investigate Category Performance → Review Monthly Pattern**

Interactions involving Product Category and target-based regional visuals are deliberately restricted where the target context would be unsupported.

## Key Management Questions

- Which Regions require attention?
- Which Regions are below Revenue plan?
- Which Regions are below Profit plan?
- Is underperformance associated with growth, profitability or both?
- Which categories show margin pressure?
- Are there categories where Revenue is growing while Profit declines?
- Is regional underperformance persistent across the year?

---

# 4. Region Performance Detail

## Page Type

Drill-through page.

## Purpose

Provide detailed investigation of an individual Region selected from the exception analysis.

The page answers:

> What is driving performance within this specific Region?

## Access

Users access the page by drilling through from a Region in the Exceptions & Management Attention page.

The page is hidden from normal report navigation.

## Context

The drill-through preserves relevant reporting context including:

- Region
- Year
- Channel where applicable

## Dynamic Page Title

The page title reflects the selected Region.

Example:

> London Performance Detail

## Primary KPIs

- Revenue
- Revenue vs Target
- Gross Profit
- Profit vs Target
- Gross Margin
- Gross Margin YoY Change
- Orders
- Orders YoY

## Main Visuals

### Monthly Revenue vs Target

Compares actual monthly Revenue against plan for the selected Region.

**Purpose:**

Determines when regional target performance occurred during the reporting period.

### Channel Performance

Compares channel-level commercial and profitability performance within the selected Region.

**Purpose:**

Identifies whether regional performance differs by route to market.

### Revenue by Product Category

Shows category Revenue contribution within the selected Region.

**Purpose:**

Provides additional commercial context without introducing unsupported category-level target allocation.

### Commercial Drivers

Supporting measures include:

- Active Customers
- Active Customers YoY
- Average Order Value
- Average Order Value YoY

## Interaction Design

Channel selections may filter:

- Monthly trend
- Category analysis
- commercial measures

Category interactions with target-containing visuals are restricted where necessary to preserve valid target context.

## Navigation

A Back button returns the user to the originating report page while preserving the previous analytical context.

---

# 5. DEV Validation

## Page Type

Hidden technical QA page.

## Purpose

Provide a controlled environment for validating:

- base KPI calculations
- prior-year calculations
- target calculations
- regional target filtering
- target-context behaviour
- KPI classifications
- management-attention logic

The page is retained inside the PBIX for maintainability and technical review but is hidden from report consumers.

---

# Navigation Architecture

The primary report navigation follows:

**Executive Overview → Performance Analysis → Exceptions & Detail**

Users can then move from:

**Exceptions & Detail → Region Performance Detail**

through drill-through.

This creates the analytical journey:

1. Understand overall business health
2. Explore performance drivers
3. Identify material exceptions
4. Investigate a specific Region

---

# Interaction Design Principles

## Deliberate Cross-Filtering

Visual interactions were configured according to analytical validity rather than allowing every visual to filter every other visual.

For example:

**Region → Category**

is analytically useful because users can investigate category performance within a Region.

However:

**Category → target-based Regional comparison**

is restricted because Product Category is not part of the target grain.

This prevents unsupported target comparisons from appearing in the report.

---

# Visual Design Principles

The report follows several presentation principles:

## KPI Hierarchy

Headline financial KPIs receive greater visual prominence than supporting operational measures.

## Limited Visual Count

Pages contain a small number of purposeful visuals rather than maximising chart density.

## Consistency

Navigation, typography, spacing, KPI presentation and terminology are kept consistent across pages.

## Exception Visibility

Conditional formatting is used where it supports decision-making, particularly for target and profitability exceptions.

## Accessible Interpretation

Colour is used as a supporting signal rather than the sole mechanism for communicating business meaning.

## Executive Language

Technical measure names are replaced with concise business-facing labels within report visuals.

---

# Mobile Consideration

The Executive Overview was considered separately for mobile consumption.

The mobile experience prioritises:

1. Headline financial KPIs
2. Management insight
3. Revenue trend
4. Regional performance
5. Supporting commercial drivers

This avoids attempting to reproduce the full desktop analytical experience on a smaller screen.

---

# Report Design Summary

Each page has a distinct analytical responsibility:

| Page | Primary Question |
|---|---|
| Executive Overview | What is happening? |
| Performance Analysis | What is driving it? |
| Exceptions & Management Attention | Where should management investigate? |
| Region Performance Detail | What is happening within this Region? |
| DEV Validation | Are the calculations and model behaviour correct? |

The report therefore functions as an executive decision-support experience rather than a collection of independent charts.

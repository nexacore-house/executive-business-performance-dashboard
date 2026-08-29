Purpose:
Provides the primary absolute profitability measure used in executive reporting, target analysis and time comparisons.

Gross Margin %
Gross Margin % =
DIVIDE(
    [Gross Profit],
    [Revenue]
)

Purpose:
Measures the proportion of Revenue retained as Gross Profit.

DIVIDE() is used instead of the / operator to provide safe handling of zero or blank denominators.

Average Order Value

Conceptually:

Average Order Value =
DIVIDE(
    [Revenue],
    [Orders]
)

Purpose:
Provides a commercial driver showing average revenue generated per transaction.

2. Time Intelligence

Time-intelligence measures compare current performance with prior periods and support trend analysis.

Measure	Purpose
Active Customers PY	Prior-year active customer count
Active Customers YoY %	Year-on-year change in active customers
Average Order Value PY	Prior-year Average Order Value
Average Order Value YoY %	Year-on-year change in Average Order Value
Gross Margin PY %	Prior-year Gross Margin
Gross Margin YoY Change	Percentage-point movement in Gross Margin
Gross Profit PY	Prior-year Gross Profit
Gross Profit YoY %	Year-on-year Gross Profit growth
Gross Profit YoY Variance	Absolute Gross Profit change against prior year
Gross Profit YTD	Year-to-date Gross Profit
Orders PY	Prior-year order volume
Orders YoY %	Year-on-year change in Orders
Revenue MoM %	Month-on-month Revenue percentage change
Revenue MoM Variance	Absolute Revenue movement against previous month
Revenue PM	Previous-month Revenue
Revenue PY	Prior-year Revenue
Revenue PYTD	Prior-year-to-date Revenue
Revenue YoY %	Year-on-year Revenue growth
Revenue YoY Variance	Absolute Revenue movement against prior year
Revenue YTD	Year-to-date Revenue
Prior-Year Pattern

A typical prior-year measure follows the pattern:

Revenue PY =
CALCULATE(
    [Revenue],
    DATEADD(
        DimDate[Date],
        -1,
        YEAR
    )
)

Higher-level YoY measures then reuse the prior-year measure rather than repeating the date calculation.

Revenue YoY %

Conceptually:

Revenue YoY % =
DIVIDE(
    [Revenue] - [Revenue PY],
    [Revenue PY]
)

Purpose:
Shows the rate at which Revenue has grown or contracted compared with the equivalent prior-year period.

For 2023, the measure intentionally returns blank where no 2022 comparison data exists.

Gross Profit YoY %

Conceptually:

Gross Profit YoY % =
DIVIDE(
    [Gross Profit] - [Gross Profit PY],
    [Gross Profit PY]
)

Purpose:
Allows Gross Profit growth to be compared with Revenue growth and helps identify situations where profitability is not keeping pace with commercial growth.

Gross Margin YoY Change
Gross Margin YoY Change =
[Gross Margin %] - [Gross Margin PY %]

Purpose:
Measures the movement in Gross Margin relative to the previous year.

Important:
This measure represents a percentage-point change rather than percentage growth.

For example:

27.20% - 27.65% = -0.45pp

3. Targets & Variance

These measures support actual-versus-plan reporting.

Measure	Purpose
Gross Margin vs Target Valid	Target-safe Gross Margin variance
Margin vs Target	Difference between actual and target margin
Profit Target	Planned Gross Profit
Profit Target Attainment %	Gross Profit expressed relative to target
Profit Target Valid	Target-safe Profit Target
Profit vs Target	Absolute Gross Profit variance against target
Profit vs Target %	Percentage Gross Profit variance against target
Profit vs Target % Valid	Target-safe percentage Profit variance
Profit vs Target Valid	Target-safe absolute Profit variance
Revenue Target	Planned Revenue
Revenue Target Attainment %	Revenue expressed relative to target
Revenue Target Valid	Target-safe Revenue Target
Revenue vs Target	Absolute Revenue variance against target
Revenue vs Target %	Percentage Revenue variance against target
Revenue vs Target % Valid	Target-safe percentage Revenue variance
Revenue vs Target Valid	Target-safe absolute Revenue variance
Target Gross Margin %	Gross Margin implied by Revenue and Profit targets
Revenue Variance

Conceptually:

Revenue vs Target =
[Revenue] - [Revenue Target]

Percentage variance:

Revenue vs Target % =
DIVIDE(
    [Revenue] - [Revenue Target],
    [Revenue Target]
)

Purpose:
Shows the magnitude and percentage of Revenue over- or under-performance against plan.

Profit Variance

Conceptually:

Profit vs Target =
[Gross Profit] - [Profit Target]

Percentage variance:

Profit vs Target % =
DIVIDE(
    [Gross Profit] - [Profit Target],
    [Profit Target]
)
Target Gross Margin %

Conceptually:

Target Gross Margin % =
DIVIDE(
    [Profit Target],
    [Revenue Target]
)

Purpose:
Creates the profitability-efficiency benchmark implied by the financial plan.

Valid Target Measures

The model includes target-safe versions such as:

Revenue Target Valid
Profit Target Valid
Revenue vs Target Valid
Revenue vs Target % Valid
Profit vs Target Valid
Profit vs Target % Valid
Gross Margin vs Target Valid

These measures prevent unsupported target comparisons from being presented to users.

Targets are valid within their defined dimensional grain, including:

Time
Region
Channel

Product Category is not part of the target grain.

Therefore, Product Category filtering must not result in an apparently valid target allocation.

This is a deliberate semantic-model design decision rather than a missing calculation.

4. KPI Status

KPI Status measures convert quantitative performance into concise management classifications and labels.

Measure	Purpose
Gross Margin Target Label	User-facing label describing Gross Margin target position
Gross Margin Trend Status	Classifies Gross Margin movement
Gross Margin YoY Label	User-facing Gross Margin YoY description
Gross Profit YoY Label	User-facing Gross Profit growth label
Profit Growth Status	Classifies Gross Profit growth
Profit Target Direction	Indicates direction of Profit target variance
Profit Target Label	User-facing Profit target comparison
Profit Target Status	Classifies Profit performance against plan
Revenue Growth Status	Classifies Revenue growth
Revenue Target Direction	Indicates direction of Revenue target variance
Revenue Target Label	User-facing Revenue target comparison
Revenue Target Status	Classifies Revenue performance against plan
Revenue YoY Label	User-facing Revenue YoY description

These measures separate:

calculation logic

from:

presentation/business interpretation

This allows quantitative measures to remain reusable while management-friendly labels are controlled centrally.

5. Executive Metrics

Executive Metrics combine lower-level KPIs into concise decision-support outputs used by the report experience.

Measure	Purpose
Executive Performance Headline	Generates the main executive management narrative
Gross Margin YoY Change Display	Presentation-oriented Gross Margin change
Growth Quality	Classifies the relationship between Revenue, Profit and Margin movement
Management Attention Flag	Numeric flag identifying areas requiring investigation
Management Attention Status	User-facing management attention classification
Overall Target Position	Summarises overall performance against plan
Region Detail Title	Generates dynamic Region drill-through page title
Regions Below Profit Target	Counts Regions below Profit plan
Regions Below Revenue Target	Counts Regions below Revenue plan
Regions Requiring Attention	Counts Regions meeting management-attention conditions
Selected Period Label	Provides dynamic reporting-period context
Growth Quality

Growth Quality evaluates the relationship between:

Revenue YoY
Gross Profit YoY
Gross Margin YoY Change

and translates those measures into management-friendly classifications.

Examples include:

Healthy Growth
Growth with Margin Pressure
Revenue Growth, Profit Decline
Profit Improvement Despite Revenue Decline
Business Contraction

A representative pattern is:

Growth Quality =
VAR RevenueGrowth = [Revenue YoY %]
VAR ProfitGrowth = [Gross Profit YoY %]
VAR MarginChange = [Gross Margin YoY Change]

RETURN
SWITCH(
    TRUE(),

    ISBLANK(RevenueGrowth),
        BLANK(),

    RevenueGrowth > 0
        && ProfitGrowth > 0
        && MarginChange >= 0,
        "Healthy Growth",

    RevenueGrowth > 0
        && ProfitGrowth > 0
        && MarginChange < 0,
        "Growth with Margin Pressure",

    RevenueGrowth > 0
        && ProfitGrowth <= 0,
        "Revenue Growth, Profit Decline",

    RevenueGrowth <= 0
        && ProfitGrowth > 0,
        "Profit Improvement Despite Revenue Decline",

    "Business Contraction"
)

Business Purpose:
Allows users to identify situations where topline growth alone could conceal deteriorating profitability.

Management Attention Flag

This measure provides a numeric exception flag used to identify Regions requiring management investigation.

The flag supports downstream measures including:

Regions Requiring Attention
Management Attention Status

Keeping the numeric flag separate from the user-facing text status allows the logic to be reused in counts and other calculations.

Regions Requiring Attention

Representative pattern:

Regions Requiring Attention =
SUMX(
    VALUES(DimRegion[Region]),
    IF(
        [Management Attention Flag] = 1,
        1,
        0
    )
)

Purpose:
Counts the number of Regions currently meeting defined management-attention conditions.

Region Detail Title

Representative pattern:

Region Detail Title =
VAR RegionName =
    SELECTEDVALUE(DimRegion[Region])
RETURN
IF(
    NOT ISBLANK(RegionName),
    RegionName & " Performance Detail",
    "Region Performance Detail"
)

Purpose:
Provides contextual labelling on the Region drill-through page.

6. Validation

Validation measures were created specifically to test target behaviour and semantic-model integrity.

Measure	Purpose
Target Context Valid	Identifies whether the current context supports target comparison
Target Max Region Key	Diagnostic check of Region target filtering
Target Min Region Key	Diagnostic check of Region target filtering
Target Rows	Counts target records available in the current context

These measures are retained in the PBIX for technical QA but are not intended as executive-facing KPIs.

Target Context Validation

The target-validation framework exists because Actual Sales and Targets do not share every analytical dimension.

The model must distinguish between:

Supported target context

Examples:

Year
Month
Region
Channel
Region + Channel

and:

Unsupported target context

Example:

Product Category

The Target Context Valid logic supports target-safe measures so that unsupported comparisons return blank instead of presenting a misleading target value.

Measure-Layer Design Principles

The DAX layer follows several design principles.

1. Measure branching

Higher-level calculations reuse established base measures instead of repeating aggregation logic.

Example:

Revenue
   ↓
Revenue PY
   ↓
Revenue YoY %
   ↓
Revenue Growth Status
   ↓
Growth Quality / Executive Headline

This improves maintainability and keeps business logic consistent.

2. Separation of calculation and presentation

Numeric measures calculate business results.

Status and label measures translate those results into executive-facing language.

This prevents presentation requirements from contaminating reusable financial calculations.

3. Safe division

DIVIDE() is preferred for ratio calculations to provide controlled behaviour when denominators are zero or blank.

4. Explicit target-context handling

Targets are not assumed to be valid under every report filter.

Target-safe measures validate the reporting context before exposing target comparisons.

This prevents technically possible but analytically invalid calculations.

5. Meaningful blanks

Where a comparison cannot legitimately be calculated, the solution returns blank rather than replacing missing context with zero.

Examples include:

2023 YoY measures where 2022 data is unavailable
Target comparisons under unsupported Product Category context

A blank communicates unavailable comparison context; zero would incorrectly imply no change or no variance.

6. Reusable exception logic

Management-attention logic is implemented as measures rather than being hard-coded independently into individual visuals.

This allows the same business rules to support:

exception matrices
summary cards
conditional formatting
management labels
drill-through investigation
Summary

The DAX layer supports six analytical functions:

Foundational business calculations
Time-based performance comparison
Actual-versus-target analysis
KPI status classification
Executive decision-support logic
Semantic-model validation

The objective is not simply to calculate dashboard values, but to maintain consistent business logic across executive reporting, analytical exploration and exception investigation.

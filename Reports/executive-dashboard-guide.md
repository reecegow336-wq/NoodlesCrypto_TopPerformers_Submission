# Executive Dashboard Guide
## NoodlesCrypto Top Performers – Power BI

## 1. Overview

The NoodlesCrypto Executive Dashboard provides a management-level view of social engagement performance across cryptocurrency tokens and social platforms.

The dashboard supports:

- Executive KPI monitoring
- Token engagement comparison
- Historical engagement trend analysis
- Twitter and Reddit platform comparison
- Currency-level analysis
- Dynamic Top N analysis
- Time-intelligence reporting
- Executive storytelling and recommendations

The report uses optimized analytical views from the data warehouse together with reusable DAX measures in Power BI.

---

# 2. Report Structure

The final Power BI report contains five pages:

1. Executive Overview
2. Platform Analysis
3. Time Series Analysis
4. Currency Deep Dive
5. Executive Storytelling

Each page is designed for a different analytical purpose while using shared business measures and dimensions.

---

# 3. Executive Overview

## Purpose

Provides a high-level view of token performance and allows users to quickly identify the strongest-performing currencies.

## Primary Data Source

`vw_executivedashboard`

Supporting tables:

- `dimcurrency`
- `DimDate`
- `Top N Count`

## Main KPIs

- Total Engagements
- Total Likes
- Total Comments
- Total Impressions
- Avg Engagement Score

## Main Visuals

- KPI cards
- Engagement trend analysis
- Currency engagement bar chart
- Platform Avg Engagement Score
- Currency performance table
- Engagement Rank
- Dynamic Top N control

## Ranking

Currencies are ranked using the final `Engagement Rank` measure based on Avg Engagement Score.

The ranking is displayed in descending order so that the strongest-performing currency receives Rank 1.

## Dynamic Top N

The Top N control allows the report user to adjust the number of currencies included in Top N analysis.

The supporting measures are:

- `Top N Count Value`
- `Top N Currency`

---

# 4. Platform Analysis

## Purpose

Compares engagement performance between the supported social media platforms.

The report currently contains:

- Reddit
- Twitter

## Primary Data Source

`vw_socialanalytics`

Supporting source:

`vw_platformdaily`

## Main Measures

- Platform Total Engagements
- Platform Total Comments
- Platform Avg Engagement Score
- Engagement by Platform
- Platform Engagement Share %
- Likes Share %
- Comments Share %

## Main Analysis

The page allows users to compare:

- Overall engagement by platform
- Average engagement quality
- Likes and comments contribution
- Relative platform engagement share

This helps distinguish between engagement quantity and engagement quality.

---

# 5. Time Series Analysis

## Purpose

Tracks engagement behaviour over time and highlights major increases, decreases and unusual activity spikes.

## Primary Data Source

`vw_timeseries`

Supporting table:

`DimDate`

## Main Measures

- Total Engagements (Time)
- Engagement YTD
- Engagement Last 30 Days
- Avg Engagement Rolling 7D
- Engagements Previous Day
- Engagement Growth %
- Engagement MoM Change %

## Main Analysis

The page is used to:

- Analyse historical engagement
- Identify unusual engagement spikes
- Compare recent performance with prior periods
- Measure rolling engagement behaviour
- Review month-over-month and day-over-day changes

## Date Filtering

Date-based visuals use the available date fields and time-series context to allow analysis over different reporting periods.

---

# 6. Currency Deep Dive

## Purpose

Provides detailed investigation of token and platform behaviour.

## Primary Data Sources

- `vw_executivedashboard`
- `vw_timeseries`
- `vw_platformdaily`
- `vw_socialanalytics`
- `dimcurrency`

## Currency Filter

The currency slicer uses:

`dimcurrency[Symbol]`

The currency slicer filters currency-aware visuals such as the token-level table.

## Date Filtering

Date slicers control the date-aware and time-series visuals on the page.

The date slicers are used to change:

- Engagement trends
- Historical engagement analysis
- Date-aware platform engagement

## Main Visuals

- Currency selection slicer
- Engagement trend over time
- Currency KPI / metric table
- Historical engagement analysis
- Platform engagement donut

## Important Filter Behaviour

The data model contains analytical views with different levels of granularity.

Because of this:

- Currency filters apply to currency-aware visuals.
- Date filters apply to time-series and date-aware platform visuals.
- Platform visuals use the platform-specific analytical datasets.

This behaviour is intentional and reflects the structure of the underlying warehouse views.

---

# 7. Executive Storytelling

## Purpose

Transforms the detailed dashboard analysis into a concise management-level summary.

The page is designed to answer:

- What is happening?
- Which tokens are performing best?
- How is engagement changing?
- Which platform contributes the most engagement?
- What should management monitor next?

## KPI Cards

The page includes:

- Total Engagements
- Avg Engagement Score
- Engagement MoM Change %
- Engagement Last 30 Days

## Reporting Period

A Reporting Period slicer allows management to adjust the time period used for trend analysis.

## Main Visuals

### Engagement Trend Over Time

Shows historical engagement movement and major engagement spikes.

Data source:

`vw_timeseries`

Measure:

`Total Engagements (Time)`

### Top 10 Performing Tokens

Ranks the strongest currencies by Avg Engagement Score.

Data source:

`vw_executivedashboard`

Measure:

`Avg Engagement Score`

### Engagement by Platform

Compares Reddit and Twitter using the date-aware platform measure.

Measure:

`Platform Engagements Date Aware`

## Executive Insights

The report includes an executive narrative highlighting the key findings from the dashboard.

Current findings include:

- Engagement activity shows a significant recent spike.
- A small group of tokens is driving the strongest engagement performance.
- Reddit currently contributes more engagement than Twitter.
- Management should monitor leading tokens and recent engagement momentum for emerging opportunities.

---

# 8. Key Metrics Explained

| Metric | Description |
|---|---|
| Total Engagements | Total engagement generated by the selected reporting context |
| Avg Engagement Score | Average engagement performance score |
| Total Likes | Total likes recorded |
| Total Comments | Total comments recorded |
| Total Retweets | Total retweets / shares recorded |
| Total Posts | Total number of social posts |
| Total Impressions | Total social impressions |
| Engagement YTD | Engagement accumulated from the start of the year |
| Engagement Last 30 Days | Engagement within the latest rolling 30-day period |
| Avg Engagement Rolling 7D | Average daily engagement across the latest seven-day period |
| Engagement MoM Change % | Percentage change compared with the previous month |
| Engagement Rank | Currency ranking based on Avg Engagement Score |
| Platform Engagement Share % | Percentage of overall engagement contributed by each platform |
| Engagement Level | High / Medium / Low engagement classification |

---

# 9. Engagement Classification

The `Engagement Level` measure classifies token performance as:

- High – Avg Engagement Score of 40 or above
- Medium – Avg Engagement Score from 20 to below 40
- Low – Avg Engagement Score below 20

This provides a simple management-friendly interpretation of token performance.

---

# 10. Data Model

The report uses a dimensional Power BI model containing analytical views and supporting dimensions.

## Main Analytical Views

- `vw_executivedashboard`
- `vw_timeseries`
- `vw_platformdaily`
- `vw_socialanalytics`

## Supporting Dimensions

- `DimDate`
- `dimcurrency`
- `dimplatform`

## Supporting Parameter Tables

- `Top N Count`
- `Parameter`

Relationships between dimensions and analytical views allow filtering at the appropriate data grain.

---

# 11. DAX Layer

Reusable business measures are documented separately in:

`reports/dax-measures-reference.md`

The DAX layer supports:

- Executive KPIs
- Time intelligence
- Dynamic Top N analysis
- Token ranking
- Platform comparison
- Engagement classification
- Date-aware reporting

Reviewers can use the DAX reference file to understand the measure logic without opening Power BI.

---

# 12. Refresh and Performance

## Local Refresh

In Power BI Desktop:

**Home → Refresh**

This reloads the report data from the configured data source.

## Performance Design

The dashboard uses optimized warehouse views rather than raw transactional tables.

This provides:

- Reduced model complexity
- Faster report queries
- Reusable business logic
- Improved scalability
- Cleaner executive reporting

---

# 13. Troubleshooting

## No Data Appears

Check:

- Current date range
- Currency selection
- Platform filters
- Whether a visual uses a different analytical grain

## Visual Does Not Respond to Currency Selection

Confirm that the visual uses a currency-aware dataset.

Not every analytical view contains a currency field.

## Visual Does Not Respond to Date Selection

Confirm that the visual uses:

- `vw_timeseries`
- `vw_platformdaily`
- or another date-aware source

## Unexpected Ranking

Confirm the report is using the final `Engagement Rank` measure documented in the DAX reference.

---

# 14. Report Files

The main report deliverables are stored under:

`reports/`

Required files include:

- `NoodlesCrypto_ExecutiveDashboard.pbix`
- `executive-dashboard-guide.md`
- `dax-measures-reference.md`

Report screenshots are stored under:

`reports/screenshots/`

The screenshot set includes:

- `executive-overview.png`
- `platform-analysis.png`
- `time-series-analysis.png`
- `currency-deep-dive.png`
- `executive-storytelling.png`

---

# 15. Final Dashboard Summary

The completed NoodlesCrypto Executive Dashboard provides a five-page analytical reporting solution covering:

- Executive KPI reporting
- Token performance
- Platform comparison
- Historical engagement trends
- Currency-level analysis
- Time intelligence
- Dynamic Top N ranking
- Executive storytelling

The report is designed so that management can move from high-level performance indicators into detailed analytical views and finish with an executive interpretation of the most important findings.


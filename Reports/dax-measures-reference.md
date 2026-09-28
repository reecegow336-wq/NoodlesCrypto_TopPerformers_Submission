# DAX Measures Reference
## NoodlesCrypto Executive Dashboard – Power BI

This document contains the DAX measures created and used for the NoodlesCrypto Executive Dashboard.

The measures support executive KPI reporting, time intelligence, engagement analysis, token ranking, platform comparison, dynamic Top N filtering, and executive storytelling.

Each measure documents:

- Name
- Category
- Purpose
- Data Source
- DAX Formula
- Example Output
- Dependencies
- DimDate usage
- Slicers affected
- Report page
- Visual usage

---

# 1. Executive KPI Measures

## 1.1 Total Engagements

**Name:** Total Engagements  
**Category:** KPI  
**Purpose:** Calculates total engagement for the current filter context.  
**Data Source:** `vw_executivedashboard`

### DAX Formula

```DAX
Total Engagements =
SUM(vw_executivedashboard[TotalEngagements])
```

**Example Output:** `3K`  
**Dependencies:** `vw_executivedashboard[TotalEngagements]`  
**DimDate:** No direct dependency  
**Slicer Affected:** Currency and applicable report filters  

**Used In:**
- Executive Overview – Total Engagements KPI
- Executive Storytelling – Total Engagements KPI

---

## 1.2 Avg Engagement Score

**Name:** Avg Engagement Score  
**Category:** KPI  
**Purpose:** Calculates the average engagement score for the current filter context.  
**Data Source:** `vw_executivedashboard`

### DAX Formula

```DAX
Avg Engagement Score =
AVERAGE(vw_executivedashboard[AvgEngagementScore])
```

**Example Output:** `25.99`  
**Dependencies:** `vw_executivedashboard[AvgEngagementScore]`  
**DimDate:** No direct dependency  
**Slicer Affected:** Currency and applicable report filters  

**Used In:**
- Executive Overview – Avg Engagement Score KPI
- Executive Overview – Currency Ranking Table
- Executive Storytelling – Avg Engagement Score KPI
- Executive Storytelling – Top 10 Performing Tokens

---

## 1.3 Total Likes

**Name:** Total Likes  
**Category:** KPI  
**Purpose:** Calculates the total number of likes.  
**Data Source:** `vw_executivedashboard`

### DAX Formula

```DAX
Total Likes =
SUM(vw_executivedashboard[TotalLikes])
```

**Example Output:** `20.80K`  
**Dependencies:** `vw_executivedashboard[TotalLikes]`  
**DimDate:** No direct dependency  
**Slicer Affected:** Currency and applicable report filters  

**Used In:**
- Executive Overview
- Currency analysis tables

---

## 1.4 Total Comments

**Name:** Total Comments  
**Category:** KPI  
**Purpose:** Calculates total comments.  
**Data Source:** `vw_executivedashboard`

### DAX Formula

```DAX
Total Comments =
SUM(vw_executivedashboard[TotalComments])
```

**Example Output:** `12.15K`  
**Dependencies:** `vw_executivedashboard[TotalComments]`  
**DimDate:** No direct dependency  
**Slicer Affected:** Currency and applicable report filters  

**Used In:**
- Executive Overview
- Currency analysis tables

---

## 1.5 Total Retweets

**Name:** Total Retweets  
**Category:** KPI  
**Purpose:** Calculates total retweets.  
**Data Source:** `vw_executivedashboard`

### DAX Formula

```DAX
Total Retweets =
SUM(vw_executivedashboard[TotalRetweets])
```

**Example Output:** `1.45K`  
**Dependencies:** `vw_executivedashboard[TotalRetweets]`  
**DimDate:** No direct dependency  
**Slicer Affected:** Currency and applicable report filters  

**Used In:**
- Executive Overview
- Platform / currency analysis tables

---

## 1.6 Total Posts

**Name:** Total Posts  
**Category:** KPI  
**Purpose:** Calculates total social media posts from the platform daily dataset.  
**Data Source:** `vw_platformdaily`

### DAX Formula

```DAX
Total Posts =
SUM(vw_platformdaily[TotalPosts])
```

**Example Output:** Depends on selected reporting period  
**Dependencies:** `vw_platformdaily[TotalPosts]`  
**DimDate:** No direct dependency  
**Slicer Affected:** Date and Platform  

**Used In:**
- Time Series Analysis
- Engagement-per-post calculations

---

## 1.7 Total Impressions

**Name:** Total Impressions  
**Category:** KPI  
**Purpose:** Calculates total impressions across the time-series dataset.  
**Data Source:** `vw_timeseries`

### DAX Formula

```DAX
Total Impressions =
SUM(vw_timeseries[TotalImpressions])
```

**Example Output:** `674.73K`  
**Dependencies:** `vw_timeseries[TotalImpressions]`  
**DimDate:** No direct dependency  
**Slicer Affected:** Date  

**Used In:**
- Executive Overview
- Time Series Analysis

---

## 1.8 Avg Engagement per Post

**Name:** Avg Engagement per Post  
**Category:** KPI  
**Purpose:** Measures the average number of engagements generated per social post.  
**Data Source:** Executive dashboard and platform daily views

### DAX Formula

```DAX
Avg Engagement per Post =
DIVIDE(
    [Total Engagements],
    [Total Posts],
    0
)
```

**Example Output:** Engagement-per-post ratio  
**Dependencies:** `[Total Engagements]`, `[Total Posts]`  
**DimDate:** No direct dependency  
**Slicer Affected:** Date, Currency and Platform where applicable  

**Used In:**
- Time Series Analysis
- Supporting engagement efficiency analysis

---

# 2. Time Intelligence Measures

## 2.1 Total Engagements (Time)

**Name:** Total Engagements (Time)  
**Category:** Time Intelligence / Helper  
**Purpose:** Calculates engagement from the dedicated time-series view so engagement changes correctly across dates.  
**Data Source:** `vw_timeseries`

### DAX Formula

```DAX
Total Engagements (Time) =
SUM(vw_timeseries[TotalEngagements])
```

**Example Output:** Daily historical engagement values  
**Dependencies:** `vw_timeseries[TotalEngagements]`  
**DimDate:** No direct dependency  
**Slicer Affected:** Date  

**Used In:**
- Time Series Analysis
- Currency Deep Dive – Engagement Over Time
- Executive Storytelling – Engagement Trend Over Time

---

## 2.2 Engagement YTD

**Name:** Engagement YTD  
**Category:** Time Intelligence  
**Purpose:** Calculates total engagement from the beginning of the year through the current date context.  
**Data Source:** `vw_executivedashboard`, `DimDate`

### DAX Formula

```DAX
Engagement YTD =
TOTALYTD(
    [Total Engagements],
    DimDate[FullDate]
)
```

**Example Output:** Current year-to-date engagement  
**Dependencies:** `[Total Engagements]`, `DimDate[FullDate]`  
**DimDate:** Yes  
**Time Intelligence:** Year-to-date calculation  
**Slicer Affected:** Date and Currency  

**Used In:**
- Time Series Analysis

---

## 2.3 Engagement Last 30 Days

**Name:** Engagement Last 30 Days  
**Category:** Time Intelligence  
**Purpose:** Calculates engagement across the latest rolling 30-day period.  
**Data Source:** `vw_executivedashboard`, `DimDate`

### DAX Formula

```DAX
Engagement Last 30 Days =
CALCULATE(
    [Total Engagements],
    DATESINPERIOD(
        DimDate[FullDate],
        MAX(DimDate[FullDate]),
        -30,
        DAY
    )
)
```

**Example Output:** `3K`  
**Dependencies:** `[Total Engagements]`, `DimDate[FullDate]`  
**DimDate:** Yes  
**Time Intelligence:** Rolling 30-day window  
**Slicer Affected:** Date and Currency  

**Used In:**
- Time Series Analysis
- Executive Storytelling – Engagement Last 30 Days KPI

---

## 2.4 Avg Engagement Rolling 7D

**Name:** Avg Engagement Rolling 7D  
**Category:** Time Intelligence  
**Purpose:** Calculates the average daily engagement across the most recent seven-day period.  
**Data Source:** `vw_timeseries`

### DAX Formula

```DAX
Avg Engagement Rolling 7D =
AVERAGEX(
    DATESINPERIOD(
        vw_timeseries[FullDate],
        MAX(vw_timeseries[FullDate]),
        -7,
        DAY
    ),
    CALCULATE(
        SUM(vw_timeseries[TotalEngagements])
    )
)
```

**Example Output:** Rolling seven-day average engagement  
**Dependencies:** `vw_timeseries[FullDate]`, `vw_timeseries[TotalEngagements]`  
**DimDate:** No – date grain comes directly from `vw_timeseries`  
**Time Intelligence:** Rolling seven-day average  
**Slicer Affected:** Date  

**Used In:**
- Time Series Analysis
- Supporting rolling engagement analysis

---

## 2.5 Engagements Previous Day

**Name:** Engagements Previous Day  
**Category:** Time Intelligence  
**Purpose:** Returns total engagement for the previous day.  
**Data Source:** `vw_timeseries`, `DimDate`

### DAX Formula

```DAX
Engagements Previous Day =
CALCULATE(
    [Total Engagements (Time)],
    DATEADD(
        DimDate[FullDate],
        -1,
        DAY
    )
)
```

**Example Output:** Previous day's total engagement  
**Dependencies:** `[Total Engagements (Time)]`, `DimDate[FullDate]`  
**DimDate:** Yes  
**Time Intelligence:** Previous-day comparison  
**Slicer Affected:** Date  

**Used In:**
- Time Series Analysis
- Engagement Growth %

---

## 2.6 Engagement Growth %

**Name:** Engagement Growth %  
**Category:** Time Intelligence  
**Purpose:** Calculates percentage growth in engagement compared with the previous day.  
**Data Source:** `vw_timeseries`, `DimDate`

### DAX Formula

```DAX
Engagement Growth % =
DIVIDE(
    [Total Engagements (Time)] - [Engagements Previous Day],
    [Engagements Previous Day],
    0
) * 100
```

**Example Output:** Positive or negative percentage change  
**Dependencies:** `[Total Engagements (Time)]`, `[Engagements Previous Day]`  
**DimDate:** Yes  
**Time Intelligence:** Day-over-day comparison  
**Slicer Affected:** Date  

**Used In:**
- Time Series Analysis

---

## 2.7 Engagement MoM Change %

**Name:** Engagement MoM Change %  
**Category:** Time Intelligence  
**Purpose:** Compares current engagement with engagement from the previous month.  
**Data Source:** `vw_executivedashboard`, `DimDate`

### DAX Formula

```DAX
Engagement MoM Change % =
VAR PreviousMonthEngagement =
    CALCULATE(
        [Total Engagements],
        DATEADD(
            DimDate[FullDate],
            -1,
            MONTH
        )
    )
RETURN
    DIVIDE(
        [Total Engagements] - PreviousMonthEngagement,
        PreviousMonthEngagement,
        0
    ) * 100
```

**Example Output:** `0.00%` depending on reporting context  
**Dependencies:** `[Total Engagements]`, `DimDate[FullDate]`  
**DimDate:** Yes  
**Time Intelligence:** Month-over-month comparison  
**Slicer Affected:** Date and Currency  

**Used In:**
- Time Series Analysis
- Executive Storytelling – Engagement MoM Change % KPI

---

# 3. Ranking & Top N Measures

## 3.1 Engagement Rank

**Name:** Engagement Rank  
**Category:** Ranking  
**Purpose:** Ranks currencies by average engagement score in descending order.  
**Data Source:** `vw_executivedashboard`

### DAX Formula

```DAX
Engagement Rank =
RANKX(
    ALL(vw_executivedashboard),
    [Avg Engagement Score],
    ,
    DESC,
    DENSE
)
```

**Example Output:** `1, 2, 3, 4 ... 10`  
**Dependencies:** `[Avg Engagement Score]`, `vw_executivedashboard`  
**DimDate:** No direct dependency  
**Slicer Affected:** Currency and applicable report filters  

**Used In:**
- Executive Overview – Currency Engagement Ranking Table

**Note:**  
This is the final working version used to correct the ranking issue where every token previously displayed rank `1`.

---

## 3.2 Top N Count Value

**Name:** Top N Count Value  
**Category:** Ranking / Helper  
**Purpose:** Returns the Top N value selected by the user, defaulting to 10.  
**Data Source:** `Top N Count`

### DAX Formula

```DAX
Top N Count Value =
SELECTEDVALUE(
    'Top N Count'[Top N Count],
    10
)
```

**Example Output:** `10`  
**Dependencies:** `'Top N Count'[Top N Count]`  
**DimDate:** No  
**Slicer Affected:** Top N Count  

**Used In:**
- Executive Overview
- Dynamic Top N filtering

---

## 3.3 Top N Currency

**Name:** Top N Currency  
**Category:** Ranking  
**Purpose:** Identifies currencies that fall inside the dynamically selected Top N based on engagement.  
**Data Source:** `vw_executivedashboard`, `Top N Count`

### DAX Formula

```DAX
Top N Currency =
VAR SelectedTopN = [Top N Count Value]

VAR CurrencyRank =
    RANKX(
        ALL('vw_executivedashboard'[CurrencySymbol]),
        CALCULATE(
            SUM('vw_executivedashboard'[TotalEngagements])
        ),
        ,
        DESC,
        DENSE
    )

RETURN
    IF(
        CurrencyRank <= SelectedTopN,
        1,
        0
    )
```

**Example Output:** `1` for a Top N token, otherwise `0`  
**Dependencies:** `[Top N Count Value]`, `CurrencySymbol`, `TotalEngagements`  
**DimDate:** No direct dependency  
**Slicer Affected:** Top N and Currency  

**Used In:**
- Executive Overview
- Dynamic Top N token filtering

---

# 4. Platform Analysis Measures

## 4.1 Platform Total Engagements

**Name:** Platform Total Engagements  
**Category:** KPI  
**Purpose:** Calculates total engagement from the social analytics view.  
**Data Source:** `vw_socialanalytics`

### DAX Formula

```DAX
Platform Total Engagements =
SUM(vw_socialanalytics[TotalEngagements])
```

**Example Output:** Platform-specific engagement total  
**Dependencies:** `vw_socialanalytics[TotalEngagements]`  
**DimDate:** No  
**Slicer Affected:** Platform  

**Used In:**
- Platform Analysis

---

## 4.2 Platform Total Comments

**Name:** Platform Total Comments  
**Category:** KPI  
**Purpose:** Calculates total comments within the social analytics dataset.  
**Data Source:** `vw_socialanalytics`

### DAX Formula

```DAX
Platform Total Comments =
SUM(vw_socialanalytics[TotalComments])
```

**Example Output:** Platform comment total  
**Dependencies:** `vw_socialanalytics[TotalComments]`  
**DimDate:** No  
**Slicer Affected:** Platform  

**Used In:**
- Platform Analysis

---

## 4.3 Platform Avg Engagement Score

**Name:** Platform Avg Engagement Score  
**Category:** KPI  
**Purpose:** Calculates average engagement score by platform.  
**Data Source:** `vw_socialanalytics`

### DAX Formula

```DAX
Platform Avg Engagement Score =
AVERAGE(vw_socialanalytics[AvgEngagementScore])
```

**Example Output:** Average platform engagement score  
**Dependencies:** `vw_socialanalytics[AvgEngagementScore]`  
**DimDate:** No  
**Slicer Affected:** Platform  

**Used In:**
- Platform Analysis
- Currency Deep Dive supporting platform analysis

---

## 4.4 Engagement by Platform

**Name:** Engagement by Platform  
**Category:** KPI / Helper  
**Purpose:** Calculates engagement while retaining the platform filter context.  
**Data Source:** `vw_socialanalytics`

### DAX Formula

```DAX
Engagement by Platform =
SUM(vw_socialanalytics[TotalEngagements])
```

**Example Output:** Reddit or Twitter engagement total  
**Dependencies:** `vw_socialanalytics[TotalEngagements]`  
**DimDate:** No  
**Slicer Affected:** Platform  

**Used In:**
- Platform Analysis

---

## 4.5 Platform Engagement Share %

**Name:** Platform Engagement Share %  
**Category:** Helper / Formatting  
**Purpose:** Calculates each platform's percentage share of total engagement.  
**Data Source:** `vw_socialanalytics`

### DAX Formula

```DAX
Platform Engagement Share % =
DIVIDE(
    [Engagement by Platform],
    CALCULATE(
        [Engagement by Platform],
        ALL(vw_socialanalytics[PlatformName])
    ),
    0
)
```

**Example Output:** Percentage of engagement attributed to each platform  
**Dependencies:** `[Engagement by Platform]`, `PlatformName`  
**DimDate:** No  
**Slicer Affected:** Platform  

**Used In:**
- Platform Analysis

---

## 4.6 Likes Share %

**Name:** Likes Share %  
**Category:** Helper / Formatting  
**Purpose:** Calculates likes as a percentage of total platform engagement.  
**Data Source:** `vw_socialanalytics`

### DAX Formula

```DAX
Likes Share % =
DIVIDE(
    SUM(vw_socialanalytics[TotalLikes]),
    [Platform Total Engagements],
    0
) * 100
```

**Example Output:** Likes percentage  
**Dependencies:** `vw_socialanalytics[TotalLikes]`, `[Platform Total Engagements]`  
**DimDate:** No  
**Slicer Affected:** Platform  

**Used In:**
- Platform Analysis

---

## 4.7 Comments Share %

**Name:** Comments Share %  
**Category:** Helper / Formatting  
**Purpose:** Calculates comments as a percentage of total platform engagement.  
**Data Source:** `vw_socialanalytics`

### DAX Formula

```DAX
Comments Share % =
DIVIDE(
    SUM(vw_socialanalytics[TotalComments]),
    [Platform Total Engagements],
    0
) * 100
```

**Example Output:** Comments percentage  
**Dependencies:** `vw_socialanalytics[TotalComments]`, `[Platform Total Engagements]`  
**DimDate:** No  
**Slicer Affected:** Platform  

**Used In:**
- Platform Analysis

---

## 4.8 Platform Engagements Date Aware

**Name:** Platform Engagements Date Aware  
**Category:** KPI / Time-Aware Helper  
**Purpose:** Calculates platform engagement using the platform daily view so platform visuals respond correctly to date filtering.  
**Data Source:** `vw_platformdaily`

### DAX Formula

```DAX
Platform Engagements Date Aware =
SUM(vw_platformdaily[TotalEngagementScore])
```

**Example Output:** Approximately `62.61K` across the full reporting period  
**Dependencies:** `vw_platformdaily[TotalEngagementScore]`  
**DimDate:** No direct dependency – uses the platform daily date grain  
**Slicer Affected:** Date and Platform  

**Used In:**
- Currency Deep Dive – Platform Engagement Donut
- Executive Storytelling – Engagement by Platform

---

# 5. Helper / Formatting Measures

## 5.1 Engagement Level

**Name:** Engagement Level  
**Category:** Helper / Formatting  
**Purpose:** Classifies token performance as High, Medium, or Low based on average engagement score.  
**Data Source:** `vw_executivedashboard`

### DAX Formula

```DAX
Engagement Level =
SWITCH(
    TRUE(),
    [Avg Engagement Score] >= 40, "High",
    [Avg Engagement Score] >= 20, "Medium",
    "Low"
)
```

**Example Output:** `High`, `Medium`, or `Low`  
**Dependencies:** `[Avg Engagement Score]`  
**DimDate:** No  
**Slicer Affected:** Currency and applicable report filters  

**Used In:**
- Executive analysis
- Engagement classification
- Supporting conditional formatting / storytelling

---

## 5.2 Engagement Quality

**Name:** Engagement Quality  
**Category:** Helper / Formatting  
**Purpose:** Provides an additional four-level engagement classification.  
**Data Source:** `vw_executivedashboard`

### DAX Formula

```DAX
Engagement Quality =
SWITCH(
    TRUE(),
    [Avg Engagement Score] >= 0.8, "Excellent",
    [Avg Engagement Score] >= 0.6, "Good",
    [Avg Engagement Score] >= 0.4, "Average",
    "Low"
)
```

**Example Output:** `Excellent`, `Good`, `Average`, or `Low`  
**Dependencies:** `[Avg Engagement Score]`  
**DimDate:** No  
**Slicer Affected:** Currency  

**Used In:**
- Supporting engagement classification logic

---

## 5.3 Engagement Share %

**Name:** Engagement Share %  
**Category:** Helper / Formatting  
**Purpose:** Calculates a currency's contribution to overall engagement.  
**Data Source:** `vw_executivedashboard`

### DAX Formula

```DAX
Engagement Share % =
DIVIDE(
    [Total Engagements],
    CALCULATE(
        [Total Engagements],
        ALL(vw_executivedashboard)
    ),
    0
) * 100
```

**Example Output:** Currency engagement percentage  
**Dependencies:** `[Total Engagements]`  
**DimDate:** No direct dependency  
**Slicer Affected:** Currency  

**Used In:**
- Executive Overview
- Supporting currency analysis

---

# 6. Additional Time-Series Helper Measures

## 6.1 Engagement Today

**Name:** Engagement Today  
**Category:** Time Intelligence  
**Purpose:** Returns engagement for the latest date in the current filter context.  
**Data Source:** `vw_executivedashboard`, `DimDate`

### DAX Formula

```DAX
Engagement Today =
CALCULATE(
    [Total Engagements],
    LASTDATE(DimDate[FullDate])
)
```

**Example Output:** Latest day's engagement  
**Dependencies:** `[Total Engagements]`, `DimDate[FullDate]`  
**DimDate:** Yes  
**Slicer Affected:** Date  

**Used In:**
- Supporting trend analysis

---

## 6.2 Engagement Yesterday

**Name:** Engagement Yesterday  
**Category:** Time Intelligence  
**Purpose:** Calculates engagement for the previous day.  
**Data Source:** `vw_executivedashboard`, `DimDate`

### DAX Formula

```DAX
Engagement Yesterday =
CALCULATE(
    [Total Engagements],
    DATEADD(
        DimDate[FullDate],
        -1,
        DAY
    )
)
```

**Example Output:** Previous day's engagement  
**Dependencies:** `[Total Engagements]`, `DimDate[FullDate]`  
**DimDate:** Yes  
**Slicer Affected:** Date  

**Used In:**
- Supporting change analysis

---

## 6.3 Engagement Change %

**Name:** Engagement Change %  
**Category:** Time Intelligence  
**Purpose:** Calculates the percentage change between today's engagement and yesterday's engagement.  
**Data Source:** Executive dashboard / DimDate

### DAX Formula

```DAX
Engagement Change % =
DIVIDE(
    [Engagement Today] - [Engagement Yesterday],
    [Engagement Yesterday],
    0
)
```

**Example Output:** Daily percentage change  
**Dependencies:** `[Engagement Today]`, `[Engagement Yesterday]`  
**DimDate:** Yes  
**Slicer Affected:** Date  

**Used In:**
- Supporting time-series analysis

---

## 6.4 Engagement Trend

**Name:** Engagement Trend  
**Category:** Helper / Formatting  
**Purpose:** Indicates whether short-term engagement is trending upward or downward.  
**Data Source:** Engagement rolling measures

### DAX Formula

```DAX
Engagement Trend =
IF(
    [Avg Engagement Rolling 7D] > [Engagement 30D Avg],
    "Up ▲",
    "Down ▼"
)
```

**Example Output:** `Up ▲` or `Down ▼`  
**Dependencies:** `[Avg Engagement Rolling 7D]`, `[Engagement 30D Avg]`  
**DimDate:** Indirect  
**Slicer Affected:** Date  

**Used In:**
- Supporting trend analysis

---

## 6.5 High Engagement Flag

**Name:** High Engagement Flag  
**Category:** Helper  
**Purpose:** Flags observations where engagement exceeds the defined high-engagement threshold.  
**Data Source:** Executive dashboard

### DAX Formula

```DAX
High Engagement Flag =
IF(
    [Total Engagements] >= 10000,
    1,
    0
)
```

**Example Output:** `1` or `0`  
**Dependencies:** `[Total Engagements]`  
**DimDate:** No direct dependency  
**Slicer Affected:** Applicable report filters  

**Used In:**
- Supporting engagement analysis

---

# 7. Required Measure Group Summary

## Executive KPI Measures

- Total Engagements
- Avg Engagement Score
- Total Likes
- Total Comments
- Total Retweets
- Total Posts

## Time Intelligence Measures

- Engagement YTD
- Engagement Last 30 Days
- Engagement MoM Change %
- Avg Engagement Rolling 7D

## Ranking & Top N Measures

- Top N Currency
- Top N Count Value
- Engagement Rank

## Helper / Formatting Measures

- Engagement Level
- Platform Engagement Share %

## Additional Supporting Measures

- Total Engagements (Time)
- Total Impressions
- Avg Engagement per Post
- Engagements Previous Day
- Engagement Growth %
- Platform Total Engagements
- Platform Total Comments
- Platform Avg Engagement Score
- Engagement by Platform
- Platform Engagements Date Aware
- Likes Share %
- Comments Share %
- Engagement Quality
- Engagement Share %
- Engagement Today
- Engagement Yesterday
- Engagement Change %
- Engagement Trend
- High Engagement Flag

---

# 8. Final Dashboard Coverage

The measures documented in this file support the five completed Power BI report pages.

## Executive Overview

Provides:

- Executive KPI summary
- Engagement performance
- Currency comparison
- Dynamic Top N filtering
- Correct token engagement ranking
- Conditional engagement scoring

## Platform Analysis

Provides:

- Reddit and Twitter comparison
- Platform engagement totals
- Average platform engagement score
- Likes and comments share
- Platform engagement contribution

## Time Series Analysis

Provides:

- Historical engagement trends
- Year-to-date engagement
- Rolling 30-day analysis
- Rolling seven-day averages
- Previous-day comparisons
- Engagement growth analysis
- Month-over-month change

## Currency Deep Dive

Provides:

- Currency selection
- Currency-level performance analysis
- Date-driven engagement trends
- Platform engagement comparison
- Date-aware platform engagement

The currency slicer filters currency-aware visuals while date slicers control the time-series and platform-date visuals.

## Executive Storytelling

Provides:

- Total Engagements KPI
- Avg Engagement Score KPI
- Engagement MoM Change %
- Engagement Last 30 Days
- Reporting Period slicer
- Engagement Trend Over Time
- Top 10 Performing Tokens
- Engagement by Platform
- Executive Insights narrative

---

# 9. Final Notes

The Power BI semantic layer combines several SQL analytical views:

- `vw_executivedashboard`
- `vw_timeseries`
- `vw_platformdaily`
- `vw_socialanalytics`

Supporting dimension tables include:

- `DimDate`
- `dimcurrency`
- `dimplatform`

The DAX layer converts these datasets into reusable business measures for:

- Executive reporting
- KPI monitoring
- Time intelligence
- Token ranking
- Dynamic Top N analysis
- Platform comparison
- Engagement classification
- Executive storytelling

The completed dashboard provides decision-ready insight without requiring reviewers to inspect the underlying SQL or Power BI model.
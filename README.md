# 🌿 Bellabeat Case Study — How Can a Wellness Company Play It Smart?

**Smart Device Usage Analysis & Marketing Strategy Recommendations for Bellabeat Leaf**

![Status](https://img.shields.io/badge/status-complete-6B8E4E)
![Tool](https://img.shields.io/badge/tool-Excel-217346)
![Dataset](https://img.shields.io/badge/dataset-FitBit%20Fitness%20Tracker%20(Kaggle)-lightgrey)
![License](https://img.shields.io/badge/data%20license-CC0-blue)

> Data analysis case study for **Bellabeat**, a high-tech manufacturer of health-focused smart products for women. This project analyzes public FitBit fitness tracker data to uncover consumer smart device usage trends and turns those insights into actionable marketing recommendations for **Bellabeat Leaf**.

---

## Quick Links
 
| Resource | Link |
|---|---|
| Interactive Dashboard (Excel) | [`DailySummary_cleaned.xlsx`](https://docs.google.com/spreadsheets/d/1levI-4P-6wO4BQdfA7uZCGNAotb3Sysj/edit?usp=sharing&ouid=111398435741608142577&rtpof=true&sd=true) |
| Original Case Study Brief | [`Case_Study_2_How_can_a_wellness_company_play_it_smart.pdf`](https://drive.google.com/file/d/1V3SDVTG4xwUdtZvpch2ky7sP4_qprNxZ/view?usp=sharing) |
| Dataset Source | [FitBit Fitness Tracker Data (Kaggle)](https://www.kaggle.com/datasets/arashnic/fitbit) |
 
---
<img width="395" height="440" alt="Screenshot 2026-07-03 185231" src="https://github.com/user-attachments/assets/e4d54815-f17f-4639-b0d2-ad55c162d386" />

## 📌 Table of Contents

- [Executive Summary](#executive-summary)
- [01 — Ask: Business Task](#01--ask-business-task)
- [02 — Prepare: Data Sources](#02--prepare-data-sources)
- [03 — Process: Data Cleaning](#03--process-data-cleaning)
- [04 — Analyze: Summary of Analysis](#04--analyze-summary-of-analysis)
- [05 — Share: Visualizations & Key Findings](#05--share-visualizations--key-findings)
- [06 — Act: Recommendations](#06--act-recommendations)
- [Conclusion](#conclusion)

---

## Executive Summary

This report analyzes Fitbit smart device usage data to uncover behavioral trends in daily activity, sedentary time, and sleep, then translates those trends into targeted marketing recommendations for **Bellabeat Leaf** — the product best aligned with the dataset's activity, sleep, and stress-tracking focus. The analysis follows the six-step data analysis process: **Ask → Prepare → Process → Analyze → Share → Act**.

| Total Users | Avg. Daily Steps | Avg. Calories | Avg. Sleep |
|:---:|:---:|:---:|:---:|
| **33** Fitbit participants | **7,638** (recommended: 8,000) | **2,304 kcal** / day | **7.0 hrs** (efficiency: 91.5%) |

**Main Findings**
- Average daily steps (7,638) remain below the commonly recommended goal of 8,000–10,000 steps/day.
- Sedentary behavior dominates daily routines — the single most common daily pattern is being sedentary for the **entire 24-hour period** (mode = 1,440 minutes/day).
- Physical activity occurs in short, infrequent **bursts** rather than being spread evenly across the day — confirmed at both the hourly level (extreme right-skew, mode = 0) and daily level.
- Sleep quality is generally good: average duration ~7 hours with 91.5% sleep efficiency, correcting the initial assumption that sleep quality would be poor.
- Activity peaks sharply on **Saturday** (8,153 steps) but drops to its lowest point on **Sunday** (6,933 steps) — as a result, weekday and weekend averages are roughly similar overall, with a slight weekday edge (7,669 vs. 7,551 steps).

**Business Outcome:** Three marketing recommendations were developed to improve user engagement with Bellabeat Leaf, each directly grounded in a specific statistical finding from the dataset (see [Act](#06--act-recommendations)).

---

## 01 — Ask: Business Task

**Business Objective**
Analyze smart device fitness tracker usage data to understand consumer health behavior patterns, then translate those insights into a marketing strategy recommendation for one specific Bellabeat product, in support of Bellabeat's growth in the global smart device market.

**Stakeholders**
- Urška Sršen — Cofounder & Chief Creative Officer, Bellabeat
- Sando Mur — Cofounder, Bellabeat Executive Team
- Bellabeat Executive Team
- Bellabeat Marketing Analytics Team

**Business Questions**
1. What are some trends in smart device usage?
2. How could these trends apply to Bellabeat customers?
3. How could these trends help influence Bellabeat marketing strategy?

**Business Task Statement**
> Analyze FitBit Fitness Tracker data to identify trends in daily activity, sleep, and sedentary behavior, then develop specific marketing strategy recommendations for **Bellabeat Leaf**, while accounting for the known limitations of the dataset.

**Success Metrics**

*A. Analysis Success Criteria*
- Trends are identified with clear statistical support.
- Insights are relevant and mapped to one specific Bellabeat product.
- Recommendations are actionable, not generic.
- Data credibility (ROCCC) is evaluated and limitations are documented.

*B. Assumed Business Metrics (no target figures provided in the original brief)*
- App engagement rate (% daily active users)
- Feature adoption rate (% of users activating new recommended features)
- Membership conversion rate (% upgrading to paid membership)
- Retention rate (30 / 60 / 90 days)

**Scope**
- **In-scope:** public FitBit dataset (33 users confirmed via data profiling — the Kaggle description states 30, but the actual unique user count is 33), focused on one Bellabeat product (Leaf).
- **Out-of-scope:** Bellabeat internal data, user demographic data, direct field validation.

**Assumptions**
- FitBit user behavior can serve as a general proxy for smart device users, including prospective Bellabeat customers.
- Insights from aggregate data are sufficiently representative for high-level strategic direction (not detailed operational decisions).

**Risks & Constraints**
- Small sample size (33 users) → risk of over-generalization.
- No gender/demographic data → gap against Bellabeat's focus on women.
- Data originates from 2016 → may not fully reflect current behavior.

---

## 02 — Prepare: Data Sources

Dataset: **[FitBit Fitness Tracker Data](https://www.kaggle.com/datasets/arashnic/fitbit)** (Kaggle, CC0 — Public Domain, made available via Möbius). Consists of 18 CSV files at varying time granularities, covering activity, sleep, weight, heart rate, calories, and intensity data.

| Level | Files | Description |
|---|---|---|
| Daily | dailyActivity_merged, dailyCalories_merged, dailyIntensities_merged, dailySteps_merged, sleepDay_merged, weightLogInfo_merged | 1 row = 1 user per day |
| Hourly | hourlyCalories_merged, hourlyIntensities_merged, hourlySteps_merged | 1 row = 1 user per hour |
| Minute (Narrow) | minuteCaloriesNarrow, minuteIntensitiesNarrow, minuteMETsNarrow, minuteStepsNarrow, minuteSleep | 1 row = 1 user per minute (long format) |
| Minute (Wide) | minuteCaloriesWide, minuteIntensitiesWide, minuteStepsWide | 1 row = 1 user per hour, split into 60 minute columns |
| Second | heartrate_seconds_merged | 1 row = 1 user per second (finest granularity) |

> **Note:** dailyCalories, dailyIntensities, and dailySteps are subsets of `dailyActivity_merged`, which is used as the single source of truth for daily-level analysis.

**Data Profiling Results**

| File | Unique Users | % Coverage vs. dailyActivity |
|---|:---:|:---:|
| dailyActivity_merged | 33 | 100% |
| sleepDay_merged | 24 | 73% |
| weightLogInfo_merged | 8 | 24% |

> **Correction:** The actual verified user count is **33**, not 30 as stated in the Kaggle dataset description. Date range is consistent across all three main files (~31 days, 12 April – 12 May 2016), with no period mismatch.

**Data Credibility Evaluation (ROCCC)**

| Criterion | Rating | Justification |
|---|:---:|---|
| Reliable | Low | Small sample (33 users); 6 of 33 users have incomplete activity data (<20 days) |
| Original | Medium | Data was re-collected by a third party (Möbius), not directly from Fitbit/respondents |
| Comprehensive | Low | No demographic data (age, gender, location); sleep coverage only 73%, weight coverage only 24% |
| Current | Low | Data from 2016, only ~31-day period — does not capture seasonal or long-term trends |
| Cited | Unclear | Original data collection methodology is not transparently verified |

---

## 03 — Process: Data Cleaning

**Tools used:** Microsoft Excel (pivot tables, formulas) for aggregation and dashboard visualization.

| Issue | Affected Table(s) | Action Taken |
|---|---|---|
| Inconsistent date column names (`ActivityDate` vs. `ActivityDay` vs. `SleepDay` vs. `Date`) | dailyActivity, dailyCalories/Intensities/Steps, sleepDay, weightLogInfo | Standardized to a single `Date` column before joins |
| Missing values in `Fat` column (~97% missing: 65 of 67 rows) | weightLogInfo_merged | Column dropped — confirmed unusable |
| Duplicate rows (3 full-row duplicates) | sleepDay_merged | Removed via *Remove Duplicates* → 413 rows reduced to 410 unique rows |
| Uneven user coverage across files | sleepDay (73%), weightLogInfo (24%) | weightLogInfo excluded as a primary insight source; used only as a limitation note |
| Highly granular minute/second-level data | minute*, heartrate_seconds | Aggregated to hourly/daily level before use in business insights |
| Redundant daily-level files | dailyCalories/Intensities/Steps vs. dailyActivity | `dailyActivity_merged` used as the single source of truth |

**Cleaning Log**

| Table | Before | After | Change |
|---|:---:|:---:|---|
| weightLogInfo — `Fat` column | 67 rows (65 missing, ~97%) | Column dropped | Removed in `weightLogInfo_cleaned.xlsx` |
| sleepDay — duplicates | 413 rows | 410 rows | 3 full-row duplicates removed in `sleepDay_cleaned.xlsx` |

---

## 04 — Analyze: Summary of Analysis

**Hourly Level** (`hourlyIntensities` & `hourlySteps`)

| Statistic | TotalIntensity | StepTotal |
|---|:---:|:---:|
| Mean | 12.0 | 320.2 |
| Median | 3.0 | 40.0 |
| Mode | 0.0 | 0.0 |
| Std Dev | 21.1 | 690.4 |
| Skewness | 3.45 | 4.83 |
| Min – Max | 0 – 180 | 0 – 10,554 |
| Count | 22,099 | 22,099 |

Both columns are heavily right-skewed with Mode = 0 and Median far below Mean — most hours of the day show no activity at all, with a small number of hours showing extreme spikes pulling the average upward. This confirms activity happens in short **bursts**, not evenly across the day.

**Daily Level — Activity** (`dailyActivity_merged`)

| Statistic | TotalSteps | Calories | SedentaryMin. | VeryActiveMin. |
|---|:---:|:---:|:---:|:---:|
| Mean | 7,637.9 | 2,303.6 | 991.2 (~16.5h) | 21.2 |
| Median | 7,405.5 | 2,134.0 | 1,057.5 (~17.6h) | 4.0 |
| Mode | 0.0 | 1,980.0 | 1,440.0 (=24h) | 0.0 |
| Std Dev | 5,087.2 | 718.2 | 301.3 | 32.8 |
| Skewness | 0.65 | 0.42 | -0.29 | 2.18 |
| Count | 940 | 940 | 940 | 940 |

- **TotalSteps:** mean (7,638) is below the WHO recommendation of 10,000 steps/day.
- **SedentaryMinutes:** mode = 1,440 minutes (exactly 24 hours) — the strongest statistical evidence that most user time is spent inactive.
- **VeryActiveMinutes:** median only 4 minutes/day, mode 0, but mean 21.2 minutes — a small subset of highly active users pulls the average up.

**Daily Level — Sleep** (`sleepDay_merged`)

| Statistic | TotalMinutesAsleep | TotalTimeInBed |
|---|:---:|:---:|
| Mean | 419.5 (~7.0h) | 458.6 (~7.6h) |
| Median | 433.0 (~7.2h) | 463.0 (~7.7h) |
| Mode | 442.0 | 546.0 |
| Std Dev | 118.3 | 127.1 |
| Skewness | -0.61 | -0.22 |
| Count | 413* | 413* |

*\*Computed before duplicate removal (n = 413); the 3-row difference has a negligible effect on Mean/Median.*

- Average sleep duration ~7 hours — close to the ideal range (7–9 hours), correcting the initial assumption of poor sleep duration.
- **Sleep Efficiency** = 419.5 / 458.6 ≈ **91.5%** — considered good (ideal is >85%).

**Weekly Activity Pattern**

| Day | Avg. Steps |
|---|:---:|
| Monday | 7,780.9 |
| Tuesday | 8,125.0 |
| Wednesday | 7,559.4 |
| Thursday | 7,405.8 |
| Friday | 7,448.2 |
| **Saturday** | **8,153.0** (peak) |
| **Sunday** | **6,933.2** (lowest) |

Activity peaks sharply on **Saturday** but drops to its lowest point on **Sunday**. As a net result, the overall weekday average (7,668.7 steps) is actually slightly **higher** than the overall weekend average (7,550.6 steps) — the two are roughly comparable, driven by Sunday's steep drop offsetting Saturday's peak.

**Key Insights Summary**
1. Average daily activity (7,638 steps) remains below the 10,000 steps/day recommendation.
2. Sedentary time is strongly dominant at both daily and hourly levels.
3. Time spent very active is minimal and infrequent (median 4 min/day, mode 0).
4. Activity follows a "burst" pattern rather than being evenly distributed.
5. Sleep quality is actually fairly good (~7 hrs, ~91.5% efficiency).
6. Weekly activity is uneven (Saturday peak, Sunday drop) but weekday/weekend averages end up roughly similar.

---

## 05 — Share: Visualizations & Key Findings

Findings are communicated through the accompanying **Fitness Tracker Analysis Dashboard** (`DailySummary_cleaned.xlsx`), designed for an executive audience using KPI cards, contrast-driven charts, and concise insight callouts.

| Visualization | Purpose |
|---|---|
| KPI Summary Cards | Total users, average daily steps, average calories, average sleep duration at a glance |
| Average Daily Steps by Weekday | Shows the Saturday peak / Sunday drop pattern |
| Average Time Spent by Activity Level | Shows sedentary time dominance vs. active categories |
| Average Sleep Duration by Weekday | Shows sleep consistency across the week |
| Weekend vs. Weekday Activity Comparison | Shows the near-parity between weekday and weekend averages |
| Daily Steps vs. Calories Burned | Moderate positive correlation (R² = 0.35) |
| Sleep Duration vs. Daily Steps | Weak correlation (R² = 0.0362) — more sleep does not predict more activity |

**Key Business Insights**
- **Daily Activity:** Users average 7,638 daily steps, slightly below the recommended 8,000/day goal. Peaks Saturday, lowest Sunday.
- **Activity Intensity:** Most daily time is sedentary; moderate/vigorous activity is a small share of routines.
- **Sleep Pattern:** ~7 hours/night average, ~91.5% efficiency.
- **Sleep vs. Activity:** Little to no strong relationship — longer sleep ≠ higher activity.
- **Weekly Pattern:** Sharp Saturday peak and Sunday drop make weekday/weekend averages roughly similar overall.

---

## 06 — Act: Recommendations

Three marketing recommendations were developed for **Bellabeat Leaf** — chosen because its activity, sleep, and stress-tracking functions most directly align with the behavioral patterns found in this dataset.

### Recommendation 1 — Personalized Haptic Step-Goal Reminders
Introduce personalized haptic reminders on Bellabeat Leaf to encourage users to reach the recommended daily step goal of 8,000 steps. Since sleep quality data shows efficiency is already strong (91.5%), Leaf's product focus should prioritize activity nudges over sleep-quality features.

### Recommendation 2 — Inactivity Vibration Alerts
Enable Leaf's built-in vibration alert to trigger after 60 minutes of continuous inactivity, directly targeting the finding that the most common daily pattern is full-day sedentary behavior (mode = 1,440 minutes/day) and that active minutes occur in short, infrequent bursts.

### Recommendation 3 — Targeted Movement Challenges (Weekday Dip & Sunday Drop)
Launch movement challenges on the lowest-activity weekdays — Thursday and Friday average the fewest weekday steps (~7,406 and ~7,448) — powered by Leaf activity data synced to the Bellabeat app, while also addressing the sharp drop in activity on Sundays (6,933 steps, the lowest of any day).

**Expected Business Impact**
- Increase daily physical activity.
- Reduce sedentary behavior.
- Improve weekday engagement.
- Increase Bellabeat Leaf adoption.
- Support data-driven marketing campaigns.

**Data Limitations**
- Dataset contains data from only 33 Fitbit users.
- Observation period is limited to one month (12 April – 12 May 2016).
- Fitbit users may not fully represent Bellabeat's target customers (primarily women).
- Weight records are incomplete (only 24% user coverage) and were excluded from core insights.
- Results indicate behavioral trends rather than population-wide conclusions.

**Future Improvements**
- Incorporate demographic variables (age and gender) for user segmentation.
- Analyze seasonal activity patterns using longer observation periods.
- Evaluate user retention after implementing marketing campaigns.
- Develop predictive models to personalize activity recommendations.

---

## Conclusion

This analysis set out to answer three business questions: what trends exist in smart device usage, how those trends apply to Bellabeat customers, and how they can inform Bellabeat's marketing strategy. Across 33 Fitbit users observed over a one-month period, the data shows a consistent story: users fall short of recommended daily step goals, spend the overwhelming majority of their day sedentary, and are physically active only in short, infrequent bursts. At the same time, sleep quality is a genuine strength — averaging ~7 hours per night at 91.5% efficiency — meaning intervention effort is better directed at activity than at sleep.

These trends translate directly to Bellabeat customers, who share the same core need: gentle, consistent prompts to move more throughout the day rather than sleep-focused features. **Bellabeat Leaf** was selected as the product of focus because its activity, sleep, and stress-tracking capabilities are best positioned to act on these findings. The three recommendations — personalized haptic step-goal reminders, inactivity vibration alerts, and targeted movement challenges on low-activity weekdays and Sundays — are each grounded directly in a specific statistical pattern uncovered in this analysis, rather than generic wellness advice.

These findings should be read as directional behavioral trends rather than population-wide conclusions, given the dataset's small sample size, one-month observation window, and lack of demographic data relative to Bellabeat's core audience. The suggested next step is to pilot these three Leaf features with a subset of users, track the assumed engagement and retention metrics defined in [Ask](#01--ask-business-task), and use the results to refine both the feature design and the broader Bellabeat marketing strategy.

---

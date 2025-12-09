# E-Commerce Session Analysis & Data Integrity Audit   
[![Open in Deepnote](https://deepnote.com/buttons/launch-in-deepnote.svg)](https://deepnote.com/workspace/PolData-40264208-503b-448c-a998-f4e7dbcd20de/project/Digital-Marketing-Optimization-4f991c85-a4f1-4651-91c2-0876d552a54d/notebook/Notebook-9c37f2feab6546e8aa92af9dbbd3eeaa?utm_source=share-modal&utm_medium=product-shared-content&utm_campaign=notebook&utm_content=4f991c85-a4f1-4651-91c2-0876d552a54d)

![Project Banner](https://img.shields.io/badge/Status-Complete-success) ![Python](https://img.shields.io/badge/Python-3.11-blue)

### Executive Summary

This project analyzes Q4 2016 web traffic data for the Google Merchandise Store. The primary objectives were to audit the raw dataset for integrity issues, specifically **timezone-based duplicate sessions**, and provide actionable recommendations to optimize marketing spend and user experience.

**Key Achievement:** Identified a systemic "midnight split" anomaly in the raw data generation. While this edge case affected a minor volume in this sample, I included a robust deduplication pipeline to **prevent** metric inflation and ensure 100% accuracy for future scalable reporting.

---

### Visual Insights

*(These visualizations were generated using Python/Matplotlib as part of the analysis.)*



**1. Daily Web Engagement**

*Traffic trends showing standard work-week spikes and weekend dips.*

![91 Total Unique Session By DOW.png](Analysis/Visualizations/91%20Total%20Unique%20Session%20By%20DOW.png)



**2. Device Performance Gap**

*The critical "Mobile Gap": 24% of traffic but only 4.7% of revenue.*

![92 Devices Performance.png](Analysis/Visualizations/92%20Devices%20Performance.png)



**3. Marketing Efficiency Strategy (Dual-Axis Analysis)**

*This combo chart contrasts Volume (Revenue) vs. Efficiency (Conversion Rate). It highlights that while **Social** drives traffic, it fails to convert (0.2%), whereas **Referral** is highly efficient (6.4%), validating the recommendation to scale ad spend.*

![93 Channels Performance.png](Analysis/Visualizations/93%20Channels%20Performance.png)

---

### Project Context & Workflow

#### **1. Situation**

The business stakeholders required a clear view of Q4 performance to plan for the upcoming year. However, the raw data (99k+ rows) contained inconsistencies:

- Duplicate session IDs suggesting data recording errors.
- Timestamps in UTC, misaligned with the business's US Pacific operations.
- Some wrong geolocation data (for example, regions mismatching countries).

#### **2. Task**

My role as a Data Analyst was to:

1. **Audit and Clean** the dataset to establish a trusted "Data Grain."
2. **Engineer Features** to handle Timezone conversions and Daylight Saving Time (DST).
3. **Analyze Performance** to identify the most efficient acquisition channels.

#### **3. Action (The Technical Approach)**

I utilized **Python (Pandas)** for data orchestration and **DuckDB** for high-performance SQL querying within a Jupyter Notebook (I used Deepnote.com as work environment). 

- **Advanced Data Cleaning**:
    - **Timezone Logic**: I wrote SQL to convert UNIX timestamps to Pacific Time (PST/PDT), explicitly coding logic to handle the **Nov 6th Daylight Saving Time switch**. This ensured sessions were attributed to the correct business day.
    - **Deduplication**: I discovered that sessions crossing midnight UTC were split into two rows. I engineered a deduplication pipeline using `GROUP BY` and aggregation functions (`SUM` for `pageviews`, `MAX` for revenue) to merge these back into unique sessions.
    - **Outlier Removal**: Programmatically identified and dropped geolocation errors (for example, "Region: Abu Dhabi" inside "Country: USA") to prevent skew.
- **Strategic Analysis**:
    - Segmented users by **Device Category** to calculate Revenue per Session.
    - Calculated **Conversion Rates** by Marketing Channel to measure efficiency vs. volume.

#### **4. Results & Recommendations**

The analysis yielded three critical business insights:

- **The Mobile Experience Gap**:
    - **Finding**: Mobile users make up **24%** of traffic but contribute only **4.7%** of revenue.
    - **Recommendation**: Prioritize a UX/UI audit of the mobile checkout flow. A fractioned mobile experience is hindering significant potential revenue .
- **Marketing Efficiency**:
    - **Finding**: **Referral** traffic is the efficiency leader with a **6.3% conversion rate**. Conversely, **Social** media drives traffic but fails to convert (**0.16%**).
    - **Recommendation**: Move budget from low-performing Social campaigns to boost high-converting Referral partnerships.
- **Data Integrity & Scalability**:
    - **Finding**: Identified a logic flaw where sessions crossing midnight UTC were split into duplicates.
    - **Action**: Engineered a deduplication process using SQL aggregation.
    - **Impact**: Although the error rate in this specific quarter was low, implementing this fix establishes a **trusted data baseline**, ensuring that future analysis remains accurate and immune to this double counting error.

---

### Technical Skills Demonstrated

- **Languages**: Python, SQL (DuckDB dialect).
- **Libraries**: Pandas, Matplotlib, Seaborn.
- **Techniques**:
    - Complex SQL Aggregations & Window Functions.
    - Timezone Normalization & Date Math.
    - Data Profiling & Statistical Summaries.
    - Data Visualization (Dual-Axis & Grouped Bar Charts).

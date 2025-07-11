# An Analytical Report on the South East Queensland Public Transport Network

## Technology Stack
**Language:**  
- Python 3

**Data Manipulation & Analysis:**  
- **Pandas** – Flexible data structures and powerful data analysis tools  
- **SQLAlchemy** – ORM for managing SQL databases in Python  
- **Psycopg2** – PostgreSQL adapter for executing raw SQL queries

**Database:**  
- **PostgreSQL** – Relational database for structured GTFS data storage

**Data Visualization:**  
- **Matplotlib** & **Seaborn** – For creating static charts and statistical heatmaps  
- **Folium** – For rendering interactive geospatial maps with Leaflet.js

**Development & Version Control:**  
- **Jupyter Notebook** – For analysis, documentation, and interactive visualization  
- **Git & GitHub** – For version control and project presentation.
---


## Table of Contents

1. [Executive Summary](#1-executive-summary)  
2. [Introduction](#2-introduction)  
3. [Problem Statement & Hypotheses](#3-problem-statement--hypotheses)  
4. [Methodology](#4-methodology)  
5. [Analysis and Findings](#5-analysis-and-findings)  
6. [Limitations of the Analysis](#6-limitations-of-the-analysis)  
7. [Conclusion & Recommendations](#7-conclusion--recommendations)  
---
### 1. Executive Summary

This report presents a comprehensive analysis of the South East Queensland (SEQ) public transport network using scheduled data from Translink's General Transit Feed Specification (GTFS). The analysis reveals a system that is heavily **optimized for weekday commuters** and **geographically centered around the Brisbane CBD**.

Key findings indicate that a small number of high-frequency bus routes, such as the **CityGlider (60 & 61)** and university-focused **Route 66**, form the backbone of the network. Service levels drop by nearly 50% on weekends. The network's busiest hubs, including **King George Square Bus Station** and **Central Train Station**, are concentrated in the CBD and exhibit classic bimodal peak activity during morning (7-9 AM) and evening (4-6 PM) commuter periods. This analysis provides a foundational understanding of the network's operational structure, which is critical for urban planning and service optimization.

### 2. Introduction

Understanding the structure and usage patterns of a public transport network is essential for effective urban planning, resource allocation, and improving citizen mobility. This project undertakes a deep-dive analysis of the SEQ public transport system, operated by Translink. By processing and analyzing the publicly available GTFS data, we aim to transform raw, tabular data into actionable insights about the network's scale, key corridors, operational patterns, and geographic distribution.

### 3. Problem Statement & Hypotheses

The primary challenge is to process a complex, multi-file relational dataset to answer fundamental questions about the network's characteristics. This project tests the following hypotheses:

*   **Hypothesis 1 (Route Dominance):** A small subset of bus routes will account for a disproportionately large share of all scheduled trips.
*   **Hypothesis 2 (Weekday Bias):** Scheduled services will be significantly more frequent on weekdays compared to weekends, reflecting a commuter-centric design.
*   **Hypothesis 3 (CBD Centrality):** The busiest transport hubs (both bus and train) will be geographically concentrated in Brisbane's Central Business District (CBD).
*   **Hypothesis 4 (Commuter Peaks):** Network activity at major hubs will peak during typical morning and evening rush hours.

### 4. Methodology

The analysis was conducted using a two-phase methodology:

1.  **Data Processing (ETL):** Raw GTFS [`seq-translink-etl/data`](seq-translink-etl/data/) files were ingested into a PostgreSQL database using a Python script. This phase included critical data cleaning steps: handling missing values, correcting data types, removing duplicates, and standardizing text fields. This resulted in a clean, reliable, and analysis-ready relational database.
2.  **Data Analysis & Visualization:** A Jupyter Notebook was used to connect to the database, load the raw data, and perform all data cleaning. Subsequent analysis was performed using SQL queries, including **window functions (`RANK()`, `ROW_NUMBER()`)**, to aggregate and extract insights. The results were visualized using Python libraries (Matplotlib, Seaborn, Folium).

### 5. Analysis and Findings

#### 5.1. Top 10 Most Frequent Routes
![Top 10 Bus Routes](images/top_10_bus_route.png)
**Finding:** As predicted by **Hypothesis 1**, a few routes dominate service frequency. **The CityGlider (60, 61) and UQ Lakes (66)** routes have substantially more scheduled trips than others, establishing them as the primary arteries of the bus network.

#### 5.2. Service Levels by Day of the Week
![Trips per Weekday](images/service_levels_by_day_of_the_week.png)
**Finding:** This chart strongly supports **Hypothesis 2**. There is a clear and significant drop in service levels on Saturday and Sunday compared to the consistent, high volume of trips from Monday to Friday.

#### 5.3. Busiest Transport Hubs
![Top 10 Bus Stops](images/busiest_bus_hub.png)
**Finding:** The busiest bus and train stops are overwhelmingly located in or directly adjacent to the Brisbane CBD (e.g., King George Square, Cultural Centre, Central Station). This confirms **Hypothesis 3**, highlighting the CBD's role as the network's central nexus.

#### 5.4. Geographic Distribution of All Stops
![Map of All Stops](images/bus_vs_train.png)
**Finding:** This interactive map shows a high density of stops in the urban core of Brisbane, with services extending to surrounding regions. The clustering capability allows for an intuitive exploration of service coverage.

#### 5.5. Weekly & Hourly Activity Heatmaps
![Weekly Heatmap](images/weekly_activity_heatmaps.png)
![Hourly Heatmap](images/hourly_activity_heatmaps.png)
**Finding:** These heatmaps provide compelling evidence for **Hypothesis 4**. The weekly heatmap reinforces the weekday vs. weekend service drop-off across all major stops. The hourly heatmap clearly illustrates the bimodal commuter pattern, with activity peaking between 7-9 AM and 4-6 PM.

#### 6. Analysis with Window Functions

To gain deeper insights, we used SQL window functions for ranking and sequential analysis.

##### **Service Span of Key Routes**
**Finding:** By using `ROW_NUMBER()` to identify the first and last trips of the day for key routes, we can visualize their operational hours. The chart clearly shows that high-frequency routes like the **CityGlider (60)** not only have many trips but also the longest service span, starting early in the morning and running late into the night, confirming their role as the network's core arteries.

##### **Ranking Routes by Number of Stops**
```
Top 15 Bus Routes Ranked by Number of Unique Stops Serviced:
   route_short_name                route_long_name  stop_count  rank_val    dense_rank_val
0               599     Great Circle Line anti-clockwise         173         1               1
1               598        Great Circle Line clockwise           172         2               2
2               330  Bracken Ridge to City, Queen Street         109         3               3
...
```
**Finding:** Using `RANK()` and `DENSE_RANK()`, I identified the routes with the most extensive coverage. The **"Great Circle Line" routes (598/599)** service the highest number of unique stops, indicating they are crucial for connecting a wide range of suburbs rather than just a direct point-to-point corridor. This analysis helps distinguish between high-frequency routes and high-coverage routes.
### 7. Limitations of the Analysis

It is crucial to acknowledge the limitations of this study, which offer avenues for future work:

*   **Scheduled vs. Actual Data:** This analysis is based on the GTFS *schedule*. It does not reflect real-world conditions such as traffic delays, vehicle breakdowns, or trip cancellations.
*   **No Passenger Data:** The metric "activity count" (number of scheduled arrivals/departures) is a proxy for how "busy" a stop is. It does not represent actual passenger numbers (boardings and alightings).
*   **Static Dataset:** The analysis is a snapshot based on a single GTFS data release. It does not capture seasonal variations, holiday schedules, or long-term trends in the network.

### 7. Conclusion & Recommendations

This analysis successfully processed raw transit data to reveal the core operational characteristics of the SEQ public transport network. The findings confirmed all initial hypotheses, painting a picture of a system that is **CBD-centric and tailored to a weekday-commuting population**.

Based on these findings and limitations, the following next steps are recommended:

*   **Performance Analysis:** Integrate real-time GTFS data to analyze on-time performance and identify routes or times of day prone to delays.
*   **Accessibility Study:** Use network graph analysis to identify "transport deserts" or areas with poor access to key amenities like hospitals and employment centers.
*   **Develop an Interactive Dashboard:** Create a web-based dashboard (using Streamlit or Dash) or Power BI to allow planners and the public to explore these insights dynamically.
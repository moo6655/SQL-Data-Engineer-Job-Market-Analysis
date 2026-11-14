# Exploratory Data Analysis w/ SQL: Job Market Analytics

![Project 1 Overview](../Images/1_1_Project1_EDA.png)

A SQL project analyzing the data engineer job market using real-world job posting data. It demonstrates my ability to **write production-quality analytical SQL, design efficient queries, and turn business questions into data-driven insights**.

## 🧾 Executive Summary (For Hiring Managers)

- ✅ **Project scope:** Designed and executed **3 targeted SQL queries** to uncover what drives hiring demand and pay in the data engineering market.
- ✅ **Data modeling:** Connected **fact, dimension, and bridge tables** inside a star schema to turn raw job listings into structured insights.
- ✅ **Analytics:** Combined **aggregations, conditional filtering, and custom scoring** to rank skills by popularity, salary, and overall career ROI.
- ✅ **Outcomes:** Pinpointed **core market trends**—proving why SQL and Python form the baseline while cloud and infrastructure tools drive top compensation.

If you only have a minute, review these:

- [01_top_demanded_skills.sql](./01_top_demanded_skills.sql) – Measures skill frequency across job listings using multi-table joins.
- [02_top_paying_skills.sql](./02_top_paying_skills.sql) – Calculates median salaries to reveal the highest-earning technical skills.
- [03_optimal_skills.sql](./03_optimal_skills.sql) – Ranks skills by balancing job volume against compensation to find the best return on effort.

## 🧩 Problem & Context

Breaking into or advancing in data engineering requires knowing which tools actually matter to employers. This project answers three practical career questions:

- 🎯 **Most in-demand:** Which technical skills appear most often in data engineering job descriptions?
- 💰 **Highest paid:** Which specialized tools command the highest median compensation?
- ⚖️ **Best trade-off:** Which skills offer the strongest mix of abundant job openings and high pay?

To answer these questions, I queried a relational data warehouse organized in a **star schema**:

![Data warehouse](../Images/1_2_Data_Warehouse.png)

- **Fact Table:** `job_postings_fact` – Stores core job listing records, including role titles, remote work flags, posting dates, and yearly salary figures.
- **Dimension Tables:**
  - `company_dim` – Holds employer details tied to each job posting.
  - `skills_dim` – Acts as a master lookup catalog of skill names and categories.
- **Bridge Table:** `skills_job_dim` – Connects job postings to skills, resolving the many-to-many relationship where one job requires multiple tools.

By joining these tables together, I translated thousands of individual job records into clear hiring benchmarks.

## 🧰 Tech Stack

- 🐤 **Query Engine:** DuckDB for fast, local analytical processing on large datasets.
- 🧮 **Language:** SQL for data extraction, statistical aggregation, and custom metric creation.
- 📊 **Data Model:** Star schema architecture using fact, dimension, and bridge tables.
- 🛠️ **Development:** VS Code for writing clean scripts paired with the DuckDB CLI for rapid testing.
- 📦 **Version Control:** Git and GitHub for organizing, documenting, and sharing reproducible code.

## 🏗 Analysis Overview

### Query Structure

- [Top Demanded Skills](./01_top_demanded_skills.sql) – Ranks the top 10 most requested tools across data engineering postings by counting skill occurrences.
- [Top Paying Skills](./02_top_paying_skills.sql) – Identifies the top 25 highest-earning skills by calculating median annual salaries for postings with disclosed pay.
- [Optimal Skills](./03_optimal_skills.sql) – Evaluates remote data engineering roles with at least 100 postings, combining demand and median salary into a single value score to highlight high-ROI skills.

## 💻 SQL Skills Demonstrated

### Query Design & Optimization

- **Complex Joins:** Linked `job_postings_fact`, `skills_job_dim`, and `skills_dim` with `INNER JOIN` operations to map every job to its required skills.
- **Aggregations:** Used `COUNT()`, `MEDIAN()`, and `ROUND()` to summarize large volumes of listings into clean, readable metrics.
- **Filtering:** Applied multi-condition `WHERE` clauses (`job_title_short`, `job_work_from_home`, and non-null salaries) to isolate exact target cohorts.
- **Sorting & Limiting:** Ranked outputs cleanly using `ORDER BY ... DESC` and `LIMIT` to spotlight top performers.

### Data Analysis Techniques

- **Grouping:** Used `GROUP BY` to roll up job counts and salary distributions at the individual skill level.
- **Calculated Metrics:** Built custom composite formulas combining job demand and median salary to evaluate skill value beyond raw volume.
- **HAVING Clause:** Filtered out low-sample outliers after aggregation by requiring a minimum threshold of job postings (`COUNT(...) > 100`).
- **NULL Handling:** Excluded incomplete compensation records (`salary_year_avg IS NOT NULL`) so missing salary data never skewed median calculations.
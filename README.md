# Finance-Recruitment-Intelligence-Workforce-Analytics
## Project Overview

This project was developed as part of the **30 Days Data Analytics Challenge – Week 2**. It transforms raw finance recruitment data into actionable business intelligence using **Power BI**. A global financial recruitment organisation needed deeper insights into hiring trends, salary competitiveness, skill demand, and recruitment efficiency. This solution delivers **three executive-level interactive dashboards** to drive strategic decisions in talent acquisition, salary benchmarking, and workforce planning.

## Business Objectives

- Analyze finance job demand across roles, departments, industries, and locations
- Evaluate salary competitiveness by job title and experience level
- Identify in-demand skills and finance tools
- Assess recruitment efficiency and recruiter performance
- Understand workforce trends by company size and revenue

## Tools Used
- Power BI Desktop
- Power Query (ETL & Data Cleaning)
- DAX (Data Modelling & Calculations)
- Microsoft Excel

## Data Preparation Highlights

- Loaded flat Excel table into Power Query
- Fixed data types, rounded ratings, handled nulls
- Created dimension tables by referencing and removing duplicates
- Built a custom Date dimension table
- Merged foreign keys back into the Fact table

  ### Advanced Skills Handling
- The `Required Skills` column contained comma-separated values.
- Used **Unpivot Columns** technique to transform the multi-value skills into a long format.
- Created a dedicated **`Skills DIM`** bridge table to enable proper many-to-many relationship handling.
- This allowed accurate skill frequency analysis and cross-filtering in the "Skill and Salary Analysis" dashboard.

- ## Data Modeling (Star Schema)

I designed and implemented a clean **Star Schema** from a single flat table for better performance, scalability, and maintainability.

### Model Structure

- **Fact Table**: `Fact_Jobs` (core transactional metrics)
- **Dimension Tables**:
  - `Dim_Job`
  - `Dim_Company`
  - `Dim_Location`
  - `Dim_Recruiter`
  - `Dim_Date` (Calendar Table)
  - `Skills DIM` (for skill analysis)


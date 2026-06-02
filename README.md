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
![Data Modelling](https://github.com/adeolaolotu/Finance-Recruitment-Intelligence-Workforce-Analytics/blob/e98a8ea614b9c9bd56fea22039665b5d4bc9ae92/Star%20Schema.png)

## Key DAX Measures

I created a dedicated `_Measures` table to organize all calculations:

```dax
// Basic Count Measures
Total Jobs = COUNT('Job details DIM'[Job ID])

Salary Range = [Average Max Salary]-[Average Min Salary]

% Jobs requiring certification = DIVIDE([Jobs requiring Certification],[Total Jobs],0) 

// Time Intelligence
Total Jobs LY = 
    CALCULATE(
        [Total Jobs], 
        SAMEPERIODLASTYEAR('Calendar'[Date])
    )

// Year-over-Year Growth with Conditional Formatting
Total Jobs YOY = 
    VAR _CY = [Total Jobs]
    VAR _PV = [Total Jobs LY]
    VAR Per = DIVIDE(_CY - _PV, _CY)
    VAR _Format = SWITCH(
        TRUE(), 
        Per > 0, UNICHAR(11165) & " " & FORMAT(Per, "0.0%"),   // Up arrow
        Per < 0, UNICHAR(11167) & " " & FORMAT(Per, "0.0%"),   // Down arrow
        "No Change"
    )
    RETURN _Format
```
### Other Key Measures Include:
- Average Salary Midpoint
- Hiring Success Rate
- Avg Time to Hire
- Applicants per Job
- Remote Job Ratio
- Skill Frequency / Total Unique Skills

## Dashboards

### 1. Finance Job Market Overview
- KPIs: Total Jobs, Applicants, Hiring Companies, Open vs Closed Ratio, Average Experience
- Top Finance Roles, Work Mode & Employment Type Breakdown
- Geographic Distribution (Map) & Department-wise Hiring Trends

  ![Finance Job Market Overview](https://github.com/adeolaolotu/Finance-Recruitment-Intelligence-Workforce-Analytics/blob/faf95d48f1b657591da28bf861c3af58fb2100ae/Finance%20Job%20Market%20Overview.png)

### 2. Skill and Salary Analysis
- Salary Trends by Experience Level & Job Title
- Most Requested Skills & Finance Tools Demand Analysis
- Education & Certification Requirements

 ![Skill and Salary Analysis](https://github.com/adeolaolotu/Finance-Recruitment-Intelligence-Workforce-Analytics/blob/faf95d48f1b657591da28bf861c3af58fb2100ae/Skill%20and%20Salary%20Analysis.png)

### 3. Recruitment Performance and Efficiency
- Average Time to Hire, Hiring Success Rate, Recruiter Performance
- Time to Hire by Department
- Hiring Status & Company Size Analysis

  ![Recruitment Performance and Efficiency](https://github.com/adeolaolotu/Finance-Recruitment-Intelligence-Workforce-Analytics/blob/faf95d48f1b657591da28bf861c3af58fb2100ae/Recruitment%20Performance%20and%20Efficiency.png)

  ## Key Insights
- Data Analyst, Credit Analyst, and Internal Auditor are the most frequently posted positions, indicating strong market demand in these areas.
- SQL, SAP, Power BI, Tableau, and Excel are the top requested finance tools, highlighting the importance of technical proficiency in modern finance roles.
- Average salary midpoint stands at $77K, with a clear decline as experience level decreases. Executive and Senior roles command significantly higher compensation.
- Average Time to Hire is 32.89 days, with notable variation across departments and recruiters.
- Only 5.26% of applicants are successfully hired, suggesting a highly competitive talent market.
- Hybrid and Remote roles attract substantial applicant interest, though Full-Time Onsite positions still dominate job postings.

## Recommendations
- Focus recruitment efforts on Data Analysts, Credit Analysts, and Internal Auditors to meet current market demand.
- Partner with training providers to upskill candidates in high-demand tools (SQL, Power BI, SAP, Python) to improve candidate quality and placement speed.
- Expand Hybrid and Remote work options to increase applicant pools and improve hiring success rates.
- Implement recruiter performance dashboards and standardized processes to reduce the average Time to Hire below 30 days.
- Use salary benchmarking by experience level and revenue size to attract top talent, particularly for Senior and Executive roles.
- Prioritize candidates with relevant certifications (CFA, CPA, ICAN, ACCA) as over 81% of roles require them.

## How To Use
1. Download the .pbix file
2. Open in Power BI Desktop
3. Refresh data if needed

## References
[Finance Recruitment Intelligence Workforce Analytics Dataset](https://github.com/adeolaolotu/Finance-Recruitment-Intelligence-Workforce-Analytics/blob/de43a87e0a833fa6aed6ecd0de8d89f5acf5c352/Finance%20Recruitment%20Intelligence%20%26%20Workforce%20Analytics%20Dataset%20.%20Week%202%20Challenge.xlsx)

[PowerBI File](https://github.com/adeolaolotu/Finance-Recruitment-Intelligence-Workforce-Analytics/blob/f9bb02d323ea8444573ba25f3c69ffd2a7ea09eb/Finance%20Recruitment%20Intelligence%20Analysis.pbix)

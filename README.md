# HR Attrition & Workforce Analytics Dashboard

## Overview

This project analyses employee attrition, workforce demographics, and retention patterns using the IBM HR Analytics Employee Attrition dataset. The dashboard was developed in Power BI to help identify key drivers of employee turnover and provide insights into workforce retention risks across departments, job roles, income bands, and employee tenure groups.

The solution includes a multi-page interactive dashboard designed for HR and workforce analytics reporting.

---

## Objectives

- Analyse employee attrition trends across the organisation
- Identify workforce segments with the highest retention risk
- Explore relationships between overtime, work-life balance, compensation, and attrition
- Build an interactive HR analytics dashboard using Power BI
- Deliver business-focused workforce insights through data visualisation

---

## Tools & Technologies

- Power BI Desktop
- Power Query
- DAX (Data Analysis Expressions)
- Data Modelling
- Interactive Dashboard Design

---

## Dataset

**IBM HR Analytics Employee Attrition Dataset (Kaggle)**

Dataset includes:
- Employee demographics
- Department and job role data
- Compensation and salary information
- Job satisfaction metrics
- Work-life balance indicators
- Attrition status
- Tenure and experience metrics

---

# Data Preparation

## Data Cleaning

- Corrected data types for numeric and compensation-related fields
- Formatted salary-related columns as currency
- Removed unnecessary constant-value columns:
  - `EmployeeCount`
  - `Over18`
  - `StandardHours`

---

## Data Modelling

Created a simplified star-schema style model using:
- Employees (fact table)
- Department (dimension table)
- Job Role (dimension table)
- Education Level (dimension table)

Relationships were configured as:
- One-to-many
- Single-direction filtering

---

# Calculated Columns

## Age Group

```DAX
Age Group =
SWITCH(
    TRUE(),
    Employees[Age] < 30, "Under 30",
    Employees[Age] < 40, "30-39",
    Employees[Age] < 50, "40-49",
    "50+"
)
```

---

## Tenure Group

```DAX
Tenure Group =
SWITCH(
    TRUE(),
    Employees[Years At Company] < 3, "0-2 Years",
    Employees[Years At Company] < 6, "3-5 Years",
    Employees[Years At Company] < 10, "6-9 Years",
    "10+ Years"
)
```

---

## Income Band

```DAX
Income Band =
SWITCH(
    TRUE(),
    Employees[Monthly Income] < 5000, "Low Income",
    Employees[Monthly Income] < 10000, "Mid Income",
    "High Income"
)
```

---

## Education Level

```DAX
Education Level =
SWITCH(
    Employees[Education],
    1, "Below College",
    2, "College",
    3, "Bachelor",
    4, "Master",
    5, "Doctor"
)
```

---

## Work Life Balance Label

```DAX
Work Life Balance Label =
SWITCH(
    Employees[Work Life Balance],
    1, "Bad",
    2, "Good",
    3, "Better",
    4, "Best"
)
```

---

## Job Satisfaction Label

```DAX
Job Satisfaction Label =
SWITCH(
    Employees[Job Satisfaction],
    1, "Low",
    2, "Medium",
    3, "High",
    4, "Very High"
)
```

---

# DAX Measures

## Total Employees

```DAX
Total Employees =
DISTINCTCOUNT(Employees[Employee ID])
```

---

## Attrition Count

```DAX
Attrition Count =
CALCULATE(
    COUNTROWS(Employees),
    Employees[Attrition] = "Yes"
)
```

---

## Active Employees

```DAX
Active Employees =
[Total Employees] - [Attrition Count]
```

---

## Attrition Rate

```DAX
Attrition Rate =
DIVIDE(
    [Attrition Count],
    [Total Employees]
)
```

---

## Median Monthly Income

```DAX
Median Monthly Income =
MEDIAN(Employees[Monthly Income])
```

---

## Average Tenure

```DAX
Average Tenure =
AVERAGE(Employees[Years At Company])
```

---

## Average Job Satisfaction

```DAX
Average Job Satisfaction =
AVERAGE(Employees[Job Satisfaction])
```

---

## Overtime Attrition

```DAX
Overtime Attrition =
CALCULATE(
    [Attrition Count],
    Employees[Overtime] = "Yes"
)
```

---

# Dashboard Pages

## Page 1 — HR Attrition & Workforce Analytics

### Focus Areas
- Workforce overview
- Attrition monitoring
- Department analysis
- Demographic analysis

### Key Visuals
- KPI cards
- Attrition count by department
- Attrition count by job role
- Attrition rate by age group
- Attrition rate by income band
- Employee gender distribution

---

## Page 2 — Workforce Retention & Attrition Analysis

### Focus Areas
- Retention risk analysis
- Workforce behaviour patterns
- Attrition drivers

### Key Visuals
- Overtime vs attrition
- Attrition rate by tenure group
- Job satisfaction analysis
- Work-life balance vs attrition
- Interactive slicers for filtering

---

# Key Findings

- Overall employee attrition rate reached **16.1%**
- Employees with **0–2 years tenure** showed the highest attrition rates
- Employees with poor work-life balance experienced significantly higher turnover
- Overtime employees demonstrated substantially higher attrition levels
- Lower-income employees showed higher retention risk compared to higher-income groups
- Research & Development recorded the highest department attrition count
- Laboratory Technicians and Sales Executives showed the highest job-role attrition levels
- Employees under **30 years old** experienced the highest attrition rates

---

# Business Value

- Demonstrates workforce analytics and HR reporting capabilities
- Highlights employee retention risk factors
- Supports data-driven HR decision-making
- Provides interactive workforce monitoring through Power BI
- Showcases analytical storytelling and KPI development skills

---

# Challenges Faced

- Translating coded HR survey metrics into readable business labels
- Designing meaningful employee segmentation categories
- Building clean, readable multi-page dashboards
- Ensuring consistent formatting and logical visual hierarchy
- Managing attrition analysis using a non-time-series dataset

---

# Publish Link
- https://app.powerbi.com/groups/me/reports/adf1f13d-4d4b-42a7-8c93-1463c3fd6a6a/dbc298f4ae4768a5ec1e?experience=power-bi

---

# Outcome

Successfully developed a multi-page HR analytics dashboard in Power BI that provides actionable insights into employee attrition, workforce composition, and retention trends. The project demonstrates practical skills in data modelling, DAX development, dashboard design, and workforce analytics.

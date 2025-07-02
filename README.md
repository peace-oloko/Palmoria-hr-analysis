# Palmoria-hr-analysis
Exploratory data analysis of Palmora Company data

## Overview
Analyzed Palmoria Group’s HR data to identify gender-related insights and bonus allocation issues.

## Tools Used
- Power BI visuals (bar, pie,etc.)
- Power Query for cleaning data
- DAX formulas for calculating bonus and total pay
- Data model relationships (many-to-one)
- Filtering and grouping (like by gender, salary band, etc.)

## Key Insights
- Gender imbalance in some regions and departments
- Evidence of gender pay gap
- Several employees earning below regulatory minimum
- Bonus allocations vary by rating and department

## Deliverables
- Overall gender split
- Rating by Gender
- Gender pay gap and Requirment band
- Bonus calculations per employee
- Total payouts by region and company
- Clear visualizations showing findings

## Data Analysis

The Palmoria case was analyzed using Power BI with DAX, Power Query, and visual tools.

### Data Cleaning (Power Query)

- Replaced blank/missing gender values with `"Unspecified"`
- Removed rows where:
  - Salary is 0 or blank
  - Department is "NULL" or empty

### Key Measures and Visuals

#### Gender Distribution
- Visuals: Pie chart and stacked column
- Fields: Gender by Location (Region) and Department

#### Rating by Gender
- Stacked column chart showing count of employees by performance rating and gender

#### Gender Pay Gap
- Average Salary by Gender, by Department, and by Region (Location)
- Visuals: Stacked column charts

#### Minimum Wage Compliance
- Filter: Salary < 90,000 (non-compliant employees)
- Created a new column:

```DAX
SalaryBand = 
  SWITCH(TRUE(),
    [Salary] < 10000, "<$10k",
    [Salary] < 20000, "$10k–$20k",
    [Salary] < 30000, "$20k–$30k",
    [Salary] < 40000, "$30k–$40k",
    [Salary] < 50000, "$40k–$50k",
    [Salary] < 60000, "$50k–$60k",
    [Salary] < 70000, "$60k–$70k",
    [Salary] < 80000, "$70k–$80k",
    [Salary] < 90000, "$80k–$90k",
    [Salary] < 100000, "$90k–$100k",
    ">$100k"
  )

Bonus Calculation DAX
```dax
BonusPercent = RELATED('Bonus Rules'[BonusPercent]) / 100

BonusPay = [Salary] * [BonusPercent]

TotalPay = [Salary] + [BonusPay]




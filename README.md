# HR Analytics Dashboard – Power BI

A one-page Power BI dashboard that analyzes employee attrition: how many employees leave, in which departments, age groups and job roles, and how it relates to education, gender and job satisfaction. Education buttons filter the whole page.

**Tools:** Power BI · DAX · Power Query
**Data:** 1,470 employee records with 41 columns (`HR Data.xlsx`) – [TODO: add data source / link and confirm it is a sample or fictional dataset]

## Business questions

1. What is the overall attrition rate, and how many employees are active?
2. Which departments, job roles, education fields and age groups lose the most employees?
3. How does attrition differ by gender and age?
4. How satisfied are employees in each job role?

## Dashboard

KPI cards (employees, attrition, attrition rate, active employees, average age), department attrition, employees by age group and gender, a job satisfaction matrix by job role, attrition by education field, and attrition by gender within each age group. The buttons at the top (High School, Associates, Bachelor's, Master's, Doctoral) filter every visual by education level.

![Dashboard](images/01_dashboard.png)

*The screenshot shows the Associates Degree filter (282 employees, 44 of them left). The key findings below use all 1,470 employees unless stated otherwise.*

## Key findings (all employees)

All figures were recomputed from the raw data; the dashboard values match for the selected education level.

- **Overall:** **1,470 employees, 237 left (16.1% attrition)**, 1,233 are still active, and the average age is 36.9.
- **Education level:** attrition is highest for employees with a high school education (**18.2%**) and lowest for those with a doctoral degree (**10.4%**); Associates is 15.6%, Bachelor's 17.3% and Master's 14.6%.
- **Department:** Sales has the highest rate (**20.6%**), then HR (19.0%) and R&D (13.8%). R&D has the most leavers (133) simply because it is the biggest department.
- **Age:** employees under 25 leave at **39.2%**, compared with about **10%** for the 35–44 and 45–54 groups.
- **Overtime:** employees who work overtime leave at **30.5%**, about **three times** the rate of those who do not (10.4%).
- **Job role:** Sales Representatives (39.8%), Laboratory Technicians (23.9%) and HR staff (23.1%) have the highest attrition; Research Directors (2.5%) and Managers (4.9%) the lowest.
- **Travel and marital status:** frequent business travelers leave at 24.9% versus 8.0% for non-travelers, and single employees at 25.5% versus 12.5% for married employees.
- **Satisfaction and pay:** employees with the lowest job satisfaction rating (1) leave at 22.8% versus 11.3% for the highest rating (4). Leavers had a lower median monthly income (3,202 vs. 5,204) and shorter tenure (median 3 vs. 6 years).

## Data notes and limitations

- The education buttons filter all visuals; there is no "All" button, so deselect the active button to see all employees.
- The "Attrition Rate by Gender for Different Age Groups" section shows the **number of leavers** by gender in each age group, not rates.
- The Under 25 (97 employees) and Over 55 (69) groups are small, so their percentages change a lot with a few employees.
- Attrition is a yes/no flag without dates, so no trend over time can be shown, and relationships such as overtime vs. attrition are associations, not proof of cause.
- Two constant helper columns from the source file (`-2` and `0`) are hidden in the model.

## Data model and key measures

**Model:** one table, `HR data` (1,470 rows). Power Query adds three columns: `Attrition Count` (1 if the employee left), `Age Class` (sort order of the age bands) and `Education Sort` (orders the education buttons from High School to Doctoral).

**Key measures (DAX):**

```DAX
Attrition Rate =
SUM('HR data'[Attrition Count]) / SUM('HR data'[Employee Count])

Active Employees =
SUM('HR data'[Employee Count]) - SUM('HR data'[Attrition Count])
```

The KPI cards for employees and attrition sum `Employee Count` and `Attrition Count`, and average age averages `Age`.

## How to open

1. Download `HR Dashboard.pbix` and `HR Data.xlsx` from this repository.
2. Open the `.pbix` in Power BI Desktop and, if prompted, point the data source to your local copy of the Excel file.

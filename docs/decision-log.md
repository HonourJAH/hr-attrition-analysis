# Decision Log

This log records every finding from profiling and every decision taken in cleaning, in the order they were made. Each entry states what was found, what was decided, why, and the limit of the decision.

The dataset is the IBM HR Analytics Employee Attrition and Performance file. It was created by IBM data scientists, so the employees are fictional. Every finding in this project describes patterns in this dataset and not in a real organisation.

## Part 1: Raw data and first profiling

### Decision 1: Keep the raw file unchanged and load it as a connection only

- **Found:** The source file is WA_Fn-UseC_-HR-Employee-Attrition.csv, with 35 columns.
- **Decided:** The file is stored unchanged in data/raw and loaded into Power Query with data type detection switched off, so every column stays as text. The query is named raw_hr_attrition and loaded as a connection only, so no second copy of the raw data sits in a worksheet.
- **Why:** Automatic type detection can silently change values. Keeping the raw layer as plain text means any later problem can be traced to the source file and not to a loading step.
- **Limit:** Because every column is text at this stage, the profile cannot show minimum, maximum or average values. Those checks are done in the typed query (Decisions 5 to 7).

### Decision 2: Accept the row count and the employee identifier

- **Found:** The file has 1,470 rows. EmployeeNumber has 1,470 distinct values and 1,470 unique values, so each employee appears exactly once.
- **Decided:** No duplicate removal is needed, and EmployeeNumber is used as the employee identifier.
- **Why:** With no repeated identifier there are no repeated employee rows, so there is no worst-case duplicate effect to measure.
- **Limit:** The check shows that no identifier is repeated. It does not show that the same real person was not entered under two identifiers, which this file cannot reveal.

### Decision 3: Accept the data as complete

- **Found:** Every one of the 35 columns shows 0% empty and 0% error.
- **Decided:** No rows are removed and no values are filled in.
- **Why:** There is nothing missing to treat.
- **Limit:** Complete does not mean correct. A value can be present and still be impossible or placeholder-like. Range checks are done in Decisions 6 and 7.

### Decision 4: Leave out the three constant columns from the cleaned copy

- **Found:** EmployeeCount (1 in every row), StandardHours (80 in every row) and Over18 (Y in every row) each hold a single value.
- **Decided:** These three columns are left out of the cleaned copy. They stay in the raw data.
- **Why:** A column with one value cannot differ between employees who left and employees who stayed, so it cannot help answer any business question.
- **Limit:** Removing them changes no figure in the project. The row count stays at 1,470.

## Part 2: Data types and range checks

### Decision 5: Set data types in a separate query

- **Found:** After type detection, 25 columns are whole numbers and 10 columns are text, with 0% error and 0% empty in every column.
- **Decided:** Types are set in a second query, typed_hr_attrition, which references raw_hr_attrition, so the raw query is never edited. EmployeeNumber is kept as text because it identifies an employee and is never added or averaged.
- **Why:** Pivots can only add, average or find the minimum of numeric columns. A separate query also records exactly what changed between the raw file and the analysis.
- **Limit:** Zero errors means every value in the 25 numeric columns is a valid whole number. It does not mean the values are sensible, which is the purpose of the range checks below.

| Data type | Columns |
| --- | --- |
| Whole number | 25 |
| Text | 10 |
| Total | 35 |

### Decision 6: Accept the value ranges

- **Found:** Every continuous column falls inside a plausible range, and every coded column stays inside its documented scale.
- **Decided:** No values are corrected, capped or removed.
- **Why:** No age is under 18, no count or number of years is negative, and no code falls outside its documented scale.
- **Limit:** A plausible range does not prove each individual value is correct. The data is fictional, so there is no source record to check against.

Table 2.1: Range checks on continuous columns

| Column | Minimum | Maximum | Distinct values |
| --- | --- | --- | --- |
| Age | 18 | 60 | 43 |
| DistanceFromHome | 1 | 29 | 29 |
| MonthlyIncome | 1,009 | 19,999 | 1,349 |
| NumCompaniesWorked | 0 | 9 | 10 |
| PercentSalaryHike | 11 | 25 | 15 |
| TotalWorkingYears | 0 | 40 | 40 |
| YearsAtCompany | 0 | 40 | 37 |
| YearsInCurrentRole | 0 | 18 | 19 |
| YearsSinceLastPromotion | 0 | 15 | 16 |
| YearsWithCurrManager | 0 | 17 | 18 |

Table 2.2: Range checks on coded columns

| Column | Documented codes | Distinct values found |
| --- | --- | --- |
| Education | 1 to 5 | 5 |
| EnvironmentSatisfaction | 1 to 4 | 4 |
| JobInvolvement | 1 to 4 | 4 |
| JobSatisfaction | 1 to 4 | 4 |
| RelationshipSatisfaction | 1 to 4 | 4 |
| WorkLifeBalance | 1 to 4 | 4 |
| JobLevel | 1 to 5 | 5 |
| StockOptionLevel | 0 to 3 | 4 |
| PerformanceRating | 1 to 4 | 3 and 4 only |

### Decision 7: Do not use PerformanceRating to compare high and low performers

- **Found:** The documented scale for PerformanceRating runs from 1 to 4, but the data holds only the values 3 and 4 (minimum 3, maximum 4).
- **Decided:** The column stays in the cleaned copy, but no business question treats it as a measure of low versus high performance.
- **Why:** A column with only two values, both at the top of the scale, cannot separate weak performers from strong ones. The documented meaning of the full scale fails for this dataset.
- **Limit:** A comparison between ratings 3 and 4 can still be reported, but it describes a difference between two groups at the upper end of the scale and not a difference between poor and good performance.

### Baseline totals

| Measure | Value |
| --- | --- |
| Employees (rows) | 1,470 |
| Columns in the raw file | 35 |
| Attrition = No (stayed) | 1,233 |
| Attrition = Yes (left) | 237 |
| Attrition rate | 16.1% |

Every table in later parts of this project is reconciled back to these totals.

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

## Part 3: Clean copy and validation

### Decision 8: Build the clean copy by removing the constant columns

- **Found:** The typed query holds 35 columns, three of which carry a single value (Decision 4).
- **Decided:** A third query, clean_hr_attrition, references typed_hr_attrition and removes EmployeeCount, StandardHours and Over18. It is the only query loaded into a worksheet, and every pivot and chart in this project reads from it. The chain is raw_hr_attrition, then typed_hr_attrition, then clean_hr_attrition.
- **Why:** Keeping each change in its own query means anyone can open a step and see exactly what was changed between the source file and the analysis.
- **Limit:** The clean copy contains the same 1,470 employees as the raw file. Nothing else was changed, so any problem in the source values, such as the two-level PerformanceRating, carries through.

### Decision 9: Validate the clean copy against the raw data

- **Found:** A separate query, raw_checks, counts employees and adds up Age and MonthlyIncome from the raw data, grouped by Attrition. The same figures were recalculated from the clean table with COUNTIFS and SUMIFS, and compared on a validation sheet.
- **Decided:** The clean copy is accepted. All seven comparisons match and every difference is 0 (Table 3.1).
- **Why:** Matching counts show that no employee was dropped. Matching sums show that no age or income value changed.
- **Limit:** The check covers the row count and the sums of two columns by Attrition group. It does not compare every column. The only change in the clean query is the removal of three columns, so the other columns are unaffected by construction.

Table 3.1: Raw data compared with the clean copy

| Measure | Raw | Clean | Difference |
| --- | --- | --- | --- |
| Employees: Total | 1,470 | 1,470 | 0 |
| Employees: Yes | 237 | 237 | 0 |
| Employees: No | 1,233 | 1,233 | 0 |
| Total Age: Yes | 7,965 | 7,965 | 0 |
| Total Age: No | 46,313 | 46,313 | 0 |
| Total MonthlyIncome: Yes | 1,134,541 | 1,134,541 | 0 |
| Total MonthlyIncome: No | 8,424,768 | 8,424,768 | 0 |

### Baseline totals

| Measure | Value |
| --- | --- |
| Employees (rows) | 1,470 |
| Columns in the raw file | 35 |
| Columns in the clean copy (before AttritionFlag) | 32 |
| Columns in the clean copy (with AttritionFlag) | 33 |
| Columns in the clean copy (with AttritionFlag and label columns) | 40 |
| Columns in the clean copy (with AttritionFlag, label columns and band columns) | 43 |
| Attrition = No (stayed) | 1,233 |
| Attrition = Yes (left) | 237 |
| Attrition rate | 16.1% |

Every table in later parts of this project is reconciled back to these totals.

## Part 4: Preparing the clean copy for analysis

### Decision 10: Add an AttritionFlag column

- **Found:** Attrition holds the words Yes and No. A PivotTable can add up or average numbers but not words, so an attrition rate cannot be calculated from the column as it stands.
- **Decided:** A column named AttritionFlag was added to clean_hr_attrition with a conditional column in Power Query: 1 where Attrition is Yes and 0 where it is No, stored as a whole number. The Attrition column itself was kept.
- **Why:** The average of a 1 and 0 column is the share of employees who left, so a PivotTable can show the attrition rate for any group directly.
- **Limit:** The flag holds the same information as Attrition and adds no new facts. The sum of the flag was validated against the raw count of employees who left (Table 4.1).

Table 4.1: Check of the AttritionFlag column

| Measure | Raw | Clean | Difference |
| --- | --- | --- | --- |
| Employees who left (Attrition = Yes) | 237 | 237 | 0 |

Table 4.2: Result of the flag

| Group | Employees | Share of employees |
| --- | --- | --- |
| AttritionFlag = 1 (left) | 237 | 16.1% |
| AttritionFlag = 0 (stayed) | 1,233 | 83.9% |
| Total | 1,470 | 100.0% |

### Decision 11: Add readable labels for Education with a lookup table

- **Found:** Education is stored as a code from 1 to 5. A PivotTable built on the code would show 1, 2, 3, 4 and 5, which a reader cannot interpret without a legend.
- **Decided:** A lookup table named lookup_education was created on the lookups sheet, pairing each code with its label. A column named EducationLevel was added to the clean table with XLOOKUP, returning the label for each employee. Any code without a label would show "Not found".
- **Why:** Labels make every table and chart readable on its own, and the lookup table is the single place where the meaning of each code is recorded.
- **Limit:** The labels come from the description published with the dataset on Kaggle. The file itself contains only the codes, so nothing in the data confirms what each code means. The check shows that every employee received a label and that the counts add up to 1,470 (Tables 4.3 and 4.4). It cannot show that the published meanings are correct.

Table 4.3: Employees by education code

| Code | Label | Employees |
| --- | --- | --- |
| 1 | Below College | 170 |
| 2 | College | 282 |
| 3 | Bachelor | 572 |
| 4 | Masters | 398 |
| 5 | Doctors | 48 |
| Total | | 1,470 |

Table 4.4: Check of the EducationLevel column

| Measure | Expected | Clean | Difference |
| --- | --- | --- | --- |
| Rows without a label | 0 | 0 | 0 |

### Decision 12: Add readable labels for the three satisfaction columns with one shared lookup table

- **Found:** EnvironmentSatisfaction, JobSatisfaction and RelationshipSatisfaction are stored as codes from 1 to 4. The dataset documentation gives all three the same scale: 1 Low, 2 Medium, 3 High and 4 Very High.
- **Decided:** One lookup table named lookup_satisfaction_scale was created on the lookups sheet, and used by three new columns in the clean table: EnvironmentSatisfactionLevel, JobSatisfactionLevel and RelationshipSatisfactionLevel. Each column is filled with XLOOKUP, and any code without a label would show "Not found".
- **Why:** The three columns share one scale, so one table keeps the labels consistent. If a label ever needs to change, it changes in one place.
- **Limit:** The labels come from the dataset documentation, not from the file, which holds only the codes. The ratings are what employees reported about themselves, so a group's average describes what employees said and not their actual conditions. The check shows that every employee received a label in all three columns (Tables 4.5 and 4.6).

Table 4.5: Employees by satisfaction code

| Code | Label | EnvironmentSatisfaction | JobSatisfaction | RelationshipSatisfaction |
| --- | --- | --- | --- | --- |
| 1 | Low | 284 | 289 | 276 |
| 2 | Medium | 287 | 280 | 303 |
| 3 | High | 453 | 442 | 459 |
| 4 | Very High | 446 | 459 | 432 |
| Total | | 1,470 | 1,470 | 1,470 |

Table 4.6: Check of the satisfaction label columns

| Measure | Expected | Clean | Difference |
| --- | --- | --- | --- |
| EnvironmentSatisfactionLevel: rows without a label | 0 | 0 | 0 |
| JobSatisfactionLevel: rows without a label | 0 | 0 | 0 |
| RelationshipSatisfactionLevel: rows without a label | 0 | 0 | 0 |

### Decision 13: Add readable labels for WorkLifeBalance, JobInvolvement and PerformanceRating

- **Found:** WorkLifeBalance, JobInvolvement and PerformanceRating are stored as codes from 1 to 4. The dataset documentation gives WorkLifeBalance the labels 1 Bad, 2 Good, 3 Better and 4 Best. It gives JobInvolvement the same scale as the satisfaction columns, and PerformanceRating the labels 1 Low, 2 Good, 3 Excellent and 4 Outstanding.
- **Decided:** Two lookup tables were created on the lookups sheet: lookup_work_life_balance and lookup_performance_rating. JobInvolvement reuses lookup_satisfaction_scale from Decision 12, so the same labels are held in one place. Three columns were added to the clean table with XLOOKUP: WorkLifeBalanceLevel, JobInvolvementLevel and PerformanceRatingLevel. Any code without a label would show "Not found".
- **Why:** Labels make every table and chart readable on its own. The performance table lists all four documented codes so that the two codes that never occur are visible (Decision 7).
- **Limit:** The labels come from the dataset documentation, not from the file, which holds only the codes. The file does not say who gave the ratings or how. The check shows that every employee received a label in all three columns (Tables 4.7 and 4.8). It cannot show that the published meanings are correct.

Table 4.7: Employees by code for WorkLifeBalance and PerformanceRating

| Code | WorkLifeBalance label | Employees | PerformanceRating label | Employees |
| --- | --- | --- | --- | --- |
| 1 | Bad | 80 | Low | 0 |
| 2 | Good | 344 | Good | 0 |
| 3 | Better | 893 | Excellent | 1,244 |
| 4 | Best | 153 | Outstanding | 226 |
| Total | | 1,470 | | 1,470 |

Table 4.8: Check of the label columns

| Measure | Expected | Clean | Difference |
| --- | --- | --- | --- |
| WorkLifeBalanceLevel: rows without a label | 0 | 0 | 0 |
| JobInvolvementLevel: rows without a label | 0 | 0 | 0 |
| PerformanceRatingLevel: rows without a label | 0 | 0 | 0 |

### Decision 14: Keep JobLevel and StockOptionLevel as numbers

- **Found:** JobLevel (1 to 5) and StockOptionLevel (0 to 3) are coded columns, but the dataset documentation gives no meaning for the codes beyond the level itself.
- **Decided:** No lookup tables or label columns were created for these two columns. They stay numeric in the clean table.
- **Why:** A label would have to be invented, and an invented label would look like documented fact. The numbers already carry the order, with a higher number meaning a higher level.
- **Limit:** A reader of a pivot sees "Job level 3" and cannot tell what a level 3 job is. The findings describe these columns as levels and make no claim about the roles or the stock options behind them.

Table 4.9: Columns in the clean copy

| Stage | Columns |
| --- | --- |
| After removing the three constant columns (Decision 8) | 32 |
| After adding AttritionFlag (Decision 10) | 33 |
| After adding the seven label columns (Decisions 11 to 13) | 40 |
| After adding the three band columns (Decision 15) | 43 |

### Decision 15: Group Age, YearsAtCompany and MonthlyIncome into bands

- **Found:** Age has 43 distinct values, YearsAtCompany has 37 and MonthlyIncome has 1,349 (Table 2.1). A table with one row per value is too spread out to compare groups of employees.
- **Decided:** Three columns were added to the clean table with conditional columns in Power Query: AgeBand, TenureBand (from YearsAtCompany) and MonthlyIncomeBand. The band edges, set before any attrition rate was looked at, are in Table 4.10. A value outside every band would show "Not banded".
- **Why:** HR decisions are made about groups such as new joiners or the lowest paid, and not about individual ages or salaries. Fixing the edges before looking at results means they cannot be chosen to fit a pattern.
- **Limit:** The edges are a choice, and different edges could give different group results. The dataset does not state the currency of MonthlyIncome, so the income bands carry no currency. Some bands may hold fewer than 100 employees. Groups under 100 are flagged and not interpreted. The check shows that every employee fell into a band in all three columns (Table 4.11).

Table 4.10: Band edges

| Column | Band |
| --- | --- |
| AgeBand | Under 25 |
| AgeBand | 25 to 34 |
| AgeBand | 35 to 44 |
| AgeBand | 45 to 54 |
| AgeBand | 55 and over |
| TenureBand | Under 2 years |
| TenureBand | 2 to 4 years |
| TenureBand | 5 to 9 years |
| TenureBand | 10 to 19 years |
| TenureBand | 20 years and over |
| MonthlyIncomeBand | Under 3,000 |
| MonthlyIncomeBand | 3,000 to 4,999 |
| MonthlyIncomeBand | 5,000 to 6,999 |
| MonthlyIncomeBand | 7,000 to 9,999 |
| MonthlyIncomeBand | 10,000 and over |

Table 4.11: Check of the band columns

| Measure | Expected | Clean | Difference |
| --- | --- | --- | --- |
| AgeBand: rows not banded | 0 | 0 | 0 |
| TenureBand: rows not banded | 0 | 0 | 0 |
| MonthlyIncomeBand: rows not banded | 0 | 0 | 0 |

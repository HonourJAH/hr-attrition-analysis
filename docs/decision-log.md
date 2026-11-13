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
| Columns in the clean copy (with AttritionFlag, label columns, band columns and PromotionGapBand) | 44 |
| Columns in the clean copy (with AttritionFlag, label columns, band columns, PromotionGapBand and DistanceBand) | 45 |
| Columns in the clean copy (with AttritionFlag, label columns, band columns, PromotionGapBand, DistanceBand and SalaryHikeBand) | 46 |
| Columns in the clean copy (with AttritionFlag, label columns, band columns, PromotionGapBand, DistanceBand, SalaryHikeBand, RiskFactorCount and RiskFactorCombination) | 48 |
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
| After adding PromotionGapBand (Decision 16) | 44 |
| After adding DistanceBand (Decision 17) | 45 |
| After adding SalaryHikeBand (Decision 19) | 46 |
| After adding RiskFactorCount and RiskFactorCombination (Decision 21) | 48 |

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

### Decision 16: Group YearsSinceLastPromotion into a promotion gap band

- **Found:** YearsSinceLastPromotion has 16 distinct values, from 0 to 15 (Table 2.1). A table with one row per value is too spread out to compare groups of employees.
- **Decided:** A column named PromotionGapBand was added to the clean table with a conditional column in Power Query. The band edges, set before any attrition rate was looked at, are in Table 4.12. A value outside every band would show "Not banded".
- **Why:** Bands let the findings compare groups such as employees promoted recently and employees who have waited many years. Fixing the edges before looking at results means they cannot be chosen to fit a pattern.
- **Limit:** The edges are a choice, and different edges could give different group results. A value of 0 could mean promoted within the last year or never promoted, and the data does not say which. The documented meaning was checked against the data: no employee has a promotion gap longer than their time at the company (Table 4.13).

Table 4.12: Band edges for PromotionGapBand

| Band | Years since last promotion |
| --- | --- |
| 0 years | 0 |
| 1 to 2 years | 1 to 2 |
| 3 to 5 years | 3 to 5 |
| 6 to 10 years | 6 to 10 |
| 11 years and over | 11 or more |

Table 4.13: Checks of the PromotionGapBand column

| Measure | Expected | Clean | Difference |
| --- | --- | --- | --- |
| PromotionGapBand: rows not banded | 0 | 0 | 0 |
| Rows where the promotion gap is longer than the years at the company | 0 | 0 | 0 |

### Decision 17: Group DistanceFromHome into a distance band

- **Found:** DistanceFromHome has 29 distinct values, from 1 to 29 (Table 2.1). A table with one row per value is too spread out to compare groups of employees.
- **Decided:** A column named DistanceBand was added to the clean table with a conditional column in Power Query. The band edges, set before any attrition rate was looked at, are in Table 4.14. A value outside every band would show "Not banded".
- **Why:** Bands let the findings compare employees who live close to work with those who live far away. Fixing the edges before looking at results means they cannot be chosen to fit a pattern.
- **Limit:** The edges are a choice, and different edges could give different group results. The dataset does not state the unit of distance (kilometres or miles), so the bands carry no unit. The check shows that every employee fell into a band (Table 4.15).

Table 4.14: Band edges for DistanceBand

| Band | DistanceFromHome |
| --- | --- |
| 1 to 2 | 1 to 2 |
| 3 to 5 | 3 to 5 |
| 6 to 10 | 6 to 10 |
| 11 to 20 | 11 to 20 |
| 21 and over | 21 or more |

Table 4.15: Check of the DistanceBand column

| Measure | Expected | Clean | Difference |
| --- | --- | --- | --- |
| DistanceBand: rows not banded | 0 | 0 | 0 |

### Decision 18: Check that each label matches its code

- **Found:** The checks in Decisions 11 to 13 and 15 to 17 confirmed that every employee received a label or band. They did not confirm that the label was the right one for the employee's code.
- **Decided:** Three further checks were added to the validation sheet for Education, JobInvolvement and PerformanceRating. Each converts the label back to its code with a reverse XLOOKUP and counts the rows where the code does not match the original. All three counts are 0 (Table 4.16).
- **Why:** A label column that points at the wrong code still shows no errors, so only a check against the original code can catch it.
- **Limit:** The reverse lookup shows that the labels in these three columns are consistent with the lookup tables. It does not show that the lookup tables themselves are correct, which comes from the dataset documentation. The other label columns (EnvironmentSatisfactionLevel, JobSatisfactionLevel, RelationshipSatisfactionLevel and WorkLifeBalanceLevel) were not checked this way. Their group sizes in the pivots agree with the counts in the lookup tables (Tables 4.3, 4.5 and 4.7).

Table 4.16: Label against code checks

| Measure | Expected | Clean | Difference |
| --- | --- | --- | --- |
| EducationLevel: rows where the label does not match the code | 0 | 0 | 0 |
| JobInvolvementLevel: rows where the label does not match the code | 0 | 0 | 0 |
| PerformanceRatingLevel: rows where the label does not match the code | 0 | 0 | 0 |

### Decision 19: Group PercentSalaryHike into a salary hike band and use TrainingTimesLastYear as it is

- **Found:** PercentSalaryHike has 15 distinct values, from 11 to 25 (Table 2.1), which is too spread out to compare groups of employees. TrainingTimesLastYear was not included in the range checks in Decision 6. Its minimum is 0 and its maximum is 6, with 7 distinct values (Table 4.19).
- **Decided:** A column named SalaryHikeBand was added to the clean table with a conditional column in Power Query. The band edges, set before any attrition rate was looked at, are in Table 4.17. A value outside every band would show "Not banded". TrainingTimesLastYear is used as it is, because 7 values are few enough to compare directly.
- **Why:** Bands let the findings compare employees who received small and large salary increases. Fixing the edges before looking at results means they cannot be chosen to fit a pattern.
- **Limit:** The edges are a choice, and different edges could give different group results. The check shows that every employee fell into a band (Table 4.18). The range of TrainingTimesLastYear is plausible, but the data does not say what kind of training was counted.

Table 4.17: Band edges for SalaryHikeBand

| Band | PercentSalaryHike |
| --- | --- |
| 11 to 12 | 11 to 12 |
| 13 to 14 | 13 to 14 |
| 15 to 17 | 15 to 17 |
| 18 to 20 | 18 to 20 |
| 21 to 25 | 21 to 25 |

Table 4.18: Check of the SalaryHikeBand column

| Measure | Expected | Clean | Difference |
| --- | --- | --- | --- |
| SalaryHikeBand: rows not banded | 0 | 0 | 0 |

Table 4.19: Range check on TrainingTimesLastYear

| Column | Minimum | Maximum | Distinct values |
| --- | --- | --- | --- |
| TrainingTimesLastYear | 0 | 6 | 7 |

### Decision 20: Treat PerformanceRating and PercentSalaryHike as moving together

- **Found:** Salary hike and performance rating are almost the same measure in this dataset. Every employee with a hike under 18 is rated Excellent (1,079 employees), and every employee with a hike of 21 to 25 is rated Outstanding (171 employees). Only the 18 to 20 band holds both ratings (Table 4.20).
- **Decided:** Both columns stay in the clean table. Business question 9 reports them separately and states that they overlap. No business question treats a salary hike effect as separate from a rating effect, except inside the 18 to 20 band.
- **Why:** A rating and a salary increase that always go together cannot be separated by the data, so comparing them as if they were independent would count one pattern twice.
- **Limit:** The data does not show whether the rating decided the increase or the other way round. The documented meaning of two independent columns fails for this dataset, as it did for PerformanceRating in Decision 7.

Table 4.20: Salary hike band by performance rating (employees)

| Salary hike band | Excellent | Outstanding | Total |
| --- | --- | --- | --- |
| 11 to 12 | 408 | 0 | 408 |
| 13 to 14 | 410 | 0 | 410 |
| 15 to 17 | 261 | 0 | 261 |
| 18 to 20 | 165 | 55 | 220 |
| 21 to 25 | 0 | 171 | 171 |
| Total | 1,244 | 226 | 1,470 |

### Decision 21: Count five risk factors and label each combination

- **Found:** Business questions 2, 3, 4, 7 and 8 each found a factor with a clear pattern that held in its checks. Each question looked at one factor at a time, so none of them shows what happens when the factors occur together.
- **Decided:** Two columns were added to the clean table with custom columns in Power Query. RiskFactorCount holds the number of the five risk factors an employee has (0 to 5), and RiskFactorCombination holds a text label of the exact combination, such as "Overtime + Level 1", or "None". The five factors are listed in Table 4.21. Age and marital status were left out, because question 5 treats them as descriptions of who leaves and not as something an employer can act on. Distance from home, work-life balance, promotion gap, salary increase, performance rating and training were left out because their patterns were weaker or absent. Combinations with fewer than 30 employees are shown but not ranked.
- **Why:** A count and a label let the findings compare groups that have none, one or several risk factors, and let a manager see which combinations carry the most leavers. A minimum of 30 employees is used for ranking because one leaver changes the rate of a group of 30 by about 3 percentage points, and a ranking by rate alone would put groups of one or two employees first.
- **Limit:** The five factors were chosen from patterns found in this same data, so the rise in the attrition rate with the number of factors is built in and overstates how well the count would work for any other group of employees. The count gives each factor equal weight, and the factors overlap (for example, many employees in their first two years are also at job level 1). The 30-employee limit is a choice. The query uses the code JobInvolvement = 1 and not the label, because the label columns are Excel formulas outside the query. The checks are in Table 4.22.

Table 4.21: The five risk factors

| Risk factor | Defined as | Source question | Employees | Left | Attrition rate |
| --- | --- | --- | --- | --- | --- |
| Overtime | OverTime = Yes | 2 | 416 | 127 | 30.5% |
| Job level 1 | JobLevel = 1 | 3 | 543 | 143 | 26.3% |
| Under 2 years at the company | TenureBand = Under 2 years | 4 | 215 | 75 | 34.9% |
| Frequent travel | BusinessTravel = Travel_Frequently | 7 | 277 | 69 | 24.9% |
| Low job involvement | JobInvolvement = 1 | 8 | 83 | 28 | 33.7% |
| Total risk factors across all employees | | | 1,534 | | |

Table 4.22: Checks of the risk factor columns

| Measure | Expected | Clean | Difference |
| --- | --- | --- | --- |
| Sum of RiskFactorCount across all employees | 1,534 | 1,534 | 0 |
| Rows labelled None compared with rows with a count of 0 | 469 | 469 | 0 |
| Employees across the six risk factor counts | 1,470 | 1,470 | 0 |
| Leavers across the six risk factor counts | 237 | 237 | 0 |
| Employees across the 30 combinations | 1,470 | 1,470 | 0 |
| Leavers across the 30 combinations | 237 | 237 | 0 |

### Decision 22: Build the dashboard from pivots and slicers on separate sheets

- **Found:** Business questions 1 to 9 each answer one question with their own pivots. A manager cannot combine them without asking an analyst.
- **Decided:** Two sheets were added to the workbook. The dashboard_data sheet holds five pivots (time at the company, number of risk factors, job role, overtime, and the headline figures). The attrition_dashboard sheet holds four PivotCharts, the three headline figures (employees, leavers and attrition rate), and five slicers: Department, JobLevel, OverTime, BusinessTravel and TenureBand. Every slicer is connected to all five pivots. A note under the headline figures says that rates for groups of fewer than 30 employees are unreliable.
- **Why:** Slicers let a manager select a group and see every chart and the headline figures change together. The note puts the same size warning used in the ranking next to the rates.
- **Limit:** The charts show rates and not counts, and the dashboard does not hide groups under 30 employees, so only the headline Employees figure shows how large a selected group is. A bar can rest on very few employees. For example, with JobLevel 1 selected, the 20 years and over bar reads 0.0% and rests on one employee. The checks are in Table 4.23.

Table 4.23: Dashboard checks, with the slicer setting and the headline figures

| Slicer setting | Employees | Left | Attrition rate | Matches |
| --- | --- | --- | --- | --- |
| No slicer selected | 1,470 | 237 | 16.1% | Baseline totals |
| OverTime = Yes | 416 | 127 | 30.5% | Table 2.1 |
| Department = Sales | 446 | 92 | 20.6% | Table 1.1 |
| JobLevel = 1 | 543 | 143 | 26.3% | Table 3.2 |
| TenureBand = Under 2 years | 215 | 75 | 34.9% | Table 4.1 |

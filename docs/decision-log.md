# Decision Log

This log records every finding from profiling and every decision taken in cleaning, in the order they were made. Each entry states what was found, what was decided, why, and the limit of the decision.

The dataset is the IBM HR Analytics Employee Attrition and Performance file. It was created by IBM data scientists, so the employees are fictional. Every finding in this project describes patterns in this dataset and not in a real organisation.

## Part 1: Raw data and first profiling

### Decision 1: Keep the raw file unchanged and load it as a connection only

- **Found:** The source file is WA_Fn-UseC_-HR-Employee-Attrition.csv, with 35 columns.
- **Decided:** The file is stored unchanged in data/raw and loaded into Power Query with data type detection switched off, so every column stays as text. The query is named raw_hr_attrition and loaded as a connection only, so no second copy of the raw data sits in a worksheet.
- **Why:** Automatic type detection can silently change values. Keeping the raw layer as plain text means any later problem can be traced to the source file and not to a loading step.
- **Limit:** Because every column is text at this stage, the profile cannot yet show minimum, maximum or average values. Those checks follow once types are set in a separate cleaned query.

### Decision 2: Accept the row count and the employee identifier

- **Found:** The file has 1,470 rows. EmployeeNumber has 1,470 distinct values and 1,470 unique values, so each employee appears exactly once.
- **Decided:** No duplicate removal is needed, and EmployeeNumber is used as the employee identifier.
- **Why:** With no repeated identifier there are no repeated employee rows, so there is no worst-case duplicate effect to measure.
- **Limit:** The check shows that no identifier is repeated. It does not show that the same real person was not entered under two identifiers, which this file cannot reveal.

### Decision 3: Accept the data as complete

- **Found:** Every one of the 35 columns shows 0% empty and 0% error.
- **Decided:** No rows are removed and no values are filled in.
- **Why:** There is nothing missing to treat.
- **Limit:** Complete does not mean correct. A value can be present and still be impossible or placeholder-like. Range checks come after data types are set.

### Decision 4: Leave out the three constant columns from the cleaned copy

- **Found:** EmployeeCount (1 in every row), StandardHours (80 in every row) and Over18 (Y in every row) each hold a single value.
- **Decided:** These three columns are left out of the cleaned copy. They stay in the raw data.
- **Why:** A column with one value cannot differ between employees who left and employees who stayed, so it cannot help answer any business question.
- **Limit:** Removing them changes no figure in the project. The row count stays at 1,470.

### Baseline totals

| Measure | Value |
| --- | --- |
| Employees (rows) | 1,470 |
| Columns in the raw file | 35 |
| Attrition = No (stayed) | 1,233 |
| Attrition = Yes (left) | 237 |
| Attrition rate | 16.1% |

Every table in later parts of this project is reconciled back to these totals.

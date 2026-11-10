# Findings

This report answers ten business questions about employee attrition, one at a time. The data is the IBM HR Analytics Employee Attrition and Performance file, which IBM data scientists created, so the 1,470 employees are fictional. Every pattern below describes this dataset and not a real organisation.

How to read the tables:

- Attrition rate means the number of employees who left divided by the number of employees in the group.
- Groups with fewer than 100 employees are marked "Yes" in the column "Under 100 employees". Their figures are shown so the totals can be checked, but the text does not draw conclusions from them, because one or two leavers more or fewer would change the rate by several percentage points.
- A difference between groups is an association. It does not show that membership of the group caused the difference.
- Every figure in the text appears in a numbered table in the same section.

## Business question 1: How many employees left, and how do attrition rates differ by department and job role?

### Findings

Table 1.1: Attrition by department

| Department | Employees | Left | Attrition rate | Under 100 employees |
| --- | --- | --- | --- | --- |
| Human Resources | 63 | 12 | 19.0% | Yes |
| Research & Development | 961 | 133 | 13.8% | No |
| Sales | 446 | 92 | 20.6% | No |
| Total | 1,470 | 237 | 16.1% | No |

Table 1.2: Attrition by job role, in order of the number of employees who left

| Job role | Employees | Left | Attrition rate | Share of all leavers | Under 100 employees |
| --- | --- | --- | --- | --- | --- |
| Laboratory Technician | 259 | 62 | 23.9% | 26.2% | No |
| Sales Executive | 326 | 57 | 17.5% | 24.1% | No |
| Research Scientist | 292 | 47 | 16.1% | 19.8% | No |
| Sales Representative | 83 | 33 | 39.8% | 13.9% | Yes |
| Human Resources | 52 | 12 | 23.1% | 5.1% | Yes |
| Manufacturing Director | 145 | 10 | 6.9% | 4.2% | No |
| Healthcare Representative | 131 | 9 | 6.9% | 3.8% | No |
| Manager | 102 | 5 | 4.9% | 2.1% | No |
| Research Director | 80 | 2 | 2.5% | 0.8% | Yes |
| Total | 1,470 | 237 | 16.1% | 100.0% | No |

Table 1.3: Attrition by job role within each department

| Department | Job role | Employees | Left | Attrition rate | Under 100 employees |
| --- | --- | --- | --- | --- | --- |
| Human Resources | Human Resources | 52 | 12 | 23.1% | Yes |
| Human Resources | Manager | 11 | 0 | 0.0% | Yes |
| Research & Development | Healthcare Representative | 131 | 9 | 6.9% | No |
| Research & Development | Laboratory Technician | 259 | 62 | 23.9% | No |
| Research & Development | Manager | 54 | 3 | 5.6% | Yes |
| Research & Development | Manufacturing Director | 145 | 10 | 6.9% | No |
| Research & Development | Research Director | 80 | 2 | 2.5% | Yes |
| Research & Development | Research Scientist | 292 | 47 | 16.1% | No |
| Sales | Manager | 37 | 2 | 5.4% | Yes |
| Sales | Sales Executive | 326 | 57 | 17.5% | No |
| Sales | Sales Representative | 83 | 33 | 39.8% | Yes |
| Total | | 1,470 | 237 | 16.1% | No |

- Overall, 237 of the 1,470 employees left, an attrition rate of 16.1% (Table 1.1).
- By department, Sales had the highest rate among the departments with 100 or more employees (20.6% of 446), and Research & Development had the lowest (13.8% of 961). Human Resources (19.0% of 63) is under 100 employees and is not interpreted (Table 1.1).
- By job role, Laboratory Technician had the highest rate among the roles with 100 or more employees (23.9% of 259), followed by Sales Executive (17.5% of 326) and Research Scientist (16.1% of 292). Manufacturing Director (6.9%), Healthcare Representative (6.9%) and Manager (4.9%) had the lowest rates (Table 1.2).
- Three roles account for most of the leavers: Laboratory Technician (62 of 237, 26.2%), Sales Executive (57, 24.1%) and Research Scientist (47, 19.8%) (Table 1.2).
- The department rates hide large differences between roles. In Sales, Sales Executives had a rate of 17.5%, close to the overall 16.1%, while 33 of the 83 Sales Representatives left (39.8%). The Sales Representative group is under 100 employees, so its exact rate is uncertain, but it is far above every other role in Sales (Table 1.3).
- In Research & Development, Laboratory Technicians (23.9%) left far more often than Healthcare Representatives (6.9%) and Manufacturing Directors (6.9%), which are both groups of over 100 employees (Table 1.3).
- The Human Resources role (52 employees), the Research Director role (80) and the Manager rows within each department (11, 54 and 37) are under 100 employees and are not interpreted (Tables 1.2 and 1.3).

### What this means

A department rate on its own would point attention at Sales as a whole, but the figures show the high rate in Sales comes mostly from one role, Sales Representative, while Sales Executives are close to the company-wide rate. In the same way, the figures for Research & Development hide that Laboratory Technicians leave far more often than other roles in that department.

Rates and counts answer different questions. Laboratory Technician has both a high rate and the most leavers, so it is the clearest place to look first. Sales Executive has a rate close to the overall one, but it accounts for 24.1% of leavers because it is a large role. Sales Representative has the highest rate of all, but it is a small group and accounts for 13.9% of leavers.

### Limitations

- These are associations. The figures show where leavers are concentrated, not why they left.
- Department and job role are only two of the factors in the data. Overtime, pay, time at the company and other factors may explain part of the differences, and later questions examine them.
- The groups under 100 employees are shown for completeness and are not interpreted, except for the note on Sales Representatives, where the gap from every other Sales role is too large to come from one or two people.
- The data has no date, so it cannot show whether these rates are rising or falling.
- The employees are fictional, so the pattern may not match any real organisation.

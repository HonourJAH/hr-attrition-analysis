# Findings

This report answers ten business questions about employee attrition, one at a time. The data is the IBM HR Analytics Employee Attrition and Performance file, which IBM data scientists created, so the 1,470 employees are fictional. Every pattern below describes this dataset and not a real organisation.

How to read the tables:

- Attrition rate means the number of employees who left divided by the number of employees in the group.
- A difference between groups is an association. It does not show that membership of the group caused the difference.
- Where a group is so small that a few leavers more or fewer would change its rate noticeably, the text says that the data cannot tell whether the group really differs.
- Every figure in the text appears in a numbered table in the same section.

## Business question 1: How many employees left, and how do attrition rates differ by department and job role?

### Findings

Table 1.1: Attrition by department

| Department | Employees | Left | Attrition rate |
| --- | --- | --- | --- |
| Human Resources | 63 | 12 | 19.0% |
| Research & Development | 961 | 133 | 13.8% |
| Sales | 446 | 92 | 20.6% |
| Total | 1,470 | 237 | 16.1% |

Table 1.2: Attrition by job role, in order of the number of employees who left

| Job role | Employees | Left | Attrition rate | Share of all leavers |
| --- | --- | --- | --- | --- |
| Laboratory Technician | 259 | 62 | 23.9% | 26.2% |
| Sales Executive | 326 | 57 | 17.5% | 24.1% |
| Research Scientist | 292 | 47 | 16.1% | 19.8% |
| Sales Representative | 83 | 33 | 39.8% | 13.9% |
| Human Resources | 52 | 12 | 23.1% | 5.1% |
| Manufacturing Director | 145 | 10 | 6.9% | 4.2% |
| Healthcare Representative | 131 | 9 | 6.9% | 3.8% |
| Manager | 102 | 5 | 4.9% | 2.1% |
| Research Director | 80 | 2 | 2.5% | 0.8% |
| Total | 1,470 | 237 | 16.1% | 100.0% |

Table 1.3: Attrition by job role within each department

| Department | Job role | Employees | Left | Attrition rate |
| --- | --- | --- | --- | --- |
| Human Resources | Human Resources | 52 | 12 | 23.1% |
| Human Resources | Manager | 11 | 0 | 0.0% |
| Research & Development | Healthcare Representative | 131 | 9 | 6.9% |
| Research & Development | Laboratory Technician | 259 | 62 | 23.9% |
| Research & Development | Manager | 54 | 3 | 5.6% |
| Research & Development | Manufacturing Director | 145 | 10 | 6.9% |
| Research & Development | Research Director | 80 | 2 | 2.5% |
| Research & Development | Research Scientist | 292 | 47 | 16.1% |
| Sales | Manager | 37 | 2 | 5.4% |
| Sales | Sales Executive | 326 | 57 | 17.5% |
| Sales | Sales Representative | 83 | 33 | 39.8% |
| Total | | 1,470 | 237 | 16.1% |

- Overall, 237 of the 1,470 employees left, an attrition rate of 16.1% (Table 1.1).
- By department, Sales had the highest rate (20.6% of 446 employees) and Research & Development the lowest (13.8% of 961). Human Resources had 19.0% of 63 employees. With so few employees, the data cannot tell whether this differs from the company-wide rate (Table 1.1).
- By job role, Sales Representative had the highest rate (39.8%, 33 of 83 employees), followed by Laboratory Technician (23.9% of 259), Human Resources (23.1% of 52), Sales Executive (17.5% of 326) and Research Scientist (16.1% of 292). The Human Resources role is a small group, so the data cannot tell whether its rate differs from the company-wide rate (Table 1.2).
- Manufacturing Director (6.9% of 145), Healthcare Representative (6.9% of 131), Manager (4.9% of 102) and Research Director (2.5% of 80) had the lowest rates (Table 1.2).
- Three roles account for most of the leavers: Laboratory Technician (62 of 237, 26.2%), Sales Executive (57, 24.1%) and Research Scientist (47, 19.8%) (Table 1.2).
- The department rates hide large differences between roles. In Sales, Sales Executives had a rate of 17.5%, close to the overall 16.1%, while 33 of the 83 Sales Representatives left (39.8%). The Sales Representative group is smaller, so its exact rate is less certain, but the gap from every other role in Sales is too large to come from one or two employees (Table 1.3).
- In Research & Development, Laboratory Technicians left at 23.9%, far more often than Healthcare Representatives (6.9%) and Manufacturing Directors (6.9%) (Table 1.3).
- The Manager role is split across three departments into groups of 11, 54 and 37 employees. These groups are too small to compare with each other, so the Manager role is best read as a whole (4.9% of 102) (Tables 1.2 and 1.3).

### What this means

A department rate on its own would point attention at Sales as a whole, but the figures show the high rate in Sales comes mostly from one role, Sales Representative, while Sales Executives are close to the company-wide rate. In the same way, the figures for Research & Development hide that Laboratory Technicians leave far more often than other roles in that department.

Rates and counts answer different questions. Laboratory Technician has both a high rate and the most leavers, so it is the clearest place to look first. Sales Executive has a rate close to the overall one, but it accounts for 24.1% of leavers because it is a large role. Sales Representative has the highest rate of all, but it is a smaller group and accounts for 13.9% of leavers.

### Limitations

- These are associations. The figures show where leavers are concentrated, not why they left.
- Department and job role are only two of the factors in the data. Overtime, pay, time at the company and other factors may explain part of the differences, and later questions examine them.
- For the Human Resources department and role, and for the Manager role split by department, the groups are too small to tell whether the rates differ from the company-wide rate.
- The data has no date, so it cannot show whether these rates are rising or falling.
- The employees are fictional, so the pattern may not match any real organisation.

## Business question 2: Do employees who work overtime leave more often, and does this hold within each department and job role?

### Findings

Table 2.1: Attrition by overtime

| Overtime | Employees | Share of employees | Left | Share of all leavers | Attrition rate |
| --- | --- | --- | --- | --- | --- |
| No | 1,054 | 71.7% | 110 | 46.4% | 10.4% |
| Yes | 416 | 28.3% | 127 | 53.6% | 30.5% |
| Total | 1,470 | 100.0% | 237 | 100.0% | 16.1% |

Table 2.2: Attrition by overtime within each department

| Department | Overtime | Employees | Left | Attrition rate |
| --- | --- | --- | --- | --- |
| Human Resources | No | 46 | 7 | 15.2% |
| Human Resources | Yes | 17 | 5 | 29.4% |
| Research & Development | No | 690 | 59 | 8.6% |
| Research & Development | Yes | 271 | 74 | 27.3% |
| Sales | No | 318 | 44 | 13.8% |
| Sales | Yes | 128 | 48 | 37.5% |
| Total | No | 1,054 | 110 | 10.4% |
| Total | Yes | 416 | 127 | 30.5% |

Table 2.3: Difference in attrition rate between overtime and no overtime, by department

| Department | Rate without overtime | Rate with overtime | Difference (percentage points) | Overtime rate as a multiple of the rate without overtime |
| --- | --- | --- | --- | --- |
| Human Resources | 15.2% | 29.4% | 14.2 | 1.9 |
| Research & Development | 8.6% | 27.3% | 18.7 | 3.2 |
| Sales | 13.8% | 37.5% | 23.7 | 2.7 |
| Total | 10.4% | 30.5% | 20.1 | 2.9 |

Table 2.4: Attrition by overtime within each job role, in order of the number of employees who left

| Job role | Employees without overtime | Left | Rate | Employees with overtime | Left | Rate | Share of the role working overtime | Difference (percentage points) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Laboratory Technician | 197 | 31 | 15.7% | 62 | 31 | 50.0% | 23.9% | 34.3 |
| Sales Executive | 232 | 26 | 11.2% | 94 | 31 | 33.0% | 28.8% | 21.8 |
| Research Scientist | 195 | 14 | 7.2% | 97 | 33 | 34.0% | 33.2% | 26.8 |
| Sales Representative | 59 | 17 | 28.8% | 24 | 16 | 66.7% | 28.9% | 37.9 |
| Human Resources | 39 | 7 | 17.9% | 13 | 5 | 38.5% | 25.0% | 20.6 |
| Manufacturing Director | 106 | 6 | 5.7% | 39 | 4 | 10.3% | 26.9% | 4.6 |
| Healthcare Representative | 94 | 7 | 7.4% | 37 | 2 | 5.4% | 28.2% | -2.0 |
| Manager | 75 | 1 | 1.3% | 27 | 4 | 14.8% | 26.5% | 13.5 |
| Research Director | 57 | 1 | 1.8% | 23 | 1 | 4.3% | 28.8% | 2.5 |
| Total | 1,054 | 110 | 10.4% | 416 | 127 | 30.5% | 28.3% | 20.1 |

- Overall, 416 of the 1,470 employees (28.3%) work overtime. Of these, 30.5% left, against 10.4% of the employees who do not work overtime, about three times as often (Tables 2.1 and 2.3).
- Employees who work overtime made up 28.3% of the workforce but 53.6% of the leavers (127 of 237) (Table 2.1).
- The gap holds in every department. Employees who work overtime left more often in Human Resources (29.4% against 15.2%), Research & Development (27.3% against 8.6%) and Sales (37.5% against 13.8%). The differences are 14.2, 18.7 and 23.7 percentage points (Tables 2.2 and 2.3).
- In Human Resources only 17 employees work overtime, so the data cannot tell whether the gap there (1.9 times) really differs from the other two departments. It points the same way (Tables 2.2 and 2.3).
- The gap also holds inside job roles. Overtime employees left more often in 8 of the 9 roles (Table 2.4).
- In the three large roles with the most leavers, the rate with overtime was well above the rate without: Laboratory Technician 50.0% against 15.7%, Sales Executive 33.0% against 11.2%, and Research Scientist 34.0% against 7.2% (Table 2.4).
- The one exception is Healthcare Representative (5.4% with overtime, 7.4% without). It rests on 2 leavers among 37 employees who work overtime, which is too few to tell whether the role differs from the others (Table 2.4).
- Overtime is not concentrated in the roles that lose the most employees. The share of each role working overtime ranges from 23.9% to 33.2%, close to the 28.3% for the company. Laboratory Technician has the lowest share (23.9%) and one of the highest attrition rates (Table 2.4).
- Job role still matters among employees who do not work overtime. Sales Representatives left at 28.8%, Laboratory Technicians at 15.7% and Research Scientists at 7.2% (Table 2.4).
- Sales Representatives who work overtime had the highest rate in the table: 16 of 24 left (66.7%). The group is small, but the gap from the 28.8% for Sales Representatives without overtime is far too large to come from one or two employees (Table 2.4).
- For Research Director (1 leaver in each group), Human Resources and Manager, the groups are too small to compare the rates with confidence (Table 2.4).

### What this means

Employees who work overtime left much more often than those who do not, and this is not explained by department or by job role. The gap appears in every department and in nearly every role, and overtime is spread fairly evenly across roles. Overtime and job role are therefore two separate patterns that add up. Sales Representatives and Laboratory Technicians have high attrition with or without overtime, and overtime raises it further.

For an HR manager, workload is a direct place to look, starting with the roles where overtime and high attrition coincide: Laboratory Technician, Sales Executive, Research Scientist and Sales Representative.

### Limitations

- This is an association. The data does not show that overtime caused employees to leave.
- Overtime is recorded only as Yes or No. The data does not show how many hours, how often, or whether the overtime was paid.
- The data does not show when overtime happened relative to the decision to leave. Overtime could also be a result of colleagues leaving and work being shared among those who stayed.
- Pay has not yet been taken into account, and it may explain part of the gap. Question 3 examines it.
- For Human Resources, Manager and Research Director, and for Healthcare Representative with overtime, the groups are too small to compare with confidence.
- The data has no date, so it cannot show whether the pattern changed over time.
- The employees are fictional, so the pattern may not match any real organisation.

## Business question 3: Is lower pay linked to higher attrition, and does it still hold within each job level?

### Findings

Shares in the tables are rounded to one decimal place, so a column of shares can add up to 99.9% or 100.1% instead of exactly 100.0%.

Table 3.1: Attrition by monthly income band

| Monthly income band | Employees | Share of employees | Left | Share of all leavers | Attrition rate |
| --- | --- | --- | --- | --- | --- |
| Under 3,000 | 395 | 26.9% | 113 | 47.7% | 28.6% |
| 3,000 to 4,999 | 354 | 24.1% | 50 | 21.1% | 14.1% |
| 5,000 to 6,999 | 286 | 19.5% | 27 | 11.4% | 9.4% |
| 7,000 to 9,999 | 154 | 10.5% | 22 | 9.3% | 14.3% |
| 10,000 and over | 281 | 19.1% | 25 | 10.5% | 8.9% |
| Total | 1,470 | 100.0% | 237 | 100.0% | 16.1% |

Table 3.2: Attrition by job level

| Job level | Employees | Share of employees | Left | Share of all leavers | Attrition rate |
| --- | --- | --- | --- | --- | --- |
| 1 | 543 | 36.9% | 143 | 60.3% | 26.3% |
| 2 | 534 | 36.3% | 52 | 21.9% | 9.7% |
| 3 | 218 | 14.8% | 32 | 13.5% | 14.7% |
| 4 | 106 | 7.2% | 5 | 2.1% | 4.7% |
| 5 | 69 | 4.7% | 5 | 2.1% | 7.2% |
| Total | 1,470 | 100.0% | 237 | 100.0% | 16.1% |
| Of which: levels 2 to 5 combined | 927 | 63.1% | 94 | 39.7% | 10.1% |

Table 3.3: Attrition by monthly income band within each job level

| Job level | Monthly income band | Employees | Left | Attrition rate |
| --- | --- | --- | --- | --- |
| 1 | Under 3,000 | 381 | 112 | 29.4% |
| 1 | 3,000 to 4,999 | 162 | 31 | 19.1% |
| 2 | Under 3,000 | 14 | 1 | 7.1% |
| 2 | 3,000 to 4,999 | 192 | 19 | 9.9% |
| 2 | 5,000 to 6,999 | 284 | 26 | 9.2% |
| 2 | 7,000 to 9,999 | 44 | 6 | 13.6% |
| 3 | 5,000 to 6,999 | 2 | 1 | 50.0% |
| 3 | 7,000 to 9,999 | 110 | 16 | 14.5% |
| 3 | 10,000 and over | 106 | 15 | 14.2% |
| 4 | 10,000 and over | 106 | 5 | 4.7% |
| 5 | 10,000 and over | 69 | 5 | 7.2% |
| Total | | 1,470 | 237 | 16.1% |

Table 3.4: Where the lowest income band sits

| Measure | Employees or leavers in job level 1 | All employees or leavers in the band | Share in job level 1 |
| --- | --- | --- | --- |
| Employees with a monthly income under 3,000 | 381 | 395 | 96.5% |
| Leavers with a monthly income under 3,000 | 112 | 113 | 99.1% |

- Employees with a monthly income under 3,000 left at 28.6%, against 8.9% for those on 10,000 and over. This band holds 26.9% of the employees but 47.7% of the leavers (Table 3.1).
- The pattern is not a steady fall as pay rises. The 7,000 to 9,999 band (14.3%) had a higher rate than the 5,000 to 6,999 band (9.4%) (Table 3.1).
- Job level explains most of the gap. Level 1 holds 36.9% of the employees but 60.3% of the leavers, a rate of 26.3%. Levels 2 to 5 together had a rate of 10.1% (94 leavers among 927 employees) (Table 3.2).
- The lowest income band is almost entirely level 1: 381 of its 395 employees (96.5%) and 112 of its 113 leavers (99.1%). The 28.6% for this band is therefore mostly a level 1 figure (Table 3.4).
- Within level 1, pay still goes with attrition. Employees under 3,000 left at 29.4% and those on 3,000 to 4,999 at 19.1%, a gap of 10.3 percentage points. Both groups are large (Table 3.3).
- In levels 2 and 3, higher pay does not go with lower attrition. In level 2, the 3,000 to 4,999 band left at 9.9% and the 5,000 to 6,999 band at 9.2%. In level 3, the 7,000 to 9,999 band left at 14.5% and the 10,000 and over band at 14.2% (Table 3.3).
- Levels 4 and 5 each have only one income band (10,000 and over), so pay cannot be compared within them. Their rates are 4.7% and 7.2% (Table 3.3).
- Two cells are too small to read. Level 2 under 3,000 has 14 employees and 1 leaver, and level 3 at 5,000 to 6,999 has 2 employees and 1 leaver, so the 50.0% for the second one carries no information (Table 3.3).

### What this means

Low pay on its own does not explain the high attrition in the lowest income band. That band is mostly entry-level (level 1) jobs, and level 1 employees left far more often than employees at any other level. Pay matters inside level 1, where the lower-paid group left more often than the higher-paid group, but at levels 2 and 3 the data shows no such difference.

For an HR manager, the first place to look is level 1 as a whole, and then pay within it. Raising pay for the whole company's lowest band would not target the problem as well as looking at what level 1 jobs have in common.

### Limitations

- This is an association. The data does not show that pay caused employees to leave.
- Monthly income is shown in the dataset's own units. The data does not state the currency, and does not say whether it is before or after tax, or whether it includes bonuses.
- Time at the company has not yet been taken into account. Pay rises with time at the company, so new joiners may be both lower paid and more likely to leave. Question 4 examines time at the company.
- The income bands were fixed before any attrition rate was looked at (Decision 15), but different band edges could give different group results.
- Levels 4 and 5 contain only one income band each, so pay cannot be compared inside them.
- The data has no date, so it cannot show whether pay or attrition changed over time.
- The employees are fictional, so the pattern may not match any real organisation.

## Business question 4: How does attrition change with time at the company, and does the pattern hold within department, pay and job level?

### Findings

Shares in the tables are rounded to one decimal place, so a column of shares can add up to 99.9% or 100.1% instead of exactly 100.0%.

Table 4.1: Attrition by time at the company

| Time at the company | Employees | Share of employees | Left | Share of all leavers | Attrition rate |
| --- | --- | --- | --- | --- | --- |
| Under 2 years | 215 | 14.6% | 75 | 31.6% | 34.9% |
| 2 to 4 years | 365 | 24.8% | 66 | 27.8% | 18.1% |
| 5 to 9 years | 524 | 35.6% | 58 | 24.5% | 11.1% |
| 10 to 19 years | 273 | 18.6% | 29 | 12.2% | 10.6% |
| 20 years and over | 93 | 6.3% | 9 | 3.8% | 9.7% |
| Total | 1,470 | 100.0% | 237 | 100.0% | 16.1% |
| Of which: under 5 years combined | 580 | 39.5% | 141 | 59.5% | 24.3% |

Table 4.2: Attrition by time at the company within each department

| Time at the company | Department | Employees | Left | Attrition rate |
| --- | --- | --- | --- | --- |
| Under 2 years | Human Resources | 5 | 4 | 80.0% |
| Under 2 years | Research & Development | 149 | 47 | 31.5% |
| Under 2 years | Sales | 61 | 24 | 39.3% |
| 2 to 4 years | Human Resources | 20 | 5 | 25.0% |
| 2 to 4 years | Research & Development | 241 | 32 | 13.3% |
| 2 to 4 years | Sales | 104 | 29 | 27.9% |
| 5 to 9 years | Human Resources | 23 | 2 | 8.7% |
| 5 to 9 years | Research & Development | 341 | 33 | 9.7% |
| 5 to 9 years | Sales | 160 | 23 | 14.4% |
| 10 to 19 years | Human Resources | 8 | 0 | 0.0% |
| 10 to 19 years | Research & Development | 171 | 17 | 9.9% |
| 10 to 19 years | Sales | 94 | 12 | 12.8% |
| 20 years and over | Human Resources | 7 | 1 | 14.3% |
| 20 years and over | Research & Development | 59 | 4 | 6.8% |
| 20 years and over | Sales | 27 | 4 | 14.8% |
| Total | | 1,470 | 237 | 16.1% |

Table 4.3: Attrition by time at the company within each monthly income band

| Time at the company | Monthly income band | Employees | Left | Attrition rate |
| --- | --- | --- | --- | --- |
| Under 2 years | Under 3,000 | 122 | 56 | 45.9% |
| Under 2 years | 3,000 to 4,999 | 34 | 9 | 26.5% |
| Under 2 years | 5,000 to 6,999 | 28 | 5 | 17.9% |
| Under 2 years | 7,000 to 9,999 | 10 | 3 | 30.0% |
| Under 2 years | 10,000 and over | 21 | 2 | 9.5% |
| 2 to 4 years | Under 3,000 | 140 | 33 | 23.6% |
| 2 to 4 years | 3,000 to 4,999 | 118 | 21 | 17.8% |
| 2 to 4 years | 5,000 to 6,999 | 47 | 6 | 12.8% |
| 2 to 4 years | 7,000 to 9,999 | 26 | 3 | 11.5% |
| 2 to 4 years | 10,000 and over | 34 | 3 | 8.8% |
| 5 to 9 years | Under 3,000 | 110 | 19 | 17.3% |
| 5 to 9 years | 3,000 to 4,999 | 139 | 13 | 9.4% |
| 5 to 9 years | 5,000 to 6,999 | 138 | 13 | 9.4% |
| 5 to 9 years | 7,000 to 9,999 | 67 | 10 | 14.9% |
| 5 to 9 years | 10,000 and over | 70 | 3 | 4.3% |
| 10 to 19 years | Under 3,000 | 22 | 5 | 22.7% |
| 10 to 19 years | 3,000 to 4,999 | 57 | 7 | 12.3% |
| 10 to 19 years | 5,000 to 6,999 | 71 | 3 | 4.2% |
| 10 to 19 years | 7,000 to 9,999 | 49 | 6 | 12.2% |
| 10 to 19 years | 10,000 and over | 74 | 8 | 10.8% |
| 20 years and over | Under 3,000 | 1 | 0 | 0.0% |
| 20 years and over | 3,000 to 4,999 | 6 | 0 | 0.0% |
| 20 years and over | 5,000 to 6,999 | 2 | 0 | 0.0% |
| 20 years and over | 7,000 to 9,999 | 2 | 0 | 0.0% |
| 20 years and over | 10,000 and over | 82 | 9 | 11.0% |
| Total | | 1,470 | 237 | 16.1% |

Table 4.4: Attrition by time at the company within each job level

| Time at the company | Job level | Employees | Left | Attrition rate |
| --- | --- | --- | --- | --- |
| Under 2 years | 1 | 136 | 60 | 44.1% |
| Under 2 years | 2 | 49 | 9 | 18.4% |
| Under 2 years | 3 | 18 | 5 | 27.8% |
| Under 2 years | 4 | 5 | 1 | 20.0% |
| Under 2 years | 5 | 7 | 0 | 0.0% |
| 2 to 4 years | 1 | 201 | 46 | 22.9% |
| 2 to 4 years | 2 | 114 | 16 | 14.0% |
| 2 to 4 years | 3 | 28 | 4 | 14.3% |
| 2 to 4 years | 4 | 13 | 0 | 0.0% |
| 2 to 4 years | 5 | 9 | 0 | 0.0% |
| 5 to 9 years | 1 | 171 | 30 | 17.5% |
| 5 to 9 years | 2 | 240 | 18 | 7.5% |
| 5 to 9 years | 3 | 74 | 9 | 12.2% |
| 5 to 9 years | 4 | 26 | 0 | 0.0% |
| 5 to 9 years | 5 | 13 | 1 | 7.7% |
| 10 to 19 years | 1 | 34 | 7 | 20.6% |
| 10 to 19 years | 2 | 124 | 9 | 7.3% |
| 10 to 19 years | 3 | 84 | 11 | 13.1% |
| 10 to 19 years | 4 | 24 | 2 | 8.3% |
| 10 to 19 years | 5 | 7 | 0 | 0.0% |
| 20 years and over | 1 | 1 | 0 | 0.0% |
| 20 years and over | 2 | 7 | 0 | 0.0% |
| 20 years and over | 3 | 14 | 3 | 21.4% |
| 20 years and over | 4 | 38 | 2 | 5.3% |
| 20 years and over | 5 | 33 | 4 | 12.1% |
| Total | | 1,470 | 237 | 16.1% |

Table 4.5: Overlap between the first two years, the lowest income band and job level 1

| Group | Employees in the group | All employees in the time band | Share |
| --- | --- | --- | --- |
| Under 2 years with a monthly income under 3,000 | 122 | 215 | 56.7% |

| Group | Employees | Share of all employees | Left | Share of all leavers | Attrition rate |
| --- | --- | --- | --- | --- | --- |
| Job level 1 with under 2 years at the company | 136 | 9.3% | 60 | 25.3% | 44.1% |

- The attrition rate fell steeply with time at the company: 34.9% for employees with under 2 years, 18.1% at 2 to 4 years and 11.1% at 5 to 9 years. It then levelled off at 10.6% for 10 to 19 years and 9.7% for 20 years and over (Table 4.1).
- Employees with under 5 years at the company were 39.5% of the workforce (580 employees) but 59.5% of the leavers (141), a combined rate of 24.3% (Table 4.1).
- The pattern holds in both large departments. Research & Development fell from 31.5% under 2 years to 9.9% at 10 to 19 years, and Sales fell from 39.3% to 12.8% over the same range (Table 4.2).
- The gap between departments also holds over time. Sales had a higher rate than Research & Development in every time band: 39.3% against 31.5% under 2 years, 27.9% against 13.3% at 2 to 4 years, 14.4% against 9.7% at 5 to 9 years, 12.8% against 9.9% at 10 to 19 years, and 14.8% against 6.8% at 20 years and over (Table 4.2).
- Human Resources groups are too small to compare. For example, 4 of the 5 Human Resources employees with under 2 years left (Table 4.2).
- The pay finding from question 3 holds within time at the company. Employees on a monthly income under 3,000 had the highest rate in every time band up to 19 years: 45.9% against 9.5% for 10,000 and over under 2 years, 23.6% against 8.8% at 2 to 4 years, and 17.3% against 4.3% at 5 to 9 years (Table 4.3).
- Pay and time at the company overlap. Of the 215 employees with under 2 years at the company, 122 (56.7%) were on a monthly income under 3,000 (Table 4.5).
- In the 20 years and over group, 82 of the 93 employees earned 10,000 or more (11.0% left), so pay cannot be compared within that group (Table 4.3).
- Job level matters within every time band that has enough employees. Level 1 had the highest rate in the four bands from under 2 years to 19 years: 44.1% under 2 years, 22.9% at 2 to 4 years, 17.5% at 5 to 9 years and 20.6% at 10 to 19 years (Table 4.4).
- Time at the company matters within job levels. In level 1 the rate fell from 44.1% under 2 years to 22.9% at 2 to 4 years and 17.5% at 5 to 9 years. In level 2 it fell from 18.4% to 14.0%, 7.5% and 7.3% across the first four bands (Table 4.4).
- The highest-risk group in the data so far is job level 1 employees with under 2 years at the company. They were 136 employees (9.3% of the workforce) and 60 of the 237 leavers (25.3%), a rate of 44.1% (Table 4.5).
- The 20 years and over group has only 1 employee at level 1, so job levels cannot be compared within it. Several other cells, such as level 4 and level 5 under 2 years (5 and 7 employees), are too small to read (Table 4.4).

### What this means

Attrition is concentrated in the first years at the company, and this is not explained by department, pay or job level alone. The pattern appears in both large departments, inside the lowest-paid group, and within job levels. At the same time, the earlier findings also hold within time at the company: Sales has higher attrition than Research & Development, lower pay goes with higher attrition, and level 1 has higher attrition than other levels.

Taken together, the group most worth an HR manager's attention is new employees in entry-level jobs, particularly those on the lowest pay. The data points to the first two years as the period when most of the leaving happens, which makes onboarding and early-career experience a place to look.

### Limitations

- This is an association. The data does not show why employees left at any stage.
- Time at the company is recorded in whole years, and the data does not say whether it was counted up to the day each leaver left. A leaver in the under 2 years group therefore had 0 or 1 whole years of service in the data.
- Age and overtime are not taken into account in this question. Younger employees are likely to have shorter service, and question 2 showed that overtime goes with higher attrition.
- The time bands were fixed before any attrition rate was looked at (Decision 15), but different band edges could give different group results.
- Several cells are too small to read, including the Human Resources department, level 4 and level 5 under 2 years, and most of the 20 years and over group.
- The data has no date, so it cannot show whether attrition in the first years rose or fell over calendar time.
- The employees are fictional, so the pattern may not match any real organisation.

## Business question 5: How do age and marital status relate to attrition, and does the pattern hold once time at the company is taken into account?

### Findings

Shares in the tables are rounded to one decimal place, so a column of shares can add up to 99.9% or 100.1% instead of exactly 100.0%.

Table 5.1: Attrition by age band

| Age band | Employees | Share of employees | Left | Share of all leavers | Attrition rate |
| --- | --- | --- | --- | --- | --- |
| Under 25 | 97 | 6.6% | 38 | 16.0% | 39.2% |
| 25 to 34 | 554 | 37.7% | 112 | 47.3% | 20.2% |
| 35 to 44 | 505 | 34.4% | 51 | 21.5% | 10.1% |
| 45 to 54 | 245 | 16.7% | 25 | 10.5% | 10.2% |
| 55 and over | 69 | 4.7% | 11 | 4.6% | 15.9% |
| Total | 1,470 | 100.0% | 237 | 100.0% | 16.1% |
| Of which: under 35 combined | 651 | 44.3% | 150 | 63.3% | 23.0% |
| Of which: 35 and over combined | 819 | 55.7% | 87 | 36.7% | 10.6% |

Table 5.2: Attrition by marital status

| Marital status | Employees | Share of employees | Left | Share of all leavers | Attrition rate |
| --- | --- | --- | --- | --- | --- |
| Divorced | 327 | 22.2% | 33 | 13.9% | 10.1% |
| Married | 673 | 45.8% | 84 | 35.4% | 12.5% |
| Single | 470 | 32.0% | 120 | 50.6% | 25.5% |
| Total | 1,470 | 100.0% | 237 | 100.0% | 16.1% |

Table 5.3: Attrition by marital status within each age band

| Age band | Marital status | Employees | Left | Attrition rate |
| --- | --- | --- | --- | --- |
| Under 25 | Divorced | 11 | 1 | 9.1% |
| Under 25 | Married | 30 | 9 | 30.0% |
| Under 25 | Single | 56 | 28 | 50.0% |
| 25 to 34 | Divorced | 127 | 14 | 11.0% |
| 25 to 34 | Married | 243 | 39 | 16.0% |
| 25 to 34 | Single | 184 | 59 | 32.1% |
| 35 to 44 | Divorced | 119 | 14 | 11.8% |
| 35 to 44 | Married | 239 | 18 | 7.5% |
| 35 to 44 | Single | 147 | 19 | 12.9% |
| 45 to 54 | Divorced | 54 | 3 | 5.6% |
| 45 to 54 | Married | 127 | 13 | 10.2% |
| 45 to 54 | Single | 64 | 9 | 14.1% |
| 55 and over | Divorced | 16 | 1 | 6.3% |
| 55 and over | Married | 34 | 5 | 14.7% |
| 55 and over | Single | 19 | 5 | 26.3% |
| Total | | 1,470 | 237 | 16.1% |

Table 5.4: Attrition by age band within each time at the company band

| Time at the company | Age band | Employees | Left | Attrition rate |
| --- | --- | --- | --- | --- |
| Under 2 years | Under 25 | 43 | 26 | 60.5% |
| Under 2 years | 25 to 34 | 66 | 29 | 43.9% |
| Under 2 years | 35 to 44 | 75 | 15 | 20.0% |
| Under 2 years | 45 to 54 | 20 | 3 | 15.0% |
| Under 2 years | 55 and over | 11 | 2 | 18.2% |
| 2 to 4 years | Under 25 | 42 | 9 | 21.4% |
| 2 to 4 years | 25 to 34 | 152 | 39 | 25.7% |
| 2 to 4 years | 35 to 44 | 100 | 11 | 11.0% |
| 2 to 4 years | 45 to 54 | 58 | 6 | 10.3% |
| 2 to 4 years | 55 and over | 13 | 1 | 7.7% |
| 5 to 9 years | Under 25 | 12 | 3 | 25.0% |
| 5 to 9 years | 25 to 34 | 230 | 30 | 13.0% |
| 5 to 9 years | 35 to 44 | 174 | 12 | 6.9% |
| 5 to 9 years | 45 to 54 | 86 | 10 | 11.6% |
| 5 to 9 years | 55 and over | 22 | 3 | 13.6% |
| 10 to 19 years | 25 to 34 | 106 | 14 | 13.2% |
| 10 to 19 years | 35 to 44 | 109 | 10 | 9.2% |
| 10 to 19 years | 45 to 54 | 44 | 2 | 4.5% |
| 10 to 19 years | 55 and over | 14 | 3 | 21.4% |
| 20 years and over | 35 to 44 | 47 | 3 | 6.4% |
| 20 years and over | 45 to 54 | 37 | 4 | 10.8% |
| 20 years and over | 55 and over | 9 | 2 | 22.2% |
| Total | | 1,470 | 237 | 16.1% |

Table 5.5: Overlap between age and the first two years at the company

| Group | Employees in the group | All employees with under 2 years | Share |
| --- | --- | --- | --- |
| Under 35 with under 2 years at the company | 109 | 215 | 50.7% |

- The attrition rate fell with age up to the middle of working life: 39.2% for employees under 25, 20.2% at 25 to 34 and 10.1% at 35 to 44. It stayed at 10.2% for 45 to 54 and was 15.9% for 55 and over, a smaller group of 69 employees (Table 5.1).
- Employees under 35 were 44.3% of the workforce (651 employees) but 63.3% of the leavers (150), a combined rate of 23.0%. Employees aged 35 and over had a combined rate of 10.6% (87 leavers among 819 employees) (Table 5.1).
- Single employees left at 25.5%, against 12.5% for married and 10.1% for divorced employees. They were 32.0% of the workforce but 50.6% of the leavers (Table 5.2).
- Within every age band, single employees had the highest rate. The gap is wide in the younger bands: 50.0% against 30.0% for married employees under 25, and 32.1% against 16.0% at 25 to 34. At 35 to 44 the three groups are close (single 12.9%, divorced 11.8%, married 7.5%). The marital pattern is therefore mostly a pattern among employees under 35 (Table 5.3).
- The age pattern holds within time at the company. Employees under 35 had higher rates than those aged 35 to 44 in every time band where the comparison can be made: 60.5% (under 25) and 43.9% (25 to 34) against 20.0% under 2 years, 21.4% and 25.7% against 11.0% at 2 to 4 years, 25.0% and 13.0% against 6.9% at 5 to 9 years, and 13.2% (25 to 34) against 9.2% at 10 to 19 years (Table 5.4).
- Age and time at the company overlap. Of the 215 employees with under 2 years at the company, 109 (50.7%) were under 35, so part of the age pattern is new joiners (Table 5.5).
- The high rate for employees under 25 (39.2%) is less clear-cut once time at the company is held the same. At 2 to 4 years, those under 25 did not leave more often than those aged 25 to 34 (21.4% against 25.7%) (Table 5.4).
- Several cells are too small to read: divorced employees under 25 (11 employees), under 25 at 5 to 9 years (12), every time band for 55 and over (9 to 22 employees), and the divorced and single groups at 55 and over (16 and 19) (Tables 5.3 and 5.4).

### What this means

Age and marital status both go with attrition, and they overlap. Employees under 35 and single employees leave more often, and the marital gap is mostly found among the younger employees. Part of the age pattern is new joiners, because half of the employees in their first two years are under 35, but the age pattern also remains when time at the company is held the same.

Age and marital status describe who is leaving. They are not something an employer can change, and they should not be used to select or treat employees differently. The useful reading for an HR manager is about career stage: younger employees, particularly in their first years, are the group where leaving is most common, and support for them early in their career is the place to look.

### Limitations

- This is an association. The data does not show why employees left.
- Overtime and job level are not taken into account in this question, and either could account for part of the age pattern. Question 2 showed that overtime goes with higher attrition, and question 3 showed that job level 1 has the highest attrition.
- The data does not say whether age and marital status were recorded at the time each employee left or at another date.
- The age bands were fixed before any attrition rate was looked at (Decision 15), but different band edges could give different group results.
- Several cells are too small to read, as listed above, and the 55 and over band has only 69 employees.
- The data has no date, so it cannot show whether the pattern changed over time.
- The employees are fictional, so the pattern may not match any real organisation.

## Business question 6: Does a long gap since the last promotion go with higher attrition, once time at the company is taken into account?

### Findings

Shares in the tables are rounded to one decimal place, so a column of shares can add up to 99.9% or 100.1% instead of exactly 100.0%.

Table 6.1: Attrition by years since the last promotion

| Years since last promotion | Employees | Share of employees | Left | Share of all leavers | Attrition rate |
| --- | --- | --- | --- | --- | --- |
| 0 years | 581 | 39.5% | 110 | 46.4% | 18.9% |
| 1 to 2 years | 516 | 35.1% | 76 | 32.1% | 14.7% |
| 3 to 5 years | 158 | 10.7% | 16 | 6.8% | 10.1% |
| 6 to 10 years | 149 | 10.1% | 27 | 11.4% | 18.1% |
| 11 years and over | 66 | 4.5% | 8 | 3.4% | 12.1% |
| Total | 1,470 | 100.0% | 237 | 100.0% | 16.1% |

Table 6.2: Attrition by years since the last promotion within each time at the company band

| Time at the company | Years since last promotion | Employees | Left | Attrition rate |
| --- | --- | --- | --- | --- |
| Under 2 years | 0 years | 202 | 67 | 33.2% |
| Under 2 years | 1 to 2 years | 13 | 8 | 61.5% |
| 2 to 4 years | 0 years | 113 | 20 | 17.7% |
| 2 to 4 years | 1 to 2 years | 246 | 45 | 18.3% |
| 2 to 4 years | 3 to 5 years | 6 | 1 | 16.7% |
| 5 to 9 years | 0 years | 205 | 20 | 9.8% |
| 5 to 9 years | 1 to 2 years | 183 | 17 | 9.3% |
| 5 to 9 years | 3 to 5 years | 59 | 8 | 13.6% |
| 5 to 9 years | 6 to 10 years | 77 | 13 | 16.9% |
| 10 to 19 years | 0 years | 54 | 3 | 5.6% |
| 10 to 19 years | 1 to 2 years | 58 | 4 | 6.9% |
| 10 to 19 years | 3 to 5 years | 73 | 6 | 8.2% |
| 10 to 19 years | 6 to 10 years | 64 | 13 | 20.3% |
| 10 to 19 years | 11 years and over | 24 | 3 | 12.5% |
| 20 years and over | 0 years | 7 | 0 | 0.0% |
| 20 years and over | 1 to 2 years | 16 | 2 | 12.5% |
| 20 years and over | 3 to 5 years | 20 | 1 | 5.0% |
| 20 years and over | 6 to 10 years | 8 | 1 | 12.5% |
| 20 years and over | 11 years and over | 42 | 5 | 11.9% |
| Total | | 1,470 | 237 | 16.1% |

Table 6.3: Attrition by years since the last promotion within each job level

| Job level | Years since last promotion | Employees | Left | Attrition rate |
| --- | --- | --- | --- | --- |
| 1 | 0 years | 260 | 78 | 30.0% |
| 1 | 1 to 2 years | 222 | 51 | 23.0% |
| 1 | 3 to 5 years | 33 | 4 | 12.1% |
| 1 | 6 to 10 years | 26 | 9 | 34.6% |
| 1 | 11 years and over | 2 | 1 | 50.0% |
| 2 | 0 years | 214 | 22 | 10.3% |
| 2 | 1 to 2 years | 189 | 17 | 9.0% |
| 2 | 3 to 5 years | 60 | 3 | 5.0% |
| 2 | 6 to 10 years | 63 | 10 | 15.9% |
| 2 | 11 years and over | 8 | 0 | 0.0% |
| 3 | 0 years | 69 | 9 | 13.0% |
| 3 | 1 to 2 years | 56 | 6 | 10.7% |
| 3 | 3 to 5 years | 37 | 8 | 21.6% |
| 3 | 6 to 10 years | 40 | 7 | 17.5% |
| 3 | 11 years and over | 16 | 2 | 12.5% |
| 4 | 0 years | 23 | 1 | 4.3% |
| 4 | 1 to 2 years | 28 | 0 | 0.0% |
| 4 | 3 to 5 years | 17 | 1 | 5.9% |
| 4 | 6 to 10 years | 13 | 0 | 0.0% |
| 4 | 11 years and over | 25 | 3 | 12.0% |
| 5 | 0 years | 15 | 0 | 0.0% |
| 5 | 1 to 2 years | 21 | 2 | 9.5% |
| 5 | 3 to 5 years | 11 | 0 | 0.0% |
| 5 | 6 to 10 years | 7 | 1 | 14.3% |
| 5 | 11 years and over | 15 | 2 | 13.3% |
| Total | | 1,470 | 237 | 16.1% |

Table 6.4: Employees with 5 or more years at the company, by years since the last promotion

| Group | Employees | Left | Attrition rate |
| --- | --- | --- | --- |
| 6 to 10 years since the last promotion | 149 | 27 | 18.1% |
| All other promotion gap bands | 741 | 69 | 9.3% |
| Total employees with 5 or more years at the company | 890 | 96 | 10.8% |

Table 6.5: Overlap between a promotion gap of 0 years and the first two years at the company

| Group | Employees in the group | All employees with under 2 years | Share |
| --- | --- | --- | --- |
| Under 2 years at the company with 0 years since the last promotion | 202 | 215 | 94.0% |

- The attrition rate did not rise steadily with the gap since the last promotion. It was highest at 0 years (18.9%), lowest at 3 to 5 years (10.1%), and high again at 6 to 10 years (18.1%) (Table 6.1).
- The 0 years group is mostly new joiners. Of the 215 employees with under 2 years at the company, 202 (94.0%) are in it, so its high overall rate largely repeats the finding of question 4. Among employees with 5 to 9 and 10 to 19 years at the company, the 0 years group had some of the lowest rates (9.8% and 5.6%) (Tables 6.2 and 6.5).
- Among long-serving employees, a gap of 6 to 10 years went with a higher rate. Within 5 to 9 years at the company, the rate was 9.8% at 0 years, 9.3% at 1 to 2 years, 13.6% at 3 to 5 years and 16.9% at 6 to 10 years. Within 10 to 19 years it was 5.6%, 6.9% and 8.2% for the first three bands, then 20.3% at 6 to 10 years (Table 6.2).
- For employees with 5 or more years at the company, the 6 to 10 years group left at 18.1% (27 of 149), against 9.3% (69 of 741) for all other gap bands (Table 6.4).
- Within 2 to 4 years at the company, there was no pattern: 17.7% at 0 years and 18.3% at 1 to 2 years (Table 6.2).
- The 6 to 10 years pattern partly holds within job level. In level 1 the rate was 34.6% against 26.3% for the level as a whole, and in level 2 it was 15.9% against 9.7% (Tables 6.3 and 3.2). In level 3 the 3 to 5 years group (21.6%) was higher than the 6 to 10 years group (17.5%) (Table 6.3).
- Several cells are too small to read: 1 to 2 years among employees with under 2 years at the company (13 employees, 61.5%), 11 years and over in level 1 (2 employees, 50.0%), most of the 20 years and over group, and most of levels 4 and 5 (Tables 6.2 and 6.3).

### What this means

There is no steady link between the time since the last promotion and attrition. The two groups with the highest rates for different reasons: employees with a gap of 0 years are mostly new joiners, whose rate repeats the first-years pattern of question 4, while those with a gap of 6 to 10 years are long-serving employees who left at about twice the rate of their long-serving colleagues with other gaps.

For an HR manager, the second group is the one to look at: employees who have been at the company 5 or more years and have not been promoted for 6 to 10 years. It is a moderate pattern based on groups of about 60 to 80 employees in each tenure band, and it does not apply to the workforce as a whole.

### Limitations

- This is an association. The data does not show whether a lack of promotion caused employees to leave, or whether the employees who were not promoted differed in other ways.
- A value of 0 years since the last promotion could mean a promotion in the last year or no promotion at all, and the data does not say which.
- Overtime and pay are not taken into account in this question.
- The promotion gap bands were fixed before any attrition rate was looked at (Decision 16), but different band edges could give different group results.
- Long gaps occur only among employees who have been at the company a long time, so the comparison within a time band covers only a narrow range of gaps.
- Several cells are too small to read, as listed above.
- The data has no date, so it cannot show whether the pattern changed over time.
- The employees are fictional, so the pattern may not match any real organisation.

## Business question 7: Do business travel and distance from home go with higher attrition, and does this hold once overtime and department are taken into account?

### Findings

Shares in the tables are rounded to one decimal place, so a column of shares can add up to 99.9% or 100.1% instead of exactly 100.0%. The business travel groups use the dataset's own labels: Non-Travel (no business travel), Travel_Rarely and Travel_Frequently. The data does not say how many days a year each group travels, and it does not state the unit of distance from home.

Table 7.1: Attrition by business travel

| Business travel | Employees | Share of employees | Left | Share of all leavers | Attrition rate |
| --- | --- | --- | --- | --- | --- |
| Non-Travel | 150 | 10.2% | 12 | 5.1% | 8.0% |
| Travel_Rarely | 1,043 | 71.0% | 156 | 65.8% | 15.0% |
| Travel_Frequently | 277 | 18.8% | 69 | 29.1% | 24.9% |
| Total | 1,470 | 100.0% | 237 | 100.0% | 16.1% |

Table 7.2: Attrition by distance from home

| Distance from home | Employees | Share of employees | Left | Share of all leavers | Attrition rate |
| --- | --- | --- | --- | --- | --- |
| 1 to 2 | 419 | 28.5% | 54 | 22.8% | 12.9% |
| 3 to 5 | 213 | 14.5% | 33 | 13.9% | 15.5% |
| 6 to 10 | 394 | 26.8% | 57 | 24.1% | 14.5% |
| 11 to 20 | 240 | 16.3% | 48 | 20.3% | 20.0% |
| 21 and over | 204 | 13.9% | 45 | 19.0% | 22.1% |
| Total | 1,470 | 100.0% | 237 | 100.0% | 16.1% |
| Of which: 11 and over combined | 444 | 30.2% | 93 | 39.2% | 20.9% |
| Of which: 1 to 10 combined | 1,026 | 69.8% | 144 | 60.8% | 14.0% |

Table 7.3: Attrition by business travel within each overtime group

| Overtime | Business travel | Employees | Left | Attrition rate |
| --- | --- | --- | --- | --- |
| No | Non-Travel | 115 | 5 | 4.3% |
| No | Travel_Rarely | 748 | 72 | 9.6% |
| No | Travel_Frequently | 191 | 33 | 17.3% |
| Yes | Non-Travel | 35 | 7 | 20.0% |
| Yes | Travel_Rarely | 295 | 84 | 28.5% |
| Yes | Travel_Frequently | 86 | 36 | 41.9% |
| Total | | 1,470 | 237 | 16.1% |

Table 7.4: Share of employees working overtime, by business travel

| Business travel | Employees | Employees working overtime | Share working overtime |
| --- | --- | --- | --- |
| Non-Travel | 150 | 35 | 23.3% |
| Travel_Rarely | 1,043 | 295 | 28.3% |
| Travel_Frequently | 277 | 86 | 31.0% |
| Total | 1,470 | 416 | 28.3% |

Table 7.5: Attrition by business travel within each department

| Department | Business travel | Employees | Left | Attrition rate |
| --- | --- | --- | --- | --- |
| Human Resources | Non-Travel | 6 | 0 | 0.0% |
| Human Resources | Travel_Rarely | 46 | 8 | 17.4% |
| Human Resources | Travel_Frequently | 11 | 4 | 36.4% |
| Research & Development | Non-Travel | 97 | 8 | 8.2% |
| Research & Development | Travel_Rarely | 682 | 88 | 12.9% |
| Research & Development | Travel_Frequently | 182 | 37 | 20.3% |
| Sales | Non-Travel | 47 | 4 | 8.5% |
| Sales | Travel_Rarely | 315 | 60 | 19.0% |
| Sales | Travel_Frequently | 84 | 28 | 33.3% |
| Total | | 1,470 | 237 | 16.1% |

Table 7.6: Share of employees who travel frequently, by department

| Department | Employees | Employees who travel frequently | Share |
| --- | --- | --- | --- |
| Human Resources | 63 | 11 | 17.5% |
| Research & Development | 961 | 182 | 18.9% |
| Sales | 446 | 84 | 18.8% |
| Total | 1,470 | 277 | 18.8% |

Table 7.7: Attrition by distance from home within each overtime group

| Overtime | Distance from home | Employees | Left | Attrition rate |
| --- | --- | --- | --- | --- |
| No | 1 to 2 | 313 | 28 | 8.9% |
| No | 3 to 5 | 147 | 13 | 8.8% |
| No | 6 to 10 | 287 | 31 | 10.8% |
| No | 11 to 20 | 164 | 19 | 11.6% |
| No | 21 and over | 143 | 19 | 13.3% |
| Yes | 1 to 2 | 106 | 26 | 24.5% |
| Yes | 3 to 5 | 66 | 20 | 30.3% |
| Yes | 6 to 10 | 107 | 26 | 24.3% |
| Yes | 11 to 20 | 76 | 29 | 38.2% |
| Yes | 21 and over | 61 | 26 | 42.6% |
| Total | | 1,470 | 237 | 16.1% |

Table 7.8: Attrition by near and far distance within each overtime group

| Overtime | Distance from home | Employees | Left | Attrition rate |
| --- | --- | --- | --- | --- |
| No | 1 to 10 | 747 | 72 | 9.6% |
| No | 11 and over | 307 | 38 | 12.4% |
| Yes | 1 to 10 | 279 | 72 | 25.8% |
| Yes | 11 and over | 137 | 55 | 40.1% |
| Total | | 1,470 | 237 | 16.1% |

- The attrition rate rose with business travel: 8.0% for employees who do not travel, 15.0% for those who travel rarely and 24.9% for those who travel frequently. Frequent travellers were 18.8% of the workforce but 29.1% of the leavers (Table 7.1).
- The travel pattern holds within overtime. In both overtime groups the rate rose with travel: 4.3%, 9.6% and 17.3% without overtime, and 20.0%, 28.5% and 41.9% with overtime (Table 7.3).
- Overtime does not explain the travel pattern. Overtime was somewhat more common among frequent travellers (31.0%) than among those who do not travel (23.3%), but the difference is small compared with the gap in attrition (Table 7.4).
- The travel pattern holds within departments. Frequent travellers had a higher rate than rare travellers in Research & Development (20.3% against 12.9%) and Sales (33.3% against 19.0%) (Table 7.5).
- Department does not explain the travel pattern either. About the same share of each department travels frequently: 17.5% in Human Resources, 18.9% in Research & Development and 18.8% in Sales (Table 7.6).
- The two factors add up. The highest rates in this question were among employees who travel frequently and work overtime (41.9%, 86 employees) and among employees who live 21 or more from work and work overtime (42.6%, 61 employees) (Tables 7.3 and 7.7).
- Distance from home is a weaker pattern. The rate was 12.9% at 1 to 2, 15.5% at 3 to 5 and 14.5% at 6 to 10, then 20.0% at 11 to 20 and 22.1% at 21 and over. It does not rise at every step, but employees living 11 or more from work (30.2% of the workforce) were 39.2% of the leavers, with a rate of 20.9% against 14.0% for those living closer (Table 7.2).
- The distance pattern holds within overtime. Employees living 11 or more from work left more often than those living closer in both groups: 12.4% against 9.6% without overtime, and 40.1% against 25.8% with overtime. The distance gap is wider among employees who work overtime (Table 7.8). Within the overtime group the rate does not rise at every step (24.5%, 30.3% and 24.3% for the three nearest bands) (Table 7.7).
- The Human Resources travel groups are too small to compare (6 employees do not travel and 11 travel frequently). The 35 employees who do not travel and work overtime are also a small group, so the exact rate of 20.0% is uncertain, but it is well above the 4.3% for non-travellers without overtime (Tables 7.3 and 7.5).

### What this means

Frequent business travel is clearly linked to higher attrition, and the link does not come from overtime or department. Living far from work is also linked to higher attrition, but the pattern is weaker and less regular. Both are most visible among employees who also work overtime, where the rates are the highest in this question.

For an HR manager, frequent travellers and employees with a long journey to work who also work overtime are the groups where the combined workload is greatest. The data suggests that travel and distance are worth reviewing together with overtime, and not separately.

### Limitations

- These are associations. The data does not show why employees left.
- The data does not say how many days a year employees travel for business, so the labels Rarely and Frequently have no exact meaning here.
- The data does not state the unit of distance from home (kilometres or miles).
- Job level, age and pay are not taken into account in this question. Frequent travel may be more common in some job levels than others.
- The distance bands were fixed before any attrition rate was looked at (Decision 17), but different band edges could give different group results.
- A few groups are too small to read, as listed above.
- The data has no date, so it cannot show whether the pattern changed over time.
- The employees are fictional, so the pattern may not match any real organisation.

## Business question 8: Which of the five rating scales shows the biggest gap in attrition between low and high ratings, and does it hold within overtime?

### Findings

The five scales are what employees said about themselves. Four use the ratings Low, Medium, High and Very High (environment satisfaction, job satisfaction, relationship satisfaction and job involvement), and work-life balance uses Bad, Good, Better and Best. For each scale, the gap is the attrition rate for the lowest rating minus the rate for the two highest ratings combined. The two highest are combined because several single ratings are small groups. This measure was fixed before any rate was looked at. Gaps are calculated from unrounded rates, so a gap can differ by 0.1 from the difference of the rounded rates shown. Shares in the tables are rounded to one decimal place.

Table 8.1: Attrition by rating on each scale, overall and by overtime

| Scale | Rating | Employees | Left | Attrition rate | Employees without overtime | Left | Attrition rate | Employees with overtime | Left | Attrition rate |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Environment satisfaction | Low | 284 | 72 | 25.4% | 222 | 40 | 18.0% | 62 | 32 | 51.6% |
| Environment satisfaction | Medium | 287 | 43 | 15.0% | 206 | 16 | 7.8% | 81 | 27 | 33.3% |
| Environment satisfaction | High | 453 | 62 | 13.7% | 320 | 32 | 10.0% | 133 | 30 | 22.6% |
| Environment satisfaction | Very High | 446 | 60 | 13.5% | 306 | 22 | 7.2% | 140 | 38 | 27.1% |
| Job satisfaction | Low | 289 | 66 | 22.8% | 205 | 36 | 17.6% | 84 | 30 | 35.7% |
| Job satisfaction | Medium | 280 | 46 | 16.4% | 211 | 20 | 9.5% | 69 | 26 | 37.7% |
| Job satisfaction | High | 442 | 73 | 16.5% | 321 | 32 | 10.0% | 121 | 41 | 33.9% |
| Job satisfaction | Very High | 459 | 52 | 11.3% | 317 | 22 | 6.9% | 142 | 30 | 21.1% |
| Relationship satisfaction | Low | 276 | 57 | 20.7% | 210 | 32 | 15.2% | 66 | 25 | 37.9% |
| Relationship satisfaction | Medium | 303 | 45 | 14.9% | 217 | 15 | 6.9% | 86 | 30 | 34.9% |
| Relationship satisfaction | High | 459 | 71 | 15.5% | 328 | 37 | 11.3% | 131 | 34 | 26.0% |
| Relationship satisfaction | Very High | 432 | 64 | 14.8% | 299 | 26 | 8.7% | 133 | 38 | 28.6% |
| Work-life balance | Bad | 80 | 25 | 31.3% | 58 | 15 | 25.9% | 22 | 10 | 45.5% |
| Work-life balance | Good | 344 | 58 | 16.9% | 240 | 26 | 10.8% | 104 | 32 | 30.8% |
| Work-life balance | Better | 893 | 127 | 14.2% | 639 | 54 | 8.5% | 254 | 73 | 28.7% |
| Work-life balance | Best | 153 | 27 | 17.6% | 117 | 15 | 12.8% | 36 | 12 | 33.3% |
| Job involvement | Low | 83 | 28 | 33.7% | 58 | 15 | 25.9% | 25 | 13 | 52.0% |
| Job involvement | Medium | 375 | 71 | 18.9% | 270 | 33 | 12.2% | 105 | 38 | 36.2% |
| Job involvement | High | 868 | 125 | 14.4% | 623 | 56 | 9.0% | 245 | 69 | 28.2% |
| Job involvement | Very High | 144 | 13 | 9.0% | 103 | 6 | 5.8% | 41 | 7 | 17.1% |
| Total (each scale) | | 1,470 | 237 | 16.1% | 1,054 | 110 | 10.4% | 416 | 127 | 30.5% |

Table 8.2: The gap between the lowest rating and the two highest ratings combined, by scale

| Rank | Scale | Lowest rating | Employees | Share of employees | Share of all leavers | Attrition rate | Employees with the two highest ratings | Attrition rate | Gap (percentage points) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | Job involvement | Low | 83 | 5.6% | 11.8% | 33.7% | 1,012 | 13.6% | 20.1 |
| 2 | Work-life balance | Bad | 80 | 5.4% | 10.5% | 31.3% | 1,046 | 14.7% | 16.5 |
| 3 | Environment satisfaction | Low | 284 | 19.3% | 30.4% | 25.4% | 899 | 13.6% | 11.8 |
| 4 | Job satisfaction | Low | 289 | 19.7% | 27.8% | 22.8% | 901 | 13.9% | 9.0 |
| 5 | Relationship satisfaction | Low | 276 | 18.8% | 24.1% | 20.7% | 891 | 15.2% | 5.5 |

Table 8.3: The gap within each overtime group

| Scale | Overtime | Employees with the lowest rating | Attrition rate | Employees with the two highest ratings | Attrition rate | Gap (percentage points) |
| --- | --- | --- | --- | --- | --- | --- |
| Job involvement | No | 58 | 25.9% | 726 | 8.5% | 17.3 |
| Job involvement | Yes | 25 | 52.0% | 286 | 26.6% | 25.4 |
| Work-life balance | No | 58 | 25.9% | 756 | 9.1% | 16.7 |
| Work-life balance | Yes | 22 | 45.5% | 290 | 29.3% | 16.1 |
| Environment satisfaction | No | 222 | 18.0% | 626 | 8.6% | 9.4 |
| Environment satisfaction | Yes | 62 | 51.6% | 273 | 24.9% | 26.7 |
| Job satisfaction | No | 205 | 17.6% | 638 | 8.5% | 9.1 |
| Job satisfaction | Yes | 84 | 35.7% | 263 | 27.0% | 8.7 |
| Relationship satisfaction | No | 210 | 15.2% | 627 | 10.0% | 5.2 |
| Relationship satisfaction | Yes | 66 | 37.9% | 264 | 27.3% | 10.6 |

Table 8.4: Share of employees working overtime among those who gave the lowest rating

| Scale | Lowest rating | Employees | Employees working overtime | Share working overtime |
| --- | --- | --- | --- | --- |
| Environment satisfaction | Low | 284 | 62 | 21.8% |
| Job satisfaction | Low | 289 | 84 | 29.1% |
| Relationship satisfaction | Low | 276 | 66 | 23.9% |
| Work-life balance | Bad | 80 | 22 | 27.5% |
| Job involvement | Low | 83 | 25 | 30.1% |
| Total (all employees) | | 1,470 | 416 | 28.3% |

- On every scale, employees who gave the lowest rating left more often than those who gave the two highest ratings. The gaps, from widest to narrowest, were job involvement (33.7% against 13.6%, a gap of 20.1 percentage points), work-life balance (31.3% against 14.7%, 16.5), environment satisfaction (25.4% against 13.6%, 11.8), job satisfaction (22.8% against 13.9%, 9.0) and relationship satisfaction (20.7% against 15.2%, 5.5) (Table 8.2).
- Job involvement is the only scale where the rate fell at every step from the lowest rating to the highest in all three views: overall (33.7%, 18.9%, 14.4%, 9.0%), without overtime (25.9%, 12.2%, 9.0%, 5.8%) and with overtime (52.0%, 36.2%, 28.2%, 17.1%) (Table 8.1).
- On the other scales the pattern is mostly a difference between the lowest rating and the rest. Environment satisfaction also fell at every step overall (25.4%, 15.0%, 13.7%, 13.5%), but not within the overtime groups. Work-life balance Best (17.6%) was higher than Better (14.2%), and in job satisfaction and relationship satisfaction the High rating (16.5% and 15.5%) was higher than Medium (16.4% and 14.9%) (Table 8.1).
- The two scales with the widest gaps describe small groups. Employees who gave the lowest rating for job involvement or work-life balance were 5.6% and 5.4% of the workforce and 11.8% and 10.5% of the leavers. On the other three scales the lowest-rating group was about 19% of the workforce and 24.1% to 30.4% of the leavers (Table 8.2).
- The gap holds within overtime. On all five scales, the lowest rating had a higher rate than the two highest ratings combined, both without and with overtime. Job involvement stayed the widest without overtime (17.3 points) and was also the widest with overtime (25.4 points) apart from environment satisfaction (26.7) (Table 8.3).
- The gaps for environment satisfaction and relationship satisfaction were wider among employees who work overtime (26.7 and 10.6 points) than among those who do not (9.4 and 5.2). The job satisfaction and work-life balance gaps were similar in both groups (9.1 and 8.7, and 16.7 and 16.1) (Table 8.3).
- Overtime does not explain the pattern. Among employees who gave the lowest rating, the share working overtime ranged from 21.8% to 30.1%, around the 28.3% for all employees, and it was lower than average on three of the five scales (Table 8.4).
- There is one exception within an overtime group. Among employees working overtime, job satisfaction Medium (37.7%) was higher than Low (35.7%) (Table 8.1).
- The lowest ratings with overtime are small groups: 22 employees for work-life balance Bad and 25 for job involvement Low. Their exact rates (45.5% and 52.0%) are uncertain, but both are well above every other rate in their scale, and the direction is the same as in the larger groups (Tables 8.1 and 8.3).

### What this means

All five scales point the same way: an employee who rates their experience lowest is more likely to leave than one who rates it highly. Job involvement and work-life balance show the strongest link, and job involvement is the clearest because its rate falls at each step. These two ratings identify small groups with a high risk. Most leavers did not give the lowest rating on them, so they are a warning sign and not a full picture of who leaves.

For an HR manager, a low job involvement or work-life balance rating is the strongest of the five survey signals to follow up. The three satisfaction scales identify larger groups, but the gap in attrition is smaller.

### Limitations

- These are associations. The data does not show why employees left, and a low rating may reflect a decision to leave that had already been made.
- The ratings are what employees said about themselves. The data does not say when each rating was given, so it cannot show whether it came before the decision to leave.
- Job level, pay and time at the company are not taken into account in this question.
- The five scales are not independent. The same employees may give low ratings on several of them, and this question does not test that.
- Some groups are small, as noted above, and the lowest rating on work-life balance and job involvement covers only 80 and 83 employees.
- The ratings come from the dataset documentation as codes. The labels were not recorded in the file itself (Decisions 12 and 13).
- The data has no date, so it cannot show whether the pattern changed over time.
- The employees are fictional, so the pattern may not match any real organisation.

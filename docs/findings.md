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

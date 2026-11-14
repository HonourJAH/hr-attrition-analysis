# Data

This project uses the IBM HR Analytics Employee Attrition and Performance dataset from Kaggle.

The data is not stored in this repository. IBM data scientists created the dataset, so the 1,470 employees are fictional.

## How to get the data

1. Download the dataset from Kaggle (search for "IBM HR Analytics Employee Attrition & Performance") and check the licence shown on its page.
2. Save the file WA_Fn-UseC_-HR-Employee-Attrition.csv in a new folder named data/raw in this project folder.
3. Do not rename the file or open and save it in Excel, so the raw data stays exactly as downloaded.

## About the file

| Measure | Value |
| --- | --- |
| Rows (one per employee) | 1,470 |
| Columns | 35 |
| Employees who left (Attrition = Yes) | 237 |
| Employees who stayed (Attrition = No) | 1,233 |
| Attrition rate | 16.1% |
| Columns with the same value in every row | 3 (EmployeeCount, StandardHours, Over18) |

## Using the data with the workbook

The raw_hr_attrition query in the workbook holds the file path from the author's computer. To rebuild the workbook with your copy, open it, go to Data, then Queries and Connections, right-click raw_hr_attrition and choose Edit, and change the file path in the Source step to your copy of the file.

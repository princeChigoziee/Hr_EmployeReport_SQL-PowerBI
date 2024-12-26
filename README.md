# HR-EMPLOYEE-REPORT-ANALYSIS 
### SQL & PowerBI
---
![HR_EmployeeReport](https://github.com/user-attachments/assets/2fc1fb89-964f-4dbb-9a05-8e7290c089dd)

## Data Used
Data - HR Data with over 2200 rows from the year 2000 to 2020

Data Cleaning & Analysis - MYSQL, Jupyter Notebook(sql magic)

Data Visualization - PowerBI

## Data Cleaning/Preparation

```sql
CREATE DATABASE `project001_db`;
USE `project001_db`;
```

```sql
SELECT *
FROM `hr`;
```

```sql
ALTER TABLE hr
CHANGE COLUMN ï»¿id emp_id VARCHAR(20) PRIMARY KEY NOT NULL;
```

```sql
DESCRIBE `hr`;
```

```sql
SELECT birthdate
FROM `hr`;
```

```sql
UPDATE `hr`
SET birthdate =
CASE
    WHEN birthdate LIKE '%-%' THEN DATE_FORMAT(STR_TO_DATE(birthdate, '%m-%d-%Y'), '%Y-%m-%d')
    WHEN birthdate LIKE '%/%' THEN DATE_FORMAT(STR_TO_DATE(birthdate, '%m/%d/%Y'), '%Y-%m-%d')
    ELSE NULL
END;
```

```sql
ALTER TABLE `hr`
MODIFY COLUMN birthdate DATE;
```

```sql
SELECT hire_date
FROM `hr`;
```

```sql
UPDATE `hr`
SET hire_date = 
CASE 
    WHEN hire_date LIKE '%-%' THEN DATE_FORMAT(STR_TO_DATE(hire_date, '%m-%d-%Y'), '%Y-%m-%d')
    WHEN hire_date LIKE '%/%' THEN DATE_FORMAT(STR_TO_DATE(hire_date, '%m/%d/%Y'), '%Y-%m-%d')
    ELSE NULL
END;
```

```sql
ALTER TABLE `hr`
MODIFY COLUMN hire_date DATE;
```

```sql
ALTER TABLE `hr`
ADD COLUMN age INT;
```

```sql
UPDATE `hr`
SET age = timestampdiff(Year, birthdate, CURDATE());
```

```sql
UPDATE `hr`
SET termdate = IF(termdate IS NOT NULL AND termdate != '', date(str_to_date(termdate, '%Y-%m-%d %H:%i:%s UTC')), '0000:00:00')
WHERE true;
```

```sql
SET sql_mode = 'ALLOW_INVALID_DATES';
ALTER TABLE `hr` 
MODIFY COLUMN termdate DATE;
```

## Questions
1. What is the gender breakdown of employees in the company?
2. What is the race/ethnicity breakdown of employees in the company?
3. What is the race/ethnicity breakdown of employees in the company?
4. What is the race/ethnicity breakdown of employees in the company?
5. What is the age distribution of employees in the company?
6. How many employees work at headquaters versus remote locations?
7. What is the average length of employment for employees who have been terminated?
8. How does the gender distribution vary across departments and job titles?
9. What is the distribution of jobtitles across the company?
10. Which department has the highest turnover rate?
11. What is the distribution of employees across locations by city and state?
12. How has the company's employee count changed over time based on hire and term dates?
13. What is the tenure distribution for each department?

## Summary Of Findings
- There are more male employees.
- White race is the most dominant While Native Hawaiian and American Indian are the least dominant.
- The youngest employee is 20 years old and the oldest years old.
- 5 age groups were created (18-24, 25-34, 35-44, 45-54, 55-64). A large number of employees were between 25-34 followed by 35-44 while the smallest group was 55-64.
- A large number of employee work at the headquaters versus remotely.

## Limitations
- Some records had negative ages and these were excluded during quering(967 records) Ages used were 18 years and above
- Some termdates were far into the future and were not included in the analysis(1599 records). The only term dates used were those less than or equal to the current date.

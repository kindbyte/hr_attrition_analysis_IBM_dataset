# 📊 HR Analytics: Attrition by Gender and Income Level

This project explores employee attrition based on gender, monthly income and age using an HR dataset from IBM.



---

📌 SQL Queries Overview

1. Attrition by Gender 📈📉

SELECT
  gender,
  COUNT(*) AS total_employees,
  SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) AS attrition_rate,
  ROUND(SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END)::decimal / COUNT(*) * 100, 2) AS percent_attrition_rate
FROM hr_employees
GROUP BY gender
ORDER BY attrition_rate ASC;
Goal: Compare attrition rates between male and female employees.
Insight: Male employees leave slightly more often than female employees. Males also represent a larger portion of the workforce.


2. Attrition by Monthly Income Range 🔎

SELECT
  CASE
    WHEN monthlyincome < 3000 THEN '1. (<3000)'
    WHEN monthlyincome BETWEEN 3000 AND 4999 THEN '2. (between 3000 and 4999)'
    WHEN monthlyincome BETWEEN 5000 AND 6999 THEN '3. (between 5000 and 6999)'
    WHEN monthlyincome BETWEEN 7000 AND 9999 THEN '4. (between 7000 and 9999)'
    WHEN monthlyincome >= 10000 THEN '5. (>= 10000)'
  END AS income_range,
  COUNT(*) AS total_employees,
  SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) AS employees_left,
  ROUND(SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END)::decimal / COUNT(*), 2) AS attrition_percent
FROM hr_employees
GROUP BY income_range
ORDER BY attrition_percent DESC;
Goal: Understand how salary levels influence employee attrition.
Insight: Lower-income employees show the highest attrition rates. The group earning below $3,000/month has the highest turnover.


3. Number of Employee by Age 📊

SELECT 
  age_group,
  count(*) as total_employees
FROM 
  (SELECT 
     CASE
       WHEN age < 25 THEN 'less than 25'
       WHEN age BETWEEN 25 AND 35 THEN 'between 25 and 35'
       WHEN age BETWEEN 35 AND 45 THEN 'between 35 and 45'
       WHEN age BETWEEN 45 AND 55 THEN 'between 45 and 55'
       ELSE '56+'
     END AS age_group,
     CASE 
       WHEN age < 25 THEN '1'
       WHEN age BETWEEN 25 AND 35 THEN '2'
       WHEN age BETWEEN 35 AND 45 THEN '3'
       WHEN age BETWEEN 45 AND 55 THEN '4'
       ELSE '5'
     END AS age_order
   FROM hr_employees) AS sub
GROUP BY age_order, age_group
ORDER BY age_order ASC;
Goal: Analyze workforce distribution across different age groups.
Insight: Shows the concentration of employees in various age brackets, helping understand the company's demographic composition.



🛠️ Tools Used

PostgreSQL – for querying the dataset
DBeaver – as a database client
Tableau Public – for data visualization and dashboard creation


📊 Dashboards
Created in Tableau:

📉 Attrition by Gender (bar chart with percentages)
💰 Attrition by Income Range (bar chart showing attrition % by income tier)
📊 Number of Employee by Age (visualization of workforce age groups)


Data Source: IBM HR Analytics Employee Attrition & Performance


create database LBP01;

use LBP01;
CREATE TABLE HR(
    Attrition VARCHAR(10),
    Business_Travel VARCHAR(50),
    CF_age_band VARCHAR(20),
    CF_attrition_label VARCHAR(50),
    Department VARCHAR(50),
    Education_Field VARCHAR(50),
    emp_no VARCHAR(20),
    Employee_Number INT,
    Gender VARCHAR(10),
    Job_Role VARCHAR(50),
    Marital_Status VARCHAR(20),
    Over_Time VARCHAR(10),
    Over18 VARCHAR(10),
    Training_Times_Last_Year INT,
    Column_2 INT,
    Column_0 INT,
    Age INT,
    CF_attrition_count INT,
    CF_attrition_counts FLOAT,
    CF_attrition_rate INT,
    CF_current_Employee INT,
    Daily_Rate INT,
    Distance_From_Home INT,
    Education VARCHAR(20),
    Employee_Count INT,
    Environment_Satisfaction INT,
    Hourly_Rate INT,
    Job_Involvement INT,
    Job_Level INT,
    Job_Satisfaction INT,
    Monthly_Income INT,
    Monthly_Rate INT,
    Num_Companies_Worked INT,
    Percent_Salary_Hike INT,
    Performance_Rating INT,
    Relationship_Satisfaction INT,
    Standard_Hours INT,
    Stock_Option_Level INT,
    Total_Working_Years INT,
    Work_Life_Balance INT,
    Years_At_Company INT,
    Years_In_Current_Role INT,
    Years_Since_Last_Promotion INT,
    Years_With_Curr_Manager INT
);



SELECT * FROM [LBP01].[dbo].[hr]

-- OVERALL ATTRITION
SELECT COUNT(CASE WHEN ATTRITION = '1' THEN 1 END) AS ATTRITION_COUNT, COUNT(*) AS TOTAL_EMPLOYEES
FROM [LBP01].[dbo].[hr]

-- PRESENCE OF OVERTIME AND ATTRITION CORRELATION
SELECT OVER_TIME, COUNT(*) AS TOTAL_EMPLOYEES
FROM [LBP01].[dbo].[hr]
WHERE ATTRITION = 1
GROUP BY OVER_TIME;

-- OVERALL GENDER DISTRIBUTION IN THE DATASET
SELECT GENDER, COUNT(*) AS TOTAL_EMPLOYEES FROM [LBP01].[dbo].[hr]
GROUP BY GENDER;

SELECT GENDER, COUNT(*) AS TOTAL_EMPLOYEES
FROM [LBP01].[dbo].[hr]
WHERE Attrition = 1
GROUP BY GENDER;

-- RELATION BETWEEN PERFORMANCE RATING AND ATTRITION
SELECT PERFORMANCE_RATING, COUNT(CASE WHEN ATTRITION = '1' THEN 1 END) AS ATTRITION_COUNT
FROM [LBP01].[dbo].[hr]
GROUP BY Performance_Rating;
-- THERE IS A NEGATIVE CORRELATION BETWEEN THE PERFORMACE RATING AND ATTRITION COUNT

-- RELATION BETWEEN THE PERCENT SALARY HIKE AND ATTRITION COUNT
SELECT  Percent_Salary_Hike, COUNT(*) AS ATTRITION_COUNT
FROM [LBP01].[dbo].[hr]
WHERE ATTRITION = 1
GROUP BY   Percent_Salary_Hike
ORDER BY ATTRITION_COUNT DESC;
-- THERE IS A NEGATIVE CORRELATION BETWEEN THE PERCENT SALARY HIKE AND ATTRITION COUNT

SELECT * FROM [LBP01].[dbo].[hr];

-- RELATION BETWEEM YEARS IN CURRENT ROLE AND ATTRITION COUNT
SELECT Years_In_Current_Role, COUNT(CASE WHEN ATTRITION = '1' THEN 1 END) AS ATTRITION_COUNT
FROM[LBP01].[dbo].[hr]
WHERE Years_In_Current_Role > (SELECT AVG(Years_In_Current_Role) FROM [LBP01].[dbo].[hr])
GROUP BY Years_In_Current_Role
ORDER BY Years_In_Current_Role;
-- EMPLOYEES WHO ARE WORKING IN THE COMPANY FROM LAST 5-10 YEARS ARE HAVING THE HIGHEST ATTRITION COUNT

-- EMPLOYEE ATTRITION BASED ON THE AGE RANGE
SELECT CASE WHEN AGE <= 29 THEN '18-29'
            WHEN AGE >= 30 AND AGE <= 39 THEN '30-39'
			WHEN AGE >= 40 AND AGE <= 49 THEN '40-49'
			WHEN AGE >= 50 AND AGE <= 59 THEN '50-59'
			ELSE '60 OR OLDER'
			END AS 'AGE RANGE', COUNT(*) AS 'NUMBER OF ATTRITION COUNT BASED ON AGE RANGE'
FROM [LBP01].[dbo].[hr]
WHERE ATTRITION = 1 AND  Years_At_Company >= 2
GROUP BY CASE WHEN AGE <= 29 THEN '18-29'
            WHEN AGE >= 30 AND AGE <= 39 THEN '30-39'
			WHEN AGE >= 40 AND AGE <= 49 THEN '40-49'
			WHEN AGE >= 50 AND AGE <= 59 THEN '50-59'
			ELSE '60 OR OLDER'
			END
ORDER BY [AGE RANGE];
-- AGE GROUP OF '18-29' AND '30-39' HAVE THE MAXIMUM ATTRITION COUNTS FOR THOSE EMPLOYEES WHO HAVE BEEN WORKING IN THE COMPANY FROM LAST 1 

SELECT * FROM [LBP01].[dbo].[hr];

SELECT DISTINCT DEPARTMENT FROM [LBP01].[dbo].[hr];

-- DEPARTMENT WISE ATTRITION COUNT
SELECT DEPARTMENT, COUNT(*) AS ATTRITION_COUNT
FROM [LBP01].[dbo].[hr]
WHERE Attrition = 1
GROUP BY Department
ORDER BY ATTRITION_COUNT DESC;
-- R&D AND SALES DEPARTMENT ARE HAVING THE MAX ATTRITION WITH ALMOST 95%

-- ENVIRONMENT SATISFACTION, JOB SATISFACTION AND RELATIONSHIP SATISFACTION ON ATTRITION COUNTS
SELECT ENVIRONMENT_SATISFACTION, COUNT(*) AS ATTRITION_COUNTS
FROM [LBP01].[dbo].[hr]
WHERE ATTRITION = 1
GROUP BY ENVIRONMENT_SATISFACTION
ORDER BY ATTRITION_COUNTS DESC;
-- THERE IS NO CORRELATION BETWEEN THE ENVIRONMENT SATISFACTION AND ATTRITION COUNTS

SELECT  Job_Satisfaction, COUNT(*) AS ATTRITION_COUNTS
FROM [LBP01].[dbo].[hr]
WHERE ATTRITION = 1
GROUP BY  Job_Satisfaction
ORDER BY ATTRITION_COUNTS DESC;
-- THERE IS NO CORRELATION BETWEEN THE JOB SATISFACTION AND ATTRITION COUNTS


SELECT RELATIONSHIP_SATISFACTION, COUNT(*) AS ATTRITION_COUNTS
FROM [LBP01].[dbo].[hr]
WHERE ATTRITION = 1
GROUP BY RELATIONSHIP_SATISFACTION
ORDER BY ATTRITION_COUNTS DESC;
-- THERE IS NO CORRELATION BETWEEN THE RELATIONSIP SATISFACTION AND ATTRITION COUNTS

-- WORK LIFE BALANCE AND ATTRITION COUNTS
SELECT WORK_LIFE_BALANCE, COUNT(*) AS ATTRITION_COUNTS
FROM [LBP01].[dbo].[hr]
WHERE Attrition = 1
GROUP BY Work_Life_Balance
ORDER BY ATTRITION_COUNTS DESC;
-- THERE IS NO RELATION BETWEEN THE WORK LIFE BALANCE AND ATTRITION COUNTS

-- DISTANCE FROM HOME AND ATTRITION COUNTS
select distance_from_home COUNT(*) AS ATTRITION_COUNTS
from [LBP01].[dbo].[hr]
where attrition = 1
group by distance_from_home
order by distance_from_home desc, attr_count desc;
-- THERE IS NO RELATION BETWEEN DISTANCE FROM HOME AND ATTRITION COUNTS


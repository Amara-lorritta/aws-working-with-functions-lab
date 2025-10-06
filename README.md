## Working with Functions
## **Overview**

This hands-on AWS lab demonstrates how to use common SQL functions with the SELECT statement and WHERE clause to summarize, manipulate, and filter data in a relational database.
You connect to a MySQL database (world) hosted on Amazon RDS, using an EC2 Command Host through AWS Systems Manager (Session Manager).

## **Objectives & Learning Outcomes**

After completing this lab, I was able to:

Use aggregate functions (SUM(), MIN(), MAX(), AVG()) to summarize data

Use SUBSTRING_INDEX() to split strings into parts

Apply LENGTH() and TRIM() to calculate string lengths and remove spaces

Use DISTINCT() to remove duplicate records

Combine functions in both the SELECT statement and the WHERE clause

## **Architecture**
<p align="center"> <img src="architecture/database-lab-architecture.png" alt="Database Architecture" width="650"/> </p>

Architecture Summary:

User (Lab Student) connects via AWS Management Console

Amazon EC2 Command Host acts as a MySQL client terminal

Amazon RDS (MySQL) hosts the world database containing city, country, and countrylanguage tables

The EC2 host runs queries using built-in SQL functions for data summarization and text manipulation

## **Commands and Steps**
```
bash
# Step 1: Connect to the MySQL database
sudo su
cd /home/ec2-user/
mysql -u root --password='re:St@rt!9'

# Step 2: Verify the world database
SHOW DATABASES;

# Step 3: Review the country table
SELECT * FROM world.country;

# Step 4: Use aggregate functions to summarize data
SELECT SUM(Population), AVG(Population), MAX(Population), MIN(Population), COUNT(Population)
FROM world.country;

# Step 5: Split region names using SUBSTRING_INDEX()
SELECT Region, SUBSTRING_INDEX(Region, " ", 1)
FROM world.country;

# Step 6: Filter records using SUBSTRING_INDEX() in WHERE clause
SELECT Name, Region
FROM world.country
WHERE SUBSTRING_INDEX(Region, " ", 1) = "Southern";

# Step 7: Use LENGTH() and TRIM() to filter short region names
SELECT Region
FROM world.country
WHERE LENGTH(TRIM(Region)) < 10;

# Step 8: Remove duplicates using DISTINCT()
SELECT DISTINCT(Region)
FROM world.country
WHERE LENGTH(TRIM(Region)) < 10;

# Step 9: Challenge – Split Micronesian/Caribbean into two columns
SELECT Region,
       SUBSTRING_INDEX(Region, "/", 1) AS "Region Name 1",
       SUBSTRING_INDEX(Region, "/", -1) AS "Region Name 2"
FROM world.country
WHERE Region LIKE "%Micronesia%/%Caribbean%";
```
## **Screenshots**

1️⃣ 01_aggregate_functions.png


2️⃣ 02_substring_index_split.png


3️⃣ 03_length_trim_filter.png


4️⃣ 04_distinct_function.png


5️⃣ 05_challenge_split_columns.png


## **Tools Used**

Amazon EC2 (Command Host) – for database connection and SQL execution

Amazon RDS (MySQL) – relational database hosting the world schema

AWS Systems Manager (Session Manager) – secure browser-based access

MySQL CLI – to run queries and view results

## **Key Takeaways**

Practiced using aggregate and string functions to summarize and manipulate data

Learned how to split and clean string values in SQL queries

Used DISTINCT() to filter duplicates and ensure data accuracy

Strengthened understanding of functions in both SELECT and WHERE clauses

Improved query readability with column aliases (AS)

## **Author**

Amarachi Emeziem
Cloud Security & IT Support Specialist | AWS & Azure Certified
LinkedIn: 
 

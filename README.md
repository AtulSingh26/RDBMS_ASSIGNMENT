# RDBMS_ASSIGNMENT



## QUESTION 1 
Create a database named employee, then import data_science_team.csv proj_table.csv and emp_record_table.csv into the employee database from the given resources. 

`CREATE DATABASE employee` USING THIS COMMAND I HAVE CREATED DATABASE.
`USE employee`   To use the database
 
 * The below screenshot is of MYSQL WORKBENCH and then click on Table data import wizard and then select the file location.
 <img width="354" alt="Screenshot 2023-02-23 at 2 54 17 PM" src="https://user-images.githubusercontent.com/122472996/220908609-c8276bc5-4773-4670-a483-7a9f3842d5d5.png">
 
 * Second Step
<img width="797" alt="Screenshot 2023-02-23 at 6 16 58 PM" src="https://user-images.githubusercontent.com/122472996/220910845-40a7af8a-4616-400e-8d2d-27bb724dcbf2.png">

* FINAL DATABASE 
<img width="287" alt="Screenshot 2023-02-23 at 6 17 25 PM" src="https://user-images.githubusercontent.com/122472996/220911149-5345cb83-d6da-45df-a14f-914ccc0cd77e.png">



 

							
						 			
				
			
		
## QUESTION 2
Create an ER diagram for the given employee database.

<img width="949" alt="220896998-e3f3e93b-0d6e-4901-9ba6-e9c32c17084b" src="https://user-images.githubusercontent.com/122472996/220919935-2326fe12-e41b-4827-bbaf-3b84f19f95b9.png">








## QUESTION 3  

Write a query to fetch EMP_ID, FIRST_NAME, LAST_NAME, GENDER, and DEPARTMENT from the employee record table, and make a list of employees and details of their department.

```
SELECT EMP_ID,FIRST_NAME,LAST_NAME,GENDER,DEPT AS DEPARTMENT
FROM emp_record_table
```
OUTPUT - 
<img width="353" alt="Screenshot 2023-02-23 at 7 02 05 PM" src="https://user-images.githubusercontent.com/122472996/220921301-8d2ebf74-5daf-44db-aa61-7dba18602ad0.png">





## QUESTION 4
Write a query to fetch EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPARTMENT, and EMP_RATING if the EMP_RATING is:

> Less than 2
```
SELECT EMP_ID,FIRST_NAME,LAST_NAME,GENDER,DEPT AS DEPARTMENT,EMP_RATING
FROM emp_record_table
WHERE EMP_RATING < 2  -- This condition it will Fetch where emp_rating is less than 2
```
OUTPUT - 

<img width="624" alt="Screenshot 2023-02-23 at 7 05 37 PM" src="https://user-images.githubusercontent.com/122472996/220922167-e6cf69ab-0b4e-4c43-8e8b-eecb32a9bd15.png">


> Greater than 4
```
SELECT EMP_ID,FIRST_NAME,LAST_NAME,GENDER,DEPT AS DEPARTMENT,EMP_RATING
FROM emp_record_table
WHERE EMP_RATING > 4 -- This condition will fetch only those rows where emp_rating is greater than 4
```
Output  - 
<img width="624" alt="Screenshot 2023-02-23 at 7 06 16 PM" src="https://user-images.githubusercontent.com/122472996/220922413-373e5c8c-ea7a-46b0-991b-30916bef42f2.png">



> Between Two and Four

```
SELECT EMP_ID,FIRST_NAME,LAST_NAME,GENDER,DEPT AS DEPARTMENT,EMP_RATING
FROM emp_record_table
WHERE EMP_RATING BETWEEN 2 AND 4  -- This will Fetch where only those where emp_rating is between 2 and 4
```

OUTPUT -
<img width="437" alt="Screenshot 2023-02-23 at 3 50 32 PM" src="https://user-images.githubusercontent.com/122472996/220922508-bd34eb45-c2c3-4f14-9e3d-6b6d8ae53ce5.png">



## QUESTION 5 
Write a query to concatenate the FIRST_NAME and the LAST_NAME of employees in the Finance department from the employee table and then give the resultant column alias as NAME.
```
SELECT CONCAT(FIRST_NAME,' ',LAST_NAME) AS 'NAME' -- CONCAT() concatinates values which is being passed.
FROM emp_record_table
WHERE DEPT = 'FINANCE'
```

OUTPUT -
<img width="186" alt="Screenshot 2023-02-23 at 4 02 52 PM" src="https://user-images.githubusercontent.com/122472996/220922566-870aea65-6c50-4ca5-845b-6492e67a1cc2.png">


## QUESTION 6 
Write a query to list only those employees who have someone reporting to them. Also, show the number of reporters (including the President).

```
SELECT mgr.EMP_ID,CONCAT (mgr.FIRST_NAME,' ',mgr.LAST_NAME) AS 'MANAGER NAME',mgr.DEPT AS DEPARTMENT, COUNT(emp.MANAGER_ID) AS 'Number of Employee Reporting'
FROM emp_record_table emp 
JOIN emp_record_table mgr
ON emp.MANAGER_ID = mgr.EMP_ID
GROUP BY  mgr.EMP_ID ;
```




OUTPUT -
<img width="447" alt="Screenshot 2023-02-23 at 4 08 22 PM" src="https://user-images.githubusercontent.com/122472996/220922612-eff4a88c-7c71-4d13-9905-fee434a20a9e.png">




## QUESTION 7 
Write a query to list down all the employees from the healthcare and finance departments using union. Take data from the employee record table.
```
SELECT EMP_ID,FIRST_NAME,LAST_NAME,GENDER,DEPT
FROM emp_record_table
WHERE DEPT = 'Healthcare'

UNION 

SELECT EMP_ID,FIRST_NAME,LAST_NAME,GENDER,DEPT
FROM emp_record_table
WHERE DEPT = 'Finance'

```

OUTPUT -
<img width="442" alt="Screenshot 2023-02-23 at 4 11 59 PM" src="https://user-images.githubusercontent.com/122472996/220922678-35080581-a2f6-4248-a0fa-688974612d3b.png">



 ## QUESTION 8
 Write a query to list down employee details such as EMP_ID, FIRST_NAME, LAST_NAME, ROLE, DEPARTMENT, and EMP_RATING grouped by dept. Also include the respective employee rating along with the max emp rating for the department.
```
SELECT EMP_ID,FIRST_NAME,LAST_NAME,GENDER,ROLE,DEPT AS DEPARTMENT,MAX(EMP_RATING) OVER(PARTITION BY DEPT ) AS 'MAX EMP RATING' 
FROM emp_record_table

```

OUTPUT  - 
<img width="662" alt="Screenshot 2023-02-23 at 4 16 06 PM" src="https://user-images.githubusercontent.com/122472996/220922816-e4b3129f-42a6-462c-bc7c-81d20658fb58.png">




 ## QUESTION 9 
Write a query to calculate the minimum and the maximum salary of the employees in each role. Take data from the employee record table.
```
SELECT distinct Role ,  MIN(SALARY) OVER(PARTITION BY ROLE) AS 'Minimum Salary'  , MAX(SALARY) OVER(PARTITION BY ROLE) AS 'Maximum Salary'
FROM EMP_RECORD_TABLE 
```

OUTPUT- <img width="370" alt="Screenshot 2023-02-23 at 4 23 50 PM" src="https://user-images.githubusercontent.com/122472996/220922925-7ee2ae16-0daa-4953-8f41-5f64227e77db.png">







## QUESTION 10 
Write a query to assign ranks to each employee based on their experience. Take data from the employee record table.

```
SELECT CONCAT(FIRST_NAME,' ',LAST_NAME) AS NAME ,ROLE, EXP AS 'Experience', DENSE_RANK() OVER(ORDER BY EXP DESC ) AS 'Rank'
from emp_record_table
```

OUTPUT-


![Uploading Screenshot 2023-02-23 at 4.32.12 PM.png…]()









## QUESTION 11 
Write a query to create a view that displays employees in various countries whose salary is more than six thousand. Take data from the employee record table.

```
CREATE VIEW DISPLAY AS 
(
     SELECT EMP_ID,CONCAT (FIRST_NAME,' ',LAST_NAME) AS NAME , SALARY
     FROM EMP_RECORD_TABLE
     WHERE SALARY > 6000
)
-- After Creating the view
SELECT 
*
FROM
DISPLAY

```


![Uploading Screenshot 2023-02-23 at 4.32.12 PM.png…]()









## QUESTION 12 
Write a nested query to find employees with experience of more than ten years. Take data from the employee record table.
```
SELECT *
FROM EMP_RECORD_TABLE
WHERE EMP_ID 
IN (
SELECT EMP_ID 
FROM EMP_RECORD_TABLE 
WHERE EXP > 10)
```

![Uploading Screenshot 2023-02-23 at 4.37.53 PM.png…]()





 ## Q13  
Write a query to create a stored procedure to retrieve the details of the employees whose experience is more than three years. Take data from the employee record table.
```

DELIMITER $$

CREATE PROCEDURE exp_emp()

BEGIN

SELECT *
FROM emp_record_table
WHERE EXP>3;


END $$

DELIMITER ;




CALL exp_emp()

```

OUTPUT 
<img width="979" alt="Screenshot 2023-02-23 at 4 39 39 PM" src="https://user-images.githubusercontent.com/122472996/220899614-1c46ce40-881f-4882-a73d-190c9a54682d.png">


## QUESTION 14 
Write a query using stored functions in the project table to check whether the job profile assigned to each employee in the data science team matches the organization’s set standard. The standard being:

* For an employee with experience less than or equal to 2 years assign 'JUNIOR DATA SCIENTIST', For an employee with the experience of 2 to 5 years assign 'ASSOCIATE DATA SCIENTIST',
* For an employee with the experience of 5 to 10 years assign 'SENIOR DATA SCIENTIST',
* For an employee with the experience of 10 to 12 years assign 'LEAD DATA SCIENTIST',
* For an employee with the experience of 12 to 16 years assign 'MANAGER'

```
DELIMITER $$
CREATE FUNCTION Employee_ROLE(
EXP int
)
RETURNS VARCHAR(40)
DETERMINISTIC
BEGIN

DECLARE Employee_ROLE VARCHAR(40);


IF EXP>12 AND 16 THEN
SET Employee_ROLE="MANAGER";

ELSEIF EXP>10 AND 12 THEN
SET Employee_ROLE ="LEAD DATA SCIENTIST";

ELSEIF EXP>5 AND 10 THEN
SET Employee_ROLE ="SENIOR DATA SCIENTIST";

ELSEIF EXP>2 AND 5 THEN
SET Employee_ROLE ="ASSOCIATE DATA SCIENTIST";


ELSEIF EXP<=2 THEN
SET Employee_ROLE ="JUNIOR DATA SCIENTIST";

END IF;
RETURN (Employee_ROLE);
END $$

DELIMITER ;

SELECT 
IF 
(
SUM(
CASE 
WHEN ROLE = Employee_ROLE(EXP) 
THEN 1 ELSE 0  
END
)  = COUNT(emp_id)  , 'ALL DATA MATCHES','NOT ALL DATA MATCHES') AS RESULT
FROM data_science_team

```

<img width="157" alt="Screenshot 2023-02-23 at 4 41 11 PM" src="https://user-images.githubusercontent.com/122472996/220898880-77a2024b-08b7-4227-bd03-be2f2514dce7.png">



## QUESTION 15
Create an index to improve the cost and performance of the query to find the employee whose FIRST_NAME is ‘Eric’ in the employee table after checking the execution plan.

```
CREATE 
INDEX INDEX_FIRST_NAME
ON emp_record_table(FIRST_NAME);

SELECT *
FROM emp_record_table
WHERE FIRST_NAME='Eric';
```

![Uploading Screenshot 2023-02-23 at 4.44.57 PM.png…]()






##  QUESTION 16 
 Write a query to calculate the bonus for all the employees, based on their ratings and salaries (Use the formula: 5% of salary * employee rating).
 
```
SELECT EMP_ID , ROLE , SALARY,EMP_RATING, ( (0.05 * SALARY) * EMP_RATING) AS BONUS
FROM emp_record_table;
```

<img width="399" alt="Screenshot 2023-02-23 at 5 19 44 PM" src="https://user-images.githubusercontent.com/122472996/220897826-465828fb-d2a5-4ac6-8693-dde7e7e63d22.png">



## QUESTION 17 
Write a query to calculate the average salary distribution based on the continent and country. Take data from the employee record table.

```
SELECT DISTINCT CONTINENT,
AVG(SALARY) OVER(PARTITION BY CONTINENT) AS 'AVERAGE BY CONTINENT', -- USED WINDOW FUNCTION
COUNTRY, 
AVG(SALARY) OVER(PARTITION BY COUNTRY) AS 'AVERAGE BY COUNTRY'
FROM emp_record_table;
```
<img width="480" alt="Screenshot 2023-02-23 at 4 56 52 PM" src="https://user-images.githubusercontent.com/122472996/220895383-969ef5a4-6bb3-4481-9c55-eff3c129f363.png">







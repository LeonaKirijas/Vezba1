# Vezba1

#Create view for finding the maximum salary from each department.

create view maxSalaryDep as
select d.department_id, d.department_name, MAX(e.salary) as max_salary
from departments d
join employees e ON d.department_id = e.department_id
group by d.department_id, d.department_name;

SELECT * FROM maxSalaryDep;

#Write an procedure to display employees who earn more than the average salary in that company

delimiter //
create procedure HighPayEmp()
begin 
	declare avg_salary DECIMAL(10,2);
    select AVG(salary) into avg_salary from employees;
    select * from employees
    where salary > avg_salary;
end //
delimiter ;
call HighPayEmp();

#Write procedure that divide people into three groups based on their salaries (groups are input parametrs for the procedure).

#Ex. group1, group2, group 3,  

DELIMITER //

CREATE PROCEDURE DevideGroups(
    IN salary_group1 INT,
    IN salary_group2 INT,
    IN salary_group3 INT
)
BEGIN
    SELECT * FROM employees WHERE salary < salary_group1;

    SELECT * FROM employees WHERE salary > salary_group1 AND salary < salary_group2;

    SELECT * FROM employees WHERE salary > salary_group2 AND salary < salary_group3;
     SELECT * FROM employees WHERE salary > salary_group3;
END //

DELIMITER ;

CALL DevideGroups(5000, 10000, 15000);

# create trigger for fetching when salary is updated for some employeer 

DELIMITER //

CREATE TRIGGER SalaryUpdateTrigger
BEFORE UPDATE ON employees
FOR EACH ROW
BEGIN
    IF NEW.salary != OLD.salary THEN
        -- Insert the old and new salary into a log table or perform any other actions
        INSERT INTO salary_log (employee_id, old_salary, new_salary, update_timestamp)
        VALUES (OLD.employee_id, OLD.salary, NEW.salary, NOW());
    END IF;
END //

DELIMITER ;

CREATE TABLE salary_log (
    log_id INT AUTO_INCREMENT PRIMARY KEY,
    employee_id INT,
    old_salary INT,
    new_salary INT,
    update_timestamp TIMESTAMP
);
UPDATE employees SET salary = 12000 WHERE employee_id = 101;

mysqldump -u your_username -p your_database_name > backup.sql
(Create a view for finding the maximum salary from each department:
sql
Copy code
CREATE VIEW MaxSalaryPerDepartment AS
SELECT department_id, MAX(salary) AS max_salary
FROM employees
GROUP BY department_id;
Write a procedure to display employees who earn more than the average salary in that company:
sql
Copy code
CREATE PROCEDURE EmployeesAboveAverageSalary AS
BEGIN
    DECLARE avg_salary INTEGER;
    SELECT AVG(salary) INTO avg_salary FROM employees;

    SELECT * FROM employees WHERE salary > avg_salary;
END;
Write a procedure that divides people into three groups based on their salaries:
sql
Copy code
CREATE PROCEDURE DivideEmployeesIntoGroups(IN group1 INTEGER, IN group2 INTEGER, IN group3 INTEGER) AS
BEGIN
    SELECT * FROM employees WHERE salary < group1;

    SELECT * FROM employees WHERE salary BETWEEN group1 AND group2;

    SELECT * FROM employees WHERE salary BETWEEN group2 AND group3;

    SELECT * FROM employees WHERE salary > group3;
END;
Create a trigger for fetching when salary is updated for some employee:
sql
Copy code
CREATE TRIGGER SalaryUpdateTrigger
AFTER UPDATE ON employees
FOR EACH ROW
BEGIN
    INSERT INTO salary_updates_log (employee_id, old_salary, new_salary, update_time)
    VALUES (OLD.employee_id, OLD.salary, NEW.salary, NOW());
END;) od teo
Mongo DB
test> use FinalTerm
switched to db FinalTerm
FinalTerm> db.MySQL.insertMany([{ name: "MySQL Row 1", value: "MySQL Data 1" },{ name: "MySQL Row 2", value: "MySQL Data 2" },{ name: "MySQL Row 3", value: "MySQL Data 3" }])
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('65a82b970b6829e5d0aae19e'),
    '1': ObjectId('65a82b970b6829e5d0aae19f'),
    '2': ObjectId('65a82b970b6829e5d0aae1a0')
  }
}
FinalTerm> db.MongoDB.insertMany([{ name: "MongoDB Document 1", value: "MongoDB Content 1" },{ name: "MongoDB Document 2
", value: "MongoDB Content 2" },{ name: "MongoDB Document 3", value: "MongoDB Content 3" }])
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('65a82ba30b6829e5d0aae1a1'),
    '1': ObjectId('65a82ba30b6829e5d0aae1a2'),
    '2': ObjectId('65a82ba30b6829e5d0aae1a3')
  }
}

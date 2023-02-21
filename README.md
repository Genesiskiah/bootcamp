# bootcamp
my learning of sql
drop database employees; 

Create database employees; 

USE employees;

create table employeedemographics
(EmployeeID int , 
Firstname varchar(50), 
Lastname varchar(50),
Age int,
Gender varchar(50) );

select * 
from employeedemographics ;

create table employeesalary 
(employeeID int, 
jobtitle varchar (50), 
salary int); 

select * from employeesalary;

Create Table WareHouseEmployeeDemographics 
(EmployeeID int, 
FirstName varchar(50), 
LastName varchar(50), 
Age int, 
Gender varchar(50) );

select * from warehouseemployeedemographics;


Insert into employeedemographics Values
(1001, 'Jim', 'Halpert', 30, 'Male'),
(1002, 'Pam', 'Beasley', 30, 'Female'),
(1003, 'Dwight', 'Schrute', 29, 'Male'),
(1004, 'Angela','Martin', 31 ,'Female'),
(1005, 'Toby', 'Flenderson', 32, 'Male'),
(1006, 'Michael', 'Scott', 35, 'Male'),
(1007, 'meredith', 'Palmer', 32, 'Female'),
(1008, 'Stanley', 'Hudson', 38, 'Male'),
(1009, 'Kevin','Malone', 31, 'Male');
 Insert into EmployeeDemographics VALUES
(1011, 'Ryan', 'Howard', 26, 'Male'),
(NULL, 'Holly', 'Flax', NULL, NULL),
(1013, 'Darryl', 'Philbin', NULL, 'Male');


insert into employeesalary values 
(1002,'Receptionist', 36000),
(1003,'Salesman', 63000),
(1004,'Accountant', 47000),
(1005,'HR', 50000),
(1006,'Regional Manager', 65000),
(1007,'Supplier Relations', 41000),
(1008,'Salesman', 48000),
(1009,'Accountant' , 42000); 

Insert into WareHouseEmployeeDemographics VALUES
(1013, 'Darryl', 'Philbin', NULL, 'Male'),
(1050, 'Roy', 'Anderson', 31, 'Male'),
(1051, 'Hidetoshi', 'Hasagawa', 40, 'Male'),
(1052, 'Val', 'Johnson', 31, 'Female');

-- table 1 select * from employeedemographics ;
-- table 2 select * from employeesalary;
-- table 3 select * from warehouseemployeedemographics;


-- commnands 
-- top , distinct , count , as , max , min , avg

-- how to select specific coloumns 
select firstname , lastname 
from employeedemographics; 

select distinct (gender) 
from employeedemographics; 

select count(lastname) AS lastnamecount 
from employeedemographics; 

-- as changes name of column 

select max(salary)
from employeesalary;

-- retuns highest salary 

select min(salary)
from employeesalary;

-- returns minimum salary 

select AVG(salary)
from employeesalary;

-- returns average salary


select * 
from employeedemographics 
WHERE Firstname = 'jim' ;

-- brings back results where equals jim 

select * 
from employeedemographics 
WHERE Firstname <> 'jim' ;

-- all the results exluding jim

select * 
from employeedemographics 
WHERE age > 30;

-- query reults find every age greater than 30

select * 
from employeedemographics 
WHERE age >= 30;

--  query reults find every age 30 and above 


select * 
from employeedemographics 
WHERE age < 32 ;

-- less than 

select * 
from employeedemographics 
WHERE age <= 32 ;

-- equal too and less than 


select * 
from employeedemographics 
WHERE age <= 32 and gender = 'male' ;

-- picks out age less than or equal to 32 and male 


select * 
from employeedemographics 
WHERE age <= 32 or gender = 'male' ;

-- brings back all males and anyone who is equal to 32 or less 


select * 
from employeedemographics 
WHERE lastname like 'S%' ;

--  wild card the percentage brings back all results in this scenario lastnames starting with s 

select * 
from employeedemographics 
WHERE lastname like '%S%' ;

-- when a wildcard is put in the beggining it will bring back results that have a S anywhere in the lastname 

select * 
from employeedemographics 
WHERE lastname like 's%o%' ;

-- this is where you want to find a last name begginig with S but contains a O somewhere theres only one person with that formation which is scott 

select * 
from employeedemographics 
WHERE firstname in ('jim', 'michael');

-- in statemnt is a condensed waay to use = for multiple things 

select gender , count(gender) 
from employeedemographics 
group by gender; 

-- this query shows total of males and females in coloumn 

select gender, age,  count(gender) 
from employeedemographics 
group by gender, age ;  

--  this shows the amount in each row
-- with group by statemenrt you can use this with multiple coloums as long as you include them in the group by clause 
 -- the count coloumn acts like a view, the age and age coloumn are real 
 
 

select gender, age,  count(gender) 
from employeedemographics 
where age > 31
group by gender, age; 


select gender,  count(gender)  as countgender
from employeedemographics
where age > 31
group by gender
order by countgender desc  ;


select * 
from employeedemographics 
order by age desc ;

select * 
from employeedemographics 
order by age , gender desc;  

select * from employeedemographics;
select * from employee salary;

-- joins when using joins its best to use tables with similar coloumn in this case employeeid typically we would want it to be a unique field 

select *
from employeedemographics 
inner join employeesalary 
on employeedemographics.employeeid = employeesalary.employeeid; 

-- inner join is going to show everything that is similar 

select *
from employeedemographics 
left join employeesalary 
on employeedemographics.employeeid = employeesalary.employeeid; 

-- left join 

select * 
from employeedemographics 
Union
select * 
from warehouseemployeedemographics; 

-- adds information from second colllumn by inserting it below in the same order 


select * 
from employeedemographics 
Union all
select * 
from warehouseemployeedemographics 
order by employeeid;

-- union all shows data as is and includes duplicates 


select employeeid , firstname, age 
from employeedemographics 
union 
select employeeid , jobtitle, salary 
from employeesalary
order by employeeid;

-- be careful when using union to combine tables and makesure data is the same 


select firstname, lastname, age,
Case  
when age > 30 then 'old' else 'young' end as agestatus
from employeedemographics 
where age is not null 
order by age;  

-- a new coloum was created which splits the data into two categories old and young, 
-- if they are over 30 they are categorized as old if there under 30 they are young 

select firstname, lastname, age,
Case  
when age > 30 then 'old' 
when age between 27 and 30 then 'young'
else 'baby' end as agestatus

from employeedemographics 
where age is not null 
order by age;

-- multiple when statement 


select firstname, lastname, age,
Case  
when age = 38 then 'stanley'
when age > 30 then 'old' 

else 'baby' end as agestatus

from employeedemographics 
where age is not null 
order by age;


select  firstname, lastname, jobtitle, salary
from employeedemographics
join employeesalary 
on employeedemographics.employeeid = employeesalary.employeeid;


select firstname, lastname, jobtitle, salary,
case 
when jobtitle = 'salesman' then salary + (salary * .10)
when jobtitle = 'accountant' then + (salary * .05)
when jobtitle = 'hr' then salary + (salary * .000001)
else salary + (salary * .03)
end  as salaryafterraise
from employeedemographics
join employeesalary 
on employeedemographics.employeeid = employeesalary.employeeid;

-- the case statement is used to categorise / label things 
-- in this example it was used along with calculations 
-- we incresased the salaries, 
-- salesman got a 10% raise 
-- acountant got 5% raise 
-- hr im not sure ??
-- everyone else got a 3% pay rise 



select jobTitle, count(jobtitle)
from employeedemographics 
join employeesalary 
on employeedemographics.employeeid = employeesalary.employeeid
group by jobTitle
having count(jobtitle) > 1;


-- having is dependant on group by statement 
-- this query shows the jobs that have more than one employee for that job title

select jobTitle, AVG(salary)
from employeedemographics 
join employeesalary 
on employeedemographics.employeeid = employeesalary.employeeid
group by jobTitle
having  avg(salary) > 45000
order by avg(salary); 
 
 -- this shows us job titles that have a average salary of over 45000 
 
 select * 
 from employeedemographics;
 
 update employeedemographics
 set employeeid = 1012 
 where firstname = 'holly' AND lastname = 'flax';
 
 -- need to work on this as its not working 

 update employeedemographics
 set age = 31, gender = 'female'
 where employeeid = 1012; 
 
 delete from employeedemographics
 where employeeid = 1005; 
 -- this is not working for me either need to work on this 
 
 select firstname as fname 
 from employeedemographics;
 
 select firstname +' ' + lastname as fullname
 from employeedemographics;
 
 -- did not work was supposed to return first and last name in one coloumn  
 
 select avg(age) as avgage
 from employeedemographics; 
 
 select demo.employeeid
 from employeedemographics as demo; 
 
 -- when using as in from section you need to reference as name in select statement 
 
 
 select demo.employeeid
 from employeedemographics as demo
 join employeesalary as sal
 on demo.employeeid = sal.employeeid;
 
 select firstname , lastname, gender, salary, 
 count(gender) over (partition by gender) as totlgender 
 from employeedemographics 
 join employeesalary 
 on employeedemographics.employeeid = employeesalary.employeeid;
 
 -- the partrition by vlause shows us here whos working and the total gender row shows that
 -- there are 3 total women who work alongside her in this employee demographics table 
 
 
 -- cte acts like a subquery 
 
 with CTE_employee as 
 (select firstname , lastname, gender, salary, 
 count(gender) over (partition by gender) as totlgender,
 AVG(salary) over (partition by gender) as avgsalary 
 from employeedemographics 
 join employeesalary 
 on employeedemographics.employeeid = employeesalary.employeeid
 where salary > '45000'
 )
 select *
 from cte_employee; 
 
 -- This query only works when run fully because it does not exist 
 

Setting delimiter to `];` from `;`(default)
`delimiter ];`

Function to find average of three numbers in sql
```sql
create function avg3no(a int, b int, c int) returns int
begin
    declare sum,avg int;
    set sum = a + b + c;
    set avg = sum/3;
    return avg;
end ];
```
Procedure to find average of three numbers in sql
```sql
create procedure avg3no(In a int, In b int, In c int, Out t int)
begin
    declare sum int;
    set sum = a + b + c;
    set t = sum/3;
end ];
```
Example to use result of procedure:
```sql
call avg3no(4, 5, 6, @avg) ];
select @avg ];
```
Function to find factorial of a number in sql
```sql
create function factorial(n int) returns int
begin
    declare f, i int default 1;
    myloop:loop
    if i>n then
    leave myloop;
    else
    set f=f*i;
    set i = i+1;
    iterate myloop;
    end if;
    end loop;
    return f;
end ];
```
Procedure to find factorial of a number in sql
```sql
create procedure factorial(In n int, Out fact int)
begin
    declare f, i int default 1;
    myloop:loop
    if i>n then
    leave myloop;
    else
    set f = f*i;
    set i = i+1;
    iterate myloop;
    end if;
    end loop;
    set fact = f;
end ];
```
Function to find fibonacci sequence and sum of the sequence
``` sql
create function fibonacci(n int) returns varchar(1000)
begin
    declare i int default 3;
    declare a, temp int default 0;
    declare b, sum int default 1;
    declare str varchar(1000);
    set str = CAST(a as char(2));
    set str = CONCAT(str, " ");
    myloop:loop
    if i > n then leave myloop;
    else
    set temp = a + b;
    set a = b;
    set b = temp;
    set i = i+1;
    set sum = sum + temp;
    set str = CONCAT(str, CAST(a as char(2)));
    set str = CONCAT(str, "");
    end if;
    end loop;
    set str = CONCAT(str, CAST(b as char(2)));
    set str = CONCAT(str, "and sum =");
    set str = CONCAT(str, CAST(sum as char(3)));
    return str;
end ];
```
Procedure to find fibonacci sequence and sum of the sequence
```sql
create procedure fibonacci(In n int, Out retStr varchar(1000))
begin
    declare i int default 3;
    declare a,temp int default 0;
    declare b,sum int default 1;
    declare str varchar(1000);
    set str = CAST(a as char(2));
    set str = CONCAT(str, "");
    myloop:loop
    if i > n then
    leave myloop;
    else
    set temp = a+b;
    set a = b;
    set b = temp;
    set i = i+1;
    set sum = sum + temp;
    set str = CONCAT(str, CAST(a as char(2)));
    set str = CONCAT(str, " ");
    end if;
    end loop;
    set str = CONCAT(str, CAST(b as char(2)));
    set str = CONCAT(str, " and sum= ");
    set str = CONCAT(str, CAST(sum as char(3)));
    set retStr = str;
end ];
```
Function to find age from given date of birth
``` sql
create function calcAge(dat date) returns varchar(25)
begin
    declare curDate date default CURRENT_DATE();
    declare tempDate date;
    declare year, month, date int default 0;
    declare str varchar(25) default "";
    set year = TIMESTAMPDIFF(YEAR, dat, curDate);
    set month = TIMESTAMPDIFF(MONTH, dat, curDate);
    set month = month - (year*12);
    set tempDate = DATE_ADD(dat, INTERVAL year YEAR);
    set tempDate = DATE_ADD(tempDate, INTERVAL month MONTH);
    set date = DATEDIFF(curDate, tempDate) + 1;
    set str = CONCAT(str, CAST(year as char(2)));
    set str = CONCAT(str, "Y ");
    set str = CONCAT(str, CAST(month as char(2)));
    set str = CONCAT(str, "M ");
    set str = CONCAT(str, CAST(date as char(2)));
    set str = CONCAT(str, "D");
    return str;
end ];
```
Example :
``` sql
select calcAge('1992-05-11') ];
```
Procedure to find age from given date of birth
```sql
create procedure calcAge(In dat date, Out retStr varchar(25))
begin
    declare curDate date default CURRENT_DATE();
    declare tempDate date;
    declare year, month, date int default 0;
    declare str varchar(25) default "";
    set year = TIMESTAMPDIFF(YEAR, dat, curDate) ;
    set month = TIMESTAMPDIFF(MONTH, dat, curDate);
    set month = month - (year * 12);
    set tempDate = DATE_ADD(dat, INTERVAL year YEAR);
    set tempDate = DATE_ADD(tempDate, INTERVAL month MONTH);
    set date = DATEDIFF(curDate, tempDate) + 1;
    set str = CONCAT(str, CAST(year as char(2)));
    set str = CONCAT(str, "Y ");
    set str = CONCAT(str, CAST(month as char(2)));
    set str = CONCAT(str, "M ");
    set str = CONCAT(str, CAST(date as char(2)));
    set str = CONCAT(str, "D");
    set retStr = str;
end ];
```


Function to run `SELECT` sql query on a table
```sql
cre1ate function totalNoEmployees() returns int
begin
    declare s int;
    select count(*) from Employee into s;
    return s;
end ];
```

Example to use it:
```sql
SELECT totalNoEmployees() ];
```

Procedure to run `SELECT` sql query on a table
```sql
create procedure totalNoEmployees(Out count int)
begin
    declare s int;
    select count(*) from Employee into s;
    set count = s;
end ];
```

Function with input to process
```sql
create function calcBudget(dept varchar(30)) returns int
begin
    declare deptnumber varchar(5);
    declare budget int default 0;
    select DNo from Department where Dept_Name = dept into deptnumber;
    select sum(Salary) from Employee where DNo = deptnumber into budget;
    return budget;
end ];
```
Procedure with input to process
```sql
create procedure calcBudget(In dept varchar(30), Out budget int)
begin
    declare deptnumber varchar(5);
    declare sumSal int default 0;
    select Dno from Department where Dept_Name = dept into deptnumber;
    select sum(Salary) from Employee where Dno = deptnumber into sumSal;
    set budget = sumSal;
end ];
```
Function to print Message on screen
```sql
create function printMsg(name varchar(50)) returns varchar(100)
begin
    declare msg varchar(100) default "Hello";
    set msg = CONCAT(msg, name);
    set msg = CONCAT(msg, " How are you?");
    return msg;
end ];
```
Procedure to print Message on screen
```sql
create procedure printMsg(In name varchar(50), Out message varchar(100))
begin
    declare msg varchar(100) default "Hello ";
    set msg = CONCAT(msg, name);
    set msg = CONCAT(msg, " How are you?");
    set message = msg;
end ];
```

Trigger(with trigger name `insertTrig`) for logging operations(into a table `LogTable`) for a particular command(INSERT) whenever ran on a table(Employee)
```sql
create trigger insertTrig after insert on Employee for each row begin insert into LogTable values (user(), 'Insert', now(), '-', '-', '-', Employee.Emp_id, Employee.Emp_name, Employee.Salary); end];
```

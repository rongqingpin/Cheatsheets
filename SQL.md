## SQL

comment: `-- ...`

---

creation:  

```SQL
CREATE DATABASE db DEFAULT CHARACTER SET utf8; -- non Latin characters allowed

DROP TABLE IF EXISTS t1;
CREATE TABLE t1 (
    c1, <TYPE>,          -- int, real, double, varchar(N), text, blob ...
    ...
    PRIMARY KEY (...)    -- all unique values
);
INSERT INTO t1 (c1, c2, ...) VALUES (x1, NULL, '...', ...);
```

`DELECT FROM t1 WHERE ...`

`UPDATE t1 SET c1 = ... WHERE ...`

---

```SQL
SELECT c1 <as ...>, f(...) <AS ...>, *, ...
                -- f: some function / variable of C
                -- *: all columns
FROM t1
WHERE c1 ? ..., ...              -- ? is some operator
GROUP BY ..., ...
HAVING P(...) ? ..., ...
ORDER BY ..., ...
LIMIT n;
```

```SQL
SELECT ... FROM t1 JOIN t2 ON t1.c1 = t2.c2 WHERE ...
```

---

### operators

**arithmetic** operator: `+`, `-`, `*`, `/`, `%` (modulo)  
note integers produce integers  

**comparison** operators: =, <> (not equal), <, >, <=, >=  

**range**: `<C1> between a and b`; both edges included  

**condition** operator: `and` (no parenthesis necessary), `or`, `xor` (exclusive, not 'both')  

**existence**: `<C1> in (a, <b, c, ...>)`  

`is null`  
`is not null`

**pattern** comparison:  
`<c1> LIKE '...'`  
`<C1> NOT LIKE '...'`  
`'%'`: any number of characters  
`'_'`: one character  

---

### more on functions

`distinct C`: unique elements

`count(...)`: `...` can be `*` (No. of rows), `C` (non-missing values), `P(C)`

`avg(...)`  
`max(...)`  
`min(...)`  
`sum(...)`

`round(..., N)`: round the value to N decimals

`length(...)`: the number of characters; applied to each element in `...`  
`left(..., N)`: output the first N character

---

### more on `select`

```SQL
select * from <table> limit N;

select <C1> from <table> order by <C1, C2, ...> ...
        -- order, default ascending (e.g. a-z), or add desc
        -- if sort by multiple columns, start from the first

select <C1>, count(*) from <table> group by <C1, ...>
select <C1>, count(*) from <table> group by <C1> order by count
select <C1>, avg(C2) from <table> group by <C1>
select <C1> from <table> group by <C1> having count(*) ? ...
```

---

`'year-0m-0d'`: ISO date format



## MySQL

`$ /<path>/mysql -u <username> -p <password>`: using MAMP, path is `/Applications/MAMP/Library/bin/`

after entering, command line starts with `mysql>`, enter after this

`> show databases;`

`> use db;`

`> describe t1;`

```... ...```: one variable (string) with blanks


## PostgreSQL

`$ psql -h localhost`: start the command line tool  
`$ psql postgres -U ...`: enter the user

after entering, the command line starts with `postgres=#`

`\du`: list all current users  
`\list`: list all databases

`\connect ...`: enter the database  
`\dt`: list the tables in this database

`\password postgres`: change password for postgres

`\q`: exit

`CREATE ROLE ... WITH LOGIN PASSWORD '...';`  
`ALTER ROLE ... CREATEDB;`

`create database ...;`  
`grant all privileges on database ... to ...;`

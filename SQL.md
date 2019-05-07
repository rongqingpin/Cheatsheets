## SQL

comment: `-- ...`

---

creation:  

```SQL
CREATE DATABASE db DEFAULT CHARACTER SET utf8;    -- non Latin characters allowed

DROP TABLE <IF EXISTS> t1;

CREATE TABLE t1 (
  t1_id <PROPERTY_TYPE> <PROPERTY_VALUE>,
  c1 <TYPE> <VALUE>,
  ...
    
  CONSTRAINT FOREIGN KEY (t2_id) REFERENCES t2 (t2_id)
    ON DELETE <CASCADE> ON UPDATE <CASCADE>,      -- RESTRICT (default) / SET NULL
    
  PRIMARY KEY (t1_id, ...),   -- all unique values; if multiple, many-to-many connection table
  INDEX (...).                -- much faster scanned
) <ENGINE = InnoDB>;
```

possible properties of columns:  
data type: `INT <UNSIGNED>`, `REAL`, `DOUBLE`, `VARCHAR(N)`, `TEXT`, `BLOB`, ...  
data values: `NOT NULL`, `AUTO_INCREMENT` (must be primary key, no need for insert), `UNIQUE`

---

update:

```SQL
INSERT INTO t1 (c1, c2, ...) VALUES (x1, NULL, '...', ...); -- t1_id auto-filled

DELETE FROM t1 <WHERE ...>     -- if not condition, then empty the table  

UPDATE t1 SET c1 = ... WHERE ...

ALTER TABLE t1 ADD INDEX (c1) <USING BTREE>

ALTER TABLE t1 DROP FOREIGN CONSTRAINT ...

ALTER TABLE t1 DROP COLUMN c1

ALTER TABLE t1 ADD COLUMN c1 c1_type
```

---

access:

```SQL
SELECT c1, f(...), *, ...
                -- f: some function / variable of C
                -- *: all columns
  AS ...
  FROM t1
  WHERE c1 ? ..., ...          -- ? is some operator
  GROUP BY ..., ...
  HAVING P(...) ? ..., ...
  ORDER BY c1, c2 DESC, ...    -- start from the first
  LIMIT n;
```

combine tables:

```SQL
SELECT t1.c1, t2.c2, ... FROM t1 JOIN t2 <JOIN ...> <ON t1.c2 = t3.c1 AND ...>  -- no 'ON' then show all combinations
```

access table info:

```SQL
SHOW CREATE TABLE t1          -- can view foreign key constraint, etc.
```

---

### operators

**arithmetic** operator: `+`, `-`, `*`, `/`, `%` (modulo)  
note integers produce integers  

**comparison** operators: =, <> (not equal), <, >, <=, >=  

**range**: `<C1> between a and b`; both edges included  

**condition** operator: `and` (no parenthesis necessary), `or`, `xor` (exclusive, not 'both')  

**existence**: `<C1> in (a, <b, c, ...>)`  

`is null`, MS access SQL has `IsNull()`  
`is not null`, MS access SQL `Not IsNull()`

**pattern** comparison:  
`<c1> LIKE '...'`  
`<C1> NOT LIKE '...'`  
`'%'`: any number of characters; in MS access SQL, wildcard is `*`  
`'_'`: one character  

---

### more on functions

`distinct C`: unique elements

`count(...)`: `...` can be `*` (No. of rows), `C` (non-missing values), `P(C)`

`avg(...)`  
`max(...)`  
`min(...)`  
`sum(...)`  
`last(...)`

`round(..., N)`: round the value to N decimals  
`fix(...)`

`length(...)`: the number of characters; applied to each element in `...`. MS Access SQL uses `Len(x)`  
`left(..., N)`: output the first N character

`CONCAT(c1, c2)`

`NOW()`: current date & time

`IIF(condition, trueVal, falseVal)`

---

`'year-0m-0d'`: ISO date format



## MySQL

`$ /<path_mysql> -u <username> -p <password> -h <link>`: using MAMP, path is `/Applications/MAMP/Library/bin/mysql` on Mac, `\MAMP\bin\mysql\bin\mysql.exe` on Windows

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


## MS Access SQL

```SQL
SELECT ...
FROM (table1 INNER JOIN table2 ON table1.c1 = table2.c2) INNER JOIN table3 ON ... -- 1 to many

SELECT ... FROM (t1 LEFT JOIN t2 ON t1.c1 = t2.c1) -- all records in t1 maintained even if null

SELECT ... FROM (SELECT ... FROM ...)

SELECT (SELECT f1(...) FROM t1) AS c1, () AS c2, ... FROM ...
```

`IIf(condition, trueCase, falseCase)`

`Int()`, `Str()`, `Val()`. `DateValue(string)`  
`CDbl()`: string to double

`Round(x, N)`

`"..." & "..."`: concatenate strings  
`LCase()`: to lower case  
`InStr(string0, 'pattern')`: the location of matched pattern  
`InStrRev(string0, 'pattern')`: the location of matched pattern, search back to start  
`Mid(string0, i1, di)`: returns `string0[i1:i1+di]`  
`Left(string0, n1)`: returns first n1 chars of string0  
`Right(string0, n1)`: returns last n1 chars of string0  
`Replace(string0, "a", "b")`: replace a by b  

`Date()`: current datetime  
`year(date1)`, `month()`: get the year / month  
`DateValue(`

## SQL

comment: `-- ...`

---

creation:  

```SQL
DROP TABLE IF EXISTS t1;
CREATE TABLE t1 (
    c1, <TYPE>,          -- int, real, varchar(N), ...
    ...
    PRIMARY KEY (...)    -- all unique values
);
INSERT INTO t1 (c1, c2, ...) VALUES (x1, NULL, '...', ...);
```

---

```SQL
select C <as ...>, P(...) <as ...>, *, ...
            -- C: column name
            -- P: some function / variable of C
            -- *: all columns
from X                          -- X is table name
where C ? ..., ...              -- ? is some operator
group by ..., ...
having P(...) ? ..., ...
order by ..., ...
limit N
```

```SQL
select ... from X1 join X2 on X1.C1 = X2.C2 where ...
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
`<C1> like '...'`  
`<C1> not like '...'`  
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

``... ...``: one variable (string) with blanks


## PostgreSQL

`psql -h localhost`: start the command line tool  
`psql postgres -U ...`: enter the user

after entering, the command line starts with `postgres=#`, enter after this:

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

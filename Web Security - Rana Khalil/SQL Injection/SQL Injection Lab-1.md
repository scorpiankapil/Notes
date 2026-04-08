# Lab #1 - SQL injection vulnerability in WHERE clause allowing retrieval of hidden data

**LAB -** https://portswigger.net/web-security/sql-injection/lab-retrieve-hidden-data

SQL Injection - product category filter 

SELECT * FROM products WHERE category = 'gifts' AND released = 1

End goal: display all products both released and unreleased.

**Solution:-**
SELECT * FROM products WHERE category =Lifestyle ' OR 1=1-- AND released = 1

Meaning of `' OR 1=1--` in SQL Injection

1. **`'`** closes the original string value in the SQL query, allowing the attacker to inject their own SQL logic.
2. **`OR 1=1`** is an always-true condition, which makes the WHERE clause true for all records.
3. **`--`** comments out the rest of the SQL query, so any remaining conditions are ignored.
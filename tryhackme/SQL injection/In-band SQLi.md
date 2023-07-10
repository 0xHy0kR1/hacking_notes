## Introduction
- In-Band just refers to the same method of communication being used to exploit the vulnerability and also receive the results.
**Example** - 
discovering an SQL Injection vulnerability on a website page and then being able to extract data from the database to the same page.

## Types of In-band SQLi
1. Error-based SQL injection
2. Union-based SQL injection
3. Boolean-based SQL injection
4. Time-based SQL injection

### Error-based SQL Injection
- This type of SQL Injection is the most useful for easily obtaining information about the database structure as error messages from the database are printed directly to the browser screen.

### Union-Based SQL Injection
- This type of Injection utilises the SQL UNION operator alongside a SELECT statement to return additional results to the page.

### Boolean-based SQL Injection
- In boolean-based SQL injection, the attacker exploits the application's response to boolean (true/false) conditions in SQL queries.
- By injecting SQL code that evaluates to either true or false, the attacker can infer information about the database based on the application's response.

### Time-based SQL injection
- Time-based SQL injection involves injecting SQL code that causes the application to delay its response.









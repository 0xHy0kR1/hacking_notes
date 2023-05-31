## String Concatenation
- Below concatenating strings in different databases
![[SQL_injection_cheat_sheet_string_concatenation.png]]

## Substring
- Note that the offset index is 1-based.
- Each of the following expressions will return the string `ba`.
![[SQL_injection_cheat_sheet_substring.png]]

## Comments
![[SQL_injection_cheat_sheet_comments.png]]

## Database version
- You can query the database to determine its type and version.
![[SQL_injection_cheat_sheet_Database_version.png]]

## Database contents
- You can list the tables that exist in the database, and the columns that those tables contain.
![[SQL_injection_cheat_sheet_Database_contents.png]]

## Conditional errors
- You can test a single boolean condition and trigger a database error
![[SQL_injection_cheat_sheet_conditional_error.png]]

## Extracting data via visible error messages
- You can test a single boolean condition and trigger a database error.
![[SQL_injection_cheat_sheet_data_extracting_via_error_messages.png]]

## Batched (or stacked) queries
- You can use batched queries to execute multiple queries in succession.
- Note that while the subsequent queries are executed, the results are not returned to the application. Hence this technique is primarily of use in relation to blind vulnerabilities where you can use a second query to trigger a DNS lookup, conditional error, or time delay.
![[SQL_injection_cheat_sheet_batched_queries.png]]

## Time delays
- You can cause a time delay in the database when the query is processed.
- The following will cause an unconditional time delay of 10 seconds.
![[SQL_injection_cheat_sheet_time_delays.png]]

## Conditional time delays
- You can test a single boolean condition and trigger a time delay if the condition is true.
![[SQL_injection_cheat_sheet_conditional_time_delays.png]]

## DNS lookup
For Remaining two topics visit --> https://portswigger.net/web-security/sql-injection/cheat-sheet
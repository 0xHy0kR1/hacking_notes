- It's worth noting that SQL syntax is not case sensitive.

## SELECT
- SELECT query used to retrieve data from the database.

**Example** - 
```sql
select * from users;
```

```sql
select username,password from users;
```

```sql
select * from users LIMIT 1;
```

```sql
select * from users where username='admin';
```

```sql
select * from users where username != 'admin';
```

```sql
select * from users where username='admin' or username='jon';
```

```sql
select * from users where username='admin' and password='p4ssword';
```

```sql
select * from users where username like 'a%';
```

```sql
select * from users where username like '%n';
```

```sql
select * from users where username like '%mi%';
```

## UNION
- The UNION statement combines the results of two or more SELECT statements to retrieve data from either single or multiple tables.
- the rules to this query are that the UNION statement must retrieve the same number of columns in each SELECT statement.
- the columns have to be of a similar data type and the column order has to be the same.
```sql
SELECT name,address,city,postcode from customers UNION SELECT company,address,city,postcode from suppliers;
```

## INSERT
- The **INSERT** statement tells the database we wish to insert a new row of data into the table.
```sql
insert into users (username,password) values ('bob','password123');
```

## UPDATE
- The **UPDATE** statement tells the database we wish to update one or more rows of data within a table.
```sql
update users SET username='root',password='pass123' where username='admin';
```

## DELETE
- The **DELETE** statement tells the database we wish to delete one or more rows of data.
```sql
delete from users where username='martin';
```

**Note** - 

1. **The semicolon in the URL signifies the end of the SQL statement, and the two dashes cause everything afterwards to be treated as a comment**.
`SELECT * from blog where id=2;-- and private=0 LIMIT 1;`
2. there are 3 types in total In-Band, Blind and Out Of Band.
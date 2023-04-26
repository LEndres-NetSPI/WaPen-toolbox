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

PS LABS SEEMS TO HAVE ISSUES! I fired off the exact same query in the browser and am not getting a successful response, however when I use repeater, my UNION attack works just fine. Do everything inside burp.

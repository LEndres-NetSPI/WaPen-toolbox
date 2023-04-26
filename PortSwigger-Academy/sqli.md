# UNION attacks

MySQL end of query = `--` and `#`, **try both**.

**PS Lab:** `SQL injection attack, querying the database type and version on MySQL and Microsoft` rejected my accurate queries because I ended my query with `--` instead of `#`. Is this accurate of a real-world setup? I'm not sure.


### Lab: SQL injection attack, listing the database contents on non-Oracle databases
This is a non-Oracle database, so we need to make user of information_schema.tables
>Pets' union select table_name,NULL from information_schema.tables--

This returns all of the tables in the database.

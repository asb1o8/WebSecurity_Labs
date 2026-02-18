## ⛳ Database-Specific Syntax

- On Oracle, every `SELECT` query must use the `FROM` keyword and specify a valid table. There is a built-in table on
  Oracle called dual which can be used for this purpose. So the injected queries on Oracle would need to look like:

      ' UNION SELECT NULL FROM DUAL--

- The payloads described use the double-dash comment sequence `--` to comment out the remainder of the original query following the injection point. On MySQL, the double-dash sequence must be followed by a space. Alternatively, the hash character `#` can be used to identify a comment.

For more details of database-specific syntax, see the [SQL injection cheat sheet](https://portswigger.net/web-security/sql-injection/cheat-sheet).




🎋 `Deeply Explored`:-
-

- Every `SELECT` query must use the `FROM` keyword and specify a valid table.
    - `SQL` standard query works even you don't use `FROM`,  but `ORACLE` doesn't.
    - Oracle requires `FROM` in every `SELECT` query, means you've to always specify a table.
    - Oracle provides a special dummy table as `DUAL`.
    - So when attacker test `UNION SELECT NULL` on `Oracle DB`, that may fail if `FROM` clause is missing. So while writing payloads for Oracle always add `FROM DUAL`.


- Double-dash & further para.
   - In SQL -- is used for comment out.
   - Attacker use  --  to ignore the remaining part of query while injection.

         SELECT * FROM users WHERE name = 'abc' -- rest of query ignored

   - A space is necessary to make the part as comment otherwise SQL will ignore it.

         ' UNION SELECT NULL -- valid
         ' UNION SELECT NULL-- invalid (no space after --)

   - In MySQL it `#` is a comment marker. Means attacker use this to ignore the remaining query

         ' UNION SELECT NULL# rest ignored

    - To ensure the remaining part of the original query don't execute while injecting payload, then attacker  use it. When an attacker injects the payload, he ensures that the original part of the query doesn’t execute.
If remaining part of the query executed then syntax error will be occur. 

    - Attackers often need to end the legitimate query so that only their injected part runs. `-- (double dash followed by a space)` or `#` are comment symbols in SQL.

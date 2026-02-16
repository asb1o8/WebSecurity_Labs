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

   - In MySQL it # is a comment marker. Means attacker # use this to ignore the remaining query

         ' UNION SELECT NULL# rest ignored

    - To ensure the remainig part of the original query don't execute while injecting payload, then attacker use it. Jab attacker payload inject karta hai, usko ensure karna hota hai ki original query ka baaki hissa execute na ho.

Agar baaki query execute ho jaaye to syntax error aa sakta hai.

Isliye -- (with space) ya # use karke attacker query ko cleanly terminate karta hai.

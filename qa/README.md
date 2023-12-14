# Q and A

## Q: What is **"transaction"**?

A SQL transaction is a grouping of one or more SQL statements that interact with a database.

## Q: When to use index?

取決於使用者的使用情況。觀察哪種 queries 最頻繁最吃 resource ，再考慮值不值得創建索引

## Q: What is a database driver?

A database driver is a software component that enables a software application to communicate with DBMS and perform database operations. A database driver acts as an intermediary between the application and the DBMS, translating the API calls made by the application into a format that the DBMS can understand and execute.

Eg. Oracle JDBC driver for Java, pq for Golang

## What is `for share`?

`FOR SHARE` is used to lock a table for reading. It allows other transactions to read the rows but not to modify them until the current transaction is committed.

## Q: How tow avoid dead lock?

1. `FOR NO KEY UPDATE;`
    ```sql
    SELECT * FROM account
    WHERE id = $1
    LIMIT 1
    FOR NO KEY UPDATE; <!-- Not update the key or ID of the column => Not affect foreign key of other table  -->
    ```
2. update data in a consistent order (eg small ID first)
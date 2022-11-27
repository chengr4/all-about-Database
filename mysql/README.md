# MySQL

- [MySQL Workbench](./mysql-workbench/)
- [MySQL Reference Manual](./mysql-reference-manual)

---

- [Locking](#locking)
- [Architecture](#architecture)

## Architecture

![Architecture of MySQL](https://media.geeksforgeeks.org/wp-content/uploads/20210211183907/MySQLArchi.png)

- Handler: Connections, 權限管理
- Server
  - SQL Parser: 它會將你所下達的 sql 指令，依據規則，轉化成抽象語法樹(Abstract Syntax Tree，AST)
  - Optimizer: Optimize AST from Parser
  - SQL Cache: for each search, see cache before parser and optimizer
- Engine: InnoDB (> version 5.6)

> To optimize MySQL performance, usually works on **Engine** and **Optimizer**

### Handler

### Server

### Engine

Why InnoDB choose b+ tree for data storage?

-  Binary search is the chosen one for searching data (O(logn))

We need a proper data structure for "binary search"

- Array (X): Needs allocating memory in advance. Creates, Deletes data can be slow
- Linked list (X): Cannot run binary search

=> BST combines the advantage of this two

- BST (X): Some edge case needs O(n) searching time

=> Balanced BST (eg red-black tree, AVL tree)

- Balanced BST (X): Data is usually stored in driver. with Balanced BST, it may have too many I/O

=> b tree: For each node has multiple data

- b tree (X): not stable when searching, bad for range search

=> finally we get b+ tree

- b+ tree (O):
  - only leave nodes have data and other nodes store index

## Locking

當不同 transaction 操作同一行 record 時，為了保證一致性，需要對記錄加鎖

### Internal Locking Methods

locks has two levels (table, row) and two types (shared, exclusive)

- Table-level locks: 
  - When different transactions lock the table, the later one will be blocked until table lock is released
  - Pros: 佔用較少 resource, prevent dead lock
  - Cons: not good for high concurrency
- Row-level locks
  - Pros: better for high concurrency
  - Cons: dead lock, 佔用較多 resource
  
> See more at https://dev.mysql.com/doc/refman/5.7/en/internal-locking.html

Shared lock

```mysql
# before mysql 8.0
select * from user where id = 1 lock in share mode;
  
# after mysql 8.0
select * from user where id = 1 for share
```

Exclusive lock

```mysql
# 通过 for update 可以给数据行加 exclusive lock
select * from user where id = 1 for update;
  
# 通过 update 或 delet e同样也可以
update user set age = 16 where id = 1;
```

#### InnoDB Locking

```mysql
show engine innodb status;
```

- Intention Locks
- Record Locks
  ```mysql
  select * from user where id = 1 for update;
  ```
  - Only works on `index`
- Gap Locks: 可以避免幻讀
  ```mysql
  select * from user where age between 22 and 26 for update;
  ```
- Next-Key Locks: 給 index 間加鎖
- Insert Intention Locks
- AUTO-INC Locks: 當主鍵設置為 `auto_increment` 時，往表中插入數據需要先獲得 `AUTO-INC Locks` 以安全的增加 `id` 的值。

### Exernal Locking

## References

1. [Bigbyto; 理解Mysql InnoDB引擎中的锁 (2021.7)](https://wiyi.org/mysql-innodb-locking.html)

# MySQL

- [MySQL Workbench](./mysql-workbench/)
- [MySQL Reference Manual](./mysql-reference-manual)

---

- [Architecture](#architecture)
- [Isolation levels in MySQL](#isolation-levels-in-mysql)
- [Design Table](#design-table)
- [Locking](#locking)

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

## Isolation levels in MySQL

|  | Read Uncommitted | Read Commited | Repeatable Read | Serializable |
| ---------- |||||
| Dirty Read |||||
| Non-repeatable |||||
| Phantom Read |||||
| Serialization Anomaly |||||

## Design Table

1. Pick proper data type
  - Four string types: `char`, `varchar`, `text`, `blob`
  - Three date types: `datetime (YYYY-MM-DD HH:MM:SS)` (8 bytes), `timestamp` (4 bytes), `unsigned int` (4 bytes)


### `char` vs `varchar`

- `char`
  - max 255 bytes
  - fixed space: `char(4)` is 4 bytes, even if you store only 1 byte
  - `char` 需要處理空白
  - For fixed, update frequently, short
- `varchar`
  - To save `n` character needs `n+1` bytes
  - max 65535 bytes, but real max is 65532 bytes
  - if strings are big enough, it changes to `text` aotomatically
  - For dynamic, not update frequently, long

| value      | char(4) | storage required | varchar(4) | storage required |
| ---------- | ------- | ---------------- | ---------- | ---------------- |
| ''         | '    '  | 4 bytes          | ''         | 1 bytes          |
| 'ab'       | 'ab  '  | 4 bytes          | 'ab'       | 3 bytes          |
| 'abcd'     | 'abcd'  | 4 bytes          | 'abcd'     | 5 bytes          |
| 'abcdefgh' | 'abcd'  | 4 bytes          | 'abcd'     | 5 bytes          |


### `text` vs `blob`

- text: 0-65536 bytes, string
- blob: 0-65536 bytes, binary
- Had better not use both of them => they need other spaces to save data, instead of in b+ tree

```sql
-- search blob field

```

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
  
> See more: https://dev.mysql.com/doc/refman/5.7/en/internal-locking.html

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
  
# 通过 update 或 delete 同样也可以
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

## Index

 - clustered Index: Main b+ tree in MySQL
 - secondary Index: self-built b+ tree in MySQL

  > by eg `ALTER TABLE table ADD INDEX age_index(age)`

  includes:
  
  - 覆蓋索引(covering index) (default)
  - 連合索引(compound index): 兩個欄位組合在一起，建立一個索引表
  - 前綴索引(prefix index)
  - 唯一索引(unique index)

Basic steps to use secondary Index:

1. 至 secondary Index 尋找 PK
2. 再至 clustered Index 取得完整資料

## Commands

| Command | Description |
| ------- | ----------- |
|`select @@transaction_isolation`||
|`set session transaction isolation level <the level>`||

## References

1. [Bigbyto; 理解Mysql InnoDB引擎中的锁 (2021.7)](https://wiyi.org/mysql-innodb-locking.html)

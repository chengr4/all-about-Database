# All About Database

## TO READ

- https://coding.fnsne.com/posts/2022-09-14/%E8%B3%87%E6%96%99%E5%BA%AB%E7%9A%84%E5%90%8C%E6%AD%A5/?fbclid=IwAR03zwbUN7ulTrMgxGTyi9gtHKiD0bvAnBybUVtD5JCI6u1SfU300XCHc18 + google isolation level

## JOINS

- Target: combine rows from two or more tables (based on a related column between them)

### INNER JOIN

- 交集

```sql
-- eg mysql
SELECT * FROM <table_name> INNER JOIN <table_name> ON <col> = <col>
```

### LEFT JOIN

- See all left table but only see matching right table

```sql
-- eg mysql
SELECT * FROM <table_name> LEFT JOIN <table_name> ON <col> = <col>
```

### FULL OUTER JOIN

Show all matching records

## Index

- Every index has its own B+ tree
  > See [B+ tree](https://github.com/chengr4/my-data-structures/blob/main/tree/README.md#b-tree)
- 每次新增、更新資料時，都會異動到所使用的 b+ tree => 當使用的 index 越多，需要維護的 index 也越多 => 若建立太多 index ，可能會降低新增或者更新的效率
- Use `EXPLAIN` => Eg. `EXPLAIN SELECT * FROM user_no WHERE name = 'mark';`

## Union

- Columns to take from queries should be the same
- 

```sql
-- eg mysql

```


### When to Use?

- Take same cols from two tables with one single query
- MySQL automtically remove duplicate entries => so use `UNION ALL` if you need duplicates

## Q/A

Q: What is "transaction"?

A: A SQL transaction is a grouping of one or more SQL statements that interact with a database.

Q: When to use index?

A: 取決於使用者的使用情況。觀察哪種 queries 最頻繁最吃 resource ，再考慮值不值得創建索引

## Cheat Sheet

## DB Design Tool

- https://dbdiagram.io/home?fbclid=IwAR1aOLukZTXPT68SNAYa1j6zd1cNIQ8DXWzhh9kCsFG7UdnGQeo_y2ZnUyM

## References

- [MySQL Database Tutorial - 24 - UNION (2012.01)](https://youtu.be/crj8x1PevcY)

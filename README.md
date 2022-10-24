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

## Cheat Sheet

## DB Design Tool

- https://dbdiagram.io/home?fbclid=IwAR1aOLukZTXPT68SNAYa1j6zd1cNIQ8DXWzhh9kCsFG7UdnGQeo_y2ZnUyM

## References

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

## Cheat Sheet

## DB Design Tool

- https://dbdiagram.io/home?fbclid=IwAR1aOLukZTXPT68SNAYa1j6zd1cNIQ8DXWzhh9kCsFG7UdnGQeo_y2ZnUyM

## References

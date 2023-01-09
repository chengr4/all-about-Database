# MySQL Reference Manual

- [Pattern Matching](#pattern-matching)
- [Index](./index/)
- [Functions and Operators](#functions-and-operators)

## Pattern Matching

> 3.3.4.7

> **Warning**   
> Do not use `=`, `<` or `>` when you use SQL patterns.

- `SELECT * FROM pet WHERE name LIKE 'b%';`: To find names **beginning with b**
- `SELECT * FROM pet WHERE name LIKE '%fy';`: To find names **ending with fy**
- `SELECT * FROM pet WHERE name LIKE '%w%';`: To find names **containing a w**
- `SELECT * FROM pet WHERE name LIKE '_____';`: To find names containing exactly five characters, use five instances of the `_` pattern character
- `SELECT * FROM pet WHERE REGEXP_LIKE(name, '^b');`: To find names beginning with b

Case-sensitive matching:

```mysql
SELECT * FROM pet WHERE REGEXP_LIKE(name, '^b' COLLATE utf8mb4_0900_as_cs);
SELECT * FROM pet WHERE REGEXP_LIKE(name, BINARY '^b');
SELECT * FROM pet WHERE REGEXP_LIKE(name, '^b', 'c');
```

## Functions and Operators

GOTO [Functions and Operators](./functions-and-operators/)

- JSON Functions
  - `JSON_EXTRACT(json_doc, path[, path] ...)`
  - `JSON_UNQUOTE(json_val)`

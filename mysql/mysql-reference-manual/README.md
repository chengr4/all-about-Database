# MySQL Reference Manual

- [Pattern Matching](#pattern-matching)
- [Index](./index/)
- [Functions and Operators](./functions-and-operators/)

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

## JSON Functions

### Functions That Search JSON Values

`JSON_EXTRACT(json_doc, path[, path] ...)`

```
mysql> SELECT JSON_EXTRACT('[10, 20, [30, 40]]', '$[1]');
+--------------------------------------------+
| JSON_EXTRACT('[10, 20, [30, 40]]', '$[1]') |
+--------------------------------------------+
| 20                                         |
+--------------------------------------------+
mysql> SELECT JSON_EXTRACT('[10, 20, [30, 40]]', '$[1]', '$[0]');
+----------------------------------------------------+
| JSON_EXTRACT('[10, 20, [30, 40]]', '$[1]', '$[0]') |
+----------------------------------------------------+
| [20, 10]                                           |
+----------------------------------------------------+
mysql> SELECT JSON_EXTRACT('[10, 20, [30, 40]]', '$[2][*]');
+-----------------------------------------------+
| JSON_EXTRACT('[10, 20, [30, 40]]', '$[2][*]') |
+-----------------------------------------------+
| [30, 40]                                      |
+-----------------------------------------------+
```

or

```
// CONTENT is a column and has json object
mysql> SELECT JSON_EXTRACT(CONTENT, '$.document.id');
```

### Functions That Modify JSON Values

`JSON_UNQUOTE(json_val)`

- return `utf8mb4` string or NULL (if arg is NULL)

```
mysql> SET @j = '"abc"';
mysql> SELECT @j, JSON_UNQUOTE(@j);
+-------+------------------+
| @j    | JSON_UNQUOTE(@j) |
+-------+------------------+
| "abc" | abc              |
+-------+------------------+
```

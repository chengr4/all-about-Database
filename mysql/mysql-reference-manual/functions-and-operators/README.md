# Functions and Operators

> Chapter 12

- [Full-Text Search Functions](#full-text-search-functions)
- [JSON Functions](#json-functions)

## String Functions and Operators

> 12.8



## Full-Text Search Functions

> 12.10

- IN NATURAL LANGUAGE MODE: ignore capital

## JSON Functions

> 12.18

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

# MySQL Reference Manual

- [JSON Functions](#json-functions)

## JSON Functions

### Functions That Modify JSON Values

`JSON_UNQUOTE(json_val)`

- return `utf8mb4` string or NULL (if arg is NULL)

eg

```
mysql> SET @j = '"abc"';
mysql> SELECT @j, JSON_UNQUOTE(@j);
+-------+------------------+
| @j    | JSON_UNQUOTE(@j) |
+-------+------------------+
| "abc" | abc              |
+-------+------------------+
```

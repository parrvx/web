The [`LIMIT`](https://www.postgresql.org/docs/18/sql-select.html#SQL-LIMIT) will reduce the number of [row](https://en.wikipedia.org/wiki/Row_(database))s to return, and the optional [`OFFSET`](https://www.postgresql.org/docs/18/sql-select.html#SQL-LIMIT) will specify where to begin counting the number [row](https://en.wikipedia.org/wiki/Row_(database))s from.

```{sql}
SELECT column, another_column, …
FROM mytable
WHERE condition(s)
ORDER BY column ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

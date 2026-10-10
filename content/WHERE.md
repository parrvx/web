A way to discard [row](https://en.wikipedia.org/wiki/Row_(database))s that have a duplicate [column](https://en.wikipedia.org/wiki/Column_(database)) value by using the [`DISTINCT`](https://www.postgresql.org/docs/18/sql-select.html#SQL-DISTINCT) keyword.

```{sql}
SELECT DISTINCT column, another_column, …
FROM mytable
WHERE condition(s);
```

The [`DISTINCT`](https://www.postgresql.org/docs/18/sql-select.html#SQL-DISTINCT) will blindly remove duplicate [row](https://en.wikipedia.org/wiki/Row_(database))s, so to discard duplicates based on specific [column](https://en.wikipedia.org/wiki/Column_(database))s using grouping and the [`GROUP BY`](https://www.postgresql.org/docs/18/sql-select.html#SQL-GROUPBY) clause.

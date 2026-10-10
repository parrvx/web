To sort your results by a given [column](https://en.wikipedia.org/wiki/Column_(database)) in ascending or descending order using the [`ORDER BY`](https://www.postgresql.org/docs/18/sql-select.html#SQL-ORDERBY) clause.

```{sql}
SELECT column, another_column, …
FROM mytable
WHERE condition(s)
ORDER BY column ASC/DESC;
```

Each [row](https://en.wikipedia.org/wiki/Row_(database)) is sorted alpha-numerically based on the specified [column](https://en.wikipedia.org/wiki/Column_(database))'s value. In some databases, you can also specify a collation to better sort data containing international text.

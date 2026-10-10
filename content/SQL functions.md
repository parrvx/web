## Aggregate functions

| Function    | Description |
| ---         | ---         |
| `COUNT(*)`, `COUNT(column)` |  	A common function used to counts the number of [row](https://en.wikipedia.org/wiki/Row_(database))s in the group if no [column](https://en.wikipedia.org/wiki/Column_(database)) name is specified. Otherwise, count the number of [row](https://en.wikipedia.org/wiki/Row_(database))s in the group with non-NULL values in the specified column. |
| `MIN(column)` | 	Finds the smallest numerical value in the specified [column](https://en.wikipedia.org/wiki/Column_(database)) for all [row](https://en.wikipedia.org/wiki/Row_(database))s in the group. |
| `MAX(column)` | 	Finds the largest numerical value in the specified [column](https://en.wikipedia.org/wiki/Column_(database)) for all [row](https://en.wikipedia.org/wiki/Row_(database))s in the group. |
| `AVG(column)` | 	Finds the average numerical value in the specified [column](https://en.wikipedia.org/wiki/Column_(database)) for all [row](https://en.wikipedia.org/wiki/Row_(database))s in the group. |
| `SUM(column)` | 	Finds the sum of all numerical values in the specified [column](https://en.wikipedia.org/wiki/Column_(database)) for the [row](https://en.wikipedia.org/wiki/Row_(database))s in the group. |

Docs: [MySQL](https://dev.mysql.com/doc/refman/9.7/en/aggregate-functions.html), [Postgres](https://www.postgresql.org/docs/18/functions-aggregate.html), [SQLite](https://www.sqlite.org/lang_aggfunc.html), [Microsoft SQL Server](https://msdn.microsoft.com/en-us/library/ms173454.aspx)

## Grouped aggregate functions

It is possible to apply the aggregate functions to individual groups of data within that group (ie. box office sales for Comedies vs Action movies).

```{sql}
SELECT AGG_FUNC(column_or_expression) AS aggregate_description, …
FROM mytable
WHERE constraint_expression
GROUP BY column;
```

The [`GROUP BY`](https://www.postgresql.org/docs/18/sql-select.html#SQL-GROUPBY) clause works by grouping [row](https://en.wikipedia.org/wiki/Row_(database))s that have the same value in the [column](https://en.wikipedia.org/wiki/Column_(database)) specified.

> [!attention] Attention
> The [`GROUP BY`](https://www.postgresql.org/docs/18/sql-select.html#SQL-GROUPBY) clause is executed after the [`WHERE`](https://www.postgresql.org/docs/18/sql-select.html#SQL-WHERE) clause (which filters the [row](https://en.wikipedia.org/wiki/Row_(database))s which are to be grouped).

To filter the grouped [row](https://en.wikipedia.org/wiki/Row_(database))s just add an additional [`HAVING`](https://www.postgresql.org/docs/18/sql-select.html#SQL-HAVING) clause which is used specifically with the [`GROUP BY`](https://www.postgresql.org/docs/18/sql-select.html#SQL-GROUPBY) clause to allow us to filter grouped [row](https://en.wikipedia.org/wiki/Row_(database))s from the result set.

```{sql}
SELECT group_by_column, AGG_FUNC(column_expression) AS aggregate_result_alias, …
FROM mytable
WHERE condition
GROUP BY column
HAVING group_condition;
```

The [`HAVING`](https://www.postgresql.org/docs/18/sql-select.html#SQL-HAVING) clause constraints are written the same way as the [`WHERE`](https://www.postgresql.org/docs/18/sql-select.html#SQL-WHERE) clause constraints, and are applied to the grouped [row](https://en.wikipedia.org/wiki/Row_(database))s.


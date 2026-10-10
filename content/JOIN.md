Using the [`JOIN`](https://www.postgresql.org/docs/18/sql-select.html#SQL-FROM) clause in a query, we can combine [row](https://en.wikipedia.org/wiki/Row_(database)) data across two separate [table](https://en.wikipedia.org/wiki/Table_(database))s using this unique key.

# `INNER JOIN`

```{sql}
SELECT column, another_table_column, …
FROM mytable
INNER JOIN another_table 
    ON mytable.id = another_table.id
WHERE condition(s)
ORDER BY column, … ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

The [`INNER JOIN`](https://www.postgresql.org/docs/18/sql-select.html#SQL-FROM) is a process that matches [row](https://en.wikipedia.org/wiki/Row_(database))s from the first [table](https://en.wikipedia.org/wiki/Table_(database)) and the second [table](https://en.wikipedia.org/wiki/Table_(database)) which have the same key (as defined by the ON constraint) to create a result [row](https://en.wikipedia.org/wiki/Row_(database)) with the combined [column](https://en.wikipedia.org/wiki/Column_(database))s from both [table](https://en.wikipedia.org/wiki/Table_(database))s. After the [table](https://en.wikipedia.org/wiki/Table_(database))s are joined, the other clauses we learned previously are then applied.

> [!info] Info
> [`INNER JOIN`](https://www.postgresql.org/docs/18/sql-select.html#SQL-FROM) can be written simply as a [`JOIN`](https://www.postgresql.org/docs/18/sql-select.html#SQL-FROM). These two are equivalent.

# `OUTER JOIN`

If the two [table](https://en.wikipedia.org/wiki/Table_(database))s have asymmetric data, then we would have to use a LEFT JOIN, RIGHT JOIN or [`FULL JOIN`](https://www.postgresql.org/docs/18/sql-select.html#SQL-FROM) instead to ensure that the data you need is not left out of the results.

```{sql}
SELECT column, another_column, …
FROM mytable
INNER/LEFT/RIGHT/FULL JOIN another_table 
    ON mytable.id = another_table.matching_id
WHERE condition(s)
ORDER BY column, … ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

These three new joins have to specify which [column](https://en.wikipedia.org/wiki/Column_(database)) to join the data on.

When joining [table](https://en.wikipedia.org/wiki/Table_(database)) A to [table](https://en.wikipedia.org/wiki/Table_(database)) B, a [`LEFT JOIN`](https://www.postgresql.org/docs/18/sql-select.html#SQL-FROM) simply includes [row](https://en.wikipedia.org/wiki/Row_(database))s from A regardless of whether a matching [row](https://en.wikipedia.org/wiki/Row_(database)) is found in B. The [`RIGHT JOIN`](https://www.postgresql.org/docs/18/sql-select.html#SQL-FROM) is the same, but reversed, keeping [row](https://en.wikipedia.org/wiki/Row_(database))s in B regardless of whether a match is found in A. Finally, a [`FULL JOIN`](https://www.postgresql.org/docs/18/sql-select.html#SQL-FROM) simply means that [row](https://en.wikipedia.org/wiki/Row_(database))s from both [table](https://en.wikipedia.org/wiki/Table_(database))s are kept, regardless of whether a matching [row](https://en.wikipedia.org/wiki/Row_(database)) exists in the other [table](https://en.wikipedia.org/wiki/Table_(database)).

Likely we'll have to write additional logic to deal with [NULL](https://en.wikipedia.org/wiki/Null_(SQL))s in the result and constraints.

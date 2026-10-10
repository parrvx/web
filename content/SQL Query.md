
# [[SELECT]]
# [[JOIN]]
# [[WHERE]]
# [[ORDER BY]]
# [[LIMIT]]
# [[NULLs]]

# Order of execution of a Query

Complete [`SELECT`](https://www.postgresql.org/docs/18/sql-select.html) query

```{sql}
SELECT DISTINCT column, AGG_FUNC(column_or_expression), …
FROM mytable
    JOIN another_table
      ON mytable.column = another_table.column
    WHERE constraint_expression
    GROUP BY column
    HAVING constraint_expression
    ORDER BY column ASC/DESC
    LIMIT count OFFSET COUNT;
```

Each query begins with *finding the data* that we need in a database, and then *filtering that data* down into something that can be processed and understood as quickly as possible. 

## Query order of execution

1. [`FROM`](https://www.postgresql.org/docs/18/sql-select.html#SQL-FROM) and [`JOIN`](https://www.postgresql.org/docs/18/sql-select.html#SQL-FROM)s

The [`FROM`](https://www.postgresql.org/docs/18/sql-select.html#SQL-FROM) clause, and subsequent [`JOIN`](https://www.postgresql.org/docs/18/sql-select.html#SQL-FROM)s are first executed to determine the total working set of data that is being queried. This includes subqueries in this clause, and can cause temporary [table](https://en.wikipedia.org/wiki/Table_(database))s to be created under the hood containing all the [column](https://en.wikipedia.org/wiki/Column_(database))s and [row](https://en.wikipedia.org/wiki/Row_(database))s of the [table](https://en.wikipedia.org/wiki/Table_(database))s being joined.

2. [`WHERE`](https://www.postgresql.org/docs/18/sql-select.html#SQL-WHERE)

Once we have the total working set of data, the first-pass [`WHERE`](https://www.postgresql.org/docs/18/sql-select.html#SQL-WHERE) constraints are applied to the individual [row](https://en.wikipedia.org/wiki/Row_(database))s, and [row](https://en.wikipedia.org/wiki/Row_(database))s that do not satisfy the constraint are discarded. Each of the constraints can only access columns directly from the [table](https://en.wikipedia.org/wiki/Table_(database))s requested in the [`FROM`](https://www.postgresql.org/docs/18/sql-select.html#SQL-FROM) clause. Aliases in the [`SELECT`](https://www.postgresql.org/docs/18/sql-select.html) part of the query are not accessible in most databases since they may include expressions dependent on parts of the query that have not yet executed.

3. [`GROUP BY`](https://www.postgresql.org/docs/18/sql-select.html#SQL-GROUPBY)

The remaining [row](https://en.wikipedia.org/wiki/Row_(database))s after the [`WHERE`](https://www.postgresql.org/docs/18/sql-select.html#SQL-WHERE) constraints are applied are then grouped based on common values in the [column](https://en.wikipedia.org/wiki/Column_(database)) specified in the [`GROUP BY`](https://www.postgresql.org/docs/18/sql-select.html#SQL-GROUPBY) clause. As a result of the grouping, there will only be as many [row](https://en.wikipedia.org/wiki/Row_(database))s as there are unique values in that [column](https://en.wikipedia.org/wiki/Column_(database)). Implicitly, this means that you should only need to use this when you have aggregate functions in your query.

4. [`HAVING`](https://www.postgresql.org/docs/18/sql-select.html#SQL-HAVING)

If the query has a [`GROUP BY`](https://www.postgresql.org/docs/18/sql-select.html#SQL-GROUPBY) clause, then the constraints in the [`HAVING`](https://www.postgresql.org/docs/18/sql-select.html#SQL-HAVING) clause are then applied to the grouped [row](https://en.wikipedia.org/wiki/Row_(database))s, discard the grouped [row](https://en.wikipedia.org/wiki/Row_(database))s that don't satisfy the constraint. Like the [`WHERE`](https://www.postgresql.org/docs/18/sql-select.html#SQL-WHERE) clause, aliases are also not accessible from this step in most databases.

5. [`SELECT`](https://www.postgresql.org/docs/18/sql-select.html)

Any expressions in the [`SELECT`](https://www.postgresql.org/docs/18/sql-select.html) part of the query are finally computed.

6. [`DISTINCT`](https://www.postgresql.org/docs/18/sql-select.html#SQL-DISTINCT)

Of the remaining [row](https://en.wikipedia.org/wiki/Row_(database))s, [row](https://en.wikipedia.org/wiki/Row_(database))s with duplicate values in the [column](https://en.wikipedia.org/wiki/Column_(database)) marked as [`DISTINCT`](https://www.postgresql.org/docs/18/sql-select.html#SQL-DISTINCT) will be discarded.

7. [`ORDER BY`](https://www.postgresql.org/docs/18/sql-select.html#SQL-ORDERBY)

If an order is specified by the [`ORDER BY`](https://www.postgresql.org/docs/18/sql-select.html#SQL-ORDERBY) clause, the [row](https://en.wikipedia.org/wiki/Row_(database))s are then sorted by the specified data in either ascending or descending order. Since all the expressions in the [`SELECT`](https://www.postgresql.org/docs/18/sql-select.html) part of the query have been computed, you can reference aliases in this clause.
8. [`LIMIT`](https://www.postgresql.org/docs/18/sql-select.html#SQL-LIMIT) / [`OFFSET`](https://www.postgresql.org/docs/18/sql-select.html#SQL-LIMIT)

Finally, the [row](https://en.wikipedia.org/wiki/Row_(database))s that fall outside the range specified by the [`LIMIT`](https://www.postgresql.org/docs/18/sql-select.html#SQL-LIMIT) and [`OFFSET`](https://www.postgresql.org/docs/18/sql-select.html#SQL-LIMIT) are discarded, leaving the final set of [row](https://en.wikipedia.org/wiki/Row_(database))s to be returned from the query.
Conclusion

Not every query needs to have all the parts we listed above, but a part of why SQL is so flexible is that it allows developers and data analysts to quickly manipulate data without having to write additional code, all just by using the above clauses.


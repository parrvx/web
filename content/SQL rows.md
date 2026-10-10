
## What is a Schema?

Schema is what describes the structure of each [table](https://en.wikipedia.org/wiki/Table_(database)), and the datatypes that each [column](https://en.wikipedia.org/wiki/Column_(database)) of the [table](https://en.wikipedia.org/wiki/Table_(database)) can contain.

A fixed structure is what allows a database to be efficient, and consistent despite storing millions or even billions of [row](https://en.wikipedia.org/wiki/Row_(database))s.

## Inserting new data

We use an [`INSERT`](https://www.postgresql.org/docs/18/sql-insert.html) statement, which declares which [table](https://en.wikipedia.org/wiki/Table_(database)) to write into, the [column](https://en.wikipedia.org/wiki/Column_(database))s of data that we are filling, and one or more [row](https://en.wikipedia.org/wiki/Row_(database))s of data to insert. In general, each [row](https://en.wikipedia.org/wiki/Row_(database)) of data you insert should contain values for every corresponding [column](https://en.wikipedia.org/wiki/Column_(database)) in the [table](https://en.wikipedia.org/wiki/Table_(database)). You can insert multiple [row](https://en.wikipedia.org/wiki/Row_(database))s at a time by just listing them sequentially.

```{sql}
INSERT INTO mytable
VALUES (value_or_expr, another_value_or_expr, …),
       (value_or_expr_2, another_value_or_expr_2, …),
       …;
```

In some cases, if you have incomplete data and the [table](https://en.wikipedia.org/wiki/Table_(database)) contains [column](https://en.wikipedia.org/wiki/Column_(database))s that support default values, you can insert [row](https://en.wikipedia.org/wiki/Row_(database))s with only the [column](https://en.wikipedia.org/wiki/Column_(database))s of data you have by specifying them explicitly.

```{sql}
INSERT INTO mytable
(column, another_column, …)
VALUES (value_or_expr, another_value_or_expr, …),
      (value_or_expr_2, another_value_or_expr_2, …),
      …;
```

In these cases, the number of values need to match the number of [column](https://en.wikipedia.org/wiki/Column_(database))s specified. Despite this being a more verbose statement to write, inserting values this way has the benefit of being forward compatible. For example, if you add a new [column](https://en.wikipedia.org/wiki/Column_(database)) to the [table](https://en.wikipedia.org/wiki/Table_(database)) with a default value, no hardcoded INSERT statements will have to change as a result to accommodate that change.

In addition, you can use mathematical and string expressions with the values that you are inserting.

This can be useful to ensure that all data inserted is formatted a certain way.
Example Insert statement with expressions

```{sql}
INSERT INTO boxoffice
(movie_id, rating, sales_in_millions)
VALUES (1, 9.9, 283742034 / 1000000);
```

## Updating rows

To update existing data, which can be done using an [`UPDATE`](https://www.postgresql.org/docs/18/sql-update.html) statement. Similar to the [`INSERT`](https://www.postgresql.org/docs/18/sql-insert.html) statement, you have to specify exactly which [table](https://en.wikipedia.org/wiki/Table_(database)), [column](https://en.wikipedia.org/wiki/Column_(database))s, and [row](https://en.wikipedia.org/wiki/Row_(database))s to update. In addition, the data you are updating has to match the data type of the [column](https://en.wikipedia.org/wiki/Column_(database))s in the [table](https://en.wikipedia.org/wiki/Table_(database)) [schema](https://www.postgresql.org/docs/18/ddl-schemas.html).

```{sql}
UPDATE mytable
SET column = value_or_expr, 
    other_column = another_value_or_expr, 
    …
WHERE condition;
```

> [!attention] Attention
> When writting the `SET`, each [column](https://en.wikipedia.org/wiki/Column_(database)) is separated by `,` comma.

The statement works by taking multiple [column](https://en.wikipedia.org/wiki/Column_(database))/value pairs, and applying those changes to each and every [row](https://en.wikipedia.org/wiki/Row_(database)) that satisfies the constraint in the [`WHERE`](https://www.postgresql.org/docs/18/sql-select.html#SQL-WHERE) clause.

> [!caution] Taking care
> Updating the wrong set of [row](https://en.wikipedia.org/wiki/Row_(database))s in a production database, or accidentally leaving out the [`WHERE`](https://www.postgresql.org/docs/18/sql-select.html#SQL-WHERE) clause (which causes the update to apply to all [row](https://en.wikipedia.org/wiki/Row_(database))s), you need to be extra careful when constructing [`UPDATE`](https://www.postgresql.org/docs/18/sql-update.html) statements. So, always write the constraint first and test it in a [`SELECT`](https://www.postgresql.org/docs/18/sql-select.html) query to make sure you are updating the right [row](https://en.wikipedia.org/wiki/Row_(database))s, and only then writing the [column](https://en.wikipedia.org/wiki/Column_(database))/value pairs to update.

## Deleting rows

To delete data from a [table](https://en.wikipedia.org/wiki/Table_(database)),it's used the [`DELETE`](https://www.postgresql.org/docs/18/sql-delete.html) statement, which describes the [table](https://en.wikipedia.org/wiki/Table_(database)) to act on, and the [row](https://en.wikipedia.org/wiki/Row_(database))s of the [table](https://en.wikipedia.org/wiki/Table_(database)) to delete through the [`WHERE`](https://www.postgresql.org/docs/18/sql-select.html#SQL-WHERE) clause.

```{sql}
DELETE FROM mytable
WHERE condition;
```

If you decide to leave out the [`WHERE`](https://www.postgresql.org/docs/18/sql-select.html#SQL-WHERE) constraint, then all [row](https://en.wikipedia.org/wiki/Row_(database))s are removed, which is a quick and easy way to clear out a [table](https://en.wikipedia.org/wiki/Table_(database)) completely (if intentional).
> [!attention] Taking extra care
> Like the [`UPDATE`](https://www.postgresql.org/docs/18/sql-update.html) statement from last lesson, it's recommended that you run the constraint in a [`SELECT`](https://www.postgresql.org/docs/18/sql-select.html) query first to ensure that you are removing the right [row](https://en.wikipedia.org/wiki/Row_(database))s. Without a proper backup or test database, it is downright easy to irrevocably remove data, so always read your [`DELETE`](https://www.postgresql.org/docs/18/sql-delete.html) statements twice and execute once.


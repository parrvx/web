# Introduction to SQL[^1]

[^1]: [SQLBolt](https://sqlbolt.com/) - Course and Practice

## What is SQL?

[SQL](https://en.wikipedia.org/wiki/SQL)(**S**tructured **Q**uery **L**anguage), is a language designed to query, manipulate, and transform data from a [Relational Database](https://en.wikipedia.org/wiki/Relational_database). 

## Relational databases

A [Relational Database](https://en.wikipedia.org/wiki/Relational_database) represents a collection of related (two-dimensional) [table](https://en.wikipedia.org/wiki/Table_(database)). Each of the [table](https://en.wikipedia.org/wiki/Table_(database)) are similar to an Excel spreadsheet, with a fixed number of named [column](https://en.wikipedia.org/wiki/Column_(database))s (the attributes or properties of the [table](https://en.wikipedia.org/wiki/Table_(database))) and any number of [row](https://en.wikipedia.org/wiki/Row_(database))s of data.

For example, if the Department of Motor Vehicles had a database, you might find a [table](https://en.wikipedia.org/wiki/Table_(database)) containing all the known vehicles that people in the state are driving. This [table](https://en.wikipedia.org/wiki/Table_(database)) might need to store the model name, type, number of wheels, and number of doors of each vehicle for example.

Table: Vehicles

| Id  | Make/Model        | # Wheels | # Doors | Type       |
| --- |	---               | ---      | ---     | ---        |
| 1   |	Ford Focus        |	 4       | 	4      | Sedan      |
| 2   |	Tesla Roadster    |	 4       | 	2      | Sports     |
| 3   |	Kawakasi Ninja    |	 2       | 	0      | Motorcycle |
| 4   |	McLaren Formula 1 |  4       | 	0      | Race       |
| 5   |	Tesla S           |	 4       | 	4      | Sedan      |

# SELECT queries

[`SELECT`](https://www.postgresql.org/docs/18/sql-select.html) statements, colloquially refered to as "queries", is a statement which declares what data we are looking for and where to find it in the database [`FROM`](https://www.postgresql.org/docs/18/sql-select.html#SQL-FROM).

Think of a [table](https://en.wikipedia.org/wiki/Table_(database)) in [SQL](https://en.wikipedia.org/wiki/SQL) as a type of an entity (ie. Dogs), and each [row](https://en.wikipedia.org/wiki/Row_(database)) as a specific instance of that type (ie. A pug, a beagle, etc). This means that the [column](https://en.wikipedia.org/wiki/Column_(database)) represents the common properties shared by all instances of that entity (ie. Color of fur, length of tail, etc).

And given a [table](https://en.wikipedia.org/wiki/Table_(database)) of [data](https://en.wikipedia.org/wiki/Data), the most basic query we could write would be one that selects for a couple [column](https://en.wikipedia.org/wiki/Column_(database)) (properties) of the [table](https://en.wikipedia.org/wiki/Table_(database)) with all the [row](https://en.wikipedia.org/wiki/Row_(database))s (instances).

```{sql}
SELECT column, another_column, …
FROM mytable;
```

The result of this query will be a two-dimensional set of [row](https://en.wikipedia.org/wiki/Row_(database))s and [column](https://en.wikipedia.org/wiki/Column_(database))s, but only with the [column](https://en.wikipedia.org/wiki/Column_(database))s that we requested.

To retrieve all the [column](https://en.wikipedia.org/wiki/Column_(database))s of [data](https://en.wikipedia.org/wiki/Data) from a [table](https://en.wikipedia.org/wiki/Table_(database)), we can then use the asterisk (`*`) shorthand in place of listing all the [column](https://en.wikipedia.org/wiki/Column_(database)) names individually.

```{sql}
SELECT * 
FROM mytable;
```

# Queries with constraints

In order to filter certain results from being returned, we need to use a [`WHERE`](https://www.postgresql.org/docs/18/sql-select.html#SQL-WHERE) clause in the query. The clause is applied to each [row](https://en.wikipedia.org/wiki/Row_(database)) of data by checking specific [column](https://en.wikipedia.org/wiki/Column_(database)) values to determine whether it should be included in the results or not.

```{sql}
SELECT column, another_column, …
FROM mytable
WHERE condition
    AND/OR another_condition
    AND/OR …;
```

More complex clauses can be constructed by joining numerous [`AND`](https://www.postgresql.org/docs/18/functions-logical.html) or [`OR`](https://www.postgresql.org/docs/18/functions-logical.html) logical keywords. 

**[Comparison Operators](https://www.postgresql.org/docs/18/functions-comparison.html)**

| Operator            | Condition                                            | SQL Example                   |
| ---                 | ---                                                  | ---                           |
| `=`, `!=`, `<`, `<=`, `>`, `>=` | Standard numerical operators                         | col_name != 4                 |
| `BETWEEN …` `AND …`     | Number is within range of two values (inclusive)     | col_name BETWEEN 1.5 AND 10.5 |
| `NOT BETWEEN …` `AND …` | Number is not within range of two values (inclusive) | col_name NOT BETWEEN 1 AND 10 |
| `IN (…)`              | Number exists in a list                              | col_name IN (2, 4, 6)         |
| `NOT IN (…)`          | Number does not exist in a list                      | col_name NOT IN (1, 3, 5)     |

Using [`WHERE`](https://www.postgresql.org/docs/18/sql-select.html#SQL-WHERE) clause with [column](https://en.wikipedia.org/wiki/Column_(database))s containing text data, the operators can do  case-insensitive string comparison and wildcard pattern matching.

**[Comparison Operators with string](https://www.postgresql.org/docs/18/functions-matching.html)**

| Operator   | Condition                                                       | Example                         |
| ---        | ---                                                             | ---                             |
| `=`          | Case sensitive exact string comparison                          | `col_name = "abc"`                |
| `!=` or `<>`   | Case sensitive exact string inequality comparison               | `col_name != "abcd"`              |
| [`LIKE`](https://www.postgresql.org/docs/18/functions-matching.html#FUNCTIONS-LIKE)       | Case insensitive exact string comparison                        | `col_name LIKE "ABC"`             |
| [`NOT LIKE`](https://www.postgresql.org/docs/18/functions-matching.html#FUNCTIONS-LIKE)   | Case insensitive exact string inequality comparison             | `col_name NOT LIKE "ABCD"`        |
| `%`          | Used in a string to match a sequence of zero or more characters | `col_name LIKE "%AT%"`            |
| `_`          | Used anywhere in a string to match a single character           | `col_name LIKE "AN_"`             |
| `IN (…)`     | String exists in a list                                         | `col_name IN ("A", "B", "C")`     |
| `NOT IN (…)` | String does not exist in a list                                 | `col_name NOT IN ("D", "E", "F")` |



> [!attention] Attention
> All strings must be quoted so that the query parser can distinguish words in the string from SQL keywords. 

# Filtering and sorting Query results

A way to discard [row](https://en.wikipedia.org/wiki/Row_(database))s that have a duplicate [column](https://en.wikipedia.org/wiki/Column_(database)) value by using the [`DISTINCT`](https://www.postgresql.org/docs/18/sql-select.html#SQL-DISTINCT) keyword.

```{sql}
SELECT DISTINCT column, another_column, …
FROM mytable
WHERE condition(s);
```

The [`DISTINCT`](https://www.postgresql.org/docs/18/sql-select.html#SQL-DISTINCT) will blindly remove duplicate [row](https://en.wikipedia.org/wiki/Row_(database))s, so to discard duplicates based on specific [column](https://en.wikipedia.org/wiki/Column_(database))s using grouping and the [`GROUP BY`](https://www.postgresql.org/docs/18/sql-select.html#SQL-GROUPBY) clause.

## Ordering results

To sort your results by a given [column](https://en.wikipedia.org/wiki/Column_(database)) in ascending or descending order using the [`ORDER BY`](https://www.postgresql.org/docs/18/sql-select.html#SQL-ORDERBY) clause.

```{sql}
SELECT column, another_column, …
FROM mytable
WHERE condition(s)
ORDER BY column ASC/DESC;
```

Each [row](https://en.wikipedia.org/wiki/Row_(database)) is sorted alpha-numerically based on the specified [column](https://en.wikipedia.org/wiki/Column_(database))'s value. In some databases, you can also specify a collation to better sort data containing international text.

## Limiting results to a subset

The [`LIMIT`](https://www.postgresql.org/docs/18/sql-select.html#SQL-LIMIT) will reduce the number of [row](https://en.wikipedia.org/wiki/Row_(database))s to return, and the optional [`OFFSET`](https://www.postgresql.org/docs/18/sql-select.html#SQL-LIMIT) will specify where to begin counting the number [row](https://en.wikipedia.org/wiki/Row_(database))s from.

```{sql}
SELECT column, another_column, …
FROM mytable
WHERE condition(s)
ORDER BY column ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

# Multi-table queries with JOINs 

## Database normalization

[Database normalization](https://en.wikipedia.org/wiki/Database_normalization) minimizes duplicate data in any single table, and allows for data in the database to grow independently of each other. As a trade-off, queries get slightly more complex and performance issues can arise when working with many large tables. So a query must combine all that data and pull out exactly the information we need.

## Multi-table queries with JOINs

[Table](https://en.wikipedia.org/wiki/Table_(database))s that share information about a single entity need to have a [primary key](https://en.wikipedia.org/wiki/Primary_key) that identifies that entity uniquely across the [database](https://en.wikipedia.org/wiki/Database). One common primary key type is an auto-incrementing integer (because they are space efficient), but it can also be a string, hashed value, so long as it is unique.

Using the [`JOIN`](https://www.postgresql.org/docs/18/sql-select.html#SQL-FROM) clause in a query, we can combine [row](https://en.wikipedia.org/wiki/Row_(database)) data across two separate [table](https://en.wikipedia.org/wiki/Table_(database))s using this unique key.

### Select query with INNER JOIN on multiple tables

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

# OUTER JOINs

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

# NULLs

To reduce the possibility of [NULL](https://en.wikipedia.org/wiki/Null_(SQL)) values in databases is a good practice. They require special attention when constructing queries, constraints (certain functions behave differently with null values) and when processing the results.

An alternative to [NULL](https://en.wikipedia.org/wiki/Null_(SQL)) values in your database is to have data-type appropriate default values, like `0` for **numerical data**, empty strings (`""`) for **text data**, etc. But if your database needs to store incomplete data, then NULL values can be appropriate if the default values will skew later analysis (for example, when taking averages of numerical data).

```{sql}
SELECT column, another_column, …
FROM mytable
WHERE column IS/IS NOT NULL
AND/OR another_condition
AND/OR …;
```

# Queries with expressions

It is possible to use expressions to write more complex logic on [column](https://en.wikipedia.org/wiki/Column_(database)) values in a query, with use of mathematical and string functions along with basic arithmetic to transform values when the query is executed, as shown in this physics example.

```{sql}
SELECT particle_speed / 2.0 AS half_particle_speed
FROM physics_data
WHERE ABS(particle_position) * 10.0 > 500;
```

Use the expression in the [`SELECT`](https://www.postgresql.org/docs/18/sql-select.html) part of the query, that they are also given a descriptive alias using the `AS` keyword.

```{sql}
SELECT col_expression AS expr_description, …
FROM mytable;
```

```{sql}
SELECT column AS better_column_name, …
FROM a_long_widgets_table_name AS mywidgets
INNER JOIN widget_sales
  ON mywidgets.id = widget_sales.widget_id;
```

# Queries with aggregates

The aggregate expressions (or functions) allow you to summarize information about a group of [row](https://en.wikipedia.org/wiki/Row_(database))s of data.

```{sql}
SELECT AGG_FUNC(column_or_expression) AS aggregate_description, …
FROM mytable
WHERE constraint_expression;
```

Without a specified grouping, each aggregate function is going to run on the whole set of result [row](https://en.wikipedia.org/wiki/Row_(database))s and return a single value. And like normal expressions, giving your aggregate functions an alias ensures that the results will be easier to read and process.

## Common aggregate functions

| Function    | Description |
| ---         | ---         |
| COUNT(*), COUNT(column)  |  	A common function used to counts the number of [row](https://en.wikipedia.org/wiki/Row_(database))s in the group if no [column](https://en.wikipedia.org/wiki/Column_(database)) name is specified. Otherwise, count the number of [row](https://en.wikipedia.org/wiki/Row_(database))s in the group with non-NULL values in the specified column. |
| MIN(column) | 	Finds the smallest numerical value in the specified [column](https://en.wikipedia.org/wiki/Column_(database)) for all [row](https://en.wikipedia.org/wiki/Row_(database))s in the group. |
| MAX(column) | 	Finds the largest numerical value in the specified [column](https://en.wikipedia.org/wiki/Column_(database)) for all [row](https://en.wikipedia.org/wiki/Row_(database))s in the group. |
| AVG(column) | 	Finds the average numerical value in the specified [column](https://en.wikipedia.org/wiki/Column_(database)) for all [row](https://en.wikipedia.org/wiki/Row_(database))s in the group. |
| SUM(column) | 	Finds the sum of all numerical values in the specified [column](https://en.wikipedia.org/wiki/Column_(database)) for the [row](https://en.wikipedia.org/wiki/Row_(database))s in the group. |

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

# Inserting rows

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

## Creating tables

When you have new entities and relationships to store in your database, you can create a new database [table](https://en.wikipedia.org/wiki/Table_(database)) using the [`CREATE TABLE`](https://www.postgresql.org/docs/18/sql-createtable.html) statement.
Create [table](https://en.wikipedia.org/wiki/Table_(database)) statement w/ optional [table](https://en.wikipedia.org/wiki/Table_(database)) constraint and default value

```{sql}
CREATE TABLE IF NOT EXISTS mytable (
    column DataType TableConstraint DEFAULT default_value,
    another_column DataType TableConstraint DEFAULT default_value,
    …
);
```

The structure of the new [table](https://en.wikipedia.org/wiki/Table_(database)) is defined by its [table](https://en.wikipedia.org/wiki/Table_(database)) [schema](https://www.postgresql.org/docs/18/ddl-schemas.html), which defines a series of [column](https://en.wikipedia.org/wiki/Column_(database))s. Each [column](https://en.wikipedia.org/wiki/Column_(database)) has a name, the type of data allowed in that [column](https://en.wikipedia.org/wiki/Column_(database)), an optional [table](https://en.wikipedia.org/wiki/Table_(database)) constraint on values being inserted, and an optional default value.

If there already exists a [table](https://en.wikipedia.org/wiki/Table_(database)) with the same name, the SQL implementation will usually throw an error, so to suppress the error and skip creating a [table](https://en.wikipedia.org/wiki/Table_(database)) if one exists, you can use the IF NOT EXISTS clause.

### Table data types

Different databases support different data types, but the common types support numeric, string, and other miscellaneous things like dates, booleans, or even binary data.

| Data type | Description |
| --- | --- |
| [`INTEGER`](https://www.postgresql.org/docs/18/datatype-numeric.html#DATATYPE-INT), [`BOOLEAN`](https://www.postgresql.org/docs/18/datatype-boolean.html) | The integer datatypes can store whole integer values like the count of a number or an age. In some implementations, the boolean value is just represented as an integer value of just 0 or 1. |
| [`FLOAT`](https://www.postgresql.org/docs/18/datatype-numeric.html#DATATYPE-FLOAT), [`DOUBLE`](https://www.postgresql.org/docs/18/datatype-numeric.html#DATATYPE-FLOAT), [`REAL`](https://www.postgresql.org/docs/18/datatype-numeric.html#DATATYPE-FLOAT) | The floating point datatypes can store more precise numerical data like measurements or fractional values. Different types can be used depending on the floating point precision required for that value. |
| [`CHARACTER(num_chars)`](https://www.postgresql.org/docs/18/datatype-character.html), [`VARCHAR(num_chars)`](https://www.postgresql.org/docs/18/datatype-character.html), [`TEXT`](https://www.postgresql.org/docs/18/datatype-character.html) | The text based datatypes can store strings and text in all sorts of locales. The distinction between the various types generally amount to underlaying efficiency of the database when working with these [column](https://en.wikipedia.org/wiki/Column_(database))s. // Both the CHARACTER and VARCHAR (variable character) types are specified with the max number of characters that they can store (longer values may be truncated), so can be more efficient to store and query with big [table](https://en.wikipedia.org/wiki/Table_(database))s. |
| [`DATE`](https://www.postgresql.org/docs/18/datatype-datetime.html), [`DATETIME`](https://www.postgresql.org/docs/18/datatype-datetime.html) | SQL can also store date and time stamps to keep track of time series and event data. They can be tricky to work with especially when manipulating data across timezones. |
| [`BLOB`](https://www.postgresql.org/docs/18/lo.html) | Finally, SQL can store binary data in blobs right in the database. These values are often opaque to the database, so you usually have to store them with the right metadata to requery them. |

Docs: MySQL, Postgres, SQLite, Microsoft SQL Server

### Table constraints

We aren't going to dive too deep into [table](https://en.wikipedia.org/wiki/Table_(database)) constraints in this lesson, but each [column](https://en.wikipedia.org/wiki/Column_(database)) can have additional [table](https://en.wikipedia.org/wiki/Table_(database)) constraints on it which limit what values can be inserted into that [column](https://en.wikipedia.org/wiki/Column_(database)). This is not a comprehensive list, but will show a few common constraints that you might find useful.

| Constraint | Description |
| --- | --- |
| `PRIMARY KEY` | This means that the values in this [column](https://en.wikipedia.org/wiki/Column_(database)) are unique, and each value can be used to identify a single [row](https://en.wikipedia.org/wiki/Row_(database)) in this [table](https://en.wikipedia.org/wiki/Table_(database)). |
| `AUTOINCREMENT` | For integer values, this means that the value is automatically filled in and incremented with each [row](https://en.wikipedia.org/wiki/Row_(database)) insertion. Not supported in all databases. |
| `UNIQUE` | This means that the values in this [column](https://en.wikipedia.org/wiki/Column_(database)) have to be unique, so you can't insert another [row](https://en.wikipedia.org/wiki/Row_(database)) with the same value in this [column](https://en.wikipedia.org/wiki/Column_(database)) as another [row](https://en.wikipedia.org/wiki/Row_(database)) in the [table](https://en.wikipedia.org/wiki/Table_(database)). Differs from the `PRIMARY KEY` in that it doesn't have to be a key for a [row](https://en.wikipedia.org/wiki/Row_(database)) in the [table](https://en.wikipedia.org/wiki/Table_(database)). |
| `NOT NULL` | This means that the inserted value can not be `NULL`. |
| `CHECK (expression)` | This allows you to run a more complex expression to test whether the values inserted are valid. For example, you can check that values are positive, or greater than a specific size, or start with a certain prefix, etc. |
| `FOREIGN KEY` | This is a consistency check which ensures that each value in this [column](https://en.wikipedia.org/wiki/Column_(database)) corresponds to another value in a [column](https://en.wikipedia.org/wiki/Column_(database)) in another [table](https://en.wikipedia.org/wiki/Table_(database)). // For example, if there are two [table](https://en.wikipedia.org/wiki/Table_(database))s, one listing all Employees by ID, and another listing their payroll information, the `FOREIGN KEY` can ensure that every [row](https://en.wikipedia.org/wiki/Row_(database)) in the payroll [table](https://en.wikipedia.org/wiki/Table_(database)) corresponds to a valid employee in the master Employee list. |

# Maybe Later
* [[DataWithBaraa]]

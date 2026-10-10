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

[[Comparison Operators]]

> [!attention] Attention
> All strings must be quoted so that the query parser can distinguish words in the string from SQL keywords. 

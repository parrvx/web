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

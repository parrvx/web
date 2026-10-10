```
DELETE FROM table_name
WHERE <condition>
```

> [!caution] Caution
> When using the `DELETE`, **ALWAYS**, and I mean,  **ALWAYS**check for the `WHERE` clause. Without it, you will DELETE all valeus from the table, and you will not be able to recover the data.


So, a good practice is to make a query for the data you want to change. 

```{sql}
SELECT *
FROM customers
WHERE id > 5;
```

And then use the same `WHERE` clause to write the `UPDATE` command.

```{sql}
DELETE FROM customers
WHERE id > 5;
```

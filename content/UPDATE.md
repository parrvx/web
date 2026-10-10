
```
UPDATE table_name
SET column1 = value1,
    column2 = value2
WHERE <condition>
```

> [!caution] Caution
> When using the `UPDATE`, **ALWAYS** check for the `WHERE` clause. Without it, you will override all valeus from that column of the table, and you will not be able to recover the data.


So, a good practice is to make a query for the data you want to change. 

```{sql}
SELECT *
FROM customers
WHERE id = 6;
```

And then use the same `WHERE` clause to write the `UPDATE` command.

```{sql}
UPDATE customers
SET score = 0
WHERE id = 6;
```

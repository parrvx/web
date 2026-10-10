To reduce the possibility of [NULL](https://en.wikipedia.org/wiki/Null_(SQL)) values in databases is a good practice. They require special attention when constructing queries, constraints (certain functions behave differently with null values) and when processing the results.

An alternative to [NULL](https://en.wikipedia.org/wiki/Null_(SQL)) values in your database is to have data-type appropriate default values, like `0` for **numerical data**, empty strings (`""`) for **text data**, etc. But if your database needs to store incomplete data, then NULL values can be appropriate if the default values will skew later analysis (for example, when taking averages of numerical data).

```{sql}
SELECT column, another_column, …
FROM mytable
WHERE column IS/IS NOT NULL
AND/OR another_condition
AND/OR …;
```

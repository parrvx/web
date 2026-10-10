
First take a look at on both tables. We need to match the query from the source with the data necessary to the target table.

```{sql}
SELECT *
FROM customers;

SELECT *
FROM persons;
```

From the source table, select and fill the information necessary.

```{sql}
SELECT
  id,
  first_name,
  NULL,
  'Unknow,'
FROM customers;
```

After that, `ISERT INTO` the target table. It's a good practice to define the columns you are inserting, just to be sure.

```{sql}
INSERT INTO persons (id, person_name, birth_date, phone)
SELECT
  id,
  first_name,
  NULL,
  'Unknow,'
FROM customers;
```

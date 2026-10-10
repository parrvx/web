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

### Data types

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

## Altering tables

As your data changes over time, SQL provides a way for you to update your corresponding tables and database schemas by using the [`ALTER TABLE`](https://www.postgresql.org/docs/18/sql-altertable.html) statement to add, remove, or modify columns and table constraints.

### Adding columns

The syntax for adding a new column is similar to the syntax when creating new rows in the [`CREATE TABLE`](https://www.postgresql.org/docs/18/sql-altertable.html) statement. You need to specify the data type of the column along with any potential table constraints and default values to be applied to both existing and new rows. In some databases like MySQL, you can even specify where to insert the new column using the FIRST or AFTER clauses, though this is not a standard feature.

```{sql}
ALTER TABLE mytable
ADD column DataType OptionalTableConstraint 
    DEFAULT default_value;
```

### Removing columns

Dropping columns is as easy as specifying the column to drop, however, some databases (including SQLite) don't support this feature. Instead you may have to create a new table and migrate the data over.

```{sql}
ALTER TABLE mytable
DROP column_to_be_deleted;
```

### Renaming the table

If you need to rename the table itself, you can also do that using the RENAME TO clause of the statement.

```{sql}
ALTER TABLE mytable
RENAME TO new_table_name;
```

### Other changes

Each database implementation supports different methods of altering their tables, so it's always best to consult your database docs before proceeding: MySQL, Postgres, SQLite, Microsoft SQL Server.

## Dropping tables

To remove an entire table, including all of its data and metadata, you can use the [`DROP TABLE`](https://www.postgresql.org/docs/18/sql-droptable.html) statement, which differs from the [`DELETE`](https://www.postgresql.org/docs/18/sql-delete.html) statement in that it also removes the table schema from the database entirely.

```{sql}
DROP TABLE IF EXISTS mytable;
```

Like the [`CREATE TABLE`](https://www.postgresql.org/docs/18/sql-altertable.html) statement, the database may throw an error if the specified table does not exist, and to suppress that error, you can use the `IF EXISTS` clause.

In addition, if you have another table that is dependent on columns in table you are removing (for example, with a `FOREIGN KEY` dependency) then you will have to either update all dependent tables first to remove the dependent rows or to remove those tables entirely.


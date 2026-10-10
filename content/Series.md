## Import the Polars Library
- The `import` keyword loads a named construct from either a Python module or from a package.
- The `polars` library is often assigned the alias `pl`.
- The `pl` alias acts as a namespace for the constructs that are nested within Polars.

```{python}
import polars as pl
```

- Add a dot after the name, then press the Tab key to see top-level attributes and functions.
- The `__version__` attribute outputs the installed version of Polars.
- The `show_versions` function returns the versions of Polars, Python, and other dependencies alongside system info.

```{python}
pl.__version__
```
```
'1.42.1'
```

```{python}
pl.show_versions()
```
```
--------Version info---------
Polars:              1.42.1
Index type:          UInt32
Platform:            Linux-6.18.13-zen1-x86_64-with-glibc2.42
Python:              3.13.15 (main, Aug  5 2026, 12:25:43) [GCC 15.3.0]
Runtime:             rt32

----Optional dependencies----
Azure CLI            <not installed>
adbc_driver_manager  <not installed>
altair               <not installed>
azure.identity       <not installed>
boto3                <not installed>
cloudpickle          <not installed>
connectorx           <not installed>
deltalake            <not installed>
fastexcel            <not installed>
fsspec               <not installed>
gevent               <not installed>
google.auth          <not installed>
great_tables         <not installed>
matplotlib           <not installed>
numpy                <not installed>
openpyxl             <not installed>
pandas               <not installed>
polars_cloud         <not installed>
pyarrow              <not installed>
pydantic             <not installed>
pyiceberg            <not installed>
sqlalchemy           <not installed>
torch                <not installed>
xlsx2csv             <not installed>
xlsxwriter           <not installed>
```

[polars.show_versions](https://docs.pola.rs/api/python/stable/reference/api/polars.show_versions.html)

## Intro to the Series
- A [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) is a single column of homogenous data. Homogenous means of the same data type.
- A [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) is a 1-dimensional data structure.

## Create a Series
- The [`pl.Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) constructor at the top of Polars supports a variety of data inputs.
- ress Shift + Tab inside the parentheses to see documentation.
- The [`values`](https://docs.pola.rs/api/python/stable/reference/series/index.html) parameter supplies the data for the [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html).

- If we pass data directly as the first parameter, olars will assume the [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) has no name (an anti-pattern).
- The recommended pattern is to pass in a [`name`](https://docs.pola.rs/api/python/stable/reference/series/index.html) as the first parameter, then the data.

## Data Type Inference
- Polars will infer the data type of the [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) from the provided values.
- The [`dtype`](https://docs.pola.rs/api/python/stable/reference/series/index.html) parameter sets the data type of the [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) values. Use it to overwrite Polars' default type inference.
- Polars may abbreviate the data type (e.g, [`pl.Float64`](https://docs.pola.rs/api/python/stable/reference/api/polars.datatypes.Float64.html) will be `f64` and [`pl.String`](https://docs.pola.rs/api/python/stable/reference/api/polars.datatypes.String.html) will be `str`).

- [`pl.Float64`](https://docs.pola.rs/api/python/stable/reference/api/polars.datatypes.Float64.html) (64 bits/8 bytes) and [`Float32`](https://docs.pola.rs/api/python/stable/reference/api/polars.datatypes.Float32.html) (32 bits/4 bytes) are both floating-point (decimal) types.
- A `f64` offers greater precision (15-17 digits) than a `f32` (7 digits) but occupies twice the memory.
- Prioritize code simplicity and business value before optimizing for efficiency.

- Polars will throw an error if the values' data type does not match the `dtype` argument.

- Set the [`strict`](https://docs.pola.rs/api/python/stable/reference/series/index.html) parameter to `False` to coerce/cast the data types into the specified [`dtype`](https://docs.pola.rs/api/python/stable/reference/series/index.html).

## Attributes
- An **attribute** is a piece of information about an object.
- To access an attribute value, write the object, then a dot and the attribute name.
- The [`name`](https://docs.pola.rs/api/python/stable/reference/series/index.html) attribute provides the name of the [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html).
- The [`dtype`](https://docs.pola.rs/api/python/stable/reference/series/index.html) attribute provides the data type of the [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html).
- The [`shape`](https://docs.pola.rs/api/python/stable/reference/series/index.html) attribute provides a tuple with the dimensions (width x height) of a Polars data structure.

```{python}
import polars as pl
chips = pl.Series("Chips", ["Doritos", "Cheetos", "Cheez-It"])
```
```
Series: 'Chips' [str]
[
	"Doritos"
	"Cheetos"
	"Cheez-It"
]
```

```{python}
chips.name
```
```
'Chips'
```

```{python}
chips.dtype
```
```
String
```

```{python}
chips.shape
```
```
(3,)
```

### Further Reading
- https://docs.pola.rs/api/python/stable/reference/series/api/polars.Series.name.html
- https://docs.pola.rs/api/python/stable/reference/series/api/polars.Series.dtype.html
- https://docs.pola.rs/api/python/stable/reference/series/api/polars.Series.shape.html

## Missing Values

- Polars marks missing entries in a [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) with a `null` value.
- Python's `None` type represents the absence of a value.
- Polars will convert a `None` in a Python list to a `null`/missing value.

```{python}
temps = pl.Series("Temperatues", [0.0, 85.3, 87.3, None, 92.4])
temps
```
```
Series: 'Temperatues' [f64]
[
	0.0
	85.3
	87.3
	null
	92.4
]
```

- Polars supports mathematical operations on [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html).
- We can add, subtract, multiply, divide, etc every [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) value with a consistent value.
- For every mathematical operation, Polars returns a new [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) storing the new values.
- Most operations on `null` values produce `null` values.
- The `+` symbol adds a scalar value to every row value.

```{python}
temps + 5.5
```
```
Series: 'Temperatues' [f64]
[
	5.5
	90.8
	92.8
	null
	97.9
]
```

- Polars will return a `NaN` (not a number) value for invalid numeric operations.
- One example of an invalid operation is dividing 0 by 0.
- `NaN` is a different value from `null`.

```{python}
temps / 0
```
```
Series: 'Temperatues' [f64]
[
	NaN
	inf
	inf
	null
	inf
]
```

- Polars considers `NaN` to be distinctly separate from `null`.
- A `NaN` is a value of a float type (`f64`).

### Further Reading
- https://docs.pola.rs/user-guide/expressions/missing-data/#null-and-nan-values
- https://docs.pola.rs/user-guide/expressions/missing-data/#not-a-number-or-nan-values

## The alias Method

- A **method** is a function attached an object.
- A **method** is a command that we issue to an object. It asks the object to performs an action.
- Write the object, a dot, the method name, and a pair of parentheses.
- Like functions, methods can accept inputs (arguments) and produce an output (return value).
- The `alias` method returns a new [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) with a new name.

```{python}
chips = pl.Series("Chips", ["Doritos", "Cheetos", "Cheez-It"])
chips
```
```
Series: 'Chips' [str]
[
	"Doritos"
	"Cheetos"
	"Cheez-It"
]
```

Here the change didn't happened on the original variable.

```{python}
chips.alias("Snacks")
```
```
Series: 'Snacks' [str]
[
	"Doritos"
	"Cheetos"
	"Cheez-It"
]
```

- The `alias` method returns a copy of the [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html). The original [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) is unaffected.
- Reassign a method's return value to a variable to overwrite the variable's original value.
- Polars methods will usually return a new object/copy. 

To make the change to the original variable, you need reassign the variable.

```{python}
chips = chips.alias("Snacks")
chips
```
```
Series: 'Snacks' [str]
[
	"Doritos"
	"Cheetos"
	"Cheez-It"
]
```
### Further Reading
- https://docs.pola.rs/user-guide/expressions/expression-expansion/#renaming-a-single-column-with-alias
- https://docs.pola.rs/api/python/stable/reference/series/api/polars.Series.alias.html

## Import a CSV File

- The comma-separated values (CSV) format stores one record per row.
- The CSV format separates each row's values with commas.

```
name,strength,magic,speed
Zorblax,9,2,5
Mira,4,9,8
Thud,10,1,2
Eloria,3,10,7
```

| name | strength | magic | speed |
| --- | --- | --- | --- |
| Zorblax | 9 | 2 | 5 |
| Mira | 4 | 9 | 8 |
| Thud | 10 | 1 | 2 |
| Eloria | 3 | 10 | 7 |


- The `read_csv` function imports a comma-separated values (CSV) file.
- The `read_csv` function returns a `DataFrame`, a table that holds 1 or more [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html).
- Notice the `shape` output includes the number of rows and the number of columns.
- The underscores in `1_000` are for readability.

```{python}
ice_creams = pl.read_csv("ice_creams.csv")
```
```
shape: (1_000, 1)
┌─────────────────────────┐
│ ice_cream_flavor        │
│ ---                     │
│ str                     │
╞═════════════════════════╡
│ Cherry Chip Drizzle     │
│ Mango Marshmallow Magic │
│ Vanilla Sprinkle Storm  │
│ Blueberry Flake Delight │
│ Vanilla Chunk Crave     │
│ …                       │
│ Mango Fudge Rush        │
│ Honey Fudge Surprise    │
│ Cinnamon Cookie Bliss   │
│ Coconut Fudge Twist     │
│ Cinnamon Crumb Magic    │
└─────────────────────────┘
```

```{python}
type(ice_creams)
```
```
<class 'polars.dataframe.frame.DataFrame'>
```

- The `to_series` method converts a `DataFrame` column into a [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html).
- With a 1-column `DataFrame`, Polars assumes it should use the only available column.
- If a `DataFrame` has multiple columns, we have to provide the column's numeric index.
- Polars assigns the columns an index (position in line) starting at 0.

```{python}
ice_creams.to_series()
```
```
shape: (1_000,)
Series: 'ice_cream_flavor' [str]
[
	"Cherry Chip Drizzle"
	"Mango Marshmallow Magic"
	"Vanilla Sprinkle Storm"
	"Blueberry Flake Delight"
	"Vanilla Chunk Crave"
	…
	"Mango Fudge Rush"
	"Honey Fudge Surprise"
	"Cinnamon Cookie Bliss"
	"Coconut Fudge Twist"
	"Cinnamon Crumb Magic"
]
```
- Method chaining invokes a method on the return value of a previous method invocation.

```{python}
ice_creams = pl.read_csv("ice_creams.csv").to_series()
ice_creams
```
```
shape: (1_000,)
Series: 'ice_cream_flavor' [str]
[
	"Cherry Chip Drizzle"
	"Mango Marshmallow Magic"
	"Vanilla Sprinkle Storm"
	"Blueberry Flake Delight"
	"Vanilla Chunk Crave"
	…
	"Mango Fudge Rush"
	"Honey Fudge Surprise"
	"Cinnamon Cookie Bliss"
	"Coconut Fudge Twist"
	"Cinnamon Crumb Magic"
]
```

### Further Reading
- https://docs.pola.rs/user-guide/io/csv/#read-write
- https://docs.pola.rs/api/python/stable/reference/api/polars.read_csv.html

## The head and tail Methods
- The `head` method returns rows from the top/beginning of the [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html).

```{python}
ice_creams.head()
```
```
shape: (10,)
Series: 'ice_cream_flavor' [str]
[
	"Cherry Chip Drizzle"
	"Mango Marshmallow Magic"
	"Vanilla Sprinkle Storm"
	"Blueberry Flake Delight"
	"Vanilla Chunk Crave"
	"Pistachio Butter Crave"
	"Espresso Brownie Rush"
	"Peach Flake Storm"
	"Coconut Flake Delight"
	"Vanilla Bits Delight"
]
```

- The `tail` method returns rows from the bottom/end of the [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html).

```{python}
ice_creams.tail()
```
```
shape: (10,)
Series: 'ice_cream_flavor' [str]
[
	"Strawberry Toffee Fantasy"
	"Apple Chunk Magic"
	"Vanilla Swirl Delight"
	"Chocolate Graham Blizzard"
	"Honey Caramel Delight"
	"Mango Fudge Rush"
	"Honey Fudge Surprise"
	"Cinnamon Cookie Bliss"
	"Coconut Fudge Twist"
	"Cinnamon Crumb Magic"
]

```

- By default, both methods return 10 rows. You can pass in a custom number of rows to return.


- The `limit` method is an alias for the `head` method.

```{python}
ice_creams.limit(10)
```
```
shape: (10,)
Series: 'ice_cream_flavor' [str]
[
	"Cherry Chip Drizzle"
	"Mango Marshmallow Magic"
	"Vanilla Sprinkle Storm"
	"Blueberry Flake Delight"
	"Vanilla Chunk Crave"
	"Pistachio Butter Crave"
	"Espresso Brownie Rush"
	"Peach Flake Storm"
	"Coconut Flake Delight"
	"Vanilla Bits Delight"
]
```

- A negative value returns all rows from the top _except for_ the specified number of rows to exclude from the bottom.
- For example, `head(-3)` returns all rows except for the last 3.

- With a negative value, the `tail` method returns all rows from the bottom except the specified number of rows to exclude from the top.
- For example, `tail(-3)` returns all rows except for the top 3.

- The `first` and `last` methods return the first and last [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) value.

```{python}
ice_creams.first()
```
```
"Cherry Chip Drizzle"
```

```{python}
ice_creams.last()
```
```
"Cinnamon Crumb Magic"
```

### Further Reading
- https://docs.pola.rs/api/python/stable/reference/series/api/polars.Series.head.html
- https://docs.pola.rs/api/python/stable/reference/series/api/polars.Series.tail.html
- https://docs.pola.rs/api/python/stable/reference/series/api/polars.Series.limit.html

## Memory Optimization and the schema_overrides Parameter
- Polars infers a column's data type from its values. It defaults to an `i64` (64-bit integer) for whole numbers.

```{python}
daily_steps = pl.read_csv("daily_steps.csv").to_series()
daily_steps.head(5)
```
```
shape: (5,)
Series: 'daily_steps' [i64]
[
	6030
	12448
	13482
	8486
	6381
]
```

- The `estimated_size` method returns the memory size of the [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) in bytes.

```{python}
daily_steps.estimated_size()
```
```
8000
```

- Most computers assign 8 bits to 1 byte. 64 bits for one integer is equal to 8 bytes.
- The [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) has 1000 rows of integers.
- 1000 integers * 8 bytes per integer = 8000 bytes.
- An `i64` supports values from -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 (-9 quintillion to 9 quintillion).

```{python}
daily_steps.min()
```
```
5000
```
```{python}
daily_steps.max()
```
```
24930
```
- The `schema_overrides` parameter accepts a dictionary to overwrite the inferred type.

```{python}
daily_steps = pl.read_csv("daily_steps.csv", schema_overrides={"daily_steps": pl.Int16}).to_series()
```

```{python}
daily_steps.estimated_size()
```
```
2000
```

- The `schema` parameter defines the mapping for every column in the data structure.
- For a 1-column `DataFrame`, the `schema_overrides` and `schema` parameters are equivalent.
- Add a key-value for each column to override. Use the column name for the key and the desired type for its value.

- An `Int16` supports values from -32,768 to 32,767.
- If the dataset has a value greater than 32,767, the import will trigger an error.
- The [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) still has 1000 rows, but each integer occupies 16 bits (2 bytes).
- 1000 integers * 2 bytes per integer = 2000 bytes (a quarter of the original).

- We can't take negative steps in a day, so an unsigned integer (0 or positive) type feels ideal.
- Unsigned integers do not support negative values but extend twice as long in the positive direction.
- An `UInt16` supports values from 0 to 65,535.

```{python}
daily_steps = pl.read_csv("daily_steps.csv", schema_overrides={"daily_steps": pl.UInt16}).to_series()
```

```{python}
daily_steps.estimated_size()
```
```
2000
```

- The size remains the same (1000 integers x 2 bytes per integer).

## Sorting a Series
- The `sort` method sorts the values of a [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html).
- An ascending sort sorts from smallest to greatest (alphabetically for strings).
- A descending sort sorts from greatest to smallest (reverse alphabetically for strings).
- The `descending` parameter sets the sort order. Its default argument is `False` (an ascending sort).

- Polars sorts capital letters before lowercase ones.

- The `sort` method returns a new sorted [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html). The original [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) is not mutated.
- The `sort` method's `in_place` parameter mutates the original [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html).
- This parameter is relatively uncommon; Polars usually returns a copy of the data structure.

### Further Reading
- https://docs.pola.rs/api/python/stable/reference/series/api/polars.Series.sort.html

## Mathematical Methods

- The `len` method returns the length of the [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) (the number of rows). Polars will include `null` values.
- The `count` method counts the number of non-null values.

- The `null_count` method counts the number of null/missing values in the [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html).
- Polars will exclude `NaN` values from the count in the `null_count` method.

- A [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) supports many common statistical operations.
- The `sum` method adds together the [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) values.
- The `mean` method calculates the average of the [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) values.
- The `product` method multiplies together the[`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) values.
- The `max` method identifies the greatest value in the [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html).
- The `min` method identifies the smallest value in the [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html).
- The `median` method identifies the midpoint/middle value of a sorted [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html).

- The `mode` method returns a [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) with the most occuring value(s). It will contain one or more values.
- The `std` method returns the standard deviation of the [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) (the deviation from the mean).

- The `describe` method returns a `DataFrame` with various statistics.

### Further Reading
- https://docs.pola.rs/user-guide/expressions/missing-data/#missing-data-metadata
- https://docs.pola.rs/api/python/stable/reference/series/api/polars.Series.len.html
- https://docs.pola.rs/api/python/stable/reference/series/api/polars.Series.count.html
- https://docs.pola.rs/api/python/stable/reference/series/api/polars.Series.null_count.html
- https://docs.pola.rs/api/python/stable/reference/series/api/polars.Series.sum.html
- https://docs.pola.rs/api/python/stable/reference/series/api/polars.Series.mode.html
- https://docs.pola.rs/api/python/stable/reference/series/api/polars.Series.median.html
- https://docs.pola.rs/api/python/stable/reference/series/api/polars.Series.product.html
- https://docs.pola.rs/api/python/stable/reference/series/api/polars.Series.std.html
- https://docs.pola.rs/api/python/stable/reference/series/api/polars.Series.describe.html

## Rounding Methods
- The `ceil` method rounds up to the next whole number.
- The `floor` method rounds down to the next whole number.
- The `round` method rounds to the closest whole number.
- Polars rounds values >= .5 up and values < .5 down.

- Precision is the number of digits after a decimal point.
- Pass the `decimals` parameter the precision to round to.
- For example, `3.456` with a precision of 2 will round to `3.46`.

### Further Reading
- https://docs.pola.rs/api/python/stable/reference/series/api/polars.Series.ceil.html
- https://docs.pola.rs/api/python/stable/reference/series/api/polars.Series.floor.html
- https://docs.pola.rs/api/python/stable/reference/series/api/polars.Series.round.html

## How Polars Differs from Pandas

- A Polars [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) does not have an index. A Pandas [`Series`](https://pandas.pydata.org/docs/reference/api/pandas.Series.html#pandas.Series) includes a numeric ascending index starting at 0.
- A Polars [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) does not support `iloc` and `loc` accessors for retrieving row data by index location or index label.
- A Polars [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) wraps strings in quotes. A Pandas [`Series`](https://pandas.pydata.org/docs/reference/api/pandas.Series.html#pandas.Series) does not wrap its strings in quotes.
- A Polars [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) applies consistent visual styles to its data structures. A Pandas [`Series`](https://pandas.pydata.org/docs/reference/api/pandas.Series.html#pandas.Series) has no visual formatting.

- The Polars [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) is a different object from the Pandas [`Series`](https://pandas.pydata.org/docs/reference/api/pandas.Series.html#pandas.Series).
- Python's `type` function returns the class that a value is made from.

- If an integer column has missing values, Pandas will store the values as floating-points.
- In comparison, Polars retains the original type of the column's values.
- The pandas [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) constructor includes a `data` parameter. The Polars' equivalent is `values`.
- Pandas uses `NaN` for missing values, Polars uses `null`.

- Pandas will coerce values into a consistent data type if possible.
- In the next example, Pandas coerces the integers 100 and 300 into floating-point values.
- Polars will raise an error if it sees inconsistency in data types (e.g., a mix integer and floating-points).
- Use `strict=False` to skip the safety checks, then coerce the Polars [`Series`](https://docs.pola.rs/api/python/stable/reference/series/index.html) data into its desired type.

### Further Reading
- https://docs.pola.rs/user-guide/migration/pandas/#differences-in-concepts-between-polars-and-pandas
- https://docs.pola.rs/user-guide/misc/comparison/#pandas
- https://docs.pola.rs/user-guide/concepts/data-types-and-structures/#appendix-full-data-types-table
- https://pandas.pydata.org/docs/

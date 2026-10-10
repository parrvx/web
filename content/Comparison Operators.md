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


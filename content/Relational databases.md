
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

# Database normalization

[Database normalization](https://en.wikipedia.org/wiki/Database_normalization) minimizes duplicate data in any single table, and allows for data in the database to grow independently of each other. As a trade-off, queries get slightly more complex and performance issues can arise when working with many large tables. So a query must combine all that data and pull out exactly the information we need.

[Table](https://en.wikipedia.org/wiki/Table_(database))s that share information about a single entity need to have a [primary key](https://en.wikipedia.org/wiki/Primary_key) that identifies that entity uniquely across the [database](https://en.wikipedia.org/wiki/Database). One common primary key type is an auto-incrementing integer (because they are space efficient), but it can also be a string, hashed value, so long as it is unique.

[[SQL]]

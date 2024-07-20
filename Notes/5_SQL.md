Standard Query Language

![SQL Logo](../images/SQLLogo.png)

To run PostgreSQL online use [pg-sql](https://pg-sql.com)

### Notes
- In SQL, keywords are written in capital letters (like `SELECT`) while variables are written in lower-case (like a column name).
- SQL doesn't execute queries from left to right. It's important to understand this when writing queries so you comprehend what's going on behing the scenes as its very useful when writing complicated queries.
- NULL value means that specific table cell is empty.


### Key Concepts

- **Schema**: The blueprint of a table. It's a set of instructions that define the data relationships between tables, the columns of a table, its value types, constraints, etc.
- **Index**:
- **Primary Key**: Uniquely identifies this record in this table. Commonly an integer or a UUID.
- **Foregin key**: Identifies a record (usually in another table) that this row is associated with. Like a photo mapped to a user_id.
- **Keywords**: Tell the database that we want to do something. Always written in capital letters (`CREATE TABLE` are some examples).
- **Identifiers**: Tell the database what thing we want to act on. Always written in lower 
case letters.

| Relationship | Hint                                                                     |
|--------------|--------------------------------------------------------------------------|
| One-To-Many  | "A user has many photos".                                                |
| Many-To-One  | "Many photos belong to a user".                                          |
| Many-To-Many | "Many students have many classes" <-> "Many classes have many students". |
| One-To-One   | "A boat has a single captain" <-> "A captain belongs to a single boat".  |

| Delete Option | Description                                                               |
|---------------|---------------------------------------------------------------------------|
| `NO ACTION`   | **The default option**; raises an error if there are dependent rows.      |
| `RESTRICT`    | Similar to `NO ACTION`; raises an error if there are dependent rows.      |
| `CASCADE`     | Deletes all rows that have a foreign key referencing the deleted row.     |
| `SET NULL`    | Sets the foreign key column in the referencing rows to `NULL`.            |
| `SET DEFAULT` | Sets the foreign key column in the referencing rows to its default value. |


### Comparisson Math Operators

Comparisson Math Operators are very useful when filtering out information (I.E when using the `WHERE` keyword).

| Operator | Description                  |
|----------|------------------------------|
| =        | Equal                        |
| <>       | Not equal                    |
| >        | Greater than                 |
| <        | Less than                    |
| >=       | Greater than or equal        |
| <=       | Less than or equal           |
| NOT IN   | Value isn't present          |
| IN       | Is value present ?           |
| BETWEEN  | Value in between two others? |
| AND      | Used to join logical ops     |
| OR       | Used to join logical ops     |


### Functions

Here's a markdown table listing some common PostgreSQL functions formatted in uppercase:

| Function                   | Description                                                            |
|----------------------------|------------------------------------------------------------------------|
| ||                         | Concatenates two strings                                               |
| CONCAT(string1, string2, ...) | Concatenates strings                                                |
| UPPER(string)              | Converts string to uppercase                                           |
| LOWER(string)              | Converts string to lowercase                                           |
| LENGTH(string)             | Returns the length of a string                                         |
| ABS(expression)            | Absolute value                                                         |
| AVG(expression)            | Average value of a set of numbers                                      |
| COUNT(expression)          | Number of rows in a result set or number of times an expression occurs |
| MAX(expression)            | Maximum value of a set of numbers                                      |
| MIN(expression)            | Minimum value of a set of numbers                                      |
| SUM(expression)            | Sum of a set of numbers                                                |
| ROUND(expression, precision) | Rounds a numeric value to a specified precision                      |
| COALESCE(expression1, expression2, ...) | Returns the first non-null expression in the list         |
| SUBSTRING(string FROM start FOR length) | Extracts substring from a string                          |
| NOW()                      | Current date and time                                                  |
| DATE_PART('unit', timestamp) | Extracts a specific part (e.g., year, month) from a timestamp        |

### Agregate Functions



---



### PostgreSQL Column Types

| Data Type                  | Description                            | Capacity/Range                                                                                     |
|----------------------------|----------------------------------------|----------------------------------------------------------------------------------------------------|
| `BIGINT`                   | Signed eight-byte integer              | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807                                            |
| `BIGSERIAL`                | Autoincrementing eight-byte integer    | 1 to 9,223,372,036,854,775,807                                                                     |
| `BIT(n)`                   | Fixed-length bit string                | Up to 1,048,576 bits (131,072 bytes)                                                               |
| `BIT VARYING(n)`           | Variable-length bit string             | Up to 1,048,576 bits (131,072 bytes)                                                               |
| `BOOLEAN`                  | Logical Boolean (true/false)           | true or false                                                                                      |
| `BOX`                      | Rectangular box on a plane             | Represented by two points                                                                          |
| `BYTEA`                    | Binary data ("byte array")             | Up to 1 GB                                                                                         |
| `CHARACTER(n)`             | Fixed-length character string          | Up to 1 billion characters                                                                         |
| `CHARACTER VARYING(n)`     | Variable-length character string       | Up to 1 billion characters                                                                         |
| `CIDR`                     | IPv4 or IPv6 network address           | IPv4: 0.0.0.0/0 to 255.255.255.255/32<br>IPv6: ::/0 to ffff:ffff:ffff:ffff:ffff:ffff:ffff:ffff/128 |
| `CIRCLE`                   | Circle on a plane                      | Defined by a center (point) and a radius                                                           |
| `DATE`                     | Calendar date (year, month, day)       | 4713 BC to 5874897 AD                                                                              |
| `DOUBLE PRECISION`         | Double precision floating-point number | 15 decimal digits precision                                                                        |
| `INET`                     | IPv4 or IPv6 host address              | IPv4: 0.0.0.0 to 255.255.255.255<br>IPv6: :: to ffff:ffff:ffff:ffff:ffff:ffff:ffff:ffff            |
| `INTEGER`                  | Signed four-byte integer               | -2,147,483,648 to 2,147,483,647                                                                    |
| `INTERVAL`                 | Time interval                          | -178000000 years to 178000000 years                                                                |
| `JSON`                     | JSON data format                       | 1 GB                                                                                               |
| `JSONB`                    | Binary JSON data format                | 1 GB                                                                                               |
| `LINE`                     | Infinite line on a plane               | Defined by a point and a direction vector                                                          |
| `LSEG`                     | Line segment on a plane                | Defined by two points                                                                              |
| `MACADDR`                  | MAC (Media Access Control) address     | 6 bytes, formatted as XX:XX:XX:XX:XX:XX                                                            |
| `MONEY`                    | Currency amount                        | -922,337,203,685,477.5808 to +922,337,203,685,477.5807                                             |
| `NUMERIC(p, s)`            | Exact numeric of selectable precision  | Up to 131,072 digits before the decimal point; up to 16,383 digits after the decimal point         |
| `PATH`                     | Geometric path on a plane              | Sequence of points                                                                                 |
| `PG_LSN`                   | Log sequence number                    | 64-bit unsigned integer                                                                            |
| `POINT`                    | Geometric point on a plane             | Coordinate (x, y)                                                                                  |
| `POLYGON`                  | Closed geometric path on a plane       | Sequence of points forming a closed loop                                                           |
| `REAL`                     | Single precision floating-point number | 6 decimal digits precision                                                                         |
| `SMALLINT`                 | Signed two-byte integer                | -32,768 to 32,767                                                                                  |
| `SMALLSERIAL`              | Autoincrementing two-byte integer      | 1 to 32,767                                                                                        |
| `SERIAL`                   | Autoincrementing four-byte integer     | 1 to 2,147,483,647                                                                                 |
| `TEXT`                     | Variable-length character string       | Up to 1 billion characters                                                                         |
| `TIME`                     | Time of day (no time zone)             | 00:00:00 to 24:00:00                                                                               |
| `TIMESTAMP`                | Date and time (no time zone)           | 4713 BC to 294276 AD                                                                               |
| `TIMESTAMP WITH TIME ZONE` | Date and time (including time zone)    | 4713 BC to 294276 AD                                                                               |
| `TSQUERY`                  | Text search query                      | Sequence of lexemes                                                                                |
| `TSVECTOR`                 | Text search document                   | Sequence of lexemes                                                                                |
| `TXID_SNAPSHOT`            | User-level transaction ID snapshot     | Varies                                                                                             |
| `UUID`                     | Universally unique identifier          | 128-bit number (UUID)                                                                              |
| `XML`                      | XML data                               | Unlimited size                                                                                     |

### Relationship Types

#### One-To-Many

One-to-many relationships can be easilly identified by the frase "has many" as in the following examples:

- A classroom `has many` students.
- An office `has many` workers.
- A house `has many` people living in it.

#### Many-To-One

Many-to-one relationships are the same as one-to-many, they're just viewed from the other side of the relationship.

- Many students `have one` classroom.
- Many workers `have one` office.
- Many people live in a house.

#### One-To-One 

One-to-one relationships are the simplest to understand and identify as they express one way roads between to objects.

- One company `has one` CEO.
- One country `has one` capitol.
- One person `has one` drivers license.

#### Many-To-Many

Many-to-many relationships are the most complex to identify because they imply that multiple records from one entity can be related to multiple records from another entity. These relationships are typically identified by the use of `many-to-many` or `have many` keywords, which must be applied from both perspectives.

- Movies `have many` actors. <-> Many actors `have many` movies.
- Many conference calls `have many` employees. <-> Many employees `have many` conference calls.
- A google doc can be edited by `many` users at the same time. <-> A single user can edit `many` different documents.

The last example from Google Docs might be easier to understand, as its opposite would be a one-to-one relationship: `A document can only be edited by a single user. <-> A user can only edit a single document`.
Another example is building a database for an E-Commerce application where you need to track which users purchase which product categories. In this context, many-to-many relationships are evident because `Users can purchase products from many different categorys. <-> Each kind of product can be purchased by many different users.`



---



### Primary Keys

- Primary Keys uniquely identify a record in a table, 
- They are usually an integer or an UUID. 
- **There can't be two rows with the same primary key in a table**.

Below is an example of how a primary key `PK` looks like in a table.

#### Users Table

| id INTEGER, PK | username VARCHAR (50) | email VARCHAR (50) |
|----------------|-----------------------|--------------------|
| 1              | user1                 | user1@example.com  |
| 2              | user2                 | user2@example.com  |
| 3              | user3                 | user3@example.com  |
| ...            | ...                   | ...                |

As you can see, the `id` field on each table is a **Primary Key**, and the `user_id` field on the `Photos` table is a **Foreign Key**

##### Notes:
- Even when you delete or modify records **the primary key will not change**, which ensures that all records can be consistently accessed using the PK.
- **Primary Key (PK)**: `id` columns are marked as primary keys ensuring each row has a unique identifier.


### Foreign Keys

Foreign keys in a relational database are columns (or combinations of columns) that establish and enforce a link between data in two tables. They create a parent-child relationship between the tables, where the child table contains values that match values in the primary key column(s) of the parent table.

- Rows can  **only have this if they belong to another record**.
- Many rows can have the same foreign key.
- Name varies, usually called something like **"xyz_id"**.
- **Exactly equal to the primary key of the referenced row**.
- Changes if the relationship changes.

You might find it easier to understand by thinking how Instagram handles its comments. Each comment belongs to a photo were it was written, so in the comments table you would have a foreign key for each comment pointing at its photo (the one where the comment was written into).

```mermaid
graph TD;
    subgraph Comments
        A1[Comment 1]
        A2[Comment 2]
        A3[Comment 3]
    end
    B[Photo]
    A1 -->B
    A2 -->B
    A3 -->B
```

Another great example comes from the tables below, notice how the `photos` table records reference a specific user using it's `id` (the Foreign Key).

#### Users Table

| id INTEGER, PK | username VARCHAR (50) | email VARCHAR (50) |
|----------------|-----------------------|--------------------|
| 1              | user1                 | user1@example.com  |
| 2              | user2                 | user2@example.com  |
| 3              | user3                 | user3@example.com  |
| ...            | ...                   | ...                |

#### Photos Table

| id INTEGER, PK | url VARCHAR (50) | user_id (FK, points to users record) |
|----------------|------------------|--------------------------------------|
| 1              | [url_1]          | 1                                    |
| 2              | [url_2]          | 3                                    |
| 3              | [url_3]          | 2                                    |
| ...            | ...              | ...                                  |

As you can see, the `id` field on each table is a **Primary Key**, and the `user_id` field on the `Photos` table is a **Foreign Key**

##### Notes:
- Even when you delete or modify records **the primary key will not change**, which ensures that all records can be consistently accessed using the PK.
- **Primary Key (PK)**: `id` columns are marked as primary keys (`PK`) in both tables, ensuring each row has a unique identifier.
- **Foreign Key (FK)**: In the `photos` table, `user_id` is a foreign key that references the `id` column in the `users` table, establishing a relationship between photos and users.
- **Data Types**: `url` and `email` are specified as `varchar(50)`, indicating the expected character limits for these columns.
  
These tables provide a basic structure for modeling photos and users in a database schema, demonstrating the use of primary keys, foreign keys, and column data types as per your requirements. Adjustments can be made based on specific database management system requirements or additional constraints.

```SQL
-- Create the users table
CREATE TABLE users (
  -- Serial means it auto-generates a value when a record is addedALTER
  -- Primary Key adds special performance benefits when looking for records
  id SERIAL PRIMARY KEY,
  user_name VARCHAR(50)
);
-- Insert some data into the users table
INSERT INTO users (user_name) VALUES ('Juan'), ('Jose'), ('Luis'), ('x123');

-- Create photos table
CREATE TABLE photos (
    id SERIAL PRIMARY KEY,
    url VARCHAR(50),
    -- Name the column as 'user_id' which holds the link to the users table
    -- References keyword is used to specify the table and the column for the Foreign Key relationship
    user_id INTEGER REFERENCES users(id)
);

-- Insert values into the photos table using the foregin key
INSERT INTO photos (url, user_id) VALUES ('http://one.jpg', 4), ('http://tg3223.jpg', 3),
('http://two.jpg', 2), ('http://on234e.jpg', 1), ('http://o23.jpg', 1);
```

Below are some examples of some queries that show how to use the foreign key constraints in a useful way:

```SQL
-- Select all photos that were posted by the user whos id is 4.
SELECT * FROM photos WHERE user_id = 1;

-- List all photos with details about the associated user for each
SELECT * FROM photos JOIN users ON users.id = photos.user_id;

-- Note in this variation of the above query, columns of both tables are available thanks to the JOIN
-- url exists on the photos table while user_name exists on the user table
SELECT url, user_name FROM photos JOIN users ON users.id = photos.user_id;
```

#### ON DELETE Options

When deleting records that have children rows pointing at them (via the foreign key), it's necessary to specify the behavior this child row should have as its foreign key value will become inexistent. Here's where `ON DELETE` options come into play; **they define the actions that take place when the refered record of a foreign key column gets deleted**.

- These `ON DELETE` options **must be placed inside the table schema that has the foreign key sentence**.

| FK ON DELETE Option     | Description                                                               |
|-------------------------|---------------------------------------------------------------------------|
| `ON DELETE NO ACTION`   | **The default option**; raises an error if there are dependent rows.      |
| `ON DELETE RESTRICT`    | Similar to `NO ACTION`; raises an error if there are dependent rows.      |
| `ON DELETE CASCADE`     | Deletes all rows that have a foreign key referencing the deleted row.     |
| `ON DELETE SET NULL`    | Sets the foreign key column in the referencing rows to `NULL`.            |
| `ON DELETE SET DEFAULT` | Sets the foreign key column in the referencing rows to its default value. |

```SQL
-- Create photos table
CREATE TABLE photos (
    id SERIAL PRIMARY KEY,
    url VARCHAR(50),
    -- Set the ON DELETE action for this foreign key column
    -- If the user_id row gets deleted this record will be deleted as well
    user_id INTEGER REFERENCES users(id) ON DELETE CASCADE
);
```

These delete options are very useful in day-to-day applications like blogs. If you delete a blog post you probably don't want to keep around its comments in your DB (**ON DELETE CASCADE**). In some cases you might want to keep the information, like in Reddit that when a user gets deleted his comments remain there but with a `deleted` user tag (**ON DELETE SET NULL**).




### Joins

- Produces values by merging together rows from different **related** tables.
- Use a join **most times** that you're asked to find data that involves multiple resources.
- Table order between `FROM` and `JOIN` often **matters**.
- Must provide context if column names colide.
- Columns can be renamed using the `AS` keyword.

![SQL Joins](../images/SQLJoins.png)

| Join       | Description                                                                        |
|------------|------------------------------------------------------------------------------------|
| INNER JOIN | Returns only the rows that have matching values in both tables.                    |
| LEFT JOIN  | Returns all rows from the left table and the matched rows from the right table.    |
| RIGHT JOIN | Returns all rows from the right table and the matched rows from the left table.    |
| FULL JOIN  | Returns all rows when there is a match in either the left or right table.          |
| CROSS JOIN | Returns the Cartesian product of the two tables, i.e., all possible pairs of rows. |


```SQL
-- Inner Join (Default)
SELECT url, username FROM photos INNER JOIN users ON user.id = photos.user_id; -- Either INNER JOIN or just JOIN will work

-- NOTE: For LEFT and RIGHT joins, THE ORDER MATTERS!

--Left Join
SELECT url, username FROM photos LEFT JOIN users ON user.id = photos.user_id;

-- Right Join
SELECT url, username FROM photos RIGHT JOIN users ON user.id = photos.user_id;

-- Full Join
SELECT url, username FROM photos FULL JOIN users ON user.id = photos.user_id;
```


### Aggregations

- Looks at many rows and calculates a single value.
- Words like `most`, `average`, `least` are a sign you need to use an aggregation.

---



### Common Queries

#### Create Table

```SQL
CREATE TABLE table_name (
    column_title COLUMN_TYPE(optional_value),
    column_title2 COLUMN_TYPE(optional_value),
);
```

#### Insert Single/Multiple Values Into A Table

```SQL
-- To insert a single value just write a single set of parenthesis with column values
INSERT INTO table_name (column_name1, column_name2) VALUES 
(column1_value1, column2_value1)
(column1_value2, column2_value2)
(column1_value3, column2_value3),
;
```

#### Retrieving Information From A Table


```SQL
-- Select all records from table
SELECT * FROM table_name;

-- Select specific columns from table
SELECT column_name, column2_name FROM table_name;

-- You can perform operations between columns when retrieving information
SELECT column_1, column_2 / column_3 FROM table_name;
```
**Notes**: 
- The order of the columns is the order of their printing. You can also print the same column multiple times.
- If your operation's result goes beyond what the column can store you will get an error. For example, if you use INTEGER as the column type and the result of a multiplication of two columns goes over its capacity (2,147,483,648) you will get an `Integer out of range` error.


```SQL
-- When performing operations on retrieval, new columns will come out with weird names. 
-- To rename the result column:
SELECT column_1, column_2 * column_3 AS result_column_name FROM table_name;

-- Concatenating column values as strings
SELECT column_1 || ', ' || column_2  AS concatenated_column_name FROM table_name;

-- The same as above but using CONCAT() instead of '||'
SELECT CONCAT(column_1, ', ', column_2) FROM table_name;
```

#### Filtering Out Records

```SQL
-- Use the WHERE keyword to filter data by using it in pair with comparisson or math operators.
SELECT column_1, column_2 WHERE column_1 > 5000 FROM table_name;

-- BETWEEEN keyword example
SELECT column_1, column_2 FROM table_name WHERE column_1 BETWEEN 5 AND 10;

-- Using a list of possible values for an 'IN' check in a query
SELECT column_1, column_2 FROM table_name WHERE column_1 IN (possible_value_1, possible_value_2, ...);

-- You could also use a negative filter to get all records whose 'column_1' is not in the list by using the 'NOT IN' keywords.
-- Note that you can chain as many 'AND' and 'OR' operators as you want
SELECT column_1, column_2 FROM table_name WHERE column_1 IN (possible_value_1, possible_value_2) AND column_2 = 'arbitrary_value';
```

#### Updating & Deleting Records

- To update records you use the `UPDATE` and `SET` keywords.
- To delete records you use the `DELETE` keyword. Be sure to **NEVER FORGET THE `FROM` STATEMENT**!

```SQL
-- Updating a single column (multiple rows may be updated)
UPDATE table_name SET column_1 = 5000 WHERE column_2 = 'arbitrary_value';

-- Deleting one or more records
DELETE FROM table_name WHERE column_1 = 5;
```

### Query Examples

```SQL
CREATE TABLE movies (
    title VARCHAR(60),
    box_office INTEGER
);
```

```SQL
INSERT INTO movies (title, box_office)
VALUES 
    ('The Avengers', 1500000000),
    ('Batman v Superman', 873000000);
```

```SQL
SELECT title, box_office FROM movies;
```

### Excercises

**Section 4**

#### Data

```SQL
CREATE TABLE users(
  id SERIAL PRIMARY KEY,
  username VARCHAR(50)
);
 
CREATE TABLE photos (
  id SERIAL PRIMARY KEY,
  url VARCHAR(200),
  user_id INTEGER REFERENCES users(id) ON DELETE CASCADE
);
 
CREATE TABLE comments (
  id SERIAL PRIMARY KEY,
  contents VARCHAR(240),
  user_id INTEGER REFERENCES users(id) ON DELETE CASCADE,
  photo_id INTEGER REFERENCES photos(id) ON DELETE CASCADE
);
 
INSERT INTO users (username) 
VALUES 
  ('Reyna.Marvin'),
        ('Micah.Cremin'),
        ('Alfredo66'),
        ('Gerard_Mitchell42'),
        ('Frederique_Donnelly');
 
INSERT INTO photos (url, user_id)
VALUES
  ('https://santina.net', 3),
        ('https://alayna.net', 5),
        ('https://kailyn.name', 3),
        ('http://marjolaine.name', 1),
        ('http://chet.net', 5),
        ('http://jerrold.org', 2),
        ('https://meredith.net', 4),
        ('http://isaias.net', 4),
        ('http://dayne.com', 4),
        ('http://colten.net', 2),
        ('https://adelbert.biz', 5),
        ('http://kolby.org', 1),
        ('https://deon.biz', 2),
        ('https://marina.com', 5),
        ('http://johnson.info', 1),
        ('https://linda.info', 2),
        ('https://tyrique.info', 4),
        ('http://buddy.info', 5),
        ('https://elinore.name', 2),
        ('http://sasha.com', 3);
 
INSERT INTO comments (contents, user_id, photo_id)
VALUES
  ('Quo velit iusto ducimus quos a incidunt nesciunt facilis.', 2, 4),
        ('Non est totam.', 5, 5),
        ('Fuga et iste beatae.', 3, 3),
        ('Molestias tempore est.', 1, 5),
        ('Est voluptatum voluptatem voluptatem est ullam quod quia in.', 1, 5),
        ('Aut et similique porro ullam.', 1, 3),
        ('Fugiat cupiditate consequatur sit magni at non ad omnis.', 1, 2),
        ('Accusantium illo maiores et sed maiores quod natus.', 2, 5),
        ('Perferendis cumque eligendi.', 1, 2),
        ('Nihil quo voluptatem placeat.', 5, 5),
        ('Rerum dolor sunt sint.', 5, 2),
        ('Id corrupti tenetur similique reprehenderit qui sint qui nulla tenetur.', 2, 1),
        ('Maiores quo quia.', 1, 5),
        ('Culpa perferendis qui perferendis eligendi officia neque ex.', 1, 4),
        ('Reprehenderit voluptates rerum qui veritatis ut.', 1, 1),
        ('Aut ipsum porro deserunt maiores sit.', 5, 3),
        ('Aut qui eum eos soluta pariatur.', 1, 1),
        ('Praesentium tempora rerum necessitatibus aut.', 4, 3),
        ('Magni error voluptas veniam ipsum enim.', 4, 2),
        ('Et maiores libero quod aliquam sit voluptas.', 2, 3),
        ('Eius ab occaecati quae eos aut enim rem.', 5, 4),
        ('Et sit occaecati.', 4, 3),
        ('Illum omnis et excepturi totam eum omnis.', 1, 5),
        ('Nemo nihil rerum alias vel.', 5, 1),
        ('Voluptas ab eius.', 5, 1),
        ('Dolor soluta quisquam voluptatibus delectus.', 3, 5),
        ('Consequatur neque beatae.', 4, 5),
        ('Aliquid vel voluptatem.', 4, 5),
        ('Maiores nulla ea non autem.', 4, 5),
        ('Enim doloremque delectus.', 1, 4),
        ('Facere vel assumenda.', 2, 5),
        ('Fugiat dignissimos dolorum iusto fugit voluptas et.', 2, 1),
        ('Sed cumque in et.', 1, 3),
        ('Doloribus temporibus hic eveniet temporibus corrupti et voluptatem et sint.', 5, 4),
        ('Quia dolorem officia explicabo quae.', 3, 1),
        ('Ullam ad laborum totam veniam.', 1, 2),
        ('Et rerum voluptas et corporis rem in hic.', 2, 3),
        ('Tempora quas facere.', 3, 1),
        ('Rem autem corporis earum necessitatibus dolores explicabo iste quo.', 5, 5),
        ('Animi aperiam repellendus in aut eum consequatur quos.', 1, 2),
        ('Enim esse magni.', 4, 3),
        ('Saepe cumque qui pariatur.', 4, 4),
        ('Sit dolorem ipsam nisi.', 4, 1),
        ('Dolorem veniam nisi quidem.', 2, 5),
        ('Porro illum perferendis nemo libero voluptatibus vel.', 3, 3),
        ('Dicta enim rerum culpa a quo molestiae nam repudiandae at.', 2, 4),
        ('Consequatur magnam autem voluptas deserunt.', 5, 1),
        ('Incidunt cum delectus sunt tenetur et.', 4, 3),
        ('Non vel eveniet sed molestiae tempora.', 2, 1),
        ('Ad placeat repellat et veniam ea asperiores.', 5, 1),
        ('Eum aut magni sint.', 3, 1),
        ('Aperiam voluptates quis velit explicabo ipsam vero eum.', 1, 3),
        ('Error nesciunt blanditiis quae quis et tempora velit repellat sint.', 2, 4),
        ('Blanditiis saepe dolorem enim eos sed ea.', 1, 2),
        ('Ab veritatis est.', 2, 2),
        ('Vitae voluptatem voluptates vel nam.', 3, 1),
        ('Neque aspernatur est non ad vitae nisi ut nobis enim.', 4, 3),
        ('Debitis ut amet.', 4, 2),
        ('Pariatur beatae nihil cum molestiae provident vel.', 4, 4),
        ('Aperiam sunt aliquam illum impedit.', 1, 4),
        ('Aut laudantium necessitatibus harum eaque.', 5, 3),
        ('Debitis voluptatum nesciunt quisquam voluptatibus fugiat nostrum sed dolore quasi.', 3, 2),
        ('Praesentium velit voluptatem distinctio ut voluptatum at aut.', 2, 2),
        ('Voluptates nihil voluptatum quia maiores dolorum molestias occaecati.', 1, 4),
        ('Quisquam modi labore.', 3, 2),
        ('Fugit quia perferendis magni doloremque dicta officia dignissimos ut necessitatibus.', 1, 4),
        ('Tempora ipsam aut placeat ducimus ut exercitationem quis provident.', 5, 3),
        ('Expedita ducimus cum quibusdam.', 5, 1),
        ('In voluptates doloribus aut ut libero possimus adipisci iste.', 3, 2),
        ('Sit qui est sed accusantium quidem id voluptatum id.', 1, 5),
        ('Libero eius quo consequatur laudantium reiciendis reiciendis aliquid nemo.', 1, 2),
        ('Officia qui reprehenderit ut accusamus qui voluptatum at.', 2, 2),
        ('Ad similique quo.', 4, 1),
        ('Commodi culpa aut nobis qui illum deserunt reiciendis.', 2, 3),
        ('Tenetur quam aut rerum doloribus est ipsa autem.', 4, 2),
        ('Est accusamus aut nisi sit aut id non natus assumenda.', 2, 4),
        ('Et sit et vel quos recusandae quo qui.', 1, 3),
        ('Velit nihil voluptatem et sed.', 4, 4),
        ('Sunt vitae expedita fugiat occaecati.', 1, 3),
        ('Consequatur quod et ipsam in dolorem.', 4, 2),
        ('Magnam voluptatum molestias vitae voluptatibus beatae nostrum sunt.', 3, 5),
        ('Alias praesentium ut voluptatem alias praesentium tempora voluptas debitis.', 2, 5),
        ('Ipsam cumque aut consectetur mollitia vel quod voluptates provident suscipit.', 3, 5),
        ('Ad dignissimos quia aut commodi vel ut nisi.', 3, 3),
        ('Fugit ut architecto doloremque neque quis.', 4, 5),
        ('Repudiandae et voluptas aut in excepturi.', 5, 3),
        ('Aperiam voluptatem animi.', 5, 1),
        ('Et mollitia vel soluta fugiat.', 4, 1),
        ('Ut nemo voluptas voluptatem voluptas.', 5, 2),
        ('At aut quidem voluptatibus rem.', 5, 1),
        ('Temporibus voluptates iure fuga alias minus eius.', 2, 3),
        ('Non autem laboriosam consectetur officiis aut excepturi nobis commodi.', 4, 3),
        ('Esse voluptatem sed deserunt ipsum eaque maxime rerum qui.', 5, 5),
        ('Debitis ipsam ut pariatur molestiae ut qui aut reiciendis.', 4, 4),
        ('Illo atque nihil et quod consequatur neque pariatur delectus.', 3, 3),
        ('Qui et hic accusantium odio quis necessitatibus et magni.', 4, 2),
        ('Debitis repellendus inventore omnis est facere aliquam.', 3, 3),
        ('Occaecati eos possimus deleniti itaque aliquam accusamus.', 3, 4),
        ('Molestiae officia architecto eius nesciunt.', 5, 4),
        ('Minima dolorem reiciendis excepturi culpa sapiente eos deserunt ut.', 3, 3);
```

**Excercises**:

1. For each comment, show the contents of the comment and the username of the user who wrote it.

2. For each comment, list the contents of the comments and the url of the photo the comment was added to.

3. Show each photo url along with the username of the poster (you should show the url even if there is no identifiable poster).

4. Show each user alongside his photos even if he doesn't have photos posted yet.

5. Users can comment on photos that they post. List the url and comment content of all photos/comments where this happened.

3. Find all the comments for the photo with ID=3, along with the username of the comment author.

4. Find the photo with ID = 10 and get the number of comments attached to it.

5. Find the average number of comments per photo.

6. Find the user with the most activity (most comments + most photos).

7. Find the photo with the most comments attached to it.

8. Calculate the average number of characters per comment.

**Answers**

1. Excercise 1:
    ```SQL
    SELECT contents, username FROM comments JOIN users ON users.id = comments.user_id;
    ```

2. Excercise 2:
    ```SQL
    SELECT contents, url FROM comments JOIN photos ON comments.photo_id = photos.id;
    ```

3. Excercise 3:
    ```SQL
    SELECT url, username FROM photos LEFT JOIN users ON photos.user_id = users.id;
    ```

4. Excercise 4:
    ```SQL
    SELECT url, username FROM photos RIGHT JOIN users ON photos.user_id = users.id;
    ```

5. Excercise 5:
    ```SQL
    SELECT url, contents FROM comments JOIN photos ON comments.photo_id = photos.id  WHERE comments.user_id = photos.user_id;
    ```
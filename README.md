# PostgreSQL

## CLI Commands

1. psql

    Login with psql command by specifying existing username and dbname with flags

    ```bash
    $ psql --username=freecodecamp --dbname=postgres
    Border style is 2.
    Title is " ".
    Pager usage is off.
    psql (12.9 (Ubuntu 12.9-2.pgdg20.04+1))
    Type "help" for help.

    postgres=>
    ```

    This will return the interactive Postgres prompt

## PostgresSQL commands

> _All commands are __capitalized__ and end with semicolon(;)_\
> Except Shortcut commands

1. \l

    List all existing databases

    ```psql
    postgres=> \l
    ```

2. CREATE DATABASE

    Create new database by giving a name

    ```psql
    postgres=> CREATE DATABASE database_name;
    ```

3. \c

    Connect to existing database

    ```pqsl
    postgres=> \c database_name
    You are now connected to database "database_name" as user "freecodecamp".
    database_name=>
    ```

    The connected database prompt is returned

4. \d

    List Tables present in the database

    ```psql
    database_name=> \d
    Did not find any relations.
    ```

    Use table_name to see info about specific table

    ```psql
    database_name=> \d table_name    
    ```

5. CREATE TABLE

    Create a TABLE in the connected database
    > Parenthesis after table_name is needed

    ```psql
    database_name=> CREATE TABLE table_name();
    ```

6. ALTER TABLE ADD COLUMN

    Add column to the table by giving the `column_name`, `table_name`, and `DATATYPE`

    ```psql
    database_name=> ALTER TABLE table_name ADD COLUMN column_name DATATYPE;
    ALTER TABLE
    ```

    > add constraint to column by _adding it after data-type_\
    > example - `ALTER TABLE table_name ADD COLUMN column_name DATATYPE NOT NULL;`

7. ALTER TABLE DROP COLUMN

    Remove column with DROP COLUMN

    ```psql
    database_name=> ALTER TABLE table_name DROP COLUMN column_name;
    ```

8. ALTER TABLE RENAME COLUMN

    Rename a column

    ```psql
    database_name=> ALTER TABLE table_name RENAME COLUMN column_name TO new_name;
    ```

9. INSERT INTO VALUES

    Insert _rows_(actual data/record) in _table_ with INSERT INTO table_name(column_1_name, column_2_name) VALUES(value1, value2)[^datatypes];

    ```psql
    database_name=> INSERT INTO second_table(username, id) VALUES("examplename", 1);
    ```

    To add multiple rows in a single command, keep appending the values for subsequent rows

    ```psql
    INSERT INTO characters(name, homeland, favorite_color)
    VALUES('Mario', 'Mushroom Kingdom', 'Red'),
    ('Luigi', 'Mushroom Kingdom', 'Green'),
    ('Peach', 'Mushroom Kingdom', 'Pink');
    ```

10. SELECT FROM

    View data in a TABLE by _querying_ it along with column-names you want to view
    > Put `*` in place of column name to view all columns

    ```psql
    SELECT * FROM second_table;
    ```

    Use `clauses` to modify how data is displayed. For example, use ORDER_BY to change the order or records

    ```psql
    SELECT * FROM characters ORDER BY character_id;
    ```

11. DELETE FROM WHERE

    Delete data from a table by specifying a condition with DELETE FROM table_name WHERE condition;

    ```psql
    DELETE FROM second_table WHERE username='Mario';
    ```

12. DROP TABLE

    Remove Table from database

    ```psql
    DROP TABLE table_name;
    ```

13. ALTER DATABASE RENAME TO

    Rename database

    ```psql
    ALTER DATABASE database_name RENAME TO new_database_name;
    ```

14. DROP DATABASE

    Remove database

    ```psql
    DROP DATABASE second_database;
    ```

15. UPDATE SET WHERE

    Change the value in a row by specifying table name, column name, new value and condition

    ```psql
    UPDATE characters SET fav_color='Red' WHERE name='Mario';
    ```

16. ALTER TABLE ADD PRIMARY KEY

    Add _primary key_(unique identifier for each row/data/record) by specifying table name and column name
    > Primary key is set for each table and there can be only one per table

    ```psql
    ALTER TABLE characters ADD PRIMARY KEY(name);
    ```

## Data Types

- VARCHAR(max length)

  character string\
  eg VARCHAR(10)

- SERIAL

  Special type that makes a _column of type INT_ with _NOT NULL constraint_,\
  and __auto increment__ the INT upon addition of new rows

[^datatypes]: [enter-correct]
[enter-correct-datatypes...(those which column accepts. check \d tablename and refer type id unsure)]

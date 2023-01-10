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

    To create table and add column in same command, use `CREATE TABLE table_name(column_name DATATYPE CONSTRAINTS);`

    ```psql
    CREATE TABLE sounds(sound_id SERIAL PRIMARY KEY);
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

8. ALTER TABLE RENAME COLUMN TO

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

    > View mulltiple/ single columns by providing __comma separated column names__\
    > `SELECT name, id FROM characters`

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
    ALTER TABLE characters ADD PRIMARY KEY(character_id);
    ```

    > Add a composite primary key generated from 2 columns with\
    > `ALTER TABLE table_name ADD PRIMARY KEY(column1, column2);`\
    > Useful for __junction_tables__

17. ALTER TABLE DROP CONSTRAINT

    Remove a constraint by running `ALTER TABLE table_name DROP CONSTRAINT constraint_name;`
    > Use \d table_name to view esisting constraints i.e constraint_names specified as string

    ```psql
    ALTER TABLE characters DROP CONSTRAINT characters_pkey;
    ```

18. ALTER TABLE ADD UNIQUE

    Add unique constraint to enforce __one-to-one relationship to tables__
    > i.e _one_ row in table A will be related to _one_ row in table B\
    > Usually add the unique constraint to references column
    `ALTER TABLE table_name ADD UNIQUE(column_name);`

    ```psql
    ALTER TABLE more_info ADD UNIQUE(character_id);
    ```

19. ALTER TABLE ADD COLUMN REFERENCES

    Add a _foreign key_ to relate _records in a table_, with _records[^1] in **another table**_\
    by creating a column that exists in another table-\
    `ALTER TABLE table_name ADD COLUMN column_name DATATYPE REFERENCES referenced_table_name(referenced_column_name);`

    ```psql
    ALTER TABLE more_info ADD COLUMN character_id INT REFERENCES characters(character_id);
    ```

20. ALTER TABLE ALTER COLUMN SET NOT NULL

    Add `NOT NULL` constraint on existing column with `ALTER TABLE table_name ALTER COLUMN column_name SET NOT NULL;`
    > To add constraint when adding new column, check command #6

    ```psql
    ALTER TABLE more_info ALTER COLUMN character_id SET NOT NULL;
    ```

21. ALTER TABLE ADD FOREIGN KEY REFERENCES

    Add foreign key to existing columns with `ALTER TABLE table_name ADD FOREIGN KEY(column_name) REFERENCES referenced_table(referenced_column);`

    ```psql
    ALTER TABLE character_actions ADD FOREIGN KEY(character_id) REFERENCES characters(character_id);
    ```

22. SELECT FROM FULL JOIN ON

    When two tables are linked with _foreign keys_, we can use __join__ to view all data from both tables using\
    `SELECT column_name FROM table_1_name FULL JOIN table_2_name ON table_1.primary_key_column_name = table_2.foreign_key_column_name;`

    ```psql
    SELECT * FROM characters FULL JOIN more_info ON characters.character_id = more_info.character_id;
    ```

    > Use consequent `FULL JOIN`'s to view more tables together using\
    `SELECT columns FROM junction_table
    FULL JOIN table_1 ON junction_table.foreign_key_column = table_1.primary_key_column
    FULL JOIN table_2 ON junction_table.foreign_key_column = table_2.primary_key_column;`
    [^junction-tables]

    ```psql
    SELECT * FROM character_actions
    FULL JOIN characters ON character_actions.character_id = characters.character_id
    FULL JOIN actions ON character_actions.action_id = actions.action_id;
    ```

## Data Types

- VARCHAR(max length)

  character string\
  eg VARCHAR(10)

- SERIAL

  Special type that makes a _column of type INT_ with _NOT NULL constraint_,\
  and __auto increment__ the INT upon addition of new rows

- DATE
- NUMERIC(x, y)

  This datatype is for decimals. x is the number of digits and y is number of digits to the right of decimal point

## Types of relations

- Table

- Sequence

  Automatically generated for _columns_ with data type _SERIAL_

## IMP- Relations between TABLES

- one to one relationship - add foreign key to tables with UNIQUE constraint
- one to many relationshhip - add foreign key without UNIQUE constraint
- many to many relationship - use a third _junction table_ to link the two tables

[^datatypes]: [enter-correct]

[^1]: [usually-primary-key-of-another-table]

[^junction-tables]: [these-are-used-to-describe-many-to-many-relations-between-2-tables..they-only-consisit-of-foreign-key-columns-for-linked-tables--and-composite-primary-key-which-is-a-combination-of-the-existing-foreign-keys]

[enter-correct-datatypes...(those which column accepts. check \d tablename and refer type id unsure)]

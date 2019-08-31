# PostgreSQL

## Overview

- Database: to store, manipulate, retrieve data
- PostgreSQL: Database name
- SQL: programming language, data held in a relational database
- stored in tables
- table has columns and rows
- PostgreSQL server has to run: `systemctl start postgresql.service`

## Bash

- connect to server: `sudo -iu postgres` => bash of user postgres
- create user: `createuser --interactive`
- create db: `createdb [db]`
- connect to psql: `psql -d [db] -U [user]`

## PSQL

- psql is a terminal-based front-end to PostgreSQL, you can type in queries, issue them to PostgreSQL, and see the query results.
- psql always needs a `;` at the end of every command
- help of psql: `help`
- help with SQL commands: `\h`
- quit psql: `\q`

- list all dbs: `\l`
- create db: `CREATE DATABASE [db];`
- connect to db: `\c [db]`
- get connection info: `\conninfo`
- delete db: `DROP DATABASE [db];`
- display all tables: `\dt`
- display specific table: `\d [table]`
- create table: `CREATE TABLE [table]([col][datatype] [constraints])`
- run file: `\i [path-to-file]`

## SQL

### Keys

- always add an id as `primary key`
- use `unique key` for data like email, username
- use `check` to only allow specific values

### Create Data

- Create data: `INSERT INTO [table] ([col]) VALUES ([value]);`

### Read Data

- Read data: `SELECT [col] FROM [table];`
- sort data: `ORDER BY`
- remove duplicates: `SELECT DISTINCT`
- clauses: `WHERE [expression]`
- limit: `LIMIT [number]`
- Offset: `OFFSET [number]`
- use Array for DRY: `IN ([values])` => `WHERE name IN ('Max', 'Heidi')`
- Range: `WHERE [col] BETWEEN [value] AND [value]`
- like: `WHERE [col] LIKE '[value]'`
- like (ignore case): `WHERE [col] ILIKE '[value]'`
- count: `SELECT [col], COUNT(*) FROM [table] GROUP BY [col];`
- count having: `SELECT [col], COUNT(*) FROM [table] GROUP BY [col] HAVING COUNT(*) > x;`
- sum/min/max/avg: `SELECT SUM/MIN/MAX/AVG([col]) FROM [table];`
- round: `SELECT ROUND([col], digits) FROM [table];`
- give alternate value: `SELECT coalesce([COL], [ALTERNATIVE]) FROM [table];`
- get current timestamp: `SELECT NOW();`
- get current date: `SELECT NOW()::DATE;`
- get current time: `SELECT NOW()::TIME;`
- get year: `SELECT EXTRACT(YEAR FROM NOW());`

## Notes

- PostgreSQL interprets " as being quotes for identifiers, ' as being quotes for strings
- use Mockaroo to create dummy data
- list of datatypes: https://www.postgresql.org/docs/current/datatype-character.html
- list of constraints: https://www.postgresql.org/docs/current/ddl-constraints.html
- aggregate functions (e.g. `count()`): https://www.postgresql.org/docs/current/functions-aggregate.htmlS

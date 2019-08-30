# PostgreSQL

## Overview

- Database: to store, manipulate, retrieve data
- PostgreSQL: Database name
- SQL: programming language, data held in a relational database
- stored in tables
- table has columns and rows

## General Commands

- psql is a terminal-based front-end to PostgreSQL, you can type in queries, issue them to PostgreSQL, and see the query results.
- psql always needs a `;` at the end of every command
- PostgreSQL server has to run: `systemctl start postgresql.service`
- connect to server: `sudo -iu postgres` => bash of user postgres

### Bash Commands

- create user: `createuser --interactive`
- create db: `createdb [db]`
- connect to psql: `psql -d [db] -U [user]`

### PSQL Commands

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
- list of datatypes: https://www.postgresql.org/docs/current/datatype-character.html
- list of constraints: https://www.postgresql.org/docs/current/ddl-constraints.html
- run file: `\i [path-to-file]`
- Create data: `INSERT INTO [table] ([col]) VALUES ([value]);`
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

## Notes

- PostgreSQL interprets " as being quotes for identifiers, ' as being quotes for strings
- use Mockaroo to create dummy data

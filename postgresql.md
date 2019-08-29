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
- create db: `createdb [dbname]`
- connect to psql: `psql -d [dbname] -U [username]`

### PSQL Commands

- help of psql: `help`
- help with SQL commands: `\h`
- quit psql: `\q`

- list all dbs: `\l`
- create db: `CREATE DATABASE [dbname];`
- connect to db: `\c [dbname]`
- get connection info: `\conninfo`
- delete db: `DROP DATABASE [dbname];`
- display all tables: `\dt`
- display specific table: `\d [tablename]`
- create table: `CREATE TABLE [tablename]([columnname][datatype] [constraints])`
- list of datatypes: https://www.postgresql.org/docs/current/datatype-character.html
- list of constraints: https://www.postgresql.org/docs/current/ddl-constraints.html

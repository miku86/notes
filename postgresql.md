# PostgreSQL

## Overview

- Database: to store, manipulate, retrieve data
- PostgreSQL: Database name
- SQL: programming language, data held in a relational database
- stored in tables
- table has columns and rows

## General Commands

- psql is a terminal-based front-end to PostgreSQL, you can type in queries, issue them to PostgreSQL, and see the query results.
- connect to server: `sudo -iu postgres`
- create user: `createuser --interactive`
- create db: `createdb [dbname]`
- connect to psql: `psql [dbname] [username]`
- connect to db: `\c [dbname]`
- list all dbs: `\l`
- display tables: `\dt`
- get connection info: `\conninfo`

---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-07-21T19:42
updated: 2025-07-22T19:49
---
`psql` is a terminal-based front-end to [[PostgreSQL]]. It enables you to type in queries interactively, issue them to PostgreSQL, and see the query results.

>[!info]- Installation
>
>From the terminal:
>- Using HomeBrew: `brew install libpq`
>- Than add symlink: `brew link --force libpq`

>[!info]- Connection
>
>```
>psql -h [HOSTNAME] -p [PORT] -U [USERNAME] -W -d [DATABASENAME]
>```
>
>Once you run that command, the prompt will ask you for your password. (Which we specified with the `-W` flag.)
>
>Alternatively, if you wat just to connect to a database in your local machine you can just write:
>- `psql` to open the run the tool
>- `\c [database_name]`
>
>To lits all the databases present in you machine, you can use `\l`.

## Basic Commands

- Create DB: `CREATE DATABASE [database_name];`
- Delete DB: `DROP DATABASE [database_name];`
- List all relations (tables): `\d`
- List information about a table: `\d table_name`
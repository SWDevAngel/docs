---
title: Create a Database and User-defined Schema
summary: Create a database and schema for your CockroachDB cluster
toc: true
---

This page provides best-practice guidance on creating databases and user-defined schemas. We briefly discuss syntax and best practices, and then we provide a simple tutorial.

As a general best practice, we discourage the use of client libraries to execute [database schema changes](online-schema-changes.html), including creating databases and user-defined schemas. Instead, use a database schema migration tool, or the [CockroachDB SQL client](cockroach-sql.html). In this guide, we write our database schema definitions in a SQL file, and then pass the file to the SQL client for execution.

## Creating databases

To create a database in a cluster, use a `CREATE DATABASE` statement.

Here are some best practices to follow when creating a database:

- Do not use the `defaultdb` database. Instead, create your own database with a `CREATE DATABASE` statement.
- Create databases as the `admin` user, and assign user privileges to lower-level objects as needed.
- Limit the number of databases you create. If you need to create multiple tables with the same name in your cluster, do so in different user-defined schemas in the same database.
- Use the `IF NOT EXISTS` keyword to avoid errors.

For reference documentation on this statement, including additional examples, see the [`CREATE DATABASE` syntax page](create-database.html).

## Creating user-defined schemas

To create a user-defined schema in a database, use a `CREATE SCHEMA` statement.

Here are some best practices to follow for creating user-defined schemas:

- Do not use the `public` schema. Instead, create a user-defined schema with `CREATE SCHEMA`.
- When naming a user-defined schema, use the fully-qualified name (e.g., `database.schema`).
- When you create a user-defined schema, take note of the owner. You can specify the owner with the `AUTHORIZATION` keyword. If `AUTHORIZATION` is not specified, the owner will be the creator.

For detailed reference documentation on this statement, including additional examples, see the [`CREATE SCHEMA` syntax page](create-schema.html).

## Create a SQL file to initialize your database schema

Create an empty file with the `.sql` file extension at the end of the filename. For example:

{% include copy-clipboard.html %}
~~~ shell
$ touch dbinit.sql
~~~

Open `dbinit.sql` in a text editor of your choice, and add a [`CREATE DATABASE`](create-database.html) statement:

{% include copy-clipboard.html %}
~~~
CREATE DATABASE IF NOT EXISTS cockroachlabs;
~~~

This statement will create a database object with the name `cockroachlabs`, if one does not currently exist. Note that if one does exist, no error will be returned.

To create a user-defined schema in the `cockroachlabs` database, add the following:

{% include copy-clipboard.html %}
~~~
CREATE SCHEMA IF NOT EXISTS cockroachlabs.movr;
~~~

This statement will create a user-defined schema named `movr` in the `cockroachlabs` database, if one does not already exist in `cockroachlabs`.

By default, CockroachDB uses a preloaded database named `defaultdb` as the default database for each session. If you did not specify the fully-qualified name (i.e., `database.schema`), CockroachDB will search the default database. You can specify the default database with a `USE <database>;` statement, in the CockroachDB connection string passed to a client, or with a `--database` flag passed to the `cockroach sql` command.

Note that you have schemas of the same name if they belong to different databases. For example, if we did not have the `USE cockroachlabs` statement,

## Execute statements from a SQL file

To execute the statements in the `dbinit.sql` file, pass the file to the [`cockroach sql`](cockroach-sql.html) command:

{% include copy-clipboard.html %}
~~~ shell
$ cockroach sql \
--user=root \
--database=cockroachlabs \
< dbinit.sql
~~~

To follow [authorization best practices](authorization.html#authorization-best-practices), we use the `root` user to create the database. We'll update the owner of the schema to the user

After you have executed the statements, you can see the database and schema in the SQL shell:

{% include copy-clipboard.html %}
~~~ shell
$ cockroach sql \
--user=root \
--database=cockroachlabs \
~~~

To view the databases in the cluster, use a [`SHOW DATABASES`](show-databases.html) statement:

{% include copy-clipboard.html %}
~~~ sql
> SHOW DATABASES;
~~~

~~~
~~~

To view the user-defined schemas in the cluster, use a [`SHOW SCHEMAS`](show-schemas.html) statement:

{% include copy-clipboard.html %}
~~~ sql
> SHOW SCHEMAS;
~~~

~~~
~~~

You're now ready to start adding tables to the user-defined schema. For guidance on creating tables, start at [Define Columns in a Table](schema-design-columns.html).

## See also

- [`CREATE DATABASE`](create-database.html)

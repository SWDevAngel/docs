---
title: Create a Table
summary: Define tables for your database schema
toc: true
---

`CREATE TABLE` statements are among the most complex database schema creation statements. They contain explicit column definitions and constraints, and can also contain index definitions.

## Creating tables

To create a table in a schema, use a `CREATE TABLE` statement.

Here are some general best practices to follow when opening a `CREATE TABLE` statement:

- When naming the table, use the fully-qualified name (e.g., `CREATE TABLE database.schema.table`).

We'll start by [defining the columns in the table](#defining-columns).

For reference documentation on this statement, including additional examples, see the [`CREATE TABLE` syntax page](create-table.html).

## Define columns

To create a table, start by defining columns in the `CREATE TABLE` statement.

Here are some best practices to follow when defining a column:

- Review the supported column [data types](data-types.html), and select the appropriate type for the data you plan to store in the column, following the best practices listed on the data type's reference page.
- Use column data types with a fixed size limit, or set a maximum size limit on column data types of variable size (e.g., `VARBIT(n)`). Values exceeding 1MB can lead to [write amplification](https://en.wikipedia.org/wiki/Write_amplification) and cause significant performance degradation.  

## Select a primary key



## Add secondary constraints



## Add the `CREATE` statements

Open the `dbinit.sql` file that you created in [Create a Database and Schema](schema-design-database-schema.html), and add the following:

Before we execute the statements in the file, we need to [select our primary key columns](schema-design-primary-key.html) and then [add additional constraints](schema-design-constraints.html).

## See also



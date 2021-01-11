---
title: Database Schema Objects
summary: An overview of the objects that make up a logical schema
toc: true
---

This page provides an overview of the logical objects that make up a database schema in CockroachDB.

In later sections of the developer guide, we provide best practices for defining these objects in a way that optimizes performance and maximizes storage resources. For detailed documentation on object name resolution, see [Name Resolution](sql-name-resolution.html).

## Databases

Database objects make up the first level of the [CockroachDB naming hierarchy](sql-name-resolution.html#naming-hierarchy). They contain [schemas](#schemas).

To avoid confusion with the general term "[database](https://en.wikipedia.org/wiki/Database)", throughout this guide we refer to the logical object as a "database", to CockroachDB by name (i.e., "CockroachDB"), and to a deployment of CockroachDB as a "[cluster](architecture/overview.html#terms)".

For guidance on creating databases, see [Create a Database and User-defined Schema](schema-design-database-schema.html).

## Schemas

Schemas make up the second level of the naming hierarchy. They contain [tables](#tables), [indexes](#indexes), and other objects like [views](#views) and [sequences](#sequences). Each schema belongs to a single database.

By default, all objects in the third level of the naming hierarchy (e.g., tables and indexes) belong to the preloaded `public` schema. Rather than using the public schema, we recommend using a user-defined schema.

To avoid confusion with the general term "[schema](https://en.wiktionary.org/wiki/schema)", in this guide we refer to the logical object as a "user-defined schema", and to the relationship structure of logical objects in a cluster as a "database schema".

For guidance on creating user-defined schemas, see [Create a Database and User-defined Schema](schema-design-database-schema.html).

## Tables

Tables, along with all objects other than [user-defined schemas](#schemas) and [databases](#databases), make up the third and lowest level of the naming hierarchy. Each table can belong to a single user-defined schema. As stated before, all tables belong to the *public* schema by default.

Tables contain rows of data. Each record in a row belongs to a particular column, of a particular data type.

For guidance on defining tables and columns, see [Tables](schema-design-tables.html).

### Constraints

Constraints enforce conditions (e.g., [uniqueness](unique.html)) on the data in a column.

For guidance on defining constraints, see [Constraints](constraints.html).

## Indexes

Indexes improve performance by helping CockroachDB queries locate data without having to scan every row of a table. The two main types of indexes are the primary key index and the secondary index.

For guidance on defining primary keys, see [Select a Primary Key](schema-design-primary-key.html). For guidance on defining secondary indexes, see [Add a Secondary Index](schema-design-indexes.html).

### Specialized indexes

CockroachDB supports specialized types of indexes, designed to improve query performance in specific use cases. For guidance on specialized indexes, see the pages listed under [Advanced Schema Design](partial-indexes.html).

## Other objects

CockroachDB supports several other objects at the third level of the naming hierarchy, including reusable [views](#views), [sequences](#sequences), and [temporary objects](#temporary-objects).

### Views

A view is a stored and named selection query.

For guidance on using views, see []().

### Sequences

Sequences store sequential data.

For guidance on using sequences, see []().

### Temporary objects

A temporary object is an object, such as a table, view, or sequence, that is not stored to persistent memory.

For guidance on using temporary objects, see []().

## Control access to objects

CockroachDB supports both user-based and role-based access control. With roles, or with direct assignment, you can grant a [SQL user](authorization#sql-users) the [privileges](authorization,html#privileges) required to view, modify, and delete database schema objects or rows of data.

By default, the user that creates an object is that object's *owner*. [Object owners](authorization.html#object-ownership) have all privileges required to view, modify, or delete that object and the data stored within it. Throughout this guide, we assume that you are the owner of all objects in the database schema.

For more information about ownership, privileges, and authorization, see [Authorization](authorization.html).

## Third-party schema migration tools

As a best practice, we encourage you to create database schemas and perform and database schema changes for your application with one of the following methods:

- Use a schema migration tool.
    CockroachDB is compatible with most PostgreSQL database schema migration tools, including [Flyway](https://flywaydb.org/) and [Liquibase](https://www.liquibase.com). For a tutorial on performing database schema changes using Liquibase, see our [Liquibase tutorial](liquibase.html). For a tutorial on performing schema changes with Flyway, see our [Flyway tutorial](flyway.html).
    
- Pass a `.sql` file populated with SQL commands to the [CockroachDB SQL client](cockroach-sql.html#execute-sql-statements-from-a-file) for execution.
    Throughout this tutorial, we use this method to perform database schema changes, as it is applicable to all application frameworks.

- Issue the commands directly to the CockroachDB from the [CockroachDB SQL shell](cockroach-sql.html#sql-shell).

## See also

- [CockroachDB naming hierarchy](sql-name-resolution.html#naming-hierarchy)
- [Authorization](authorization.html)
- [Liquibase tutorial](liquibase.html)
- [Flyway](flyway.html)

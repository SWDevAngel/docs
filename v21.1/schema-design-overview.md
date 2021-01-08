---
title: Schema Design Overview
summary: An overview of the objects that make up a logical schema
toc: true
---

Database schemas define the relationship structure of the logical objects that store data in a CockroachDB deployment. This page provides an overview of the logical objects that make up a database schema. In later sections of the developer guide, we provide best practices for designing a schema that optimizes performance and maximizes storage resources. Throughout the schema design portion of the guide, we use a single-region version of the example [`movr` database](movr.html).

## Databases

Databases make up the first level of the [CockroachDB naming hierarchy](sql-name-resolution.html#naming-hierarchy). They contain schemas.

To avoid confusion with the general term "database", we refer to the logical object as a "database", to CockroachDB by name (i.e., "CockroachDB"), and to a deployment of CockroachDB as a "cluster".

## Schemas

Schemas make up the second level of the naming hierarchy. They contain tables, indexes, and other objects like views and sequences. Each schema belongs to a single database.

By default, all objects in the third level of the naming hierarchy (e.g., tables and indexes) belong to the preloaded *public schema*. Rather than using the public schema, we recommend defining your own schema.

To avoid confusion with the general term "schema", we refer to the logical object as a "user-defined schema", and to the relationship structure of logical objects in a cluster as a "database schema".

## Tables

Tables, along with all other objects that are not user-defined schemas and databases, make up the third and lowest level of the naming hierarchy. Each table belongs to a single user-defined schema.

Tables contain rows of data. Each record in a row belongs to a particular column in a table.

### Columns

Columns

### Constraints

Contraints

## Indexes

Indexes help

### Specialized indexes



## Other objects

### Views

### Sequences

### Temporary objects

## Authorization

## Use

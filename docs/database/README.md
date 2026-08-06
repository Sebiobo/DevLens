# DevLens Database Design

## 1. Overview

The DevLens database stores the persistent data required by the platform.

The database design is based on the domain model defined in
`docs/domain-model.md`.

The initial database will use PostgreSQL.

For the initial development and deployment stages, Supabase will be
used as a managed PostgreSQL platform.

The database is responsible for storing application data such as users,
projects, repositories, analyses, analysis results, and reports.

Large files and repository artifacts will not be stored directly in
PostgreSQL. These files will be stored in object storage such as AWS S3,
while the database will store the metadata and references required to
access them.

## 2. Database Technology

### PostgreSQL

PostgreSQL is the primary relational database used by DevLens.

It was selected because it provides:

- strong relational data modeling;
- transactions and data consistency;
- mature indexing capabilities;
- support for complex queries;
- compatibility with Spring Data JPA and Hibernate;
- good scalability for the expected application workload.

### Supabase

Supabase will provide a managed PostgreSQL environment.

During early development, the application may use a local PostgreSQL
instance when necessary.

The application should remain database-platform independent enough that
the underlying PostgreSQL database can be accessed either locally or
through Supabase.

## 3. Core Entities

The initial database model contains the following core entities:

- User
- Project
- Repository
- Analysis
- Analysis Result
- Report

These entities correspond to the core concepts defined in the DevLens
domain model.

## 4. User

The `User` entity represents a person using the DevLens platform.

A user can own multiple projects.

Initial data may include:

- unique identifier;
- email;
- display name;
- authentication provider information;
- creation timestamp;
- last update timestamp.

Authentication-related data should be handled carefully and sensitive
credentials or secrets must not be stored directly unless required.

## 5. Project

The `Project` entity represents a logical workspace belonging to a user.

A project can contain multiple repositories.

Initial data may include:

- unique identifier;
- owner/user identifier;
- project name;
- description;
- creation timestamp;
- last update timestamp.

Relationship:

```text
User 1 ──────── N Project
```
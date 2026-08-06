# DevLens Domain Model

## 1. Overview

The DevLens domain model defines the core concepts, actors, and relationships
within the DevLens platform.

DevLens is designed to help developers analyze software repositories and
receive actionable insights about code quality, maintainability, security,
and other aspects of software development.

The domain model serves as a foundation for the backend architecture,
database design, and application features.

## 2. Actors

### Developer

The primary user of DevLens.

A developer can:
- create and manage projects;
- connect source code repositories;
- start repository analyses;
- view analysis results;
- review recommendations and insights.

### Git Repository Provider

An external service that hosts source code repositories.

The initial integration will target GitHub, while the architecture should
allow support for additional providers in the future.

### AI Provider

An external or internal AI service used to analyze relevant information
and generate insights and recommendations.

The application should abstract AI providers so that different models or
providers can be integrated without significantly changing the rest of
the system.

### Analysis Worker

A background component responsible for executing repository analysis tasks
asynchronously.

## 3. Core Entities

### User

Represents a person using the DevLens platform.

A user can own or have access to one or more projects.

### Project

Represents a logical workspace within DevLens.

A project groups repositories, analyses, and their associated results.

### Repository

Represents a source code repository connected to a DevLens project.

A repository contains the source code and metadata required for analysis.

### Analysis

Represents a single analysis execution performed against a repository.

An analysis has a lifecycle and can have states such as:

- Pending
- Running
- Completed
- Failed

An analysis produces one or more analysis results.

### Analysis Result

Represents the findings produced by an analysis.

Results may contain information related to:

- code quality;
- maintainability;
- security;
- architecture;
- potential issues;
- recommendations.

### Report

Represents a human-readable representation of analysis results.

A report may contain summaries, findings, recommendations, and other
information intended to help developers understand the state of their
repository.

## 4. Entity Relationships

The initial relationships between the core entities are:

```text
User
 │
 └── Project
       │
       └── Repository
              │
              └── Analysis
                    │
                    ├── Analysis Result
                    │
                    └── Report
```
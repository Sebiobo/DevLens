# DevLens API

## 1. Overview

The DevLens API provides a RESTful interface between the frontend
application and the backend services.

The API is responsible for exposing project management, repository
management, analysis execution, and analysis result functionality.

The API will use HTTP/HTTPS and JSON for communication.

## 2. API Versioning

The API will use URL-based versioning.

The initial API version is:

`/api/v1`

Example:

`GET /api/v1/projects`

## 3. Projects

### Create Project

`POST /api/v1/projects`

Creates a new project for the authenticated user.

### List Projects

`GET /api/v1/projects`

Returns the projects available to the authenticated user.

### Get Project

`GET /api/v1/projects/{projectId}`

Returns information about a specific project.

### Update Project

`PUT /api/v1/projects/{projectId}`

Updates an existing project.

### Delete Project

`DELETE /api/v1/projects/{projectId}`

Deletes a project.

## 4. Repositories

### List Project Repositories

`GET /api/v1/projects/{projectId}/repositories`

Returns the repositories associated with a project.

### Connect Repository

`POST /api/v1/projects/{projectId}/repositories`

Connects a repository to a project.

### Get Repository

`GET /api/v1/repositories/{repositoryId}`

Returns information about a repository.

### Remove Repository

`DELETE /api/v1/repositories/{repositoryId}`

Removes a repository from a project.

## 5. Analyses

### Start Analysis

`POST /api/v1/repositories/{repositoryId}/analyses`

Starts a new analysis for a repository.

The analysis should be processed asynchronously.

### List Analyses

`GET /api/v1/repositories/{repositoryId}/analyses`

Returns the analysis history for a repository.

### Get Analysis

`GET /api/v1/analyses/{analysisId}`

Returns the current status and information about an analysis.

Possible analysis states:

- Pending
- Running
- Completed
- Failed

## 6. Reports

### Get Analysis Report

`GET /api/v1/analyses/{analysisId}/report`

Returns the report generated from an analysis.

## 7. Health

### Health Check

`GET /api/v1/health`

Returns the current health status of the backend service.

Example response:

```json
{
  "status": "UP"
}
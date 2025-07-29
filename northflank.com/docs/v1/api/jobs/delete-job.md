---
source_url: https://northflank.com/docs/v1/api/jobs/delete-job
title: Delete job | Jobs | Northflank API docs
crawl_date: 2025-07-29T10:04:45.796830
watsonmd_version: 0.1.0
---

Jobs / 

# Delete job

Deletes the given job.

Required permission

Project > Jobs > General > Delete

Path parameters

    * projectId

string required

ID of the project

    * jobId

string required

ID of the job




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

DELETE /v1/projects/{projectId}/jobs/{jobId}

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }
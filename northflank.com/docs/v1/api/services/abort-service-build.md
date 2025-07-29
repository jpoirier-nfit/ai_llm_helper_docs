---
source_url: https://northflank.com/docs/v1/api/services/abort-service-build
title: Abort service build | Services | Northflank API docs
crawl_date: 2025-07-29T09:57:23.532874
watsonmd_version: 0.1.0
---

Services / 

# Abort service build

Aborts the given service build

Required permission

Project > Services > Deployment > Deploy Build

Path parameters

    * projectId

string required

ID of the project

    * serviceId

string required

ID of the service

    * buildId

string required

ID of the service build




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

DELETE /v1/projects/{projectId}/services/{serviceId}/build/{buildId}

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }
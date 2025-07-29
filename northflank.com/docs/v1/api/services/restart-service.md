---
source_url: https://northflank.com/docs/v1/api/services/restart-service
title: Restart service | Services | Northflank API docs
crawl_date: 2025-07-29T10:02:17.022965
watsonmd_version: 0.1.0
---

Services / 

# Restart service

Restarts the given service.

Required permission

Project > Services > General > Update

Path parameters

    * projectId

string required

ID of the project

    * serviceId

string required

ID of the service




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

POST /v1/projects/{projectId}/services/{serviceId}/restart

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }
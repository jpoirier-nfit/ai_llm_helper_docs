---
source_url: https://northflank.com/docs/v1/api/services/delete-service
title: Delete service | Services | Northflank API docs
crawl_date: 2025-07-29T09:24:13.035526
watsonmd_version: 0.1.0
---

Services / 

# Delete service

Deletes the given service.

Required permission

Project > Services > General > Delete

Path parameters

    * projectId

string required

ID of the project

    * serviceId

string required

ID of the service




Query parameters

    * delete_child_objects

boolean

If true, any volumes attached to this service will also be deleted.




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

DELETE /v1/projects/{projectId}/services/{serviceId}

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }
---
source_url: https://northflank.com/docs/v1/api/projects/delete-project
title: Delete project | Projects | Northflank API docs
crawl_date: 2025-07-29T10:44:49.593202
watsonmd_version: 0.1.0
---

Projects / 

# Delete project

Delete the given project. Fails if the project isn't empty.

Required permission

Project > Projects > Manage > Delete

Path parameters

    * projectId

string required

ID of the project




Query parameters

    * delete_child_objects

boolean

If true, resources belonging to this project will be deleted. Otherwise, an error will be returned if the project is not empty.




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

DELETE /v1/projects/{projectId}

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }

Example response

409 Conflict

The project couldn't be deleted as it has dependencies that have not been deleted
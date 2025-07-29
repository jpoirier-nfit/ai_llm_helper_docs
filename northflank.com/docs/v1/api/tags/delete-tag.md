---
source_url: https://northflank.com/docs/v1/api/tags/delete-tag
title: Delete tag | Tags | Northflank API docs
crawl_date: 2025-07-29T10:44:51.092594
watsonmd_version: 0.1.0
---

Tags / 

# Delete tag

Delete a resource tag.

Required permission

Account > Tags > General > Delete

Path parameters

    * resourceTagId

string required

ID of the tag




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

DELETE /v1/tags/{resourceTagId}

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }
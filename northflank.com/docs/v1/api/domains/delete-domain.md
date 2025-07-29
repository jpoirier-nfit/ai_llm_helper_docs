---
source_url: https://northflank.com/docs/v1/api/domains/delete-domain
title: Delete domain | Domains | Northflank API docs
crawl_date: 2025-07-29T10:04:44.323183
watsonmd_version: 0.1.0
---

Domains / 

# Delete domain

Deletes a domain and each of its registered subdomains.

Required permission

Account > Domains > General > Delete

Path parameters

    * domain

string required

Name of the domain




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

DELETE /v1/domains/{domain}

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }
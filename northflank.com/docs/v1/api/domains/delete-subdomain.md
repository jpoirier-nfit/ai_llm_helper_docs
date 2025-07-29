---
source_url: https://northflank.com/docs/v1/api/domains/delete-subdomain
title: Delete subdomain | Domains | Northflank API docs
crawl_date: 2025-07-29T10:04:44.401806
watsonmd_version: 0.1.0
---

Domains / 

# Delete subdomain

Removes a subdomain from a domain.

Required permission

Account > Subdomains > General > Update

Path parameters

    * domain

string required

Name of the domain

    * subdomain

string required

Name of the subdomain




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

DELETE /v1/domains/{domain}/subdomains/{subdomain}

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }

Example response

400 Bad Request

The default (empty) subdomain cannot be deleted.

Example response

404 Not Found

The subdomain does not exist.
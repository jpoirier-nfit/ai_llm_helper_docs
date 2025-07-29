---
source_url: https://northflank.com/docs/v1/api/domains/verify-domain
title: Verify domain | Domains | Northflank API docs
crawl_date: 2025-07-29T09:24:14.733354
watsonmd_version: 0.1.0
---

Domains / 

# Verify domain

Attempts to verify the domain

Required permission

Account > Domains > General > Create

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

POST /v1/domains/{domain}/verify

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }

Example response

400 Bad Request

Failed to verify the domain.
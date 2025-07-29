---
source_url: https://northflank.com/docs/v1/api/domains/verify-subdomain
title: Verify subdomain | Domains | Northflank API docs
crawl_date: 2025-07-29T10:02:17.537190
watsonmd_version: 0.1.0
---

Domains / 

# Verify subdomain

Gets details about the given subdomain

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

POST /v1/domains/{domain}/subdomains/{subdomain}/verify

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }

Example response

400 Bad Request

Failed to verify the subdomain.
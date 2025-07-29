---
source_url: https://northflank.com/docs/v1/api/domains/unassign-subdomain
title: Unassign subdomain | Domains | Northflank API docs
crawl_date: 2025-07-29T09:24:14.506835
watsonmd_version: 0.1.0
---

Domains / 

# Unassign subdomain

Removes a subdomain from its assigned service

Required permission

Account > Subdomains > General > Update

Path parameters

    * domain

string required

Name of the domain

    * subdomain

string required

Name of the subdomain




Query parameters

    * unassignPaths

boolean

Unassign all associated subdomain paths from their respective services.




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

DELETE /v1/domains/{domain}/subdomains/{subdomain}/assign

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }
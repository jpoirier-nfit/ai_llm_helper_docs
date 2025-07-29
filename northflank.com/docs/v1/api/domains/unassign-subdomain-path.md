---
source_url: https://northflank.com/docs/v1/api/domains/unassign-subdomain-path
title: Unassign subdomain path | Domains | Northflank API docs
crawl_date: 2025-07-29T09:57:24.354416
watsonmd_version: 0.1.0
---

Domains / 

# Unassign subdomain path

Unassign a subdomain path to a port.

Required permission

Account > SubdomainPaths > General > Update

Path parameters

    * domain

string required

Name of the domain

    * subdomain

string required

Name of the subdomain

    * subdomainPath

string required

Name of the path




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

DELETE /v1/domains/{domain}/subdomains/{subdomain}/paths/{subdomainPath}/assign

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }
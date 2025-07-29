---
source_url: https://northflank.com/docs/v1/api/domains/import-domain-certificate
title: Import domain certificate | Domains | Northflank API docs
crawl_date: 2025-07-29T10:04:44.342418
watsonmd_version: 0.1.0
---

Domains / 

# Import domain certificate

Import a certificate for the domain

Required permission

Account > Domains > General > Update

Path parameters

    * domain

string required

Name of the domain




Request body

  * {object}

    * certificate

{object} required

Certificate to import.

      * privateKey

string required

Certificate private key.

      * certificateChain

string required

Certificate chain. May consist of one or more certificates.




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

POST /v1/domains/{domain}/import

Example request

Request body

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data 'undefined' \
      https://api.northflank.com/v1/domains/{domain}/import

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }

Example response

400 Bad Request

Could not parse certificate.

Example response

409 Conflict

Expiry date must be at least one month in the future.
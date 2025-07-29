---
source_url: https://northflank.com/docs/v1/api/domains/remove-cdn-from-a-subdomain
title: Remove CDN from a subdomain | Domains | Northflank API docs
crawl_date: 2025-07-29T09:24:14.515266
watsonmd_version: 0.1.0
---

Domains / 

# Remove CDN from a subdomain

Removes the CDN integration from the given subdomain

Required permission

Account > Subdomains > General > Update

Path parameters

    * domain

string required

Name of the domain

    * subdomain

string required

Name of the subdomain




Request body

  * {object}

    * provider

string required

Provider for which the CDN on the subdomain should be disabled.




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

POST /v1/domains/{domain}/subdomains/{subdomain}/cdn/disable

Example request

Request body

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"provider":"cloudfront"}' \
      https://api.northflank.com/v1/domains/{domain}/subdomains/{subdomain}/cdn/disable

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }
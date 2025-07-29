---
source_url: https://northflank.com/docs/v1/api/domains/assign-service-to-subdomain
title: Assign service to subdomain | Domains | Northflank API docs
crawl_date: 2025-07-29T10:04:44.413925
watsonmd_version: 0.1.0
---

Domains / 

# Assign service to subdomain

Assigns a service port to the given subdomain

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

    * serviceId

string required

The ID of the service to assign the subdomain to.

pattern

^[A-Za-z0-9-]+$

    * projectId

string required

The ID of the project the service belongs to.

pattern

^[A-Za-z0-9-]+$

    * portName

string required

The name of the port that will be assigned to the subdomain.

min length

1

max length

8

pattern

^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

POST /v1/domains/{domain}/subdomains/{subdomain}/assign

Example request

Request body

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"serviceId":"example-service","projectId":"default-project","portName":"p01"}' \
      https://api.northflank.com/v1/domains/{domain}/subdomains/{subdomain}/assign

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }
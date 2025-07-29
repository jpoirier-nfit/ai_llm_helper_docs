---
source_url: https://northflank.com/docs/v1/api/domains/assign-subdomain-path
title: Assign subdomain path | Domains | Northflank API docs
crawl_date: 2025-07-29T09:24:14.716041
watsonmd_version: 0.1.0
---

Domains / 

# Assign subdomain path

Assign a subdomain path to a port.

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




Request body

  * {object}

    * assignment

{object} required

Data about the subdomain path assignment.

      * project

string required

The ID of the service to assign the subdomain path to.

min length

3

max length

39

pattern

^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

      * service

string required

The ID of the project the service belongs to.

min length

3

max length

39

pattern

^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

      * port

string required

The name of the port that will be assigned to the subdomain path.




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

POST /v1/domains/{domain}/subdomains/{subdomain}/paths/{subdomainPath}/assign

Example request

Request body

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"assignment":{"project":"default-project","service":"example-service","port":"p01"}}' \
      https://api.northflank.com/v1/domains/{domain}/subdomains/{subdomain}/paths/{subdomainPath}/assign

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }
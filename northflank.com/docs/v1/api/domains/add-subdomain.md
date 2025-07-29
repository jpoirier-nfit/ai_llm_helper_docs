---
source_url: https://northflank.com/docs/v1/api/domains/add-subdomain
title: Add subdomain | Domains | Northflank API docs
crawl_date: 2025-07-29T09:24:13.777454
watsonmd_version: 0.1.0
---

Domains / 

# Add subdomain

Adds a new subdomain to the domain.

Required permission

Account > Subdomains > General > Update

Path parameters

    * domain

string required

Name of the domain




Request body

  * {object}

    * subdomain

string required

A subdomain to be added.

pattern

^\\*|^@$|^([0-9a-z]([0-9a-z\\-]*[0-9a-z])?\\.)*[0-9a-z]([0-9a-z\\-]*[0-9a-z])?$

    * cdn

{object}

Optional CDN configuration. Currently only available for select users.

      * cloudfront

{object}

        * enabled

boolean required

    * options

{object}

Optional advanced configuration for the subdomain

      * tlsMode

string

Desired TLS mode for the subdomain.

one of

default, passthrough




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * recordType

string required

The record type to use for the DNS record to verify the subdomain - always CNAME for subdomains.

      * name

string required

The subdomain.

      * fullName

string required

The full domain name with subdomain

      * content

string required

The content to set the DNS record to

      * verified

boolean required

Whether the subdomain has been verified successfully and can be used.




API

CLI

JS Client

POST /v1/domains/{domain}/subdomains

Example request

Request body

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"subdomain":"site"}' \
      https://api.northflank.com/v1/domains/{domain}/subdomains

Example response

200 OK

Details about the newly added subdomain.

JSON
    
    
    {
      "data": {
        "recordType": "CNAME",
        "name": "site",
        "fullName": "site.example.com",
        "content": "site.example.com.user-1234.dns.northflank.app",
        "verified": false
      }
    }

Example response

400 Bad Request

The subdomain is not valid (possibly because it is too long) or the domain has not been verified.

Example response

409 Conflict

The subdomain has already been added to this domain.
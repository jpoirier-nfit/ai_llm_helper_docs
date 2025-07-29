---
source_url: https://northflank.com/docs/v1/api/domains/list-domains
title: List domains | Domains | Northflank API docs
crawl_date: 2025-07-29T10:04:44.273705
watsonmd_version: 0.1.0
---

Domains / 

# List domains

Lists available domains

Required permission

Account > Domains > General > Read

Query parameters

    * per_page

integer

The number of results to display per request. Maximum of 100 results per page.

    * page

integer

The page number to access.

    * cursor

string

The cursor returned from the previous page of results, used to request the next page.




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * domains

[array] required

A list of domains registered to this account.

        * {object}

Details about a domain.

          * name

string required

The domain name.

          * status

string required

The status of the domain verification.

one of

pending, verified

          * hostname

string required

The hostname to add to your domain's DNS records as a TXT record to verify the domain.

          * token

string required

The token to add as the content of the TXT record to verify the domain.

    * pagination

{object} required

Data about the endpoint pagination.

      * hasNextPage

boolean required

Is there another page of results available?

      * cursor

string

The cursor to access the next page of results.

      * count

number required

The number of results returned by this request.




API

CLI

JS Client

GET /v1/domains

Example response

200 OK

A list of domains registered to this account.

JSON
    
    
    {
      "data": {
        "domains": [
          {
            "name": "example.com",
            "status": "verified",
            "hostname": "nfverify1608026055",
            "token": "e596987b52855a4a773ef580ce2985d7746b37ce8b2a443d20fa27b913d8f57"
          }
        ]
      },
      "pagination": {
        "hasNextPage": false,
        "count": 1
      }
    }
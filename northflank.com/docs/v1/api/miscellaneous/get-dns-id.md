---
source_url: https://northflank.com/docs/v1/api/miscellaneous/get-dns-id
title: Get DNS ID | Miscellaneous | Northflank API docs
crawl_date: 2025-07-29T10:44:49.480877
watsonmd_version: 0.1.0
---

Miscellaneous / 

# Get DNS ID

Returns the partially random string used when generating host names for the authenticated account.

Required permission

Project > Projects > Manage > Read

Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * dns

string required

The partially random string associated with the authenticated account, used for generating DNS entries.




API

CLI

JS Client

GET /v1/dns-id

Example response

200 OK

Data about the DNS ID.

JSON
    
    
    {
      "data": {
        "dns": "exam-1234"
      }
    }
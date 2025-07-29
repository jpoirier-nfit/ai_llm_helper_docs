---
source_url: https://northflank.com/docs/v1/api/miscellaneous/list-regions
title: List regions | Miscellaneous | Northflank API docs
crawl_date: 2025-07-29T10:44:49.387335
watsonmd_version: 0.1.0
---

Miscellaneous / 

# List regions

Lists available project regions

Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * regions

[array] required

An array of regions

        * {object}

A region object

          * id

string required

The ID of the region.




API

CLI

JS Client

GET /v1/regions

Example response

200 OK

A list of available regions.

JSON
    
    
    {
      "data": {
        "regions": [
          {
            "id": "europe-west"
          }
        ]
      }
    }
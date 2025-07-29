---
source_url: https://northflank.com/docs/v1/api/cloud-providers/list-provider-regions
title: List provider regions | Cloud Providers | Northflank API docs
crawl_date: 2025-07-29T10:44:52.292170
watsonmd_version: 0.1.0
---

Cloud Providers / 

# List provider regions

Lists supported cloud provider regions

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

    * provider

string

If provided, only returns items belonging to this cloud provider.




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * providers

[array] required

An array of supported cloud provider regions

        * {object}

A provider region object

          * id

string required

The ID of the region

          * name

string required

The name of the region

          * availabilityZones

[array] required

The availability zones belonging to this region

            * {object}

              * id

string required

The id of the availability zone

              * name

string required

The name of the availability zone




API

CLI

JS Client

GET /v1/cloud-providers/regions

Example response

200 OK

A list of supported cloud provider regions.

JSON
    
    
    {
      "data": {
        "providers": [
          {
            "id": "europe-west1",
            "name": "europe-west1",
            "availabilityZones": [
              {
                "id": "europe-west1-b",
                "name": "europe-west1-b"
              }
            ]
          }
        ]
      }
    }
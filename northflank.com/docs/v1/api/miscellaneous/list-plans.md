---
source_url: https://northflank.com/docs/v1/api/miscellaneous/list-plans
title: List plans | Miscellaneous | Northflank API docs
crawl_date: 2025-07-29T10:44:49.397167
watsonmd_version: 0.1.0
---

Miscellaneous / 

# List plans

Lists available billing plans

Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * plans

[array] required

An array of available plans

        * {object}

A plan object

          * id

string required

The ID of the plan.

          * name

string required

The name of the plan.

          * currency

string required

The currency code of the currency used by this plan.

          * amountPerMonth

number required

The approximate monthly (30 days) cost of the plan.

          * amountPerHour

number required

The hourly cost of the plan.

          * cpuResource

number required

The CPU resource of the plan, in vCPUs.

          * ramResource

number required

The memory resource of the plan, in megabytes




API

CLI

JS Client

GET /v1/plans

Example response

200 OK

A list of available plans.

JSON
    
    
    {
      "data": {
        "plans": [
          {
            "id": "nf-compute-20",
            "name": "nf-compute-20",
            "currency": "usd",
            "amountPerMonth": 4.4,
            "amountPerHour": 0.0061,
            "cpuResource": 0.2,
            "ramResource": 512
          }
        ]
      }
    }
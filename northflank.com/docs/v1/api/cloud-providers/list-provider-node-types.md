---
source_url: https://northflank.com/docs/v1/api/cloud-providers/list-provider-node-types
title: List provider node types | Cloud Providers | Northflank API docs
crawl_date: 2025-07-29T10:44:52.320855
watsonmd_version: 0.1.0
---

Cloud Providers / 

# List provider node types

Lists supported cloud provider node types

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

    * region

string

If provided, only returns items available in this region.

    * family

string

If provided, only returns items of this family.

    * maxGenerationAge

integer

If provided, only returns items with a generation age less than or equal to the number given.

    * hasGpu

boolean

If true, only returns items with GPUs. If false, only returns items without GPUs.




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * providers

[array] required

An array of supported cloud provider node types

        * {object}

A provider node type object

          * id

string required

The ID of the node type

          * name

string required

The name of the node type

          * resources

{object} required

An listing the resources of this node type

            * vcpu

integer

Number of vCPU of this node type

            * memory

integer

Amount of memory capacity in GB of this node type

          * family

string required

Family of the node type

          * processorFamily

string required

Processor family of the node type

          * workloadType

string required

Workload this node type is optimized for




API

CLI

JS Client

GET /v1/cloud-providers/node-types

Example response

200 OK

A list of supported cloud provider node types.

JSON
    
    
    {
      "data": {
        "providers": [
          {
            "id": "n2-standard-8",
            "name": "n2-standard-8",
            "resources": {
              "vcpu": 8,
              "memory": 32
            },
            "family": "N",
            "processorFamily": "intel",
            "workloadType": "general-purpose"
          }
        ]
      }
    }
---
source_url: https://northflank.com/docs/v1/api/cloud-providers/list-cluster-nodes
title: List cluster nodes | Cloud Providers | Northflank API docs
crawl_date: 2025-07-29T10:44:52.774916
watsonmd_version: 0.1.0
---

Cloud Providers / 

# List cluster nodes

Get a list of nodes for the given cluster

Required permission

Account > Cloud > Clusters > Read

Path parameters

    * clusterId

string required

ID of the cluster




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

    * status

string

Filter the node list by state of the nodes.

one of

RUNNING, DELETED




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * nodes

[array] required

An array of nodes.

        * {object}

A node object.

          * nodeId

string

The id of the node.

          * nodeName

string

The name of the node.

          * nodePool

string

The node pool the node is a part of.

          * status

string

The status of the node.

          * zone

string

The zone the node is running in.

          * region

string

The region the node is running in.

          * instanceType

string

The type of the node.

          * createdAt

string

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

GET /v1/cloud-providers/clusters/{clusterId}/nodes

Example response

200 OK

List of nodes for the given cluster.

JSON
    
    
    {
      "data": {
        "nodes": [
          {
            "nodeId": "87a11ea9-3493-40d3-9f50-280c1d7c77a3",
            "nodeName": "gke-nf-example-cluster-nf-951dfaf6-a70a-7697bc0d-n771",
            "nodePool": "nf-951dfaf6-a70a-4550-bab6-b5364d5da20c",
            "status": "RUNNING",
            "zone": "us-central1-c",
            "region": "us-central1",
            "instanceType": "n2-standard-4",
            "createdAt": "2000-01-01T12:00:00.000Z"
          }
        ]
      },
      "pagination": {
        "hasNextPage": false,
        "count": 1
      }
    }
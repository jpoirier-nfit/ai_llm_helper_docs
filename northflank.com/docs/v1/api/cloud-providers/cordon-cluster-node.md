---
source_url: https://northflank.com/docs/v1/api/cloud-providers/cordon-cluster-node
title: Cordon cluster node | Cloud Providers | Northflank API docs
crawl_date: 2025-07-29T10:44:52.755000
watsonmd_version: 0.1.0
---

Cloud Providers / 

# Cordon cluster node

Cordon a node on the cluster to prevent new pods from scheduling on it.

Required permission

Account > Cloud > Clusters > Update

Path parameters

    * clusterId

string required

ID of the cluster

    * nodeId

string required

ID of the node




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

POST /v1/cloud-providers/clusters/{clusterId}/nodes/{nodeId}/cordon

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }
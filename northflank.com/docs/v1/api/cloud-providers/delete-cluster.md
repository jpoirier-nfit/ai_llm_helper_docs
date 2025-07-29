---
source_url: https://northflank.com/docs/v1/api/cloud-providers/delete-cluster
title: Delete cluster | Cloud Providers | Northflank API docs
crawl_date: 2025-07-29T10:44:52.797292
watsonmd_version: 0.1.0
---

Cloud Providers / 

# Delete cluster

Delete the given cluster. Fails if the cluster has associated projects.

Required permission

Account > Cloud > Clusters > Delete

Path parameters

    * clusterId

string required

ID of the cluster




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

DELETE /v1/cloud-providers/clusters/{clusterId}

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }

Example response

409 Conflict

The cluster couldn't be deleted as it has dependencies that have not been deleted
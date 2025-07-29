---
source_url: https://northflank.com/docs/v1/api/cloud-providers/delete-integration
title: Delete integration | Cloud Providers | Northflank API docs
crawl_date: 2025-07-29T10:44:52.347417
watsonmd_version: 0.1.0
---

Cloud Providers / 

# Delete integration

Delete the given integration. Fails if the integration is associated with existing clusters.

Required permission

Account > Cloud > Integrations > Delete

Path parameters

    * integrationId

string required

ID of the provider integration




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

DELETE /v1/cloud-providers/integrations/{integrationId}

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }

Example response

409 Conflict

The integration couldn't be deleted as it has dependencies that have not been deleted
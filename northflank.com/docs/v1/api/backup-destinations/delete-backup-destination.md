---
source_url: https://northflank.com/docs/v1/api/backup-destinations/delete-backup-destination
title: Delete backup destination | Backup Destinations | Northflank API docs
crawl_date: 2025-07-29T10:44:49.599032
watsonmd_version: 0.1.0
---

Backup Destinations / 

# Delete backup destination

Delete a backup destination.

Required permission

Account > BackupDestinations > General > Delete

Path parameters

    * backupDestinationId

string required

ID of the backup destination




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

DELETE /v1/backup-destinations/{backupDestinationId}

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }
---
source_url: https://northflank.com/docs/v1/api/backup-destinations/patch-backup-destination
title: Patch backup destination | Backup Destinations | Northflank API docs
crawl_date: 2025-07-29T10:44:49.634312
watsonmd_version: 0.1.0
---

Backup Destinations / 

# Patch backup destination

Updates a backup destination.

Required permission

Account > BackupDestinations > General > Update

Path parameters

    * backupDestinationId

string required

ID of the backup destination




Request body

  * {object}

    * name

string

The name of the backup destination.

min length

3

max length

100

pattern

^[a-zA-Z0-9]+((-|\s)[a-zA-Z0-9]+)*$

    * description

string

max length

200

pattern

^[a-zA-Z0-9.,?\s\\\/'"()[\\];`%^&*\\-_:!]+$

    * credentials

{object}

Credentials used for the backup destination.

      * accessKey

string required

      * secretKey

string required

      * bucketName

string required

      * region

string required

      * endpoint

string required

S3 destination including region, fe s3.us-west-2.amazonaws.com




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

PATCH /v1/backup-destinations/{backupDestinationId}

Example request

Request body

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request PATCH \
      --data '{"name":"Example Backup Destination"}' \
      https://api.northflank.com/v1/backup-destinations/{backupDestinationId}

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }
---
source_url: https://northflank.com/docs/v1/api/backup-destinations/add-backup-destination
title: Add backup destination | Backup Destinations | Northflank API docs
crawl_date: 2025-07-29T10:44:49.887684
watsonmd_version: 0.1.0
---

Backup Destinations / 

# Add backup destination

Adds a new backup destination to this account.

Required permission

Account > BackupDestinations > General > Create

Request body

  * {object}

    * name

string required

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

    * type

string required

Type of the backup destination.

one of

s3

    * prefix

string required

A prefix path to add to the bucket objects if not writing to /

pattern

^([a-zA-Z0-9-_]+)\/$

    * credentials

{object} required

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

      * name

string required

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

      * type

string required

Type of the backup destination.

one of

s3

      * prefix

string required

A prefix path to add to the bucket objects if not writing to /

pattern

^([a-zA-Z0-9-_]+)\/$

      * credentials

{object} required

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

      * id

string required

Identifier for the backup destination

      * createdAt

string

time of creation

      * updatedAt

string

time of update




API

CLI

JS Client

POST /v1/backup-destinations

Example request

Request body

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"name":"Example Backup Destination"}' \
      https://api.northflank.com/v1/backup-destinations

Example response

200 OK

Data about the newly created backup destination.

JSON
    
    
    {
      "data": {
        "name": "Example Backup Destination",
        "id": "example-backup-destination"
      }
    }
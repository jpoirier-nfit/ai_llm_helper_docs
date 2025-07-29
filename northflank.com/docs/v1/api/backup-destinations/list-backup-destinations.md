---
source_url: https://northflank.com/docs/v1/api/backup-destinations/list-backup-destinations
title: List backup destinations | Backup Destinations | Northflank API docs
crawl_date: 2025-07-29T10:44:50.007111
watsonmd_version: 0.1.0
---

Backup Destinations / 

# List backup destinations

Lists the backup destinations saved to this account. Does not display secrets.

Required permission

Account > BackupDestinations > General > Read

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




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * backupDestinations

[array] required

List of backup destinations.

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

GET /v1/backup-destinations

Example response

200 OK

A list of backup destination saved to this account.

JSON
    
    
    {
      "data": {
        "backupDestinations": [
          {
            "name": "Example Backup Destination"
          }
        ]
      },
      "pagination": {
        "hasNextPage": false,
        "count": 1
      }
    }
---
source_url: https://northflank.com/docs/v1/api/backup-destinations/list-destinations-backups
title: List destinations backups | Backup Destinations | Northflank API docs
crawl_date: 2025-07-29T10:44:49.586100
watsonmd_version: 0.1.0
---

Backup Destinations / 

# List destinations backups

Lists the backups associated with a backup destinations.

Required permission

Account > BackupDestinations > General > Read

Path parameters

    * backupDestinationId

string required

ID of the backup destination




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

[array] required

Result data.

      * {object}

Data about a backup.

        * id

string required

The identifier for the backup.

        * name

string required

The name of the backup.

        * status

string required

The current status of the backup.

one of

scheduled, in-progress, completed, aborting, aborted, failed, not-supported

        * project

{object}

          * id

string required

ID of the project this backup was taken for

          * name

string required

Name of the project this backup was taken for

        * addon

{object}

          * id

string required

ID of the addon this backup was taken for

          * name

string required

Name of the addon this backup was taken for

        * config

{object} required

Data about the backup configuration.

          * addonVersion

string

The version of the addon at the time of the backup. The addon will be restored to this version when the backup is restored.

          * addonType

string

The type of the addon this backup was taken for.

          * source

{object}

Data about the source of the backup.

            * type

string

The type of backup.

one of

global

          * size

string required

The size of the backup, in bytes

        * schedules

[array]

The schedules this backup was taken for.

          * {object}

            * interval

string required

The interval between backups. Each addon can only have one backup schedule of each interval for each backup type.

one of

hourly, daily, weekly

            * minute

[array] required

An array of minutes when the backup should be performed.

              * integer

A minute when the backup should be performed.

min

0

max

59

            * hour

[array]

An array of hours in 24 hour format when the backup should be performed. At these hours, a backup will be performed at each of the minutes provided in the `minute` field. Required for `daily` and `weekly` intervals and unavailable for `hourly` intervals.

              * integer

An hour when the backup should be performed, in 24 hour format.

min

0

max

23

            * day

[array]

An array of days of the week when the backup should be performed, where `0` represents Monday and `6` represents Sunday. On these days, a backup will be performed at each of the minutes provided in the `minute` field whenever it is an hour from the `hour` field. Required for `weekly` intervals and unavailable for `hourly` and `daily` intervals.

              * integer

A day of the week when the backup should be performed, where `0` represents Monday and `6` represents Sunday.

min

0

max

6

        * expiredBy

number required

The time the backup will expiry.

        * createdAt

string required

The time the backup was initiated.

        * completedAt

string required

The time the backup was completed.

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

GET /v1/backup-destinations/{backupDestinationId}/backups

Example response

200 OK

A list of backups saved to this backup destination.

JSON
    
    
    {
      "data": [
        {
          "id": "example-backup",
          "name": "Example Backup",
          "status": "completed",
          "project": {
            "id": "example-project",
            "name": "Example Project"
          },
          "addon": {
            "id": "example-addon",
            "name": "Example Addon"
          },
          "config": {
            "addonVersion": "4.4.8",
            "addonType": "mongodb",
            "source": {
              "type": "global"
            },
            "size": "1234"
          },
          "schedules": [
            {
              "interval": "weekly",
              "minute": [
                30
              ],
              "hour": [
                18
              ],
              "day": [
                4
              ]
            }
          ],
          "expiredBy": "1729232400000.0",
          "createdAt": "2021-01-20T11:19:53.175Z",
          "completedAt": "2021-01-20T11:19:54.494Z"
        }
      ],
      "pagination": {
        "hasNextPage": false,
        "count": 1
      }
    }
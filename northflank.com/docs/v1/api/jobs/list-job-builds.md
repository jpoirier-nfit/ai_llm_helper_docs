---
source_url: https://northflank.com/docs/v1/api/jobs/list-job-builds
title: List job builds | Jobs | Northflank API docs
crawl_date: 2025-07-29T10:04:45.832549
watsonmd_version: 0.1.0
---

Jobs / 

# List job builds

Lists builds for the given job.

Required permission

Project > Jobs > General > Read

Path parameters

    * projectId

string required

ID of the project

    * jobId

string required

ID of the job




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

      * builds

[array] required

An array of builds.

        * {object}

          * id

string required

ID of the build.

          * branch

string

Name of the branch the built commit belongs to.

          * pullRequestId

number

ID of the pull request the commit belongs to.

          * status

string

The status of the build.

one of

QUEUED, PENDING, UNSCHEDULABLE, STARTING, CLONING, BUILDING, UPLOADING, ABORTED, FAILURE, SUBMISSION_FAILURE, SUCCESS, CRASHED, IN_PROGRESS

          * sha

string

The sha of the built commit.

          * registry

{object}

            * uri

string

URI of that can be used to pull the image from the registry

          * concluded

boolean

Whether the build has finished.

          * createdAt

string

Timestamp of the build initiation.

          * success

boolean

Whether the build was successful.

          * message

string

Description of the build status.

          * buildConcludedAt

number

Timestamp of the build concluding.

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

GET /v1/projects/{projectId}/jobs/{jobId}/build

Example response

200 OK

Returns a list of builds for the given job.

JSON
    
    
    {
      "data": {
        "builds": [
          {
            "id": "joyous-view-6290",
            "branch": "main",
            "status": "SUCCESS",
            "sha": "12c15e7ee25fd78f567ebf87f9178b8ad70025b3",
            "concluded": true,
            "createdAt": "2021-07-28T15:55:38.296Z",
            "success": true,
            "message": "Image successfully built",
            "buildConcludedAt": 1606237973
          }
        ]
      },
      "pagination": {
        "hasNextPage": false,
        "count": 1
      }
    }
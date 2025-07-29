---
source_url: https://northflank.com/docs/v1/api/pipelines/list-release-flow-runs
title: List release flow runs | Pipelines | Northflank API docs
crawl_date: 2025-07-29T10:45:55.370748
watsonmd_version: 0.1.0
---

Pipelines / 

# List release flow runs

Lists runs of a release flow

Required permission

Project > Pipelines > General > Read

Path parameters

    * projectId

string required

ID of the project

    * pipelineId

string required

ID of the pipeline

    * stage

string required

Stage of the pipeline




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

      * runs

[array]

A release flow run

        * {object}

          * id

string required

ID of the release flow run

          * name

string

Optional name for the release flow run

          * description

string

Optional description for the release flow run

          * status

string required

Status of the template run

one of

pending, running, success, failure, aborted, aborting, queued, unknown, skipped

          * startedAt

string

Timestamp the run started at.

          * concluded

boolean required

Whether the run has concluded (aborted, success, failed)

          * concludedAt

string

Timestamp the run concluded at.

          * createdAt

string required

Timestamp the run was created at.

          * updatedAt

string required

Timestamp the run was last updated at.

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

GET /v1/projects/{projectId}/pipelines/{pipelineId}/release-flows/{stage}/runs

Example response

200 OK

A list of runs for this release flow.

JSON
    
    
    {
      "data": {
        "runs": [
          {
            "id": "110ddb52-bdcd-482d-8ac2-05ba580afe2f",
            "name": "Example run",
            "description": "This is an example description",
            "status": "success",
            "startedAt": "2021-01-01 12:01:00.000Z",
            "concluded": true,
            "concludedAt": "2021-01-01 12:10:00.000Z",
            "createdAt": "2021-01-01 12:00:00.000Z",
            "updatedAt": "2021-01-01 12:00:00.000Z"
          }
        ]
      },
      "pagination": {
        "hasNextPage": false,
        "count": 1
      }
    }
---
source_url: https://northflank.com/docs/v1/api/jobs/list-jobs
title: List jobs | Jobs | Northflank API docs
crawl_date: 2025-07-29T09:24:14.749762
watsonmd_version: 0.1.0
---

Jobs / 

# List jobs

Gets a list of jobs belonging to the project

Required permission

Project > Jobs > General > Read

Path parameters

    * projectId

string required

ID of the project




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

      * jobs

[array] required

An array of job objects.

        * {object}

          * id

string required

Identifier for the job

          * projectId

string required

ID of the project that the job belongs to

          * appId

string required

Full identifier used for job deployment

          * name

string required

Job name

          * tags

[array] required

An array of previously defined tags to help identify and group the resource.

            * string

min length

3

max length

100

pattern

^[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*$

          * description

string

A short description of the job

          * jobType

string required

Type of the job (manual or cron)

one of

manual, cron

          * disabledCI

boolean required

Whether Continuous Integration is disabled

          * disabledCD

boolean required

Whether Continuous Deployment is disabled

          * suspended

boolean

Cron specific. Whether or not the job's automatic scheduling is suspended

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

GET /v1/projects/{projectId}/jobs

Example response

200 OK

A list of jobs belonging to the project.

JSON
    
    
    {
      "data": {
        "jobs": [
          {
            "id": "example-job",
            "projectId": "default-project",
            "appId": "/example-user/default-project/example-job",
            "name": "Example Job",
            "description": "This is the job description",
            "jobType": "cron",
            "disabledCI": false,
            "disabledCD": false,
            "suspended": false
          }
        ]
      },
      "pagination": {
        "hasNextPage": false,
        "count": 1
      }
    }
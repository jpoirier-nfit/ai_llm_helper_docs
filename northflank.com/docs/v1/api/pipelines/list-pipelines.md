---
source_url: https://northflank.com/docs/v1/api/pipelines/list-pipelines
title: List pipelines | Pipelines | Northflank API docs
crawl_date: 2025-07-29T09:57:19.387574
watsonmd_version: 0.1.0
---

Pipelines / 

# List pipelines

Lists all pipelines for a project

Required permission

Project > Pipelines > General > Read

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

      * pipelines

[array] required

An array of pipelines in this project.

        * {object}

A pipeline.

          * name

(multiple options: oneOf) required

The name of the pipeline.

            * string

The name of the pipeline.

min length

3

max length

39

pattern

^[a-zA-Z]((-|\s)?[a-zA-Z0-9]+((-|\s)[a-zA-Z0-9]+)*)?$

OR

            * string

A string containing one or more references that resolve to the name of the pipeline.

pattern

.*\${.*}.*

          * description

(multiple options: oneOf)

A description of the pipeline.

            * string

A description of the pipeline.

max length

200

pattern

^[a-zA-Z0-9.,?\s\\\/'"()[\\];`%^&*\\-_:!]+$

OR

            * string

A string containing one or more references that resolve to a description of the pipeline.

pattern

.*\${.*}.*

          * id

string required

Identifier for the pipeline

          * createdAt

string

time of creation

          * updatedAt

string

time of update

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

GET /v1/projects/{projectId}/pipelines

Example response

200 OK

A list of pipelines belong to the project.

JSON
    
    
    {
      "data": {
        "pipelines": [
          {
            "name": "example-pipeline",
            "id": "example-pipeline"
          }
        ]
      },
      "pagination": {
        "hasNextPage": false,
        "count": 1
      }
    }
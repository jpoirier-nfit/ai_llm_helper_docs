---
source_url: https://northflank.com/docs/v1/api/pipelines/get-pipeline
title: Get pipeline | Pipelines | Northflank API docs
crawl_date: 2025-07-29T10:11:55.751551
watsonmd_version: 0.1.0
---

Pipelines / 

# Get pipeline

Get details about a pipeline

Required permission

Project > Pipelines > General > Read

Path parameters

    * projectId

string required

ID of the project

    * pipelineId

string required

ID of the pipeline




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

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

      * preview

{object}

      * stages

[array]

        *       * nfObjects

[array]

A list of services, jobs and addons to include in the pipeline.

        * {object}

          * id

(multiple options: oneOf) required

The ID of the service, job or addon to include in the pipeline.

            * string

The ID of the service, job or addon to include in the pipeline.

pattern

^[A-Za-z0-9-]+$

OR

            * string

A string containing one or more references that resolve to the ID of the service, job or addon to include in the pipeline.

pattern

.*\${.*}.*

          * type

string required

The type of the resource to include in the pipeline.

one of

service, job, addon

          * stage

string required

The stage in the pipeline to include the resource.

one of

Development, Staging, Production




API

CLI

JS Client

GET /v1/projects/{projectId}/pipelines/{pipelineId}

Example response

200 OK

Details about a pipeline.

JSON
    
    
    {
      "data": {
        "name": "example-pipeline",
        "nfObjects": [
          {
            "id": "example-service",
            "type": "service",
            "stage": "Production"
          }
        ]
      }
    }
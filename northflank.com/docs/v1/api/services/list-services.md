---
source_url: https://northflank.com/docs/v1/api/services/list-services
title: List services | Services | Northflank API docs
crawl_date: 2025-07-29T09:24:10.698055
watsonmd_version: 0.1.0
---

Services / 

# List services

Gets a list of services belonging to the project

Required permission

Project > Services > General > Read

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

      * services

[array] required

An array of services.

        * {object}

A service object.

          * id

string required

Identifier for the service

          * appId

string required

Full identifier used for service deployment

          * projectId

string required

ID of the project the service belongs to.

          * name

string required

Service name

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

A short description of the service

          * serviceType

string required

Type of the service (combined, build or deployment)

one of

combined, build, deployment

          * disabledCI

boolean required

Whether Continuous Integration is disabled

          * disabledCD

boolean required

Whether Continuous Deployment is disabled

          * status

{object} required

Details about the current service status.

            * build

{object}

Details about the status of the most recent build.

              * status

string required

The current status of the build.

one of

QUEUED, PENDING, UNSCHEDULABLE, STARTING, CLONING, BUILDING, UPLOADING, ABORTED, FAILURE, SUBMISSION_FAILURE, SUCCESS, CRASHED, IN_PROGRESS

              * lastTransitionTime

string

The timestamp of when the build reached this status.

            * deployment

{object}

Details about the current deployment status.

              * status

string required

The current status of the deployment.

one of

PENDING, IN_PROGRESS, COMPLETED, FAILED

              * reason

string required

The reason the current deployment was started.

one of

SCALING, DEPLOYING

              * lastTransitionTime

string

The timestamp of when the deployment reached this status.

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

GET /v1/projects/{projectId}/services

Example response

200 OK

The list of services

JSON
    
    
    {
      "data": {
        "services": [
          {
            "id": "example-service",
            "appId": "/example-user/default-project/example-service",
            "projectId": "default-project",
            "name": "Example Service",
            "description": "This is the service description",
            "serviceType": "combined",
            "disabledCI": false,
            "disabledCD": false,
            "status": {
              "build": {
                "status": "SUCCESS",
                "lastTransitionTime": "2021-11-29T11:47:16.624Z"
              },
              "deployment": {
                "status": "COMPLETED",
                "reason": "DEPLOYING",
                "lastTransitionTime": "2021-11-29T11:47:16.624Z"
              }
            }
          }
        ]
      },
      "pagination": {
        "hasNextPage": false,
        "count": 1
      }
    }
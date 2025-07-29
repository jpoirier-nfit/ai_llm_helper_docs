---
source_url: https://northflank.com/docs/v1/api/services/list-service-containers
title: List service containers | Services | Northflank API docs
crawl_date: 2025-07-29T09:57:23.548597
watsonmd_version: 0.1.0
---

Services / 

# List service containers

Gets a list of containers for the given service.

Required permission

Project > Services > Deployment > View Instances

Path parameters

    * projectId

string required

ID of the project

    * serviceId

string required

ID of the service




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

      * containers

[array]

        * {object}

Data about a container.

          * name

string required

The name of the container.

          * createdAt

integer required

The timestamp the container was created.

min

1

          * status

string required

The current status of the container.

one of

TASK_RUNNING, TASK_STARTING, TASK_STAGING, TASK_KILLING, TASK_KILLED, TASK_FAILED, TASK_FINISHED

          * nodeName

string

BYOC only: the name of the node the container was scheduled to

          * nodePoolUserId

string

BYOC only: the user facing ID of the node pool that the container was scheduled to

          * nodePoolProviderId

string

BYOC only: the provider facing ID of the node pool that the container was scheduled to

          * host

string

BYOC only: the host address of the node the container was scheduled to

          * ipAddresses

[array]

BYOC only: the IP addresses mapping to the container

            * string

          * updatedAt

integer required

The timestamp the container was last updated.

min

1

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

GET /v1/projects/{projectId}/services/{serviceId}/containers

Example response

200 OK

Details about the addon's containers.

JSON
    
    
    {
      "data": {
        "containers": [
          {
            "name": "example-service-78b4d4459d-sbtn8",
            "createdAt": 1611241087,
            "status": "TASK_RUNNING",
            "updatedAt": 1611241087
          }
        ]
      },
      "pagination": {
        "hasNextPage": false,
        "count": 1
      }
    }
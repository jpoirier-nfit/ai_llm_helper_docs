---
source_url: https://northflank.com/docs/v1/api/services/get-service-pull-requests
title: Get service pull requests | Services | Northflank API docs
crawl_date: 2025-07-29T10:04:44.178545
watsonmd_version: 0.1.0
---

Services / 

# Get service pull requests

Gets information about the pull-requests of the given service.

Required permission

Project > Services > General > Read

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

      * pullRequests

[array]

A list of pull requests for this repository.

        * {object}

Details about a pull request.

          * id

integer required

ID number of the pull request.

          * state

string required

Status of the pull request.

          * title

string required

Title of the pull request.

          * source

string required

Name of the branch the pull request is merging from.

          * destination

string required

Name of the branch the pull request is being merged into.

          * sha

string required

SHA of the most recent commit of the pull request.

          * created_at

string required

The timestamp the pull request was opened.

          * updated_at

string required

The timestamp the pull request was last updated at.

          * html_url

string required

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

GET /v1/projects/{projectId}/services/{serviceId}/pull-requests

Example response

200 OK

Data about the service's available pull requests.

JSON
    
    
    {
      "data": {
        "pullRequests": [
          {
            "id": 1,
            "state": "OPEN",
            "title": "Add new feature handling",
            "source": "feature/new-feature",
            "destination": "main",
            "sha": "4f101d8821aeb3e4f81f95f3e886a2759ba7b9db",
            "created_at": "2021-03-22T11:05:52.000Z",
            "updated_at": "2021-05-11T16:05:43.000Z"
          }
        ]
      },
      "pagination": {
        "hasNextPage": false,
        "count": 1
      }
    }
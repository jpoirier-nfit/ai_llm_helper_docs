---
source_url: https://northflank.com/docs/v1/api/services/get-service-branches
title: Get service branches | Services | Northflank API docs
crawl_date: 2025-07-29T10:44:52.280598
watsonmd_version: 0.1.0
---

Services / 

# Get service branches

Gets information about the branches of the given service.

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

      * branches

[array]

A list of branches for this repository.

        * {object}

Details about a branch.

          * name

string required

Name of the branch.

          * id

string required

          * commit

{object} required

Details about the most recent commit on the branch.

            * sha

string required

SHA identifier of the commit.

            * author

{object} required

Details about the commit author.

              * login

string required

The login of the commit author.

            * message

string

Commit message of the commit.

            * date

string

Timestamp of the commit.

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

GET /v1/projects/{projectId}/services/{serviceId}/branches

Example response

200 OK

Data about the service's available branches.

JSON
    
    
    {
      "data": {
        "branches": [
          {
            "name": "main",
            "id": "MDM6UmVmMzA0MDU5MzM0OnJlZnMvaGVhZHMvbWFpbg=",
            "commit": {
              "sha": "f8aca180e989be62cba71db629d2ede05f2d10c4",
              "author": {
                "login": "northflank"
              },
              "message": "Initial commit",
              "date": "2021-09-17T14:04:39.000Z"
            }
          }
        ]
      },
      "pagination": {
        "hasNextPage": false,
        "count": 1
      }
    }
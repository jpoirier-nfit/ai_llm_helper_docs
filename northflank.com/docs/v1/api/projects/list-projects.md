---
source_url: https://northflank.com/docs/v1/api/projects/list-projects
title: List projects | Projects | Northflank API docs
crawl_date: 2025-07-29T09:24:10.441664
watsonmd_version: 0.1.0
---

Projects / 

# List projects

Lists projects for the authenticated user or team.

Required permission

Project > Projects > Manage > Read

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

      * projects

[array] required

An array of projects.

        * {object}

A project object.

          * id

string required

Identifier for the project.

          * name

string required

The name of the project.

          * description

string

A short description of the project.

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

GET /v1/projects

Example response

200 OK

A list of projects for the authenticated user

JSON
    
    
    {
      "data": {
        "projects": [
          {
            "id": "default-project",
            "name": "Default Project",
            "description": "The project description"
          }
        ]
      },
      "pagination": {
        "hasNextPage": false,
        "count": 1
      }
    }
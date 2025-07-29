---
source_url: https://northflank.com/docs/v1/api/tags/list-tags
title: List tags | Tags | Northflank API docs
crawl_date: 2025-07-29T10:44:52.266037
watsonmd_version: 0.1.0
---

Tags / 

# List tags

List the resource tags for this entity.

Required permission

Account > Tags > General > Read

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

      * tags

[array] required

A list of available resource tags.

        * {object}

          * useSpotNodes

boolean

Schedule workloads to spot nodes

          * useOnDemandNodes

boolean

Also allow workloads to schedule to on demand nodes. Only relevant if you want workloads to schedule across both spot and on demand nodes

          * nodeAffinities

[array]

            * {object}

              * preference

boolean

              * weight

number

The node affinity weight. Required when `preference` is `true`.

min

1

max

100

              * matchExpressions

[array] required

                * {object}

                  * key

string required

                  * operator

string required

one of

In, NotIn

                  * values

[array] required

                    * string

          * color

string

pattern

^#([a-fA-F0-9]{6}|[a-fA-F0-9]{3})$

          * description

string

max length

200

pattern

^[a-zA-Z0-9.,?\s\\\/'"()[\\];`%^&*\\-_:!]+$

          * name

string required

min length

3

max length

100

pattern

^[a-zA-Z0-9]+((-|\s)[a-zA-Z0-9]+)*$

          * id

string required

min length

3

max length

100

pattern

^[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*$

          * createdAt

string

time of creation

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

GET /v1/tags

Example response

200 OK

A list of tags for this entity.

JSON
    
    
    {
      "data": {
        "tags": [
          {
            "useSpotNodes": false,
            "useOnDemandNodes": false,
            "color": "#57637A",
            "name": "Example Tag",
            "id": "example-tag",
            "createdAt": "2000-01-01T12:00:00.000Z"
          }
        ]
      },
      "pagination": {
        "hasNextPage": false,
        "count": 1
      }
    }
---
source_url: https://northflank.com/docs/v1/api/tags/add-tag
title: Add tag | Tags | Northflank API docs
crawl_date: 2025-07-29T10:44:52.240705
watsonmd_version: 0.1.0
---

Tags / 

# Add tag

Add a new resource tag for this entity.

Required permission

Account > Tags > General > Create

Request body

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




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

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




API

CLI

JS Client

POST /v1/tags

Example request

Request body

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"useSpotNodes":false,"useOnDemandNodes":false,"color":"#57637A","name":"Example Tag"}' \
      https://api.northflank.com/v1/tags

Example response

200 OK

Data about the newly created tag.

JSON
    
    
    {
      "data": {
        "useSpotNodes": false,
        "useOnDemandNodes": false,
        "color": "#57637A",
        "name": "Example Tag",
        "id": "example-tag",
        "createdAt": "2000-01-01T12:00:00.000Z"
      }
    }
---
source_url: https://northflank.com/docs/v1/api/services/update-service-health-checks
title: Update service health checks | Services | Northflank API docs
crawl_date: 2025-07-29T09:57:23.644389
watsonmd_version: 0.1.0
---

Services / 

# Update service health checks

Updates health checks for the given service.

Required permission

Project > Services > General > Update

Path parameters

    * projectId

string required

ID of the project

    * serviceId

string required

ID of the service




Request body

  * {object}

    * healthChecks

[array] required

An array of health checks.

      * {object}

A health check object.

        * protocol

string required

The protocol to access the health check with.

one of

HTTP, CMD, TCP

        * type

string required

The type of health check.

one of

livenessProbe, readinessProbe, startupProbe

        * path

string

The path of the health check endpoint. Required when protocol is HTTP.

pattern

^\/([a-zA-Z0-9-._]+\/)*[a-zA-Z0-9-._]+$

        * cmd

string

The command to run for the health check. Required when protocol is CMD

        * port

integer

Port number for the health check endpoint. Required when protocol is HTTP.

min

1

        * initialDelaySeconds

integer required

Initial delay, in seconds, before the health check is first run.

min

1

max

180

        * periodSeconds

integer required

The time between each check, in seconds.

min

10

max

600

        * timeoutSeconds

integer required

The time to wait for a response before marking the health check as a failure.

min

1

max

60

        * failureThreshold

integer required

The maximum number of allowed failures.

min

1

max

255

        * successThreshold

integer

The number of successes required to mark the health check as a success.

min

1

max

255




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

POST /v1/projects/{projectId}/services/{serviceId}/health-checks

Example request

Request body

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"healthChecks":[{"protocol":"HTTP","type":"readinessProbe","path":"/health-check","port":8080,"initialDelaySeconds":10,"periodSeconds":60,"timeoutSeconds":1,"failureThreshold":3,"successThreshold":1}]}' \
      https://api.northflank.com/v1/projects/{projectId}/services/{serviceId}/health-checks

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }
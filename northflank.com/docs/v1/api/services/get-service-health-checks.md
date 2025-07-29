---
source_url: https://northflank.com/docs/v1/api/services/get-service-health-checks
title: Get service health checks | Services | Northflank API docs
crawl_date: 2025-07-29T09:57:23.626556
watsonmd_version: 0.1.0
---

Services / 

# Get service health checks

Lists the health checks for the given service.

Required permission

Project > Services > General > Read

Path parameters

    * projectId

string required

ID of the project

    * serviceId

string required

ID of the service




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * healthChecks

[array] required

An array of health checks.

        * {object}

          * protocol

string required

The protocol to access the health check with.

one of

HTTP, CMD, TCP

          * type

string required

The type of health check.

one of

livenessProbe, readinessProbe

          * path

string

The path of the health check endpoint.

          * cmd

The command to run for the health check.

          * httpPort

HTTP port number for the health check endpoint.

          * tcpSocketPort

TCP port number for the health check endpoint.

          * initialDelaySeconds

integer required

Initial delay, in seconds, before the health check is first run.

min

1

          * periodSeconds

integer required

The time between each check, in seconds.

min

1

          * timeoutSeconds

integer required

The time to wait for a response before marking the health check as a failure.

min

1

          * failureThreshold

integer required

The maximum number of allowed failures.

min

1

          * successThreshold

The number of successes required to mark the health check as a success.




API

CLI

JS Client

GET /v1/projects/{projectId}/services/{serviceId}/health-checks

Example response

200 OK

Details about the health checks for the service.

JSON
    
    
    {
      "data": {
        "healthChecks": [
          {
            "protocol": "HTTP",
            "type": "readinessProbe",
            "path": "/health-check",
            "httpPort": 3000,
            "initialDelaySeconds": 10,
            "periodSeconds": 60,
            "timeoutSeconds": 1,
            "failureThreshold": 3,
            "successThreshold": 1
          }
        ]
      }
    }
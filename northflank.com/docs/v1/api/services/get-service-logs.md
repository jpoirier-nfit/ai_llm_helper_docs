---
source_url: https://northflank.com/docs/v1/api/services/get-service-logs
title: Get service logs | Services | Northflank API docs
crawl_date: 2025-07-29T10:02:16.784316
watsonmd_version: 0.1.0
---

Services / 

# Get service logs

Get logs for a service

Required permission

Project > Services > Deployment > View Instance Logs

Path parameters

    * projectId

string required

ID of the project

    * serviceId

string required

ID of the service




Query parameters

    * deploymentId

string

Limit logs to a specific deployment.

    * type

string

Type of log. Multiple log types can be selected by specifying the query parameter repeatedly.

one of

cdn, mesh, ingress, runtime, build, backup, restore

    * containerName

string

Limits logs to a specific container.

    * queryType

string

`range` selects a log range and returns immediately.

one of

range

    * startTime

string

Fetch logs generated after this timestamp.

    * endTime

string

Fetch logs generated before this timestamp.

    * duration

integer

Range duration in seconds. If set, only one of `startTime` or `endTime` can be set.

    * lineLimit

number

Number of log lines to fetch.

    * direction

string

Ordering of log lines

one of

backward, forward

    * textIncludes

string

Filter log lines to match this search string

    * textNotIncludes

string

Filter log lines to not match this search string

    * regexIncludes

string

Filter log lines to match this regular expression

    * regexNotIncludes

string

Filter log lines to not match this regular expression




Response body

  * {object}

Response object.

    * data

[array] required

Result data.

      * {object}

        * containerId

string required

        * log

required

        * ts

string required




API

CLI

JS Client

GET /v1/projects/{projectId}/services/{serviceId}/logs

Example response

200 OK

List of logs values

JSON
    
    
    {
      "data": [
        {
          "log": "stdout F This is a log line",
          "ts": "2023-03-21T15:01:17.310Z"
        }
      ]
    }
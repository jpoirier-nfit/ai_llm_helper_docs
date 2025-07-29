---
source_url: https://northflank.com/docs/v1/api/jobs/get-job-build-logs
title: Get job build logs | Jobs | Northflank API docs
crawl_date: 2025-07-29T10:04:45.905665
watsonmd_version: 0.1.0
---

Jobs / 

# Get job build logs

Get logs for a job build

Required permission

Project > Jobs > Deployment > View Instance Logs

Path parameters

    * projectId

string required

ID of the project

    * jobId

string required

ID of the job




Query parameters

    * buildId

string

Selects logs for specific build.

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

GET /v1/projects/{projectId}/jobs/{jobId}/build-logs

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
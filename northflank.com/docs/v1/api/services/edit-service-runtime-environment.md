---
source_url: https://northflank.com/docs/v1/api/services/edit-service-runtime-environment
title: Edit service runtime environment | Services | Northflank API docs
crawl_date: 2025-07-29T10:02:17.052982
watsonmd_version: 0.1.0
---

Services / 

# Edit service runtime environment

Sets the runtime environment for the given service.

Required permission

Project > Secrets > Services > Update

Path parameters

    * projectId

string required

ID of the project

    * serviceId

string required

ID of the service




Request body

  * {object}

    * runtimeEnvironment

{object} required

An object containing the all of the environment variables to set for the service. Keys may only contain letters, numbers, hyphens, forward slashes and dots.

    * runtimeFiles

{object}

Secret files as JSON object, encrypted at rest. File path must be absolute




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * success

boolean required

True if the operation was successful.

      * restartSuccessful

boolean required

Did the service successfully restart with the new environment variables?




API

CLI

JS Client

POST /v1/projects/{projectId}/services/{serviceId}/runtime-environment

Example request

Request body

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"runtimeEnvironment":{"VARIABLE_1":"abcdef","VARIABLE_2":"12345"},"runtimeFiles":{"/dir/fileName":{"data":"VGhpcyBpcyBhbiBleGFtcGxlIHdpdGggYSB0ZW1wbGF0ZWQgJHtOT0RFX0VOVn0gdmFyaWFibGU=","encoding":"utf-8"}}}' \
      https://api.northflank.com/v1/projects/{projectId}/services/{serviceId}/runtime-environment

Example response

200 OK

Details about the updated runtime environment.

JSON
    
    
    {
      "data": {
        "success": true,
        "restartSuccessful": true
      }
    }
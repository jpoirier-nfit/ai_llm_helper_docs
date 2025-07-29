---
source_url: https://northflank.com/docs/v1/api/services/edit-service-build-arguments
title: Edit service build arguments | Services | Northflank API docs
crawl_date: 2025-07-29T09:57:23.335731
watsonmd_version: 0.1.0
---

Services / 

# Edit service build arguments

Sets the build arguments for the given service.

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

    * buildArguments

{object}

An object containing the all of the build arguments to set for the service. Keys may only contain letters, numbers, hyphens, forward slashes and dots.

    * buildFiles

{object}

Secret files as JSON object, encrypted at rest. File path must be absolute

    * dockerSecretMounts

{object}

Docker secret mount contents as JSON object, encrypted at rest. Must be a valid Docker secret mount identifier




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

POST /v1/projects/{projectId}/services/{serviceId}/build-arguments

Example request

Request body

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"buildArguments":{"ARGUMENT_1":"abcdef","ARGUMENT_2":"12345"},"buildFiles":{"/dir/fileName":{"data":"VGhpcyBpcyBhbiBleGFtcGxlIHdpdGggYSB0ZW1wbGF0ZWQgJHtOT0RFX0VOVn0gdmFyaWFibGU=","encoding":"utf-8"}},"dockerSecretMounts":{"example-secret-mount_1":{"data":"VGhpcyBpcyBhbiBleGFtcGxlIHdpdGggYSB0ZW1wbGF0ZWQgJHtOT0RFX0VOVn0gdmFyaWFibGU=","encoding":"utf-8"}}}' \
      https://api.northflank.com/v1/projects/{projectId}/services/{serviceId}/build-arguments

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }
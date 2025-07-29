---
source_url: https://northflank.com/docs/v1/api/services/get-service-runtime-environment
title: Get service runtime environment | Services | Northflank API docs
crawl_date: 2025-07-29T10:04:44.209598
watsonmd_version: 0.1.0
---

Services / 

# Get service runtime environment

Gets the runtime environment of the given service. If the API key does not have the permission 'Project > Secrets > General > Read', secrets inherited from secret groups will not be displayed.

Required permission

Project > Secrets > Services > Read

Path parameters

    * projectId

string required

ID of the project

    * serviceId

string required

ID of the service




Query parameters

    * show

string

Which secrets to display - if set to `this` only the group's secrets are displayed, if set to `inherited` only secrets from linked addons are displayed, if set to `all` or not provided, both are displayed.

one of

this, inherited, all

    * replaceTemplatedValues

string

If templated secrets should be replaced with their inferred value rather than returned as template strings.

one of

true




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * runtimeEnvironment

{object} required

The runtime environment variables, formatted as a JSON object. If the `show` parameter is set to `this`, this will only contain secrets saved to this entity. If the `show` parameter is set to `inherited`, this will only contain secrets inherited from linked secret groups. Otherwise, this will contain both.

      * runtimeFiles

{object} required

The runtime secret files, formatted as a JSON object. If the `show` parameter is set to `this`, this will only contain files saved to this entity. If the `show` parameter is set to `inherited`, this will only contain files inherited from linked secret groups. Otherwise, this will contain both.




API

CLI

JS Client

GET /v1/projects/{projectId}/services/{serviceId}/runtime-environment

Example response

200 OK

The runtime environment of the service.

JSON
    
    
    {
      "data": {
        "runtimeEnvironment": {
          "VARIABLE_1": "abcdef",
          "VARIABLE_2": "12345"
        },
        "runtimeFiles": {
          "/dir/fileName": {
            "data": "VGhpcyBpcyBhbiBleGFtcGxlIHdpdGggYSB0ZW1wbGF0ZWQgJHtOT0RFX0VOVn0gdmFyaWFibGU=",
            "encoding": "utf-8"
          }
        }
      }
    }
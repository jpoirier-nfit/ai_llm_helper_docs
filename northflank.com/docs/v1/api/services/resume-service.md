---
source_url: https://northflank.com/docs/v1/api/services/resume-service
title: Resume service | Services | Northflank API docs
crawl_date: 2025-07-29T09:24:13.633024
watsonmd_version: 0.1.0
---

Services / 

# Resume service

Resumes the given service. Optionally takes several arguments to override resumed settings.

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

    * instances

integer

The number of instances to scale the service to upon resuming

    * disabledCI

boolean

Whether CI should be disabled

    * disabledCD

boolean

Whether CD should be disabled




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

POST /v1/projects/{projectId}/services/{serviceId}/resume

Example request

Request body

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"instances":1,"disabledCI":false,"disabledCD":false}' \
      https://api.northflank.com/v1/projects/{projectId}/services/{serviceId}/resume

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }

Example response

409 Conflict

The service could not be resumed as it is not paused.
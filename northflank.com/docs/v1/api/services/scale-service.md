---
source_url: https://northflank.com/docs/v1/api/services/scale-service
title: Scale service | Services | Northflank API docs
crawl_date: 2025-07-29T09:57:23.946249
watsonmd_version: 0.1.0
---

Services / 

# Scale service

Modifies the scaling settings for the given service.

Required permission

Project > Services > Deployment > Scale Service

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

The number of instances to scale the service to

    * deploymentPlan

string

ID of the deployment plan to switch to.

min length

3

max length

100

pattern

^[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*$

    * storage

{object}

      * ephemeralStorage

{object}

        * storageSize

integer

Ephemeral storage per container in MB

min

1024

      * shmSize

integer

Configures the amount of available memory-backed disk space available to /dev/shm

min

64

    * gracePeriodSeconds

integer

The maximum amount of time the process has to shut down after receiving a SIGTERM signal before it is forcefully shut down SIGKILL by the system.

min

15

max

600




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

POST /v1/projects/{projectId}/services/{serviceId}/scale

Example request

Request body

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"instances":1,"deploymentPlan":"nf-compute-20","storage":{"ephemeralStorage":{"storageSize":1024}}}' \
      https://api.northflank.com/v1/projects/{projectId}/services/{serviceId}/scale

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }
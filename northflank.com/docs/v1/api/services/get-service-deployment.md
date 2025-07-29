---
source_url: https://northflank.com/docs/v1/api/services/get-service-deployment
title: Get service deployment | Services | Northflank API docs
crawl_date: 2025-07-29T10:44:52.828724
watsonmd_version: 0.1.0
---

Services / 

# Get service deployment

Gets information about the deployment of the given service.

Required permission

Project > Services > Deployment > View Instances

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

(multiple options: oneOf) required

Result data.

      * {object}

Service deploying a Northflank entity

        * region

string

Region where this service is deployed and/or built

        * instances

integer

Number of instances/replicas running

        * docker

{object}

Details about the Docker overrides for this deployment.

          * configType

string required

Override configuration which is used at runtime.

one of

default, customEntrypoint, customCommand, customEntrypointCustomCommand

          * customEntrypoint

string

The CMD to run instead of the default if entrypoint override is enabled.

          * customCommand

string

The CMD to run instead of the default if CMD override is enabled.

        * buildpack

{object}

Details about the Buildpack overrides for this deployment.

          * configType

string required

Type of buildpack run configuration.

one of

default, customProcess, customCommand, customEntrypointCustomCommand, originalEntrypointCustomCommand

          * customProcess

string

Custom process which should be run.

          * customEntrypoint

string

Custom entrypoint which should be run.

          * customCommand

string

Custom command which should be run.

        * storage

{object}

Details about storage settings for this deployment.

          * ephemeralStorage

{object}

Details about ephemeral storage settings for this deployment.

            * storageSize

number required

Ephemeral storage per container in MB

          * shmSize

integer

Configures the amount of available memory-backed disk space available to /dev/shm

min

64

        * internal

{object} required

          * appId

string required

Full identifier of deployed entity

          * nfObjectId

string required

ID of deployed entity

          * nfObjectType

string required

Type of deployed entity

one of

service

          * repository

string required

URL of the repository being deployed

          * branch

string required

Branch of the repo being deployed

          * buildId

string required

ID of the build currently deployed.

          * buildSHA

string required

Commit SHA being deployed. `latest` means the latest commit is automatically being deployed.

          * deployedSHA

string

Currently deployed commit SHA. If buildSHA is set to `latest`, this will show the SHA of the latest commit.

OR

      * {object}

Service deploying an external image

        * region

string

Region where this service is deployed and/or built

        * instances

integer

Number of instances/replicas running

        * docker

{object}

Details about the Docker overrides for this deployment.

          * configType

string required

Override configuration which is used at runtime.

one of

default, customEntrypoint, customCommand, customEntrypointCustomCommand

          * customEntrypoint

string

The CMD to run instead of the default if entrypoint override is enabled.

          * customCommand

string

The CMD to run instead of the default if CMD override is enabled.

        * buildpack

{object}

Details about the Buildpack overrides for this deployment.

          * configType

string required

Type of buildpack run configuration.

one of

default, customProcess, customCommand, customEntrypointCustomCommand, originalEntrypointCustomCommand

          * customProcess

string

Custom process which should be run.

          * customEntrypoint

string

Custom entrypoint which should be run.

          * customCommand

string

Custom command which should be run.

        * storage

{object}

Details about storage settings for this deployment.

          * ephemeralStorage

{object}

Details about ephemeral storage settings for this deployment.

            * storageSize

number required

Ephemeral storage per container in MB

          * shmSize

integer

Configures the amount of available memory-backed disk space available to /dev/shm

min

64

        * external

{object} required

          * imagePath

string required

Path of the external image excluding the hostname

          * registryProvider

string required

Registry provider hosting the external image

one of

acr, ecr, gar, dockerhub, github, gitlab, custom, legacy

          * privateImage

boolean required

Does the image require authentication




API

CLI

JS Client

GET /v1/projects/{projectId}/services/{serviceId}/deployment

Example response

200 OK

Data about the service deployment.

JSON
    
    
    {
      "data": {
        "region": "europe-west",
        "instances": 1,
        "docker": {
          "configType": "default"
        },
        "buildpack": {
          "configType": "default"
        },
        "storage": {
          "ephemeralStorage": {
            "storageSize": 1024
          }
        },
        "internal": {
          "appId": "/example-user/default-project/example-service",
          "nfObjectId": "example-service",
          "nfObjectType": "service",
          "repository": "https://github.com/northflank/gatsby-with-northflank",
          "branch": "master",
          "buildId": "incredible-land-3266",
          "buildSHA": "latest",
          "deployedSHA": "262ed9817b3cad5142fbceabe0c9e371e390d616"
        }
      }
    }

OR

JSON
    
    
    {
      "data": {
        "region": "europe-west",
        "instances": 1,
        "docker": {
          "configType": "default"
        },
        "buildpack": {
          "configType": "default"
        },
        "storage": {
          "ephemeralStorage": {
            "storageSize": 1024
          }
        },
        "external": {
          "imagePath": "nginx:latest",
          "registryProvider": "dockerhub",
          "privateImage": false
        }
      }
    }
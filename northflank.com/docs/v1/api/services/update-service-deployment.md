---
source_url: https://northflank.com/docs/v1/api/services/update-service-deployment
title: Update service deployment | Services | Northflank API docs
crawl_date: 2025-07-29T10:02:16.734865
watsonmd_version: 0.1.0
---

Services / 

# Update service deployment

Updates the deployment settings of the given service.

Required permission

Project > Services > Deployment > Update Deployment

Path parameters

    * projectId

string required

ID of the project

    * serviceId

string required

ID of the service




Request body

  * {object}

An external deployment

    * external

{object} required

      * imagePath

string required

Image to be deployed. When not deploying from Dockerhub the URL must be specified.

pattern

^(?:(?:https?:\/\/)?([a-zA-Z0-9\\-]+\\.[a-zA-Z0-9\\.\\-]+)(\/v1)?)?(?:\/)?([a-zA-Z/-9\\.\\-_]+)(?:\:([a-zA-Z/-9\\.\\-_\:]+)|\@([a-zA-Z/-9\\.\\-_\:]+))$

      * credentials

string

ID of the saved credentials to use to access this external image.

pattern

^[A-Za-z0-9-]+$

    * docker

{object}

Allows for customization of docker runtime

      * configType

string required

Type of entrypoint & command override configuration

one of

default, customEntrypoint, customCommand, customEntrypointCustomCommand

      * customEntrypoint

string

Custom entrypoint which should be used. Required in case where `configType` is `customEntrypoint` or `customEntrypointCustomCommand`

      * customCommand

string

Custom command which should be used. Required in case where `configType` is `customCommand` or `customEntrypointCustomCommand`




OR

  * {object}

An internal deployment

    * internal

{object} required

      * id

string

ID of the build service to deploy

min length

3

max length

54

pattern

^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

      * branch

string

Branch to deploy

      * buildSHA

(multiple options: oneOf)

Commit SHA to deploy, or 'latest' to deploy the most recent commit

        * string

A commit sha.

min length

40

max length

40

OR

        * string

Latest commit.

one of

latest

      * buildId

string

ID of the build that should be deployed

    * buildpack

{object}

Allows for customization of buildpack runtime

      * configType

string required

Type of buildpack run configuration

one of

default, customProcess, customCommand, customEntrypointCustomCommand, originalEntrypointCustomCommand

      * customProcess

string

Custom process which should be run. Required in case where `configType` is `customProcess`

      * customEntrypoint

string

Custom entrypoint which should be run. Required in case where `configType` is `customEntrypointCustomCommand`

      * customCommand

string

Custom command which should be run. Required in case where `configType` is `customCommand`, `customEntrypointCustomCommand` or `originalEntrypointCustomCommand`

    * docker

{object}

Allows for customization of docker runtime

      * configType

string required

Type of entrypoint & command override configuration

one of

default, customEntrypoint, customCommand, customEntrypointCustomCommand

      * customEntrypoint

string

Custom entrypoint which should be used. Required in case where `configType` is `customEntrypoint` or `customEntrypointCustomCommand`

      * customCommand

string

Custom command which should be used. Required in case where `configType` is `customCommand` or `customEntrypointCustomCommand`




OR

  * {object}

Don't modify the deployment

    * buildpack

{object}

Allows for customization of buildpack runtime

      * configType

string required

Type of buildpack run configuration

one of

default, customProcess, customCommand, customEntrypointCustomCommand, originalEntrypointCustomCommand

      * customProcess

string

Custom process which should be run. Required in case where `configType` is `customProcess`

      * customEntrypoint

string

Custom entrypoint which should be run. Required in case where `configType` is `customEntrypointCustomCommand`

      * customCommand

string

Custom command which should be run. Required in case where `configType` is `customCommand`, `customEntrypointCustomCommand` or `originalEntrypointCustomCommand`

    * docker

{object}

Allows for customization of docker runtime

      * configType

string required

Type of entrypoint & command override configuration

one of

default, customEntrypoint, customCommand, customEntrypointCustomCommand

      * customEntrypoint

string

Custom entrypoint which should be used. Required in case where `configType` is `customEntrypoint` or `customEntrypointCustomCommand`

      * customCommand

string

Custom command which should be used. Required in case where `configType` is `customCommand` or `customEntrypointCustomCommand`




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

POST /v1/projects/{projectId}/services/{serviceId}/deployment

Example request

Request body

An external deployment

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"external":{"imagePath":"nginx:latest","credentials":"example-credentials"},"docker":{"configType":"default"}}' \
      https://api.northflank.com/v1/projects/{projectId}/services/{serviceId}/deployment

OR

An internal deployment

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"internal":{"id":"example-build-service","branch":"master","buildId":"premium-guide-6393"},"docker":{"configType":"default"}}' \
      https://api.northflank.com/v1/projects/{projectId}/services/{serviceId}/deployment

OR

Don't modify the deployment

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"docker":{"configType":"default"}}' \
      https://api.northflank.com/v1/projects/{projectId}/services/{serviceId}/deployment

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }
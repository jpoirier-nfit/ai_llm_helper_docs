---
source_url: https://northflank.com/docs/v1/api/pipelines/run-release-flow
title: Run release flow | Pipelines | Northflank API docs
crawl_date: 2025-07-29T10:46:17.333729
watsonmd_version: 0.1.0
---

Pipelines / 

# Run release flow

Runs a given release flow with given arguments. This endpoint can be used as part of a CI pipeline to automatically trigger a release process.

Required permission

Project > Pipelines > General > Update

Path parameters

    * projectId

string required

ID of the project

    * pipelineId

string required

ID of the pipeline

    * stage

string required

Stage of the pipeline




Request body

  * {object}

    * name

string

The optional name of the release-flow run.

min length

3

max length

39

pattern

^[a-zA-Z]((-|\s)?[a-zA-Z0-9]+((-|\s)[a-zA-Z0-9]+)*)?$

    * description

string

The optional description of the release-flow run.

max length

200

pattern

^[a-zA-Z0-9.,?\s\\\/'"()[\\];`%^&*\\-_:!]+$

    * arguments

{object}

A set of arguments that can be referenced in a template using '${args.argumentName}'.

    * overrides

{object}

Overrides for specific reference values. This should be an object where each key corresponds to a ref defined in the template. The values of each of these keys should also be an object, where each key value pair provided will overwrite the value for that key in the given ref. For example, the value `{ 'example-ref': { 'branch': 'devel' } }` would set the `branch` field to `devel` for the node with ref `example-ref`.

    * releaseNodeOverrides

{object}

Overrides for release nodes. This should be an object where each key is the id of a deployment service used in a release node. The value of each of these keys should be also be an object containing the new spec of the release for that deployment service.




API

CLI

JS Client

POST /v1/projects/{projectId}/pipelines/{pipelineId}/release-flows/{stage}/runs

Example request

Request body

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"name":"Example Run","description":"This is a description for the release-flow run.","arguments":{"ARG_1":"value"},"overrides":{"example-ref":{"branch":"devel"}},"releaseNodeOverrides":{"example-service":{"type":"registry","origin":{"imagePath":"nginx:latest"}}}}' \
      https://api.northflank.com/v1/projects/{projectId}/pipelines/{pipelineId}/release-flows/{stage}/runs

Example response

200 OK

success
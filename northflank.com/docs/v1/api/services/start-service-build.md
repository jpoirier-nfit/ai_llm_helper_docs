---
source_url: https://northflank.com/docs/v1/api/services/start-service-build
title: Start service build | Services | Northflank API docs
crawl_date: 2025-07-29T09:24:13.086816
watsonmd_version: 0.1.0
---

Services / 

# Start service build

Start a new build for the given combined or build service. If given a commit sha, it will build that commit. Otherwise, the most recent relevant commit will be built. If the service provided is a build service, a branch name or pull request to build from is required.

Required permission

Project > Services > Deployment > Deploy Build

Path parameters

    * projectId

string required

ID of the project

    * serviceId

string required

ID of the service




Request body

  * (multiple options: anyOf)

Build type

    * {object}

Build from bundle

      * bundleUrl

string required

URL of the bundle to be built

      * branch

string

      * sha

string

OR

    * {object}

Build from git repository

      * sha

string

Commit sha to build. If not provided, builds the most recent relevant commit.

min length

40

max length

40

      * branch

string

Branch to build from. If `sha` is not provided, the latest commit of this branch will be built. Only supported by build services. Build services require either `branch` or `pullRequestId` field, but cannot be provided with both.

      * pullRequestId

integer

ID of a pull request to build from. If `sha` is not provided, the latest commit of this pull request will be built. Only supported by build services. Build services require either `branch` or `pullRequestId` field, but cannot be provided with both.

      * overrides

{object}

An optional object that may specify several different overrides on the build level.

        * buildArguments

{object}

Build arguments that will be set on this build only. In case of conflicts these values take precedence.

        * buildFiles

{object}

Secret files as JSON object, encrypted at rest. File path must be absolute

        * dockerSecretMounts

{object}

Docker secret mount contents as JSON object, encrypted at rest. Must be a valid Docker secret mount identifier

        * docker

{object}

Overrides for docker build settings.

          * dockerFilePath

string

The file path of the Dockerfile.

pattern

^\/([a-zA-Z0-9-._]+\/)*[a-zA-Z0-9-._]+$

          * dockerWorkDir

string

The working directory of the Dockerfile.

pattern

^\/([a-zA-Z0-9-._]+\/)*[a-zA-Z0-9-._]*$

          * dockerfileTarget

string

If your Dockerfile contains multiple build stages, you can specify the target stage by entering its name here.

pattern

^[a-zA-Z0-9-_]+$




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * id

string required

ID of the build.

      * branch

string

Name of the branch the built commit belongs to.

      * pullRequestId

number

ID of the pull request the commit belongs to.

      * sha

string

The sha of the built commit.

      * registry

{object}

        * uri

string

URI of that can be used to pull the image from the registry

      * createdAt

string

Timestamp of the build initiation.

      * status

string

The status of the build.

      * concluded

boolean

Whether the build has finished.




API

CLI

JS Client

POST /v1/projects/{projectId}/services/{serviceId}/build

Example request

Request body

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"bundleUrl":"https://example.com/archive.tar"}' \
      https://api.northflank.com/v1/projects/{projectId}/services/{serviceId}/build

Example response

200 OK

Returns data about the build initiated

JSON
    
    
    {
      "data": {
        "id": "joyous-view-6290",
        "branch": "main",
        "sha": "12c15e7ee25fd78f567ebf87f9178b8ad70025b3",
        "createdAt": "2021-07-28T15:55:38.296Z",
        "status": "PENDING",
        "concluded": false
      }
    }
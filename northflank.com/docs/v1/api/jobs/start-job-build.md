---
source_url: https://northflank.com/docs/v1/api/jobs/start-job-build
title: Start job build | Jobs | Northflank API docs
crawl_date: 2025-07-29T09:57:25.735138
watsonmd_version: 0.1.0
---

Jobs / 

# Start job build

Start a new build for the given job. Given a commit sha, it will build that commit.

Required permission

Project > Jobs > Deployment > Deploy Build

Path parameters

    * projectId

string required

ID of the project

    * jobId

string required

ID of the job




Request body

  * {object}

Start a build with the current settings

    * sha

string

Commit sha to build. If not provided, will build the most recent commit of the job's branch.

min length

40

max length

40




OR

  * {object}

Start a build with overrides for the current settings

    * sha

string

Commit sha to build. If not provided, will build the most recent commit of the job's branch.

min length

40

max length

40

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

POST /v1/projects/{projectId}/jobs/{jobId}/build

Example request

Request body

Start a build with the current settings

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"sha":"262ed9817b3cad5142fbceabe0c9e371e390d616"}' \
      https://api.northflank.com/v1/projects/{projectId}/jobs/{jobId}/build

OR

Start a build with overrides for the current settings

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"sha":"262ed9817b3cad5142fbceabe0c9e371e390d616","overrides":{"buildArguments":{"ARGUMENT_1":"abcdef","ARGUMENT_2":"12345"},"buildFiles":{"/dir/fileName":{"data":"VGhpcyBpcyBhbiBleGFtcGxlIHdpdGggYSB0ZW1wbGF0ZWQgJHtOT0RFX0VOVn0gdmFyaWFibGU=","encoding":"utf-8"}},"dockerSecretMounts":{"example-secret-mount_1":{"data":"VGhpcyBpcyBhbiBleGFtcGxlIHdpdGggYSB0ZW1wbGF0ZWQgJHtOT0RFX0VOVn0gdmFyaWFibGU=","encoding":"utf-8"}},"docker":{"dockerFilePath":"/Dockerfile","dockerWorkDir":"/"}}}' \
      https://api.northflank.com/v1/projects/{projectId}/jobs/{jobId}/build

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
---
source_url: https://northflank.com/docs/v1/api/pipelines/get-release-flow-run-details
title: Get release flow run details | Pipelines | Northflank API docs
crawl_date: 2025-07-29T10:44:48.836210
watsonmd_version: 0.1.0
---

Pipelines / 

# Get release flow run details

Get information about the given release flow run

Required permission

Project > Pipelines > General > Read

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

    * runId

string required

ID of the release flow run




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * apiVersion

string required

The version of the Northflank API to run the template against.

one of

v1.2

      * arguments

{object}

A set of arguments that can be referenced in a template using '${args.argumentName}'.

      * triggers

[array]

        * {object}

          * ref

string

A reference that can be used to access the output of this trigger in the template.

          * vcsService

string required

The VCS provider to use.

one of

bitbucket, gitlab, github, self-hosted, azure

          * selfHostedVcsId

string

If projectType is self-hosted, the ID of the self-hosted vcs to use.

pattern

^([A-Za-z0-9-]+\/[A-Za-z0-9-]+)|([0-9a-f]{24})$

          * accountLogin

string

By default, if you have multiple version control accounts of the same provider linked, Northflank will pick a linked account that has access to the repository. If `accountLogin` is provided, Northflank will instead use your linked account with that login name.

          * vcsLinkId

string

          * repoUrl

string required

URL of the Git repo that will trigger the template.

pattern

^(https:\/\/)?((www(\\.[a-zA-Z0-9\\-]{2,})+\\.)?[a-zA-Z0-9\\-]{2,})(\\.([a-zA-Z0-9\\-]{2,}))+(\/([a-zA-Z0-9\\-._]{2,}))+?$

          * branchRestrictions

[array]

            * string

pattern

^[a-zA-Z/*0-9%\\-.#_!'();,&=+]*$

          * prRestrictions

[array]

            * string

pattern

^[a-zA-Z/*0-9%\\-.#_!'();,&=+]*$

          * pathIgnoreRules

[array]

An array of path ignore rules. A commit will only be built if a file has been changed that does not match any of the ignore rules. Path ignore rules follow `.gitignore` syntax.

            * string

A path ignore rule, following `.gitignore` syntax. For example, `*.md` will ignore all files ending with `.md`.

max length

260

          * ciIgnoreFlags

[array]

An array of commit ignore flags. If a commit message contains one or more of these flags, that commit will not be built. Defaults to `["[skip ci]", "[ci skip]", "[no ci]", "[skip nf]", "[nf skip]", "[northflank skip]", "[skip northflank]"]`

            * string

A commit ignore flag.

max length

72

          * ciIgnoreFlagsEnabled

boolean

          * isAllowList

boolean

          * ignoreDrafts

boolean

If `true`, draft pull requests from this repo will not trigger the template.

      * options

{object}

Options regarding how the template is run.

        * concurrencyPolicy

string

Defines the concurrency behaviour of the template with respect to parallel runs.

one of

allow, queue, forbid

        * paused

boolean

If `true`, the template will not run when triggered by git.

      * gitops

{object}

        * vcsService

string required

The VCS provider to use.

one of

bitbucket, gitlab, github, self-hosted, azure

        * selfHostedVcsId

string

If projectType is self-hosted, the ID of the self-hosted vcs to use.

pattern

^([A-Za-z0-9-]+\/[A-Za-z0-9-]+)|([0-9a-f]{24})$

        * accountLogin

string

By default, if you have multiple version control accounts of the same provider linked, Northflank will pick a linked account that has access to the repository. If `accountLogin` is provided, Northflank will instead use your linked account with that login name.

        * vcsLinkId

string

Legacy key. Please used accountLogin instead.

        * repoUrl

string required

URL of the Git repo to sync the template with.

pattern

^(https:\/\/)?((www(\\.[a-zA-Z0-9\\-]{2,})+\\.)?[a-zA-Z0-9\\-]{2,})(\\.([a-zA-Z0-9\\-]{2,}))+(\/([a-zA-Z0-9\\-._]{2,}))+?$

        * branch

string required

The name of the branch to use.

        * filePath

string required

The file path to the template in the repository. If using an existing template, it should be in JSON format.

pattern

^\/([a-zA-Z0-9-._]+\/)*[a-zA-Z0-9-._]+$

      * $schema

string

      * spec

(multiple options: oneOf) required

A node representing an action to be performed as part of the template.

      * refs

{object}

      * id

string required

ID of the release flow run

      * name

string

Optional name for the release flow run

      * description

string

Optional description for the release flow run

      * status

string required

Status of the template run

one of

pending, running, success, failure, aborted, aborting, queued, unknown, skipped

      * startedAt

string

Timestamp the run started at.

      * concluded

boolean required

Whether the run has concluded (aborted, success, failed)

      * concludedAt

string

Timestamp the run concluded at.

      * createdAt

string required

Timestamp the run was created at.

      * updatedAt

string required

Timestamp the run was last updated at.




API

CLI

JS Client

GET /v1/projects/{projectId}/pipelines/{pipelineId}/release-flows/{stage}/runs/{runId}

Example response

200 OK

Details about a release flow run.

JSON
    
    
    {
      "data": {
        "apiVersion": "v1.2",
        "triggers": [
          {
            "vcsService": "github",
            "accountLogin": "github-user",
            "repoUrl": "https://github.com/northflank-examples/remix-postgres-redis-demo",
            "pathIgnoreRules": [
              "README.md"
            ],
            "ciIgnoreFlags": [
              "[skip ci]"
            ]
          }
        ],
        "options": {
          "concurrencyPolicy": "allow",
          "paused": false
        },
        "gitops": {
          "vcsService": "github",
          "accountLogin": "github-user",
          "repoUrl": "https://github.com/northflank-examples/remix-postgres-redis-demo",
          "branch": "main"
        },
        "spec": {
          "settings": {
            "maxAttempts": 3,
            "backoff": {
              "type": "fixed",
              "delay": 60
            }
          },
          "kind": "Workflow",
          "response": {
            "status": "success",
            "retries": {
              "attempts": 1,
              "maxAttempts": 3,
              "timestamp": 1657296265
            },
            "startTime": 1657296265,
            "endTime": 1657296265
          }
        },
        "id": "110ddb52-bdcd-482d-8ac2-05ba580afe2f",
        "name": "Example run",
        "description": "This is an example description",
        "status": "success",
        "startedAt": "2021-01-01 12:01:00.000Z",
        "concluded": true,
        "concludedAt": "2021-01-01 12:10:00.000Z",
        "createdAt": "2021-01-01 12:00:00.000Z",
        "updatedAt": "2021-01-01 12:00:00.000Z"
      }
    }
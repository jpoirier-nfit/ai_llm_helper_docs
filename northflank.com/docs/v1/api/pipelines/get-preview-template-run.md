---
source_url: https://northflank.com/docs/v1/api/pipelines/get-preview-template-run
title: Get preview template run | Pipelines | Northflank API docs
crawl_date: 2025-07-29T10:46:55.468329
watsonmd_version: 0.1.0
---

Pipelines / 

# Get preview template run

Get information about the given preview template run.

Required permission

Account > Templates > General > Read

Path parameters

    * projectId

string required

ID of the project

    * pipelineId

string required

ID of the pipeline

    * templateRunId

string required

ID of the template run




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

      * options

{object}

Options regarding how the template is run.

        * concurrencyPolicy

string

Defines the concurrency behaviour of the template with respect to parallel runs.

one of

allow, queue, forbid

        * nameFormat

string

The format of the automatically generated preview name. This is a parsed ref string.

        * prefixName

boolean

If true, the preview name will default to the front of the resource name.

        * schedule

{object}

Options regarding which hours preview environments should be active. Only available for BYOC projects.

          * mon

{object}

            * startTime

integer

min

0

max

2400

            * endTime

integer

min

0

max

2400

          * tue

{object}

            * startTime

integer

min

0

max

2400

            * endTime

integer

min

0

max

2400

          * wed

{object}

            * startTime

integer

min

0

max

2400

            * endTime

integer

min

0

max

2400

          * thu

{object}

            * startTime

integer

min

0

max

2400

            * endTime

integer

min

0

max

2400

          * fri

{object}

            * startTime

integer

min

0

max

2400

            * endTime

integer

min

0

max

2400

          * sat

{object}

            * startTime

integer

min

0

max

2400

            * endTime

integer

min

0

max

2400

          * sun

{object}

            * startTime

integer

min

0

max

2400

            * endTime

integer

min

0

max

2400

        * expiry

{object}

Settings regarding the automatic deletion of previews.

          * previewLifetime

integer

If set, preview environments will be automatically deleted after this many minutes since their last update.

min

1

          * resetOnUpdate

boolean

If `true`, the expiry time for an existing preview will be reset when it is ran again.

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

          * type

string

Type of trigger

one of

git

          * manualOnly

boolean

Should the git trigger only be triggered manually?

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

A node representing an action to be performed as part of the PreviewEnvTemplate.

      * refs

{object}

      * id

string required

Identifier for the template run

      * templateId

string required

Identifier for the template

      * status

string required

Status of the template run

one of

pending, running, success, failure

      * createdAt

string

time of creation

      * updatedAt

string

time of update




API

CLI

JS Client

GET /v1/projects/{projectId}/pipelines/{pipelineId}/preview-envs/runs/{templateRunId}

Example response

200 OK

Details about the preview template run.

JSON
    
    
    {
      "data": {
        "apiVersion": "v1.2",
        "options": {
          "concurrencyPolicy": "allow"
        },
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
        "id": "3dd592f6-ce63-45ee-acf8-13dc5ec5235c",
        "templateId": "example-template",
        "status": "pending"
      }
    }
---
source_url: https://northflank.com/docs/v1/api/pipelines/get-release-flow
title: Get release flow | Pipelines | Northflank API docs
crawl_date: 2025-07-29T10:46:33.758333
watsonmd_version: 0.1.0
---

Pipelines / 

# Get release flow

Gets details about a release flow

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

boolean required

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

      * richInputs

[array]

An array of rich UI override inputs for the Release Flow template.

        * (multiple options: oneOf)

A node representing a rich UI override for the Release Flow template.

          * {object}

BranchCommitSelector input

            * kind

string required

The kind of input.

one of

BranchCommitSelector

            * spec

{object} required

The specification for the BranchCommitSelector input.

OR

          * {object}

BuildSelector input

            * kind

string required

The kind of input.

one of

BuildSelector

            * spec

{object} required

The specification for the BuildSelector input.

      * spec

(multiple options: oneOf) required

A node representing an action to be performed as part of the template.

      * concurrencyPolicy

string

Defines the concurrency behaviour of the template with respect to parallel runs.

one of

allow, queue, forbid

      * stage

string

The stage of the pipeline this release flow belongs to.

      * status

string required

Status of the template run

one of

pending, running, success, failure, aborted, aborting, queued, unknown, skipped

      * paused

boolean required

Whether triggers are paused for this release flow. If `true`, Git triggers and webhook triggers will not run the release flow.

      * createdAt

string required

Timestamp the template was created at.

      * updatedAt

string required

Timestamp the template was last updated at.




API

CLI

JS Client

GET /v1/projects/{projectId}/pipelines/{pipelineId}/release-flows/{stage}

Example response

200 OK

Details about a release flow.

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
        "richInputs": [
          {
            "kind": "BranchCommitSelector",
            "spec": {
              "required": false,
              "inputs": {
                "source": "build-service"
              },
              "outputs": {
                "branch": "TARGET_BRANCH",
                "buildSha": "TARGET_COMMIT"
              }
            }
          }
        ],
        "spec": {
          "kind": "Workflow"
        },
        "concurrencyPolicy": "allow",
        "stage": "Development",
        "status": "success",
        "paused": false,
        "createdAt": "2021-01-01 12:00:00.000Z",
        "updatedAt": "2021-01-01 12:00:00.000Z"
      }
    }
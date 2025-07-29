---
source_url: https://northflank.com/docs/v1/api/services/update-service-build-options
title: Update service build options | Services | Northflank API docs
crawl_date: 2025-07-29T10:02:16.613726
watsonmd_version: 0.1.0
---

Services / 

# Update service build options

Updates the build options for a given service.

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

Build from a Dockerfile

    * dockerfile

{object} required

      * buildEngine

string

Build engine to use. Defaults to recommended build engine `buildkit`

one of

buildkit, kaniko

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

      * buildkit

{object}

        * useCache

boolean

Use persistent storage to cache build layers.

        * cacheStorageSize

integer

The amount of persistent storage available to each build in MB.

        * useInternalCache

boolean

DEPRECATED: This field will be removed in the near future.

        * internalCacheStorage

integer

DEPRECATED: This field will be removed in the near future.

    * prRestrictions

[array]

An array of pull request build rules. Only supported for build services. Each commit belonging to a pull request on a branch that matches one of the provided build rules will be built automatically.

      * string

A pull request build rule. Can contain `*` as a wildcard to match multiple branch names. For example, `feature/*` will build all commits from pull requests from branches that start with `feature/`.

pattern

^[^?:@$~ [\\]{}]*$

    * branchRestrictions

[array]

An array of branch build rules. Only supported for build services. Each commit belonging to a branch that matches one of the provided build rules will be built automatically.

      * string

A branch build rule. Can contain `*` as a wildcard to match multiple branch names. For example, `feature/*` will build all commits from branches that start with `feature/`.

pattern

^[^?:@$~ [\\]{}]*$

    * pathIgnoreRules

[array]

An array of path ignore rules. A commit will only be built if a file has been changed that does not match any of the ignore rules. Path ignore rules follow `.gitignore` syntax.

      * string

A path ignore rule, following `.gitignore` syntax. For example, `*.md` will ignore all files ending with `.md`.

max length

260

    * isAllowList

boolean

If `true`, the functionality of `pathIgnoreRules` will be inverted. A commit will only be built if a file has been changed that matches one or more of the rules in `pathIgnoreRules`.

    * ciIgnoreFlagsEnabled

boolean

If `true`, enables commit ignore flags. If a commit message contains one or more of the flags in `ciIgnoreFlags`, that commit will not be built.

    * ciIgnoreFlags

[array]

An array of commit ignore flags. If a commit message contains one or more of these flags, that commit will not be built. Defaults to `["[skip ci]", "[ci skip]", "[no ci]", "[skip nf]", "[nf skip]", "[northflank skip]", "[skip northflank]"]`

      * string

A commit ignore flag.

max length

72

    * dockerfileTarget

string

If your Dockerfile contains multiple build stages, you can specify the target stage by entering its name here.

    * dockerCredentials

[array]

      * string

The ID of the docker credentials to use.

pattern

^[A-Za-z0-9-]+$

    * includeGitFolder

boolean

Include .git folder inside the build context

    * fullGitClone

boolean

Include the entire git history as part of the .git folder. Only relevant if "includeGitFolder" is set.

    * storage

{object}

      * ephemeralStorage

{object}

        * storageSize

integer

Ephemeral storage per build in MB

one of

16384, 32768, 65536, 131072, 262144, 524288

min

16384

max

65536




OR

  * {object}

Build from a Buildpack

    * buildpack

{object} required

      * builder

string

Buildpack stack to use. Defaults to recommended stack `HEROKU_24`.

one of

HEROKU_24, HEROKU_22, HEROKU_22_CLASSIC, HEROKU_20, HEROKU_18, GOOGLE_22, GOOGLE_V1, CNB_ALPINE, CNB_BIONIC, PAKETO_JAMMY_TINY, PAKETO_JAMMY_BASE, PAKETO_JAMMY_FULL, PAKETO_TINY, PAKETO_BASE, PAKETO_FULL

      * buildpackLocators

[array]

Array of custom buildpacks to use.

        * string

Url or registry identifier of custom buildpack.

      * buildContext

string

The working directory to build in.

pattern

^\/([a-zA-Z0-9-._]+\/)*[a-zA-Z0-9-._]*$

      * useCache

boolean

Should build dependencies be cached?

    * pathIgnoreRules

[array]

An array of path ignore rules. A commit will only be built if a file has been changed that does not match any of the ignore rules. Path ignore rules follow `.gitignore` syntax.

      * string

A path ignore rule, following `.gitignore` syntax. For example, `*.md` will ignore all files ending with `.md`.

max length

260

    * isAllowList

boolean

If `true`, the functionality of `pathIgnoreRules` will be inverted. A commit will only be built if a file has been changed that matches one or more of the rules in `pathIgnoreRules`.

    * ciIgnoreFlagsEnabled

boolean

If `true`, enables commit ignore flags. If a commit message contains one or more of the flags in `ciIgnoreFlags`, that commit will not be built.

    * ciIgnoreFlags

[array]

An array of commit ignore flags. If a commit message contains one or more of these flags, that commit will not be built. Defaults to `["[skip ci]", "[ci skip]", "[no ci]", "[skip nf]", "[nf skip]", "[northflank skip]", "[skip northflank]"]`

      * string

A commit ignore flag.

max length

72




OR

  * {object}

Don't modify build type settings

    * prRestrictions

[array]

An array of pull request build rules. Only supported for build services. Each commit belonging to a pull request on a branch that matches one of the provided build rules will be built automatically.

      * string

A pull request build rule. Can contain `*` as a wildcard to match multiple branch names. For example, `feature/*` will build all commits from pull requests from branches that start with `feature/`.

pattern

^[^?:@$~ [\\]{}]*$

    * branchRestrictions

[array]

An array of branch build rules. Only supported for build services. Each commit belonging to a branch that matches one of the provided build rules will be built automatically.

      * string

A branch build rule. Can contain `*` as a wildcard to match multiple branch names. For example, `feature/*` will build all commits from branches that start with `feature/`.

pattern

^[^?:@$~ [\\]{}]*$

    * pathIgnoreRules

[array]

An array of path ignore rules. A commit will only be built if a file has been changed that does not match any of the ignore rules. Path ignore rules follow `.gitignore` syntax.

      * string

A path ignore rule, following `.gitignore` syntax. For example, `*.md` will ignore all files ending with `.md`.

max length

260

    * isAllowList

boolean

If `true`, the functionality of `pathIgnoreRules` will be inverted. A commit will only be built if a file has been changed that matches one or more of the rules in `pathIgnoreRules`.

    * ciIgnoreFlagsEnabled

boolean

If `true`, enables commit ignore flags. If a commit message contains one or more of the flags in `ciIgnoreFlags`, that commit will not be built.

    * ciIgnoreFlags

[array]

An array of commit ignore flags. If a commit message contains one or more of these flags, that commit will not be built. Defaults to `["[skip ci]", "[ci skip]", "[no ci]", "[skip nf]", "[nf skip]", "[northflank skip]", "[skip northflank]"]`

      * string

A commit ignore flag.

max length

72

    * dockerfileTarget

string

If your Dockerfile contains multiple build stages, you can specify the target stage by entering its name here.

    * dockerCredentials

[array]

      * string

The ID of the docker credentials to use.

pattern

^[A-Za-z0-9-]+$

    * includeGitFolder

boolean

Include .git folder inside the build context

    * fullGitClone

boolean

Include the entire git history as part of the .git folder. Only relevant if "includeGitFolder" is set.

    * storage

{object}

      * ephemeralStorage

{object}

        * storageSize

integer

Ephemeral storage per build in MB

one of

16384, 32768, 65536, 131072, 262144, 524288

min

16384

max

65536




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

POST /v1/projects/{projectId}/services/{serviceId}/build-options

Example request

Request body

Build from a Dockerfile

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"dockerfile":{"buildEngine":"buildkit","dockerFilePath":"/Dockerfile","dockerWorkDir":"/"},"prRestrictions":["feature/*"],"branchRestrictions":["feature/*"],"pathIgnoreRules":["README.md"],"isAllowList":false,"ciIgnoreFlags":["[skip ci]"],"dockerCredentials":["example-docker-credential"],"storage":{"ephemeralStorage":{"storageSize":16384}}}' \
      https://api.northflank.com/v1/projects/{projectId}/services/{serviceId}/build-options

OR

Build from a Buildpack

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"buildpack":{"builder":"HEROKU_24","buildpackLocators":["https://buildpack-registry.heroku.com/cnb/mars/create-react-app"],"buildContext":"/","useCache":false},"pathIgnoreRules":["README.md"],"isAllowList":false,"ciIgnoreFlags":["[skip ci]"]}' \
      https://api.northflank.com/v1/projects/{projectId}/services/{serviceId}/build-options

OR

Don't modify build type settings

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"prRestrictions":["feature/*"],"branchRestrictions":["feature/*"],"pathIgnoreRules":["README.md"],"isAllowList":false,"ciIgnoreFlags":["[skip ci]"],"dockerCredentials":["example-docker-credential"],"storage":{"ephemeralStorage":{"storageSize":16384}}}' \
      https://api.northflank.com/v1/projects/{projectId}/services/{serviceId}/build-options

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }
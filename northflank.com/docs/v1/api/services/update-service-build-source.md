---
source_url: https://northflank.com/docs/v1/api/services/update-service-build-source
title: Update service build source | Services | Northflank API docs
crawl_date: 2025-07-29T09:57:23.514039
watsonmd_version: 0.1.0
---

Services / 

# Update service build source

Updates the version control source for a given build or combined service.

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

    * projectUrl

string

URL of the Git repo to build.

pattern

^(https:\/\/)?((www(\\.[a-zA-Z0-9\\-]{2,})+\\.)?[a-zA-Z0-9\\-]{2,})(\\.([a-zA-Z0-9\\-]{2,}))+(\/([a-zA-Z0-9\\-._]{2,}))+?$

    * projectType

string

The VCS provider to use.

one of

bitbucket, gitlab, github, self-hosted, azure

    * projectBranch

string

The name of the branch to use.

    * selfHostedVcsId

string

If projectType is self-hosted, the ID of the self-hosted vcs to use.

pattern

^([A-Za-z0-9-]+\/[A-Za-z0-9-]+)|([0-9a-f]{24})$

    * accountLogin

string

By default, if you have multiple version control accounts of the same provider linked, Northflank will pick a linked account that has access to the repository. If `accountLogin` is provided, Northflank will instead use your linked account with that login name.




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

POST /v1/projects/{projectId}/services/{serviceId}/build-source

Example request

Request body

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"projectUrl":"https://github.com/northflank/gatsby-with-northflank","projectType":"github","projectBranch":"master","accountLogin":"github-user"}' \
      https://api.northflank.com/v1/projects/{projectId}/services/{serviceId}/build-source

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }
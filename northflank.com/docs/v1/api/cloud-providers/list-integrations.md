---
source_url: https://northflank.com/docs/v1/api/cloud-providers/list-integrations
title: List integrations | Cloud Providers | Northflank API docs
crawl_date: 2025-07-29T10:44:52.670022
watsonmd_version: 0.1.0
---

Cloud Providers / 

# List integrations

Lists integrations for the authenticated user or team.

Required permission

Account > Cloud > Integrations > Read

Query parameters

    * per_page

integer

The number of results to display per request. Maximum of 100 results per page.

    * page

integer

The page number to access.

    * cursor

string

The cursor returned from the previous page of results, used to request the next page.




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * integrations

[array] required

An array of integrations.

        * {object}

An integration object.

          * name

string required

The name of the cloud provider integration.

min length

3

max length

39

pattern

^[a-zA-Z]((-|\s)?[a-zA-Z0-9]+((-|\s)[a-zA-Z0-9]+)*)?$

          * description

string

The description of the integration.

max length

200

pattern

^[a-zA-Z0-9.,?\s\\\/'"()[\\];`%^&*\\-_:!]+$

          * provider

string required

Cloud provider to be used for the selected resource

one of

aws, azure, civo, gcp, oci, cloudflare, byok

          * features

[array]

            * string

The type of provider integration.

one of

byoc, byoc-static-egress, byoc-custom-launch-templates, byoc-custom-vpc, byoc-logs, cloudfront, route53, registry-pull, registry-push, opentofu

          * restrictions

{object}

BYOC restrictions configuration for controlling team access

            * enabled

boolean required

Enable or disable BYOC restrictions for this entity

            * teams

[array]

List of teams that have access to this BYOC cluster

              * {object}

                * teamId

string required

The ID of the team that has access to this BYOC cluster

          * aws

{object}

AWS specific data. Required when `provider` is `aws`.

            * authenticationMode

string

The provider authentication mode to use for this integration.

one of

accessKey, crossAccountRole

          * gcp

{object}

GCP specific data. Required when `provider` is `gcp`.

            * projectId

string required

GCP Project ID

            * authenticationMode

string

The provider authentication mode to use for this integration.

one of

accessKey, crossAccountRole

          * cloudflare

{object}

Cloudflare specific data. Required when `provider` is `cloudflare`.

            * credentialType

string

The type of api key

one of

apiToken, originCAKey, globalApiKey

          * id

string required

ID of the integration

pattern

^[A-Za-z0-9-]+$

          * createdAt

string required

The time the integration was created.

    * pagination

{object} required

Data about the endpoint pagination.

      * hasNextPage

boolean required

Is there another page of results available?

      * cursor

string

The cursor to access the next page of results.

      * count

number required

The number of results returned by this request.




API

CLI

JS Client

GET /v1/cloud-providers/integrations

Example response

200 OK

A list of integrations for the authenticated user

JSON
    
    
    {
      "data": {
        "integrations": [
          {
            "name": "Example Integration",
            "description": "This is a new cloud provider integration.",
            "provider": "gcp",
            "features": [
              "byoc"
            ],
            "aws": {
              "authenticationMode": "accessKey"
            },
            "gcp": {
              "authenticationMode": "accessKey"
            },
            "cloudflare": {
              "credentialType": "apiToken"
            },
            "id": "example-integration",
            "createdAt": "2021-01-20T11:19:53.175Z"
          }
        ]
      },
      "pagination": {
        "hasNextPage": false,
        "count": 1
      }
    }
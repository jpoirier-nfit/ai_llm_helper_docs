---
source_url: https://northflank.com/docs/v1/api/cloud-providers/get-integration
title: Get integration | Cloud Providers | Northflank API docs
crawl_date: 2025-07-29T10:44:52.437047
watsonmd_version: 0.1.0
---

Cloud Providers / 

# Get integration

Get information about the given integration

Required permission

Account > Cloud > Integrations > Read

Path parameters

    * integrationId

string required

ID of the provider integration




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * id

string required

ID of the integration

pattern

^[A-Za-z0-9-]+$

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

      * credentials

{object} required

Cloud provider credential input, required fields dependent on which provider is chosen.

        * keyfileJson

string

Contents of a GCP key file.

        * accessKey

string

AWS access key.

        * secretKey

string

AWS secret key.

        * roleArn

string

AWS IAM role ARN.

        * externalId

string

AWS shared secret (external id).

        * apiKey

string

API key.

        * email

string

Email address for Cloudflare global API key.

        * tenantId

string

Directory (tenant) ID 

        * clientId

string

Application (client) ID 

        * objectId

string

Object ID

        * secret

string

Secret

        * subscriptionId

string

Azure Subscription ID

        * region

string

OCI Authentication Region

        * tenancyId

string

OCI Tenancy ID

        * userId

string

User ID

        * fingerprint

string

Fingerprint

        * privateKey

string

OCI Private Key

        * passphrase

string

Passphrase

        * compartmentId

string

OCI Compartment ID

        * kubeconfig

string

Kubeconfig

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

        * serviceAccountEmail

string

Service account email that will be used for cross account access.

      * cloudflare

{object}

Cloudflare specific data. Required when `provider` is `cloudflare`.

        * credentialType

string

The type of api key

one of

apiToken, originCAKey, globalApiKey

      * createdAt

string required

The time the integration was created.




API

CLI

JS Client

GET /v1/cloud-providers/integrations/{integrationId}

Example response

200 OK

Details about the given integration.

JSON
    
    
    {
      "data": {
        "id": "example-integration",
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
        "createdAt": "2021-01-20T11:19:53.175Z"
      }
    }
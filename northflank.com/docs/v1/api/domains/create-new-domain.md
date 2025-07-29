---
source_url: https://northflank.com/docs/v1/api/domains/create-new-domain
title: Create new domain | Domains | Northflank API docs
crawl_date: 2025-07-29T10:02:17.121782
watsonmd_version: 0.1.0
---

Domains / 

# Create new domain

Registers a new domain

Required permission

Account > Domains > General > Create

Request body

  * {object}

    * domain

string required

The domain name to register.

pattern

^((www(\\.[a-zA-Z0-9\\-]{2,})+\\.)?[a-zA-Z0-9\\-]{2,})(\\.([a-zA-Z0-9\\-]{2,}))+$

    * redirect

{object}

Optional configuration regarding the domain redirect set up.

      * mode

string

Domain redirect mode to be used.

one of

wildcard, default

      * region

string

Northflank PaaS region the wildcard redirect should be pointed at.

      * cluster

string

BYOC cluster the wildcard redirect should be pointed at.

    * certificates

{object}

Optional configuration regarding the domain certificate set up.

      * mode

string

Certificate provisioning mode to be used.

one of

wildcard, wildcard-import, default

      * certificateInput

{object}

        * certificateInput

{object}

Certificate data - required when `mode` is set to `wildcard-import`

          * is

one of

wildcard-import

          * then

{object} required

            * privateKey

string required

Certificate private key.

            * certificateChain

string required

Certificate chain. May consist of one or more certificates.




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * name

string required

The domain name.

      * status

string required

The status of the domain verification.

one of

pending, verified

      * hostname

string

The hostname to add to your domain's DNS records as a TXT record to verify the domain.

      * token

string

The token to add as the content of the TXT record to verify the domain.

      * redirect

{object}

Configuration regarding the domain redirect set up.

        * mode

string required

Domain redirect mode.

        * target

{object}

          * record

string

Expected CNAME target of the wildcard redirect.

      * certificates

{object}

Configuration regarding the domain certificate set up.

        * mode

string required

Domain certificate mode.

        * dcvRecord

string

DCV CNAME record used to provision wildcard certificates.

        * dcvTarget

{object}

          * record

string

Expected CNAME target of the dcvRecord.

        * status

{object}

Certificate status for wildcard domains.

          * expiryDate

string

Expiry date of the current certificate.




API

CLI

JS Client

POST /v1/domains

Example request

Request body

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"domain":"example.com","redirect":{"mode":"default"},"certificates":{"mode":"default"}}' \
      https://api.northflank.com/v1/domains

Example response

200 OK

Details about the newly added domain.

JSON
    
    
    {
      "data": {
        "name": "example.com",
        "status": "pending",
        "hostname": "nfverify1608026055",
        "token": "e596987b52855a4a773ef580ce2985d7746b37ce8b2a443d20fa27b913d8f57",
        "redirect": {
          "mode": "default"
        },
        "certificates": {
          "mode": "default"
        }
      }
    }

Example response

400 Bad Request

The domain is not valid, possibly because it is too long.

Example response

409 Conflict

The domain is already registered with this account.
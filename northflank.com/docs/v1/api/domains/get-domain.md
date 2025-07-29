---
source_url: https://northflank.com/docs/v1/api/domains/get-domain
title: Get domain | Domains | Northflank API docs
crawl_date: 2025-07-29T10:02:17.137751
watsonmd_version: 0.1.0
---

Domains / 

# Get domain

Gets details about domain

Required permission

Account > Domains > General > Read

Path parameters

    * domain

string required

Name of the domain




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

      * subdomains

[array] required

A list of subdomains added to this domain.

        * {object}

Details about a subdomain.

          * name

string required

The subdomain added, or -default for the empty subdomain.

          * fullName

string required

The full domain including the subdomain.




API

CLI

JS Client

GET /v1/domains/{domain}

Example response

200 OK

Details about the given domain.

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
        },
        "subdomains": [
          {
            "name": "app",
            "fullName": "app.example.com"
          }
        ]
      }
    }
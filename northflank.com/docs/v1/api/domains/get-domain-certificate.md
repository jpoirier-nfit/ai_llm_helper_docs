---
source_url: https://northflank.com/docs/v1/api/domains/get-domain-certificate
title: Get domain certificate | Domains | Northflank API docs
crawl_date: 2025-07-29T10:04:44.331678
watsonmd_version: 0.1.0
---

Domains / 

# Get domain certificate

Retrieve certificate data for a domain to verify its contents.

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

      * certificateChain

string required

Certificate chain. May consist of one or more certificates.

      * certificate

string required

Certificate extracted from the certificate chain.

      * issuerCertificate

string required

Issuer certificate extracted from the certificate chain.

      * privateKey

string required

Certificate private key.




API

CLI

JS Client

GET /v1/domains/{domain}/certificate

Example response

200 OK

Details about the domain certificate.

JSON
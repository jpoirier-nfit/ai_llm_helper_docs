---
source_url: https://northflank.com/docs/v1/api/services/get-service-ports
title: Get service ports | Services | Northflank API docs
crawl_date: 2025-07-29T10:02:16.916336
watsonmd_version: 0.1.0
---

Services / 

# Get service ports

Lists the ports for the given service.

Required permission

Project > Services > General > Read

Path parameters

    * projectId

string required

ID of the project

    * serviceId

string required

ID of the service




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * ports

[array] required

An array of ports of the service.

        * {object}

          * id

string required

The id used to identify the port across requests.

pattern

^[a-z]-?[a-z0-9]+(-[a-z0-9]+)*$

          * name

string required

The name of the port used in the public url and UI.

pattern

^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

          * internalPort

integer required

The port number.

          * protocol

string required

The protocol used by the port.

one of

HTTP, HTTP/2, TCP, UDP

          * public

boolean required

If true, the port is exposed publicly.

          * dns

string

DNS entry for this port.

          * domains

[array] required

An array of domains that redirect to this port.

            * {object}

              * name

string required

The custom domain redirecting to this port.

              * certificate

{object} required

Details about the TLS certificate generation for this domain.

                * inProgress

boolean

Is the certificate in the process of being generated?

                * expiryDate

string

The timestamp when the TLS certificate will expire.

                * refreshDate

string

The timestamp when a new TLS certificate will be generated.

          * security

{object}

Details about security settings for this port.

            * credentials

[array]

An array of credentials to access the service.

              * {object}

                * username

string required

The username to access the service

min length

3

max length

39

pattern

^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

                * password

string required

The password to access the service with this username.

                * type

string required

The type of authentication used

one of

basic-auth

            * policies

[array]

An array of IP address policies.

              * {object}

                * addresses

[array] required

An array of IP addresses used for this rule

                  * string

An IP address used by this rule

                * action

string required

The action for this rule.

one of

ALLOW, DENY

            * sso

{object}

Configure SSO access control for this port.

              * organizationId

string

Organization ID of the work OS organization that should be validated.

              * directoryGroupIds

[array]

List of directory groupIds, one of which the user has to be a member of.

                * string

              * validateInternalTraffic

boolean

Enforce internal traffic through SSO authentication flow

              * setCookieOnRootDomain

boolean

Set SSO authentication cookie on root domain

              * allowInternalTrafficViaPublicDns

boolean

Allow internal traffic from same or shared projects via public DNS to skip SSO authentication flow

            * verificationMode

string

Mode used to verify multiple security features like ip policies and SSO authentication

one of

or, and

            * headers

[array]

List of header authentication settings, it checks the presence of all headers and compares it against the expected value. Wildcard (*) is supported.

              * {object}

                * regexMode

boolean

                * name

(multiple options: oneOf)

                  * string

OR

                  * string

pattern

^[a-zA-Z0-9_\\-%$+]+$

                * value

string required

          * disableNfDomain

boolean

Disable routing on the default code.run domain for public HTTP ports with custom domains.




API

CLI

JS Client

GET /v1/projects/{projectId}/services/{serviceId}/ports

Example response

200 OK

Details about the ports for the service.

JSON
    
    
    {
      "data": {
        "ports": [
          {
            "id": "eonyui",
            "name": "p01",
            "internalPort": 8080,
            "protocol": "HTTP",
            "public": true,
            "dns": "p01--example-service--default-service--user-abc1.salvo.code.run",
            "domains": [
              {
                "name": "app.example.com",
                "certificate": {
                  "inProgress": false,
                  "expiryDate": "2022-04-26T09:25:02.000Z",
                  "refreshDate": "2022-03-27T09:25:02.000Z"
                }
              }
            ],
            "security": {
              "credentials": [
                {
                  "username": "admin",
                  "password": "password123",
                  "type": "basic-auth"
                }
              ],
              "policies": [
                {
                  "addresses": [
                    "127.0.0.1"
                  ],
                  "action": "DENY"
                }
              ],
              "sso": {
                "organizationId": "org_uniquestringidentifier",
                "directoryGroupIds": [
                  "directory_group_uniquestringidentifier"
                ]
              }
            },
            "disableNfDomain": false
          }
        ]
      }
    }
---
source_url: https://northflank.com/docs/v1/api/services/update-service-ports
title: Update service ports | Services | Northflank API docs
crawl_date: 2025-07-29T09:57:23.863600
watsonmd_version: 0.1.0
---

Services / 

# Update service ports

Updates the list of ports for the given service.

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

    * ports

[array] required

An array of ports to replace or update existing ports with.

      * {object}

        * id

string

The id of an existing port. Pass this when changing in order to keep security configurations.

pattern

^[a-z]-?[a-z0-9]+(-[a-z0-9]+)*$

        * name

string required

The name used to identify the port.

min length

1

max length

8

pattern

^[a-zA-Z](-?[a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)?$

        * internalPort

integer required

The port number.

min

1

max

65535

        * public

boolean

If true, the port will be exposed publicly.

        * protocol

string required

The protocol to use for the port. Public ports only support `HTTP` and `HTTP/2`.

one of

HTTP, HTTP/2, TCP, UDP

        * domains

[array]

An array of domains to redirect to this port. Each domain must first be verified and registered to your account.

          * string

A domain to redirect to this port.

        * security

{object}

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

          * ip

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

Configure port authentication via SSO

            * organizationId

string

ID of the SSO organization that the user will have to be a member of

            * directoryGroupIds

[array]

Array of directory groups that will have access

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

          * headers

[array]

List of header authentication settings, it checks the presence of all headers and compares it against the expected value. Wildcard (*) is supported.

            * (multiple options: anyOf)

              * {object}

Matches provided headers as strings.

                * regexMode

boolean

                * name

string required

pattern

^[a-zA-Z0-9_\\-%$+]+$

                * value

string required

OR

              * {object}

Matches provided headers as regex.

                * regexMode

boolean

                * name

string required

                * value

string required

          * verificationMode

string

Mode used to verify multiple security features like ip policies and SSO authentication

one of

or, and

          * securePathConfiguration

{object}

            * enabled

boolean

Enable security policies on a path-level style

            * skipSecurityPoliciesForInternalTrafficViaPublicDns

boolean

Allow internal traffic from same or shared projects via public DNS to skip all security policies

            * rules

[array]

              * {object}

                * paths

[array] required

Array of path objects which represent the paths and their priority for which the security policies will be enforced

                  * (multiple options: oneOf)

Data about how the path should be handled.

                    * {object}

Route when the path starts with the provided prefix.

                      * path

string required

pattern

^\/([_a-zA-Z0-9-&?=.]*)((\/[_a-zA-Z0-9-&?=.]+)*(\/)?)?$

                      * routingMode

string required

Mode of the path, determining how the URI will be interpreted.

one of

prefix

                      * priority

integer required

min

0

max

100

OR

                    * {object}

Route when the path is an exact match.

                      * path

string required

pattern

^\/([_a-zA-Z0-9-&?=.]*)((\/[_a-zA-Z0-9-&?=.]+)*(\/)?)?$

                      * routingMode

string required

Mode of the path, determining how the URI will be interpreted.

one of

exact

                      * priority

integer required

min

0

max

100

OR

                    * {object}

Route when the path matches the provided regex.

                      * path

string required

                      * routingMode

string required

Mode of the path, determining how the URI will be interpreted.

one of

regex

                      * priority

integer required

min

0

max

100

                * accessMode

string required

Specify the way the path rule will behave when processing policies. This enables an allow-list/deny-list approach for access control on each path

one of

protected, unprotected

                * securityPolicies

{object}

                  * orPolicies

{object}

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

                    * ip

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

Configure port authentication via SSO

                      * organizationId

string

ID of the SSO organization that the user will have to be a member of

                      * directoryGroupIds

[array]

Array of directory groups that will have access

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

                    * headers

[array]

List of header authentication settings, it checks the presence of all headers and compares it against the expected value. Wildcard (*) is supported.

                      * (multiple options: anyOf)

                        * {object}

Matches provided headers as strings.

                          * regexMode

boolean

                          * name

string required

pattern

^[a-zA-Z0-9_\\-%$+]+$

                          * value

string required

OR

                        * {object}

Matches provided headers as regex.

                          * regexMode

boolean

                          * name

string required

                          * value

string required

                  * requiredPolicies

{object}

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

                    * ip

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

Configure port authentication via SSO

                      * organizationId

string

ID of the SSO organization that the user will have to be a member of

                      * directoryGroupIds

[array]

Array of directory groups that will have access

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

                    * headers

[array]

List of header authentication settings, it checks the presence of all headers and compares it against the expected value. Wildcard (*) is supported.

                      * (multiple options: anyOf)

                        * {object}

Matches provided headers as strings.

                          * regexMode

boolean

                          * name

string required

pattern

^[a-zA-Z0-9_\\-%$+]+$

                          * value

string required

OR

                        * {object}

Matches provided headers as regex.

                          * regexMode

boolean

                          * name

string required

                          * value

string required

        * disableNfDomain

boolean

Disable routing on the default code.run domain for public HTTP ports with custom domains.




Response body

  * {object}

Response object.

    * data

{object} required

Result data.




API

CLI

JS Client

POST /v1/projects/{projectId}/services/{serviceId}/ports

Example request

Request body

curl
    
    
    curl --header "Content-Type: application/json" \
      --header "Authorization: Bearer NORTHFLANK_API_TOKEN" \
      --request POST \
      --data '{"ports":[{"id":"p01","name":"p01","internalPort":12345,"public":true,"protocol":"HTTP","domains":["app.example.com"],"security":{"credentials":[{"username":"admin","password":"password123","type":"basic-auth"}],"ip":[{"addresses":["127.0.0.1"],"action":"DENY"}],"policies":[{"addresses":["127.0.0.1"],"action":"DENY"}],"headers":[{"regexMode":false}],"securePathConfiguration":{"rules":[{"paths":[{"routingMode":"prefix"}],"securityPolicies":{"orPolicies":{"credentials":[{"username":"admin","password":"password123","type":"basic-auth"}],"ip":[{"addresses":["127.0.0.1"],"action":"DENY"}],"policies":[{"addresses":["127.0.0.1"],"action":"DENY"}],"headers":[{"regexMode":false}]},"requiredPolicies":{"credentials":[{"username":"admin","password":"password123","type":"basic-auth"}],"ip":[{"addresses":["127.0.0.1"],"action":"DENY"}],"policies":[{"addresses":["127.0.0.1"],"action":"DENY"}],"headers":[{"regexMode":false}]}}}]}}}]}' \
      https://api.northflank.com/v1/projects/{projectId}/services/{serviceId}/ports

Example response

200 OK

The operation was performed successfully.

JSON
    
    
    {
      "data": {}
    }

Example response

404 Not Found

One of the provided domains has not been registered to this account.
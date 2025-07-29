---
source_url: https://northflank.com/docs/v1/api/projects/get-project
title: Get project | Projects | Northflank API docs
crawl_date: 2025-07-29T09:24:10.670011
watsonmd_version: 0.1.0
---

Projects / 

# Get project

Get information about the given project

Required permission

Project > Projects > Manage > Read

Path parameters

    * projectId

string required

ID of the project




Response body

  * {object}

Response object.

    * data

{object} required

Result data.

      * id

string required

Identifier for the project.

      * name

string required

The name of the project.

      * description

string

A short description of the project.

      * deployment

{object} required

        * region

string required

The region where the project's services, jobs and addons are deployed in.

      * createdAt

string required

The time the project was created.

      * services

[array] required

An array of services belonging to the project.

        * {object}

A service object.

          * id

string required

Identifier for the service.

          * appId

string required

Full identifier used for service deployment

          * name

string required

The name of the service.

          * description

string

A short description of the service.

          * serviceType

string required

Type of the service (combined, build or deployment)

one of

combined, build, deployment

      * jobs

[array] required

An array of jobs belonging to the project.

        * {object}

A job object.

          * id

string required

Identifier for the job.

          * appId

string required

Full identifier used for deployment

          * name

string required

The name of the job.

          * description

string

A short description of the job.

          * jobType

string required

Type of the job (manual or cron)

one of

manual, cron

      * addons

[array] required

An array of addons belonging to the project.

        * {object}

An addon object.

          * id

string required

Identifier for the addon.

          * appId

string required

Full identifier used for deployment

          * name

string required

The name of the addon.

          * description

string

A short description of the addon.

          * spec

{object} required

Details about the addon's specifications.

      * cluster

{object} required

Cluster information

        * id

string required

The id of the cluster associated with this project.

        * name

string required

The name of the cluster associated with this project.

        * namespace

string

Namespace this resource is located within on the cluster.

        * loadBalancers

[array]

Load balancer DNS for the cluster.

          * string




API

CLI

JS Client

GET /v1/projects/{projectId}

Example response

200 OK

Details about the given project.

JSON
    
    
    {
      "data": {
        "id": "default-project",
        "name": "Default Project",
        "description": "The project description",
        "deployment": {
          "region": "europe-west"
        },
        "createdAt": "2021-01-20T11:19:53.175Z",
        "services": [
          {
            "id": "example-service",
            "appId": "/example-user/default-project/example-service",
            "name": "Example Service",
            "description": "This is the service description",
            "serviceType": "combined"
          }
        ],
        "jobs": [
          {
            "id": "example-job",
            "appId": "/example-user/default-project/example-job",
            "name": "Example Job",
            "description": "This is the job description",
            "jobType": "cron"
          }
        ],
        "addons": [
          {
            "id": "example-addon",
            "appId": "/example-user/default-project/example-addon",
            "name": "Example Addon",
            "description": "This is the addon description",
            "spec": {
              "type": "mongodb"
            }
          }
        ],
        "cluster": {
          "id": "nf-europe-west",
          "name": "nf-europe-west",
          "namespace": "ns-8zy2mcjh9zn2",
          "loadBalancers": [
            "lb.659200800000000000000000.northflank.com"
          ]
        }
      }
    }
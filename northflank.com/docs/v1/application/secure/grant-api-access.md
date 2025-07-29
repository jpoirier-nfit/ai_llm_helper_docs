---
source_url: https://northflank.com/docs/v1/application/secure/grant-api-access
title: Grant API access | Secure | Northflank Application docs
crawl_date: 2025-07-29T10:44:49.123887
watsonmd_version: 0.1.0
---

Secure / 

# Grant API access

An API token authenticates a user or program to an application programming interface (API). The Northflank API uses [JSON Web Tokens (JWT) ](https://jwt.io/introduction) for authentication.

To create an API token you will first need to create an API role. An API role defines the permissions that a generated token has to access and update resources in your team.

Manage API roles

API roles define the permissions granted by the API tokens that you and your team members can generate. You can edit roles after they are created to update permissions in real time.

You can create or edit an API role from the [API roles page in your team account ](https://app.northflank.com/s/account/api/roles).

You must select the users the role is available to. Only the team members added to the role will be able to create API tokens with the role.

![Creating an API role in the Northflank application](https://assets.northflank.com/documentation/v1/application/secure/grant-api-access/create-api-role.png)

### Restrict a role to specific projects

You can restrict roles to only allow access to specific projects, or leave unrestricted to grant the permissions to all projects in the team.

### Select permissions

Permissions are categorised by team and project. Team permissions grant API tokens access to team administration endpoints, team resources, and cloud provider integrations. Project permissions grant users access to project resource endpoints for projects, services, jobs, addons, pipelines, volumes, secrets, and logs and metrics.

### Delete a role

If you delete a role it will revoke all the user tokens generated using the role.

Generate an API token

You and other members of your team can generate API tokens from the [tokens page ](https://app.northflank.com/s/account/api/tokens) in team settings. A user must have an API role available to them to create an API token

Team members that create an API token using the role will be able to view but not modify it, unless they have [permission to edit API roles](use-role-based-access-control).

![Creating a team API token from a role in the Northflank application](https://assets.northflank.com/documentation/v1/application/secure/grant-api-access/create-api-token.png)

To use your API token simply copy the token from either the list or the edit token page and pass it into your application. Your application will now have access to your Northflank projects and services as granted by the token.

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAACXBIWXMAAAsTAAALEwEAmpwYAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAEZSURBVHgB7ZXBDYIwFIbfa030YuIIuoEj6Ml4dALZQDdwBEdwCoPhghs4giuQSMCDoRYEUkqBB8GTfklDaN57//+nDQD8FOEFXbnubXoYtdC3wZKPhVzT4AJ7ah9SC1Pn06QJwRsGYoYb8Jr6SAmeDttlw2OEgEkwoqVoTBDacjCiqwokjcQUjQkYY1t9eAw1RW2C1H3lraGkqE+A7KC+jlZRsjIoKSoFEvcgLGiAM9x9alsK6O6riFPU1RoFqO4VGcs/w5wsQHWvwjkejaP0Dd+BOY/wBh14CbEcr+Gq7pUSyOFH6MgAsZS8IKB80Izo19TA4mEX+wsC3OCgLXqK/Axi91LgBD2gnkWeoA/3GQPFKPmH8+drvAGciFlVpRD4HQAAAABJRU5ErkJggg==)

important

Never share your API token or commit it to a repository! Tokens should be stored securely.

Next steps

[Create a team and invite membersCreate a team and invite members to collaborate on projects.](/docs/v1/application/collaborate/create-a-team)[Configure role-based access controlGrant granular permissions and manage users with roles for teams and organisations.](/docs/v1/application/secure/use-role-based-access-control)
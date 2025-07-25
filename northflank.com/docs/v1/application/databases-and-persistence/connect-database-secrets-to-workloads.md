---
source_url: https://northflank.com/docs/v1/application/databases-and-persistence/connect-database-secrets-to-workloads
title: Connect database secrets to workloads | Databases And Persistence | Northflank Application docs
crawl_date: 2025-07-25T12:06:50.254406
watsonmd_version: 0.1.0
---

Databases And Persistence / 

# Connect database secrets to workloads

Databases can be accessed and used by services within the same project.

The way you connect to your database will depend on the implementation in your application or service. Your deployment should be configured to receive connection details from [runtime variables](../secure/inject-secrets#runtime-variables).

Open the connection details page in your database to view the relevant connection strings and secrets, which you can use to connect to the database from your deployments. You can either add these manually to a specific deployment or secret group, or link the variables to a secret group.

You should not use the administration connection string or administrator account to connect from your deployments, unless deploying a secured administration interface.

Link database secrets to a secret group

You can link a database to a secret group so that the desired secrets are inherited as variables within that secret group. These secrets can then be used in any services and jobs that inherit from that secret group.

[Click here ](https://app.northflank.com/s/project/create/secret) to create a secret group.

You can select the suggested variables to automatically include the most useful and commonly used connection details, or manually select which variables to include.

Variables names are generated using the database name and connection detail, e.g. `NF_MY-DATABASE_HOST`. If your application is expecting certain variable names you can give aliases to the variables, for example adding `DB_HOST` and `ENV_DB_HOST` as aliases to `NF_MY-DATABASE_HOST` means that the variable can be accessed by all three of the aliases in the environment.

After linking the variables they will be available in any service or job in the project that inherits from that secret group.

![Linking an addon's connection details to a secret group in the Northflank application](https://assets.northflank.com/documentation/v1/application/databases-and-persistence/connect-database-secrets-to-workloads/link-addon-to-secret-group.png)

### Link an addon to a secret group

From an addon or secret group creation form, expand the list of addons or secret groups and select `configure`. You can `select suggested` to automatically select the most commonly-used secrets from the addon to configure, or manually select the secrets to include.

Secrets will be added to the group with the default alias, and you can include your own aliases where your Dockerfile or application expects a different key to access the build argument or runtime environment variable.

Alternatively, you can link an existing addon to a secret group from the addon's `connection details` page, or from an existing secret group's `linked addons` page, and then configure the linked variables.

Linked variables can be added or edited from the `linked addons` page of a secret group, or the addon can be unlinked entirely.

Access a database in a build

If you need to connect to an addon during the build process you will need to ensure that your secret group can be [inherited by build services](../secure/manage-secret-groups#secret-group-type). As builds run on separate, dedicated infrastructure from your project, your addon must be publicly exposed, and the service or job you are using to build must inherit [external connection details](access-a-database#expose-a-database-publicly).

Next steps

[Manage groups of secretsCreate and manage groups of secrets that can be inherited throughout an entire project or by specific services and jobs.](/docs/v1/application/secure/manage-secret-groups)[Expose a database with TLSSecure internal database connections or expose it publicly with TLS.](/docs/v1/application/databases-and-persistence/access-a-database)[Inject secretsSet build arguments and inject runtime variables into running deployments.](/docs/v1/application/secure/inject-secrets)[Scale a databaseIncrease the storage size, number of replicas, and the available CPU and memory to improve availability and performance.](/docs/v1/application/databases-and-persistence/scale-a-database)
---
source_url: https://northflank.com/docs/v1/application/databases-and-persistence/fork-an-addon
title: Fork an addon | Databases And Persistence | Northflank Application docs
crawl_date: 2025-07-25T12:06:50.314303
watsonmd_version: 0.1.0
---

Databases And Persistence / 

# Fork an addon

You can fork an addon to create a duplicate of an existing addon. You can use this to easily clone an addon for development and testing, or to safely migrate to an addon with a different major version or configuration.

You can create a duplicate of an existing addon manually, or in a template. The newly forked addon may have a newer minor version than the source backup, but must have the same major version.

Forking is currently available for the following addons:

  * PostgreSQL
  * MongoDB
  * MySQL



Create an addon from a backup

You can fork an addon by creating an addon of the same type. You must have an existing addon that contains a disk backup of the same major version as the fork addon.

In the advanced section of addon creation, expand the `fork existing addon` option. Select the addon you want to clone, and select the disk backup to use when creating the new forked addon. Click `create addon` and your forked addon will begin provisioning with the data from your source addon.

Your newly-forked addon will display the source addon it was created from, but will be entirely separate from the source addon.

Fork an addon in a template

You can create a backup of an existing addon and fork it in a [template](../infrastructure-as-code/write-a-template). This is particularly useful in preview environments, where you may want to use existing data to preview your changes or test a migration, without potentially corrupting your existing databases.

You can use the run backup node to schedule a disk backup of an addon, and open `fork existing addon` in an `addon` node to enter the source addon and backup. If your addon already contains usable backups, for example from a [backup schedule](backup-restore-and-import-data#schedule-backups), you can use `latest` as the `backupId` to fork from the most recent backup.

Below is an example of taking a backup and using the reference (`${refs.sourceData}`) to get the addon (`addonId`) and the backup (`id`). You can ensure the new addon is the same version as the source backup by using the reference property `config.addonVersion`.
    
    
    {
      "apiVersion": "v1.2",
      "spec": {
        "kind": "Workflow",
        "spec": {
          "type": "sequential",
          "steps": [
            {
              "kind": "AddonBackup",
              "spec": {
                "addonId": "postgres",
                "backupType": "snapshot"
              },
              "condition": "success",
              "ref": "sourceData"
            },
            {
              "kind": "Addon",
              "spec": {
                "tlsEnabled": true,
                "billing": {
                  "replicas": 1,
                  "storage": 4096,
                  "storageClass": "ssd",
                  "deploymentPlan": "nf-compute-50"
                },
                "typeSpecificSettings": {
                  "postgresqlConnectionPoolerReplicas": 2,
                  "postgresqlReadConnectionPoolerReplicas": 2
                },
                "tags": [
                  "${args.previewId}"
                ],
                "type": "postgresql",
                "name": "${args.previewId}-database",
                "version": "${refs.sourceData.config.addonVersion}",
                "source": {
                  "addonId": "${refs.sourceData.addonId}",
                  "backupId": "${refs.sourceData.id}"
                },
                "externalAccessEnabled": false,
                "ipPolicies": [],
                "pitrEnabled": false
              }
            }
          ]
        }
      }
    }
    

Next steps

[Upgrade a databaseUpgrade your database to a newer version with one click.](/docs/v1/application/databases-and-persistence/upgrade-a-database)[Scale a databaseIncrease the storage size, number of replicas, and the available CPU and memory to improve availability and performance.](/docs/v1/application/databases-and-persistence/scale-a-database)[Set up a preview environmentCreate templates in your pipelines to automatically generate temporary preview environments to view pull requests and branches.](/docs/v1/application/release/set-up-a-preview-environment)[Create a templateLearn how to create and configure a Northflank template.](/docs/v1/application/infrastructure-as-code/create-a-template)
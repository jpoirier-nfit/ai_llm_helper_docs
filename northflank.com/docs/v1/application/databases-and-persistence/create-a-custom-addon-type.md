---
source_url: https://northflank.com/docs/v1/application/databases-and-persistence/create-a-custom-addon-type
title: Create a custom addon type | Databases And Persistence | Northflank Application docs
crawl_date: 2025-07-25T12:06:50.343540
watsonmd_version: 0.1.0
---

Databases And Persistence / 

# Create a custom addon type

You can create custom addon types for your team to deploy, using Helm charts. These custom types allow you to deploy databases and other applications which Northflank does not currently offer as a managed service, or custom configurations of addons that Northflank does offer.

Custom addons can only be deployed into [clusters in your own cloud account](../bring-your-own-cloud/use-other-cloud-providers-with-northflank), and not in the Northflank managed cloud.

[Click here ](https://app.northflank.com/s/account/addon-types) to view your custom addon types.

Create a custom addon type

You can create a new custom addon type on the addon types page in your team dashboard. To create a custom addon type you must have a Helm chart bundle, as well as any values the Helm chart may require. You can create your own Helm chart, or use a [published Helm chart ](https://artifacthub.io/) for the application you want to deploy.

### Create your Helm chart bundle

A Helm chart bundle can consist of your Helm chart, any values required by your chart, templates, and CRDs. You can [create your own charts ](https://helm.sh/docs/topics/charts/), download them from a library such as [Artifact Hub ](https://artifacthub.io/), or fetch charts using [Helm pull ](https://helm.sh/docs/helm/helm_pull/).

You can create your bundle by navigating to your chart directory in your shell and running `helm package <application-name>`, or using your preferred compression or archiving tool for example `gzip -r chart-directory`. Northflank supports most compression and archive types.

### Upload your bundle

Click `create addon type` on your addon types page in the Northflank team you want to make the application available to. Drag and drop your bundle into the form, or click to select the file to upload. Northflank will run a basic check to ensure it is a valid Helm chart, and to fetch basic metadata.

### Values override

You can provide any values required by the Helm chart as JSON in the Helm values override field. The values provided at this point are only used to validate the Helm chart, and will need to be supplied when an instance of the addon type is deployed.

After uploading and validating your Helm chart bundle, you can configure the rest of the settings for the custom addon.

Configure a custom addon type

You can set the basic details for the custom addon type such as the display name, a description of the addon type, and the color. The ID for the addon type comes from the `name` value in the `Chart.yaml` from your uploaded bundle. Your custom addon type will be saved as a draft if you exit configuration, you can return to edit and create it later.

### Addon type scope

Addon types can be scoped to individual projects, or your entire cluster.

Project-scoped addon types can only deploy resources that belong to namespaced kubernetes resources. Cluster-scoped addon types can deploy cluster-wide resources that do not belong to a namespace.

### Features

You can select whether users can pause, redeploy, or reset a deployed addon.

### Configuration

You can configure the following options for an addon, which affect how it is deployed and how users can interact with the deployed addon:

  * Show template values - allows users to view the values provided to a deployed addon, which may contain sensitive secrets such as API keys
  * Enable modifying template values - allow users to change the override values for the addon, while it is running (triggers a redeployment)
  * Enable error recovery - adds a page to the addon which displays a detailed error log and allows users to attempt to recover it from an error state
  * Use Northflank labels and annotations on Kubernetes resources - deploys resources with Northflank labels and annotations to enable [logs, metrics, health checks](../observe/monitor-containers)
  * Install CRDs provided in resource bundle - enables the use of [custom resource definitions ](https://kubernetes.io/docs/tasks/extend-kubernetes/custom-resources/custom-resource-definitions/) from your Helm chart
  * Use Northflank secret injection - adapt pod secrets, container command, and probes to enable full integration with Northflank
  * Use default Northflank image pull secret - you should disable this if one or more of your template creates a custom image pull secret



### Restrict addon type to specific projects

You can restrict the addon type to specific projects in a team, so that it can only be deployed in the selected projects.

Deploy a custom addon

You can deploy your custom addon in any project running in a [cluster on your own cloud provider account](../bring-your-own-cloud/use-other-cloud-providers-with-northflank).

From the addons page, or the create new menu, open the [create new addon ](https://app.northflank.com/s/project/create/addon) form and select your custom addon type from the options.

Values required by the Helm chart such as API keys, connection details, or configuration options can be supplied as JSON in the Helm template values field. If `show template values` is enabled in the custom addon type's configuration, these values will be visible and updatable in the deployed addon. The values are stored securely, encrypted at rest on the Northflank platform.

### Use and monitor your addon

Installed secrets will be automatically detected and displayed on the connection details page of your addon.

If you have enabled Northflank labels and annotations in the addon type's configuration, you can view the containers deployed for your addon with [logs, metrics, health checks](../observe/monitor-containers). The resources for each container may vary, and are defined in the Helm chart bundle.

You can view and update the template's values and attempt to recover from an error state if this feature is enable if these features have been enabled for your addon type.

Manage a custom addon type

You can update the details, scope, features, and configuration for existing custom addon types. These settings are independent of your custom addon's versions.

### Versioning

You can manage the versions of your custom addon type, which are different versions of your Helm chart bundle, from the versions page. The version is obtained from your chart's `version` field.

You can upload a new version of your Helm chart bundle and make it `active` from the versions page. All deployments of your custom addon will be deployed with the new Helm chart and values, existing addons will use the new version when they are redeployed.

### Debugging

Helm install notes will be shown on your addon's connection details page, when it has been deployed. These notes include information, warnings, and error messages which can help you configure your Helm chart bundle or override values. You can also check the addon's containers for logs and health check messages, if you have enabled Northflank labels and annotations in the custom addon type's configuration.

If you have enabled error recovery in your addon type configuration, you can access an error recovery page in deployed addons of that type. This page displays detailed error messages in case the addon has reached an error state, and allows you to trigger an attempt to recover the addon. An error state is reached if the helm chart produces invalid Kubernetes manifests and usually requires you to change the template values.

Next steps

[Bring your own cloud to NorthflankUse all the features of the Northflank platform on other cloud hosting providers, with control over your own infrastructure.](/docs/v1/application/bring-your-own-cloud/use-other-cloud-providers-with-northflank)[Use TailscaleAllow secure access to Tailscale devices to resources within your project.](/docs/v1/application/network/use-tailscale)[Use path-based routingRoute incoming traffic to different services and ports for paths on a subdomain.](/docs/v1/application/domains/use-path-based-routing)[Audit logsMonitor and review events affecting your organisation, teams, projects, and resources.](/docs/v1/application/observe/audit-logs)
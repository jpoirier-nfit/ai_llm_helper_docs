---
source_url: https://northflank.com/docs/v1/application/run/save-registry-credentials
title: Save registry credentials | Run | Northflank Application docs
crawl_date: 2025-07-29T09:26:09.357538
watsonmd_version: 0.1.0
---

Run / 

# Save registry credentials

You can save external registry credentials in your account and use them to authorise when selecting external Docker images for deployment in services or jobs. You can view and add credentials by navigating to the registries section under integrations in your account settings.

You can enable the restriction of credentials on your account to specific projects, toggle restrictions on and select the projects you want to access the credentials in.

You can enter your credentials by selecting the registry and entering your username and password, or username and personal access token/API key depending on the registry.

[Click here ](https://app.northflank.com/s/account/integrations/registry-credentials) to add registry credentials.

![Saving registry credentials in the Northflank application](https://assets.northflank.com/documentation/v1/application/run/save-registry-credentials/save-container-registry-credentials.png)

Container registries

### DockerHub (registry.hub.docker.com)

To authenticate to DockerHub simply enter your DockerHub username and password. Alternatively you can create an [access token ](https://docs.docker.com/docker-hub/access-tokens/) to use in place of your password. You can do this from on the security page in your Docker account settings, the token should include `read` access permission.

### Google Container Registry (gcr.io)

To authenticate to a Google Container Registry select your Google registry location from the drop-down list on Northflank. On Google Cloud Platform create or use a current service account with the `Storage Object Viewer` role and [create a new key ](https://cloud.google.com/container-registry/docs/advanced-authentication#json-key). Download the JSON keyfile and import it to Northflank.

### GitHub Container Registry (ghcr.io)

To [authenticate to GitHub Container Registry ](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry) you can create a [personal access token ](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry) on your GitHub account. You can create a personal access token with the required `read: packages` permission in developer settings, on your GitHub settings page.

### GitLab (registry.gitlab.com)

To authenticate to GitLab enter your username and [personal access token ](https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html). Personal access tokens, with the permission `read registry`, can be created in your GitLab preferences on the access tokens page. If you are using a self-hosted GitLab instance, make sure you use your own domain for verification and image paths (for example `registry.yourdomain.com`).

Authenticate with JSON

You can alternatively authenticate to a container registry by providing your Docker config.json, which consists of your username and password/token encoded in base 64, separated by a colon.
    
    
    {
      "auths": {
        "[registry authentication url]": {
          "auth": "[Your auth key (username:password in base 64)]"
        }
      }
    }
    

Next steps

[Run from a container registryDeploy an image from a container registry.](/docs/v1/application/run/run-an-image-from-a-container-registry)[Set up a pipeline and release flowManage your deployments and release your updates in an intuitive pipeline with release flows.](/docs/v1/application/release/create-a-pipeline-and-release-flow)[Scale your servicesIncrease the resources available to your services, and the number of instances to deploy.](/docs/v1/application/scale/scale-on-northflank)[Add databases and persistent storageCreate and use databases and other types of persistent storage in your project's applications and services.](/docs/v1/application/databases-and-persistence/stateful-workloads-on-northflank)
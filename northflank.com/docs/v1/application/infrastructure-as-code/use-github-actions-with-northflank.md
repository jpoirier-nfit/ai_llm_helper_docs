---
source_url: https://northflank.com/docs/v1/application/infrastructure-as-code/use-github-actions-with-northflank
title: Use GitHub Actions with Northflank | Infrastructure as Code | Northflank Application docs
crawl_date: 2025-07-25T12:06:49.829010
watsonmd_version: 0.1.0
---

Infrastructure as Code / 

# Use GitHub Actions with Northflank

You can automate your workflows using [GitHub Actions ](https://github.com/features/actions). You can adapt your existing GitHub Actions to work with Northflank, or create new ones.

You can define custom workflows that are triggered by events, such as a push to a repository or the creation of a pull request.

Workflows are defined in YAML files, which specify the sequence of steps to be executed in response to an event. Each step in a workflow can run commands, set environment variables, and interact with the GitHub API or other APIs.

Actions are reusable units of code that perform a specific task, such as building and testing your code, deploying to a server, or publishing a package. [GitHub marketplace ](https://github.com/marketplace/actions) provides a library of pre-built actions that you can use in your workflows.

You can also create and publish your own custom actions to the GitHub Marketplace, where other developers can use them in their own workflows.

Create a GitHub Actions workflow

GitHub Actions workflows specify the sequence of steps to be executed in response to an event. Each step in a workflow can run commands, set environment variables, and interact with the GitHub API or other APIs. Workflows are defined by YAML files in your Git repository, saved in the `.github/workflows/` directory.

You can [learn more about writing workflows in the GitHub documentation ](https://docs.github.com/en/actions/using-workflows/about-workflows).

You can reuse other workflows from your own repository, public repositories, or workflows in your organisation account. Learn more about [workflow syntax ](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions).

### Workflow example

This example workflow builds and publishes and image, and then [triggers a Northflank release flow run](../release/create-a-pipeline-and-release-flow) to deploy it.

The workflow logs in to the [GitHub container registry ](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry), builds the pull request branch in the repository and pushes the image to <https://ghcr.io/>, and then [triggers a Northflank release flow using a webhook](../release/create-a-pipeline-and-release-flow#release-flow-settings).

The events that trigger the workflow to run are defined in `on`, the environment variables to use in the workflow are defined in `env`, and the jobs to run as part of the workflow are defined in `jobs`.

The environment variables include the container registry to use (`REGISTRY`), and the `IMAGE_NAME`, which uses the `github` context to get the `repository` name as the value.

The `build-and-push-image` job specifies the base image to run the steps on (`ubuntu-latest`), and the GitHub `permissions` it requires.

The steps include `checkout repository`, which uses the published [checkout ](https://github.com/marketplace/actions/checkout) action, `log in to the container registry` which uses the [Docker login ](https://github.com/marketplace/actions/docker-login) action, and `build and push Docker image` which uses the [build and push Docker image ](https://github.com/marketplace/actions/build-and-push-docker-images) action.

The final step runs a command (`curl`) to send a GET request to a Northflank release flow webhook, stored in the `NF_WEBHOOK` secret, and provides `image_tag` as a URL query parameter, which can then be [accessed in the release flow via the `args` object](../release/configure-a-release-flow#node-arguments-and-references) to provide an image tag to deploy.

The workflow also uses two [secrets ](https://docs.github.com/en/actions/security-guides/encrypted-secrets), `GITHUB_TOKEN` which is automatically generated and passed to the workflow, and `NF_WEBHOOK`, which is generated in your [release flow's settings](../release/create-a-pipeline-and-release-flow#release-flow-settings).
    
    
    name: Publish image and run release flow
    
    on:
      pull_request:
        types: ['opened', 'reopened', 'synchronize']
    
    env:
      REGISTRY: ghcr.io
      IMAGE_NAME: ${{ github.repository }}
    
    jobs:
      build-and-push-image:
        runs-on: ubuntu-latest
        permissions:
          contents: read
          packages: write
    
        steps:
          - name: Checkout repository
            uses: actions/checkout@v3
    
          - name: Log in to the Container registry
            uses: docker/login-action@f054a8b539a109f9f41c372932f1ae047eff08c9
            with:
              registry: ghcr.io
              username: ${{ github.actor }}
              password: ${{ secrets.GITHUB_TOKEN }}
    
          - name: Build and push Docker image
            uses: docker/build-push-action@ad44023a93711e3deb337508980b4b5e9bcdc5dc
            with:
              context: .
              push: true
              tags: ghcr.io/northflank/release-flow-webhook-test:${{ github.SHA }}
    
          - name: Trigger release flow
            run: curl -X GET ${{ secrets.NF_WEBHOOK }}?image_tag=${{ github.SHA }}
    

Use secrets with a GitHub Action workflow

You can use environment variables and secrets with GitHub Actions. [Environment variables ](https://docs.github.com/en/actions/learn-github-actions/variables#about-variables) are useful for passing data between steps, while [secrets ](https://docs.github.com/en/actions/security-guides/encrypted-secrets) are used to store sensitive information such as passwords or API keys.

You can define secrets for a repository in the `security` section of the repository `settings`. Secrets for an organisation can similarly be defined in the `security` section of the organisation `settings`. You can define which organisation repositories a secret is available in by selecting a policy from the `repository access` dropdown list.

You can also give job steps an `id`, which can then be used to refer to the output from the Action used in that step, via the `steps` context (for example, `${{ steps.<id>.outputs.<key> }}`).

Learn more about the [contexts available in workflows ](https://docs.github.com/en/actions/learn-github-actions/contexts), and see the deploy to Northflank workflow for more examples of contexts.

Deploy to Northflank using a GitHub Action

This workflow step demonstrates the [Deploy to Northflank ](https://github.com/marketplace/actions/deploy-to-northflank) action, available on the GitHub marketplace, as it would be used in a workflow.

By providing the required variables this action can be used in your workflow to deploy an image from a container registry. [Read the full guide here ](https://northflank.com/guides/use-a-git-hub-action-to-deploy-to-northflank).
    
    
             - name: Deploy to Northflank
               uses: northflank/deploy-to-northflank@v1
               with:
                  northflank-api-key: ${{ secrets.NORTHFLANK_API_KEY }}
                  project-id: ${{ env.PROJECT_ID }}
                  service-id: ${{ env.SERVICE_ID }}
                  image-path: ${{ steps.<id>.outputs.<tags> }}
                  credentials-id: ${{ env.CREDENTIALS_ID }}
    

Publish a GitHub Action

You can [write and publish ](https://docs.github.com/en/actions/creating-actions/about-custom-actions) your own GitHub Actions to interact with Northflank, as well as the GitHub API and other third-party APIs.

GitHub Actions consist of your application code and an `action.yml`. The `action.yml` file [contains the metadata for your action ](https://docs.github.com/en/actions/creating-actions/metadata-syntax-for-github-actions), including `name`, `author`, and `description`.

The `runs` attribute defines how GitHub will run your action, and the contents depend on whether you have written a [JavaScript, Docker, or composite action ](https://docs.github.com/en/actions/creating-actions/about-custom-actions#types-of-actions).

It also contains the definitions for the `inputs` accepted by, and the `outputs` returned by your action, if required.

### Example action.yml file

The example below is a truncated version of the published Deploy to Northflank JavaScript action. You can see the [repository here ](https://github.com/northflank/deploy-to-northflank), which contains the whole `action.yml`, as well as the action code (`index.ts`), `package.json`, and license.
    
    
    name: Deploy to Northflank
    author: Northflank
    description: Deploy Docker images to Northflank by updating the deployment configuration of existing services or jobs via a GitHub action.
    inputs:
      northflank-api-host:
        description: Host of the Northflank API.
        required: false
        default: https://api.northflank.com
    
    runs:
      using: node16
      main: dist/index.js
    
    branding:
      icon: upload-cloud
      color: gray-dark
    

Next steps

[GitOps on NorthflankUse templates and release flows in a Git repository to trigger changes to your config and resources.](/docs/v1/application/infrastructure-as-code/gitops-on-northflank)[Create a templateLearn how to create and configure a Northflank template.](/docs/v1/application/infrastructure-as-code/create-a-template)[Set up a pipeline and release flowManage your deployments and release your updates in an intuitive pipeline with release flows.](/docs/v1/application/release/create-a-pipeline-and-release-flow)[Configure a release flowLearn how to use the visual editor or code to configure a release flow.](/docs/v1/application/release/configure-a-release-flow)
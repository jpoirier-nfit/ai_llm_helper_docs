---
source_url: https://northflank.com/docs/v1/application/infrastructure-as-code/share-a-template
title: Share a template | Infrastructure as Code | Northflank Application docs
crawl_date: 2025-07-25T12:06:49.794713
watsonmd_version: 0.1.0
---

Infrastructure as Code / 

# Share a template

You can easily share any of your existing Northflank templates with a link, which you can copy after creating your template. This link will allow anyone with a Northflank account or team to add the template to their own account and run it, meaning users can begin using your application quickly, easily, and with minimal configuration on their part.

You should ensure there are no secrets contained within your template before sharing it. If your template requires secret values such as API tokens, the user receiving the template should add these in their own [argument overrides](create-a-template#provide-secrets-securely-to-a-template).

You can also share templates by making them available in a [git repository](gitops-on-northflank).

Use a Northflank template link

You can click the link for a Northflank template to add it to your account. If you belong to one or more teams, you must select the account to add the template to.

You will then be directed to the new template form, automatically populated with the contents of the shared template. You can [modify the template configuration](create-a-template) before saving, for example to change the project or to [enable GitOps](gitops-on-northflank) to save the template to a repository. You can also add any required [argument overrides](write-a-template#create-from-an-existing-project-or-resource) for the template. Check the documentation or guide from the source of the template for instructions on configuration and usage of the deployed application(s).

After you have created the template you will be able to run it.

warning

Northflank cannot guarantee that templates written by third parties will work correctly. You should always check the contents of a template before running it.

For example, if the template deploys a Docker image, is it the expected image from the right account?

Next steps

[Run a templateRun templates manually or automatically.](/docs/v1/application/infrastructure-as-code/run-a-template)[Create a templateLearn how to create and configure a Northflank template.](/docs/v1/application/infrastructure-as-code/create-a-template)[Write a templateLearn how to structure a Northflank template, define workflows, create resources, and perform actions.](/docs/v1/application/infrastructure-as-code/write-a-template)[GitOps on NorthflankUse templates and release flows in a Git repository to trigger changes to your config and resources.](/docs/v1/application/infrastructure-as-code/gitops-on-northflank)
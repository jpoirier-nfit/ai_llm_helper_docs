---
source_url: https://northflank.com/docs/v1/application/infrastructure-as-code/manage-template-versions
title: Manage template versions | Infrastructure as Code | Northflank Application docs
crawl_date: 2025-07-29T09:26:09.829584
watsonmd_version: 0.1.0
---

Infrastructure as Code / 

# Manage template versions

Template drafts allow you to review and manage updates to templates. Instead of directly saving changes to a template, team members create a new draft with their proposed updates. Drafts can then be reviewed, edited, and either closed or accepted.

Template drafts rely on a separate set of [role permissions](../secure/use-role-based-access-control) compared to standard templates. Only team members assigned a role with `close` and `accept` permissions will be able to manage drafts.

You can enable template drafts in an [organisation's settings](../collaborate/manage-an-organisation). This will prevent teams in your organisation from editing their templates directly, replacing `save` with `create draft`.

Drafts can be used with or without Git integration for templates, and allow you to review and manage template versions on Northflank.

Create a draft

You can create a new draft for a template by updating an existing template's content or settings [in the Northflank application](create-a-template).

After making your changes click `create draft` to preview your changes. You can add a name and description to help identify the request for changes, otherwise drafts will be given a randomly generated name if none is provided.

![Creating a template draft in the Northflank application](https://assets.northflank.com/documentation/v1/application/infrastructure-as-code/manage-template-versions/create-template-draft.png)

### GitOps and drafts

If you have [enabled GitOps](gitops-on-northflank) for your template a new pull request will be opened for each template draft, and closed when a draft is accepted or closed. Pull requests to change templates will not appear in Northflank as template drafts.

If changes to a template have been submitted as a draft it should be managed on Northflank, similarly if changes been proposed using a pull request they should be managed on your Git service.

Manage drafts

Once a draft is created it will be listed under ` drafts` in the template editor. You can open a draft see more detail.

![Reviewing a template draft in the Northflank application](https://assets.northflank.com/documentation/v1/application/infrastructure-as-code/manage-template-versions/review-template-draft.png)

### View differences

You can view the changes proposed in the draft as [template code](write-a-template). The read-only editor will display the differences between the currently existing template and the draft. Drafts will not contain updates to the template that happen after the draft has been created. You should check for any unwanted reversions if later drafts have already been accepted.

### Edit, accept, or close a draft

You can edit a draft to make more changes, reject the draft by closing it, or accept the changes to replace the existing template with the draft.

### Check history

If you have [audit logging](../observe/audit-logs) enabled you can view the history of a template draft including who created it, any updates to it, and who closed or accepted it.

Next steps

[Run a templateRun templates manually or automatically.](/docs/v1/application/infrastructure-as-code/run-a-template)[Create a templateLearn how to create and configure a Northflank template.](/docs/v1/application/infrastructure-as-code/create-a-template)[Write a templateLearn how to structure a Northflank template, define workflows, create resources, and perform actions.](/docs/v1/application/infrastructure-as-code/write-a-template)[Update a templateUpdate a template and resources within a project.](/docs/v1/application/infrastructure-as-code/run-a-template#update-a-template)[GitOps on NorthflankUse templates and release flows in a Git repository to trigger changes to your config and resources.](/docs/v1/application/infrastructure-as-code/gitops-on-northflank)
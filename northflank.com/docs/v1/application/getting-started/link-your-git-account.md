---
source_url: https://northflank.com/docs/v1/application/getting-started/link-your-git-account
title: Link your Git account | Getting Started | Northflank Application docs
crawl_date: 2025-07-29T09:26:08.965217
watsonmd_version: 0.1.0
---

Getting Started / 

# Link your Git account

Northflank integrates with Git version control systems (VCS) such as GitHub, GitLab and Bitbucket in order to build and deploy code from your repositories.

You will be prompted to link a Git account when you create a team, or if your team no longer has access to any Git provider.

You can also link self-hosted instances of GitLab, as well as multiple accounts for GitHub, GitLab, and Bitbucket.

You can manage Git integrations from your team dashboard.

[Click here ](https://app.northflank.com/s/account/integrations/vcs) to link a Git account.

![The Git integration page in the Northflank application](https://assets.northflank.com/documentation/v1/application/getting-started/link-your-git-account/git-integration-page.png)

Link your GitHub account

GitHub integrates with Northflank through the GitHub app ecosystem.

When you connect your GitHub account you will be redirected to GitHub's login and application installation page.

### Link your GitHub account

  1. Navigate to the Git integration page in your Northflank team
  2. Click `Link GitHub`
  3. Select the team or organisation you want to link



![Installing Northflank in GitHub](https://assets.northflank.com/documentation/v1/application/getting-started/link-your-git-account/github-install.jpg)

  4. Choose the repositories that you wish to build and deploy on Northflank, or grant access to all the repositories on the account



![Authorising Northflank in GitHub](https://assets.northflank.com/documentation/v1/application/getting-started/link-your-git-account/github-authorize.jpg)

You will now be redirected back to Northflank and you will see your GitHub account name on the entry for GitHub. You can now begin building and deploying code from your GitHub repositories.

The GitHub app will automatically send Northflank webhooks for events on your repositories, which means commits to your monitored branches and pull requests can be built instantly.

You can unlink GitHub from your Northflank team, which will stop Northflank from building any future commits to your repositories.

### Edit installation

You can select a GitHub account on Northflank and click `edit installation` to change which repositories are available on Northflank.

If you need to re-link a GitHub account that already has the Northflank application installed, you must toggle between your repository restrictions settings to activate the `save` button on GitHub.

### Remove GitHub

To remove your team's access to your GitHub account, select the account and click `unlink`.

To remove Northflank from your GitHub team you must uninstall the Northflank app from your GitHub settings.

Link your GitLab account

You can connect your GitLab account with Northflank via OAuth. When you connect your GitLab account you will be redirected to GitLab to complete the verification steps. All repositories your GitLab account has access to, including repositories that you do not own, are accessible with the connection.

### Link your GitLab account

  1. Navigate to the Git integration page in your Northflank team
  2. Click `Link GitLab`



![Authorising Northflank in GitLab](https://assets.northflank.com/documentation/v1/application/getting-started/link-your-git-account/gitlab-install.jpg)

You will now be redirected back to Northflank and you will see your GitLab account name on the entry for GitLab. You will be prompted to select whether to restrict access to certain GitLab namespaces.

You can now begin building and deploying code from your GitLab repositories.

### Regenerate webhooks

Northflank makes an API request to create webhooks for your GitLab repositories to enable CI. You can regenerate the webhooks if the token is accidentally deleted or exposed.

### Remove GitLab

To remove your team's access to your GitLab account, select the account and click `unlink`.

To remove Northflank from your GitLab account, go to your GitLab preferences, open the applications page, and revoke the Northflank application's access.

Link your Bitbucket account

You can connect your Bitbucket account with Northflank via OAuth. When you connect your Bitbucket account you will be redirected to Bitbucket to complete the verification steps. All repositories your Bitbucket account has access to, including repositories that you do not own, are accessible with the connection.

  1. Navigate to the Git integration page in your Northflank team
  2. Click `Link Bitbucket`



![Authorising Northflank on Bitbucket](https://assets.northflank.com/documentation/v1/application/getting-started/link-your-git-account/bitbucket-install.jpg)

You will now be redirected back to Northflank and you will see your Bitbucket account name on the entry for Bitbucket. You will be prompted to select whether to restrict access to certain namespaces.

### Regenerate webhooks

Northflank makes an API request to create webhooks for your Bitbucket repositories to enable CI. You can regenerate the webhooks if the token is accidentally deleted or exposed.

### Remove BitBucket

To remove your team's access to your Bitbucket account, select the linked account and click `unlink`.

To completely remove Northflank from your Bitbucket account, go to Bitbucket personal settings, open the app authorizations page and revoke the Northflank application's access.

Set team namespaces

On team accounts you may need to restrict access to certain namespaces on your linked Git accounts.

GitHub account restrictions are managed on GitHub by selecting which account/organisation to install the Northflank GitHub app on, and then granting access to specific repositories on that account.

Your linked GitLab and Bitbucket accounts can be restricted to certain namespaces by opening the settings on the respective entry. Select restricted and pick the contexts you want your team members to access. Remove a namespace from the list to revoke access. The namespaces available to your team will be displayed on the git integrations page in the section for the relevant service. Remove a namespace from the list in the selected account to revoke access.

New namespaces can be created in your Gitlab and Bitbucket accounts by creating new projects.

### Restrict self-hosted VCS access

You can restrict access to the repositories in your self-hosted VCS by selecting specific owners within the self-hosted VCS's settings. Team members will be able to build and run from repositories belonging to the selected namespaces, if your account has access to them.

Unrestricted access means team members will be able to create services and jobs from every repository that the linked account can access.

Next steps

[Create a projectCreate a project to contain your services, persistent data, secrets, and more.](/docs/v1/application/getting-started/create-a-project)[Build and deploy your codeQuickly and easily build and run code from a Git repository using a Dockerfile or buildpack.](/docs/v1/application/getting-started/build-and-deploy-your-code)[Add a self-hosted VCSAdd your own self-hosted Git provider and build from its repositories.](/docs/v1/application/collaborate/manage-git-integrations#add-a-self-hosted-vcs)[Save registry credentialsSave your credentials for a container registry to access private images.](/docs/v1/application/run/save-registry-credentials)
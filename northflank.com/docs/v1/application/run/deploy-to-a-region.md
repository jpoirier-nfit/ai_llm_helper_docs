---
source_url: https://northflank.com/docs/v1/application/run/deploy-to-a-region
title: Deploy to a region | Run | Northflank Application docs
crawl_date: 2025-07-29T09:26:09.379251
watsonmd_version: 0.1.0
---

Run / 

# Deploy to a region

You can deploy your code to a specific region by [creating a project](../getting-started/create-a-project) in that region. This allows jobs or services to be run closer to customers, your development team, or external service for better connectivity.

You cannot change the region of a project after it is created, and all resources deployed in that project will be deployed in that region. [Builds](../build/build-your-code-on-northflank), unless [configured to run on your own cluster](../bring-your-own-cloud/configure-your-cluster#select-build-infrastructure), are performed on Northflank build infrastructure outside your project.

Northflank currently supports the following regions:

Region| API reference| Global region  
---|---|---  
Asia Southeast| `asia-southeast`| Asia Pacific  
Europe West| `europe-west`| EMEA  
Europe West Netherlands| `europe-west-netherlands`| EMEA  
US Central| `us-central`| Americas  
US East1| `us-east1`| Americas  
US West| `us-west`| Americas  
  
Contact [[support@northflank.com](mailto:support@northflank.com)](mailto:support@northflank.com) to register your interest for regions not listed above.

You can also [integrate with other cloud providers](../bring-your-own-cloud/use-other-cloud-providers-with-northflank) to deploy your own clusters, which will allow you to create projects hosted on your chosen cloud provider, in the regions they support.

Network resources across multiple regions

Resources in a project are, by default, inaccessible from other projects. To allow resources in different projects to communicate you can either:

  * create a public port, which exposes your service or database to the public internet
  * [allow network ingress from your other projects](../network/enable-multi-project-networking) which allows you to use private, secure ports as well as TCP and UDP protocols



Next steps

[Bring your own cloud to NorthflankUse all the features of the Northflank platform on other cloud hosting providers, with control over your own infrastructure.](/docs/v1/application/bring-your-own-cloud/use-other-cloud-providers-with-northflank)[Multi-project networkingConfigure projects to securely allow ingress network traffic from other projects.](/docs/v1/application/network/enable-multi-project-networking)[Use TailscaleAllow secure access to Tailscale devices to resources within your project.](/docs/v1/application/network/use-tailscale)[Run an image continuouslyDeploy a built image as a continuously-running service.](/docs/v1/application/run/run-an-image-continuously)
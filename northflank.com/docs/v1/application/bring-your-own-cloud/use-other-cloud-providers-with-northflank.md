---
source_url: https://northflank.com/docs/v1/application/bring-your-own-cloud/use-other-cloud-providers-with-northflank
title: Use other cloud providers with Northflank | Bring Your Own Cloud | Northflank Application docs
crawl_date: 2025-07-29T09:26:09.878091
watsonmd_version: 0.1.0
---

Bring Your Own Cloud / 

# Use other cloud providers with Northflank

You can bring your own cloud to use all the features of the Northflank platform on other cloud hosting providers.

Connect your account with Northflank to create and manage Kubernetes clusters in your own cloud account, and gain complete control of your infrastructure, data storage, security, and auditing.

You will use your existing billing relationship with your cloud provider for all resources consumed by your clusters. See [cloud provider billing](../billing/cloud-provider-billing) for more information.

[Click here ](https://app.northflank.com/s/account/cloud/clusters) to start deploying into your cloud account.

Integrate your cloud account and a deploy cluster

After creating an integration with your chosen cloud provider you can deploy clusters into your cloud account.

You can create integrations with the following providers:

Provider| Engine| Available Nodes and Regions  
---|---|---  
[ Google Cloud Platform ](https://cloud.google.com/gcp)| [Google Kubernetes Engine (GKE) ](https://cloud.google.com/kubernetes-engine)| [View on Northflank ](https://northflank.com/cloud/gcp)  
[ Amazon Web Services ](https://aws.amazon.com/)| [Elastic Kubernetes Service (EKS) ](https://aws.amazon.com/eks/)| [View on Northflank ](https://northflank.com/cloud/aws)  
[ Azure ](https://azure.microsoft.com/en-gb/)| [Azure Kubernetes Service (AKS) ](https://azure.microsoft.com/en-us/services/kubernetes-service/)| [View on Northflank ](https://northflank.com/cloud/azure)  
[ Civo ](https://www.civo.com)| [Civo Kubernetes ](https://www.civo.com/kubernetes)| [View on Northflank ](https://northflank.com/cloud/civo)  
[ Oracle ](https://www.oracle.com/)| [Oracle Kubernetes Engine (OKE) ](https://www.oracle.com/cloud/cloud-native/kubernetes-engine/)| [View on Northflank ](https://northflank.com/cloud/oci)  
  
[Integrate your Google accountIntegrate your Google Cloud Platform account to create and manage Kubernetes clusters on GCP with Northflank.](/docs/v1/application/bring-your-own-cloud/gcp-on-northflank)[Integrate your Amazon accountIntegrate your Amazon Web Services account to create and manage Kubernetes clusters on AWS with Northflank.](/docs/v1/application/bring-your-own-cloud/aws-on-northflank)[Integrate your Azure accountIntegrate your Microsoft Azure account to create and manage Kubernetes clusters on Azure with Northflank.](/docs/v1/application/bring-your-own-cloud/azure-on-northflank)[Integrate your Civo accountIntegrate your Civo account to create and manage Kubernetes clusters on Civo with Northflank.](/docs/v1/application/bring-your-own-cloud/civo-on-northflank)[Integrate your Oracle accountIntegrate your Oracle Cloud Infrastructure account to create and manage Kubernetes clusters on OCI with Northflank.](/docs/v1/application/bring-your-own-cloud/oci-on-northflank)

Configure your cluster

Configure your cluster to handle builds and deployments according to your requirements.

[Select your cluster's build infrastructureBuild on your cluster, on Northflank's managed cloud, or choose a separate build cluster.](/docs/v1/application/bring-your-own-cloud/configure-your-cluster#select-build-infrastructure)[Manage your request modifiersYou can tune the minimum resources requested by pods deployed to your cluster to balance performance and node usage.](/docs/v1/application/bring-your-own-cloud/configure-your-cluster#configure-resources)[Retain cluster volumesChoose to keep volumes and volume backups when you delete a cluster.](/docs/v1/application/bring-your-own-cloud/configure-your-cluster#set-volume-deletion-preferences)[Create custom resource plansCreate custom plans for your team to deploy workloads and build code on your own clusters.](/docs/v1/application/bring-your-own-cloud/create-custom-resource-plans)

Deploy and scale node pools

Deploy and scale node pools of different node types in as many availability zones as you require and configure scheduling rules and autoscaling to optimise node usage.

[Deploy node poolsConfigure and deploy node pools on a Kubernetes cluster with Northflank.](/docs/v1/application/bring-your-own-cloud/deploy-and-scale-node-pools)[Scale node poolsSet your node count manually, or configure autoscaling to manage demand and optimise costs.](/docs/v1/application/bring-your-own-cloud/deploy-and-scale-node-pools#set-node-count-and-autoscaling)[Create node pools with spot instancesUse spot instances to reduce costs for non-critical workloads.](/docs/v1/application/bring-your-own-cloud/deploy-and-scale-node-pools#use-spot-instances)[Schedule workloads to specific node poolsAllow or disallow different types of workloads from being scheduled on a node pool.](/docs/v1/application/bring-your-own-cloud/deploy-and-scale-node-pools#set-scheduling-rules)

Deploy workloads to your cluster

Let Northflank automatically assign workloads to node pools with capacity, or use affinity rules to deploy workloads to specific node pools to projects deployed in your cluster.

Configure node pools to use spot instances to reduce cost, or deploy across multiple availability zones for high availability.

[Deploy workloads to your clusterDeploy services, jobs, and addons to your own cluster, and configure workloads to schedule on specific node pools.](/docs/v1/application/bring-your-own-cloud/deploy-workloads-to-your-cluster)[Run GPU workloadsDeploy GPU workloads on Northflank for AI, machine learning, HPC workloads, and other tasks.](/docs/v1/application/gpu-workloads/gpus-on-northflank)[Deploy workloads to spot instancesTag workloads to deploy them to spot instances.](/docs/v1/application/bring-your-own-cloud/deploy-workloads-to-your-cluster#use-spot-instances)[Deploy workloads with high availabilitySchedule a resource with zonal redundancy for high availability applications.](/docs/v1/application/bring-your-own-cloud/deploy-workloads-to-your-cluster#use-zonal-redundancy-for-high-availability)

Monitor and manage your cluster

Monitor your cluster's usage, health, and deployed workloads.

[Manage your Kubernetes clusterManage your clusters on other cloud providers using Northflank.](/docs/v1/application/bring-your-own-cloud/manage-your-cluster)[Observe your Kubernetes clusterMonitor your Kubernetes clusters, node pools, and nodes on other cloud providers using Northflank.](/docs/v1/application/bring-your-own-cloud/manage-your-cluster#monitor-your-cluster)[Cordon and drain nodesCordon and drain node pools to manage and migrate workloads.](/docs/v1/application/bring-your-own-cloud/manage-your-cluster#cordon-and-drain-node-pools)[Cloud provider billingMonitor your spend for using Northflank in your own cloud provider accounts.](/docs/v1/application/billing/pricing-on-northflank#bring-your-own-cloud)
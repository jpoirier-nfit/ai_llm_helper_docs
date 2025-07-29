---
source_url: https://northflank.com/docs/v1/application/gpu-workloads/gpus-on-northflank
title: GPUs on Northflank | Gpu Workloads | Northflank Application docs
crawl_date: 2025-07-29T09:26:10.032947
watsonmd_version: 0.1.0
---

Gpu Workloads / 

# GPUs on Northflank

You can deploy services and run jobs on Northflank with GPU access, using Northflank's managed cloud or in your own cloud account.

This lets you run GPU workloads for AI, ML, data analysis, simulations, graphics rendering, and other tasks which require high-performance computing on Northflank.

Deploy GPUs on Northflank's managed cloud

You can create GPU-enabled projects on Northflank's managed cloud and only pay for the resources consumed, so you can deploy workloads with access powerful GPUs without having to configure your own Kubernetes clusters.

[Deploy a GPU project on NorthflankDeploy a GPU-enabled project on Northflank's managed cloud.](/docs/v1/application/gpu-workloads/deploy-gpus-on-northflank-cloud#deploy-a-gpu-enabled-project)[Deploy a GPU workload on Northflank's managed cloudDeploy a GPU-enabled workload on Northflank's managed cloud.](/docs/v1/application/gpu-workloads/deploy-gpus-on-northflank-cloud#deploy-a-gpu-workload-on-northflank)

Deploy GPUs in your own cloud

You can deploy and manage GPU-enabled nodes on [other cloud providers](../bring-your-own-cloud/use-other-cloud-providers-with-northflank) using Northflank. This allows you to retain control of your infrastructure and existing billing relationships, while using Northflank to deploy GPU workloads.

Any Northflank projects deployed to your cluster will be able to make use of the GPU-enabled nodes.

[Deploy GPU node poolsDeploy node pools with GPU nodes on a Kubernetes cluster with Northflank.](/docs/v1/application/gpu-workloads/deploy-gpus-in-your-own-cloud#deploy-a-cluster-and-a-gpu-node-pool)[Configure workloads to deploy on GPU nodesCreate a project on your own cluster with GPU nodes and configure workloads to deploy to it.](/docs/v1/application/gpu-workloads/deploy-gpus-in-your-own-cloud#configure-workloads-to-deploy-on-gpu-nodes)[Allow multiple workloads to use a GPU with timeslicingYou can enable timeslicing to enable multiple GPU workloads to schedule per GPU, and set the number of slices to allow on each GPU.](/docs/v1/application/gpu-workloads/deploy-gpus-in-your-own-cloud#allow-multiple-workloads-to-use-a-gpu-with-timeslicing)[Schedule GPU workloads to specific nodesEnsure that your GPU workloads can be scheduled on your cluster.](/docs/v1/application/gpu-workloads/deploy-gpus-in-your-own-cloud#gpu-workload-scheduling)

Configure and deploy GPU workloads

Generally your GPU workloads will not require any extra configuration to run on Northflank, and you can select a GPU model for your service or job when creating or updating a service.

You will need to build with, or deploy, images compatible with the GPU model you wish to use, and you will need to correctly configure your deployed applications to make use of available GPUs.

[Configure applications to use GPUsYou can directly deploy or build your applications with Docker images that are optimised for your desired GPU model and AI/ML libraries.](/docs/v1/application/gpu-workloads/configure-and-optimise-workloads-for-gpus#configure-applications-to-use-gpus)[Build with GPU-optimised imagesYou can directly deploy or build your applications with Docker images that are optimised for your desired GPU model and AI/ML libraries.](/docs/v1/application/gpu-workloads/configure-and-optimise-workloads-for-gpus#build-with-gpu-optimised-images)[Right-size resources for GPU workloadsScale CPU, memory, and ephemeral storage to handle GPU workloads.](/docs/v1/application/gpu-workloads/configure-and-optimise-workloads-for-gpus#right-size-resources)[Persist models and dataYou can directly deploy or build your applications with Docker images that are optimised for your desired GPU model and AI/ML libraries.](/docs/v1/application/gpu-workloads/configure-and-optimise-workloads-for-gpus#persist-models-and-training-data)
---
source_url: https://northflank.com/docs/v1/application/gpu-workloads/deploy-gpus-on-northflank-cloud
title: Deploy GPUs on Northflank's managed cloud | Gpu Workloads | Northflank Application docs
crawl_date: 2025-07-29T09:26:10.040030
watsonmd_version: 0.1.0
---

Gpu Workloads / 

# Deploy GPUs on Northflank's managed cloud

You can run GPU workloads on Northflank's managed cloud.

This allows you to use GPU acceleration for your applications and services and only pay for the resources consumed. To deploy GPU workloads on Northflank you must create a GPU-enabled project.

You can deploy combined and deployment services and jobs with GPU access. Northflank GPUs do not currently support timeslicing.

Check the [pricing page ](https://northflank.com/pricing) to find out more about GPU pricing.

Deploy a GPU-enabled project

To deploy GPU workloads on Northflank's managed cloud, you'll first need to [create a new project ](https://app.northflank.com/s/account/projects/new) in a GPU-enabled region.

Select your desired region from the list under `GPU`, and create your project as normal. Any services or jobs deployed in this project will have a GPU option available in resources.

Different regions may have different availability of specific GPU models.

Deploy a GPU workload on Northflank

To deploy workloads with GPU access, [create a new service or job ](https://app.northflank.com/s/project/create/service) as normal, or navigate to the resources page of an existing service or job.

Select an available GPU from the drop-down list as well as the number of GPUs to deploy with. Each instance of a service will have access to the number of GPU models selected.

GPU Count| Instances deployed| GPUs per instance| Total GPUs in the service  
---|---|---|---  
1| 1| 1| 1  
4| 1| 4| 4  
8| 2| 8| 16  
  
You may need to configure your workload to make use of GPU hardware, or multiple GPUs.

Next steps

[Configure applications to use GPUsYou can directly deploy or build your applications with Docker images that are optimised for your desired GPU model and AI/ML libraries.](/docs/v1/application/gpu-workloads/configure-and-optimise-workloads-for-gpus#configure-applications-to-use-gpus)[Build with GPU-optimised imagesYou can directly deploy or build your applications with Docker images that are optimised for your desired GPU model and AI/ML libraries.](/docs/v1/application/gpu-workloads/configure-and-optimise-workloads-for-gpus#build-with-gpu-optimised-images)[Right-size resources for GPU workloadsScale CPU, memory, and ephemeral storage to handle GPU workloads.](/docs/v1/application/gpu-workloads/configure-and-optimise-workloads-for-gpus#right-size-resources)[Persist models and dataYou can directly deploy or build your applications with Docker images that are optimised for your desired GPU model and AI/ML libraries.](/docs/v1/application/gpu-workloads/configure-and-optimise-workloads-for-gpus#persist-models-and-training-data)
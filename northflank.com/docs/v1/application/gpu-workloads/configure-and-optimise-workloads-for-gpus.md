---
source_url: https://northflank.com/docs/v1/application/gpu-workloads/configure-and-optimise-workloads-for-gpus
title: Configure and optimise workloads for GPUs | Gpu Workloads | Northflank Application docs
crawl_date: 2025-07-29T09:26:10.061790
watsonmd_version: 0.1.0
---

Gpu Workloads / 

# Configure and optimise workloads for GPUs

You can deploy a range of pre-built Docker images to run applications and services that can take advantage of GPU acceleration, or build and deploy your own applications.

Often, workloads that require GPUs will also have greater requirements for CPU, memory, and storage, and you will also need to ensure that your Docker image and application frameworks are compatible with the GPUs you want to use.

Configure applications to use GPUs

Check your application or library's documentation to ensure it is correctly configured to utilise the GPU. You may have to install specific ROCm versions of your packages for AMD GPUs.

Below are examples for [PyTorch ](https://pytorch.org) and [TensorFlow ](https://www.tensorflow.org) to access a single GPU.

### PyTorch

    
    
    import torch
    device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
    model = MyModel().to(device)
    

### TensorFlow

    
    
    import tensorflow as tf
    print(tf.config.list_physical_devices('GPU'))
    

If you are building with libraries such as PyTorch or TensorFlow, you must ensure that you install package versions that are compatible with the CUDA or ROCm version specified by your base image.

Build with GPU-optimised images

You can directly deploy Docker images to Northflank optimised for your selected GPU, or use them as base images for your Docker builds. This helps ensure that you're using platform versions optimised for your GPU, as well as the library versions in your application.

For example you could use `nvidia/cuda:12.8.0-cudnn-runtime-ubuntu22.04` to specify a CUDA version to use in your base image, or `pytorch/pytorch:2.6.0-cuda11.8-cudnn9-devel` which includes the PyTorch libraries as well as the specific CUDA platform and cuDNN library.

## Recommended platform versions

GPU model| Recommended versions  
---|---  
NVIDIA L4| CUDA 12.0+  
NVIDIA A100| CUDA 11.0–12.4  
NVIDIA A10G| CUDA 11.1–12.3  
NVIDIA M60| CUDA 7.5–10.2  
AMD Radeon Pro V520| OpenCL 2.2  
NVIDIA T4| CUDA 10.0–12.2  
NVIDIA V100| CUDA 9.0–12.2  
NVIDIA K80| CUDA 7.5–11.1 (deprecated)  
NVIDIA H100| CUDA 12.0+  
Habana Gaudi HL-205| SynapseAI  
NVIDIA A10| CUDA 11.1–12.3  
AMD Radeon Instinct MI25| ROCm 2.x–5.x  
NVIDIA L40S| CUDA 12.0+  
NVIDIA H200| CUDA 12.0+  
NVIDIA P100| CUDA 8.0–11.4  
AMD MI300X / Instinct MI300X| ROCm 6.0+  
  
Right-size resources

While GPU workloads offload the heavy processing to the GPU, you will need to [allocate sufficient vCPU, memory](../scale/scale-cpu-and-memory), and ephemeral storage to services and jobs to handle large amounts of data or file sizes.

When dealing with large datasets or AI models you may encounter crashes due to insufficient ephemeral storage as your container tries to use it for temporary disk storage. You can increase the ephemeral storage for your services and jobs, but you should also save models, checkpoints, and data to persistent volumes to reduce ephemeral disk usage.

You can check the [metrics, logs, and health](../observe/monitor-containers) for your containers to pinpoint bottlenecks and diagnose crashes.

If you're deploying on your own cloud, you can [create custom plans](../bring-your-own-cloud/create-custom-resource-plans) to make best use of the high vCPU and memory of GPU nodes.

Persist models and training data

Your services and jobs are stateless, and will not persist any changes or downloads between restarts. You can add volumes to persist data, so you don’t have to repeatedly download models and datasets, and you can save model checkpoints .

You can [mount persistent volumes](../databases-and-persistence/add-a-volume) for your applications at the default paths for model caches, for example:

Framework/image| Default model/data path| Purpose  
---|---|---  
**vLLM**| `/root/.cache/huggingface`| Hugging Face model and tokenizer cache  
**Ollama**| `/root/.ollama`| Model downloads  
**Jupyter Notebook**| `/home/jovyan`| Notebook data  
  
You should refer to your application or library's documentation to find the default paths, or environment variable keys to override the default directories for downloads.

### Use external storage

You can also configure your application to use external storage to persist models, datasets, configuration, and other data outside your service and job containers.

This allows you to scale your instances up while persisting data, and to share data between different services and jobs.

You can deploy [databases](../databases-and-persistence/stateful-workloads-on-northflank) as well as [MinIO, an S3-compatible datastore](../databases-and-persistence/deploy-databases-on-northflank/deploy-minio-on-northflank) and implement the relevant SDKs/libraries in your application.

Next steps

[Deploy a GPU project on NorthflankDeploy a GPU-enabled project on Northflank's managed cloud.](/docs/v1/application/gpu-workloads/deploy-gpus-on-northflank-cloud#deploy-a-gpu-enabled-project)[Deploy GPU workloads in your own cloudDeploy GPU nodes and workloads in your own cloud provider account.](/docs/v1/application/gpu-workloads/deploy-gpus-in-your-own-cloud)
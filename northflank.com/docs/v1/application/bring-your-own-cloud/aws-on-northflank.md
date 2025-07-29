---
source_url: https://northflank.com/docs/v1/application/bring-your-own-cloud/aws-on-northflank
title: Amazon Web Services on Northflank | Bring Your Own Cloud | Northflank Application docs
crawl_date: 2025-07-29T09:26:09.932377
watsonmd_version: 0.1.0
---

Bring Your Own Cloud / 

# Amazon Web Services on Northflank

You can integrate your Amazon Web Services account to create and manage clusters using Northflank.

To add your AWS account navigate to the clusters page in your account settings and create a new integration.

[Click here ](https://app.northflank.com/s/account/cloud/clusters/integrations/new/aws) to create a new AWS integration.

You can create an integration using a cross-account role (recommended), or with an IAM user (legacy method).

After integrating your account, you can create a new cluster.

Generate and view required permissions

When you create your AWS account integration you can select the features you want to use with Northflank, such as custom VPC and static egress. Additional features may require extra permissions.

After selecting the features you want to use you can review the required permissions in a table, or the entire inline policy as JSON, and copy it to your clipboard.

You can check existing integrations have all the necessary permissions by opening an integration from your team's clusters page and clicking `verify all permissions`.

You can view the inline policy required for Northflank to set up a cluster on AWS with a custom VPC and static egress below.

AWS inline policy
    
    
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Sid": "Northflank",
          "Effect": "Allow",
          "Action": [
            "ec2:AllocateAddress",
            "ec2:AssociateRouteTable",
            "ec2:CreateNatGateway",
            "ec2:CreateRoute",
            "ec2:CreateRouteTable",
            "ec2:CreateSubnet",
            "ec2:CreateTags",
            "ec2:DeleteNatGateway",
            "ec2:DeleteRoute",
            "ec2:DeleteRouteTable",
            "ec2:DeleteSubnet",
            "ec2:DescribeAddresses",
            "ec2:DescribeNatGateways",
            "ec2:DescribeRouteTables",
            "ec2:DescribeSubnets",
            "ec2:DescribeVpcs",
            "ec2:DisassociateRouteTable",
            "ec2:ReleaseAddress",
            "eks:AssociateAccessPolicy",
            "eks:CreateAccessEntry",
            "eks:CreateAddon",
            "eks:CreateCluster",
            "eks:CreateNodegroup",
            "eks:DeleteAccessEntry",
            "eks:DeleteAddon",
            "eks:DeleteCluster",
            "eks:DeleteNodegroup",
            "eks:DescribeAccessEntry",
            "eks:DescribeAddon",
            "eks:DescribeCluster",
            "eks:DescribeNodegroup",
            "eks:DescribeUpdate",
            "eks:DisassociateAccessPolicy",
            "eks:ListAccessEntries",
            "eks:ListAccessPolicies",
            "eks:ListAddons",
            "eks:ListAssociatedAccessPolicies",
            "eks:ListClusters",
            "eks:ListIdentityProviderConfigs",
            "eks:ListInsights",
            "eks:ListNodegroups",
            "eks:ListTagsForResource",
            "eks:ListUpdates",
            "eks:TagResource",
            "eks:UntagResource",
            "eks:UpdateAccessEntry",
            "eks:UpdateAddon",
            "eks:UpdateClusterConfig",
            "eks:UpdateClusterVersion",
            "eks:UpdateNodegroupConfig",
            "eks:UpdateNodegroupVersion",
            "iam:AttachRolePolicy",
            "iam:CreateOpenIDConnectProvider",
            "iam:CreateRole",
            "iam:CreateServiceLinkedRole",
            "iam:DeleteOpenIDConnectProvider",
            "iam:DeleteRole",
            "iam:DeleteRolePolicy",
            "iam:DetachRolePolicy",
            "iam:GetOpenIDConnectProvider",
            "iam:GetRole",
            "iam:ListAttachedRolePolicies",
            "iam:PassRole",
            "iam:PutRolePolicy",
            "iam:SimulatePrincipalPolicy",
            "iam:TagOpenIDConnectProvider",
            "iam:TagRole"
          ],
          "Resource": [
            "*"
          ]
        }
      ]
    }
    

Add your account with a cross-account role

It is recommended that you use a cross-account role to integrate your AWS account with Northflank. This method is more secure, as Northflank doesn't store a long-term secret but rather requests a new token every time account access is required.

Requirements

You will need the following to get started:

  * permission to create new [roles ](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies-cross-account-resource-access.html) in your AWS account
  * sufficient quotas to deploy your cluster



To integrate AWS with a cross-account role:

  1. Navigate to your Northflank account settings and open the clusters page
  2. [Create a new cloud provider integration ](https://app.northflank.com/s/account/cloud/clusters/integrations/new/aws) and select Amazon Web Services as the provider
  3. Select Amazon Web Services as the provider and choose the features you want to use with Northflank. Select `cross account role` as the credential method and copy the custom trust policy.
  4. Open your [AWS IAM console ](https://console.aws.amazon.com/iam/home) and open the `roles` page
  5. Create a new role, select `custom trust policy` and paste in the trust policy from Northflank. Skip the remaining steps, name and save the role.
  6. Return to Northflank and review the permissions required for your integration. Copy the AWS inline policy and return to your AWS console.
  7. Find your new AWS IAM role in the list on the roles page, open it, click `add permissions`, and select `create inline policy`. Paste in and save the inline policy you copied from Northflank.
  8. Copy the IAM role ARN to Northflank and `create` the integration



You can now configure and deploy new clusters in your AWS account. You can update your integration with a new shared secret and IAM role ARN. If this role does not have permission to manage existing clusters, you will be unable to edit those clusters and deleting them via AWS may leave orphaned resources.

Add your account with an IAM user

You can add your account to Northflank by providing the access and secret keys for an IAM user. This is a legacy method, it is recommended that you instead integrate using a cross-account role.

Requirements

You will need the following to get started:

  * permission to create new [IAM users ](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html) in your AWS account
  * sufficient quotas to deploy your cluster



To add your AWS account to Northflank with an IAM user:

  1. Navigate to your Northflank account settings and open the clusters page
  2. [Create a new cloud provider integration ](https://app.northflank.com/s/account/cloud/clusters/integrations/new/aws)
  3. Select Amazon Web Services as the provider and choose the features you want to use with Northflank
  4. Review the required permissions and copy the AWS inline policy
  5. Open your [AWS IAM console ](https://console.aws.amazon.com/iam/home), open the `users` page and create a new user without console access. Skip the remaining steps and save the user.
  6. In the new user click `add permissions` and select `create inline policy`. Paste in and save the inline policy you copied from Northflank.
  7. Open `security credentials` in your new user and click `create access key`. Select the `third-party service` use case and click `next`. Enter a description that will help you recognise your key (e.g. `Northflank BYOC`) and `create access key`.
  8. Enter the `access key` and `secret key` for the user you created into the Northflank integration form and `create` the integration



You can edit the integration at any time to update the secrets, if required. If the new secrets do not have permission to manage existing clusters, you will be unable to edit those clusters and deleting them via AWS may leave orphaned resources.

Check your quotas

To successfully deploy a cluster on AWS using Northflank you must have the required resources available to your account for your desired region.

[Check the node types](deploy-and-scale-node-pools#select-node-type) you wish to deploy and ensure your cluster has access to the relevant resources. The specific quotas for each provider may differ, you will need to ensure you have sufficient quotas for your required node type, vCPU, and disk type for your desired regions.

You can change your [AWS service quotas ](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html) by selecting the relevant region in the console and navigating to the `service quotas` page. You may need to [opt-in to a region ](https://docs.aws.amazon.com/accounts/latest/reference/manage-acct-regions.html) first. Choose the relevant AWS service from the dashboard, or search for it on the `AWS services` page, then search for the relevant resource quotas to increase.

For example, to increase the number of node pools you can deploy on AWS using the `m5.large` node type select the relevant region in the console, search for and open the AWS service `Amazon Elastic Compute Cloud (Amazon EC2)`, search for `Running On-Demand Standard (A, C, D, H, I, M, R, T, Z) instances` and click `request quota increase`.

Create a cluster

To add a new cluster, navigate to the clusters page in your account settings and click `create cluster`.

[Click here ](https://app.northflank.com/s/account/cloud/clusters/new/aws) to create a new AWS cluster.

![Create a new cluster in the Northflank application](https://assets.northflank.com/documentation/v1/application/bring-your-own-cloud/create-a-kubernetes-cluster-with-Northflank/create-cluster.png)

Enter a name for the cluster and select AWS as the cloud provider. Choose your integration credentials and select the region to deploy in.

### Select a Virtual Private Cloud

When you create a cluster you can select which [Virtual Private Cloud ](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html) to use. The VPC defines public and private networks in your clusters, allowing access to other AWS services and the internet.

The [default VPC ](https://docs.aws.amazon.com/vpc/latest/userguide/work-with-default-vpc.html) includes public subnets for each availability zone, and its components cannot be modified. You should not use the default VPC for production deployments.

For production deployments you should use a custom VPC to deploy into a private node pool with no public access, or to access other services in your AWS account. Separate VPCs are defined for each region.

You can select which subnets (and therefore availability zones) will host the control plane components for your cluster, this has no impact on the subnets that you can select for node pools. You should select between 2 and 4 subnets for the cluster's control plane.

### Configure node pools

You can now configure the node pools for your cluster. Node pools can also be added, deleted, and updated after creating your cluster. Click `add node pool` to add another pool.

Minimum cluster requirements

Each cluster requires at least one node pool, and a combined minimum of 4 vCPU and 8GB memory across all node pools.

The number of pods that can be scheduled on each node is determined by networking and node scheduling limits.

#### Cluster networking limits

The AWS Load Balancer only allows a maximum of 500 targets per availability zone. This total includes each node pool deployed to the availability zone for that cluster.

To help avoid issues with networking capacity you should create node pools with fewer, larger nodes rather than lots of smaller nodes.

See [deploy and scale node pools](deploy-and-scale-node-pools) for more information on configuring nodes and node pools.

### Configure advanced options

After adding your initial node pools you can configure advanced options for the cluster, such as build infrastructure, resource request modifiers, and volume deletion options.

When you create the cluster Northflank will begin installing system components in node pools according to their capacity. This may take up to 20 minutes.

Use a custom VPC

When you create a new cluster you can select a custom VPC that you have defined in your account and selected region. You can create and manage your VPCs in the [AWS console ](https://console.aws.amazon.com/vpcconsole/). You must create a subnet in each availability zone that you want to use, and your VPC must include at least one public subnet.

Learn more about [Amazon EKS networking requirements for VPC and subnets ](https://docs.aws.amazon.com/eks/latest/userguide/network-reqs.html).

### Subnets

Public subnets must be associated with an internet gateway, and private subnets require a NAT gateway for egress. You can use a single NAT for multiple private subnets, but this may become a bottleneck for high-traffic applications. Workloads deployed to a node pool with a private subnet will be able to communicate with other resources in your VPC and initiate internet connections via the NAT gateway, but will not be exposed to unsolicited ingress requests. [Read more about connecting your VPC here ](https://docs.aws.amazon.com/vpc/latest/userguide/extend-intro.html).

### Security

You can enable the control plane IP allow list option to block all except Northflank’s egress IP from accessing the cluster’s Kubernetes API endpoint.

### IP addresses

Subnets need to have sufficient available IPs for pods and load balancers. Northflank requires at least 32 available IPs for public subnets that will host load balancers. Private subnets which will host node pools require a minimum of 64 available IPs, we strongly recommend to allocate much more (CIDR range /22, /21, or /20) depending on the number of workloads you expect to run. The default CIDR ranges provided by Amazon when configuring a subnet should be sufficient for most use-cases.

Default VPC configuration

The default subnets in the default VPC are public, i.e. nodes will be assigned a public IP. In default VPC mode, subnets for the cluster and node pools are selected by availability zone. Northflank will use the default subnet for the selected availability zone.

  * You should select between 2 and 4 availability zones for your cluster’s control plane.
  * You can create node pools across 2 or more availability zones for high-availability of workloads.
  * You should enable the control plane IP allow list option to block all bar Northflank’s egress IP from accessing the cluster’s Kubernetes API endpoint.



Custom VPC example

#### VPC setup

  * IPv4 CIDR block: 10.0.0.0/16
  * No IPv6 CIDR block
  * Use 3 or more availability zones
  * Add 3 public subnets, one for each availability zone; ensure “auto-assign public IP” is enabled; a /20 CIDR block is recommended
  * Add an internet gateway and associate it with the public subnets via route tables
  * Add 3 private subnets, one for each availability zone; a /20 CIDR block is recommended
  * Add 1 NAT gateway per availability zone (if you want to reduce cost, you can also use just one NAT for the entire VPC)
  * Associate each private subnet with a corresponding NAT via route tables
  * Enable DNS hostnames
  * Enable DNS resolution



#### Northflank cluster creation

  * Select 3 private subnets for your cluster’s control plane
  * Create node pools on private subnets.
  * Create 2 or more node pools across multiple (private) subnets for high-availability of workloads.
  * Enable the control plane IP allow list option to block all bar Northflank’s egress IP from accessing the cluster’s Kubernetes API endpoint.



### Cluster subnet selection

You can select which subnets (and therefore availability zones) will host the control plane components for your cluster, this has no impact on the subnets that you can select for node pools. You should select between 2 and 4 subnets for the cluster's control plane.

Your VPC must have one public subnet to allow Northflank to manage the cluster, although you are recommended to have at least two public subnets in different availability zones. You do not need to select a public subnet for the cluster.

Enable egress via a static IP

If you are using the default VPC you can enable static egress to route the cluster’s outgoing traffic through a static IP. This is useful if you use external services that only accept requests from specified IP addresses.

If you are using a custom VPC, you must set up your own static egress IP for your cluster in AWS.

Deploy to private nodes

You can use Northflank to deploy workloads to nodes in private subnets. This prevents public ingress requests to these workloads, they will only be able to receive traffic from resources in your VPC and from external sources where your workloads have initiated the request.

You will need to create a cluster with a custom VPC that has private subnets configured on it, then select an availability zone with a private subnet when you create a new node pool.

You can then [create a project on your cluster](deploy-workloads-to-your-cluster), and use [node pool labels and Northflank tags](deploy-workloads-to-your-cluster#deploy-workloads-to-specific-node-pools) to schedule workloads to your private nodes.

Use AWS Launch Templates

Northflank supports the use of [AWS Launch Templates ](https://docs.aws.amazon.com/eks/latest/userguide/launch-templates.html) to specify cluster resources. You can use Launch Templates to take advantage of [capacity blocks for ML training ](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-capacity-blocks.html), which allow you to reserve GPU nodes for a specific time period at a known price, up to 8 weeks in advance.

You can select a Launch Template when creating a node pool in an AWS cluster on Northflank. The specifications in the Launch Template will override some of the options selected for the node pool in Northflank.

### Configure Northflank permissions

You must give Northflank permissions to use Launch Templates in your AWS integration. You can create a new integration, or update permissions for an existing integration by adding `Custom Launch Templates` to desired features.

For an existing integration, update your IAM role by copying the new AWS inline policy then `verify all permissions` in Northflank. For a new integration, follow the instructions as normal.

AWS Launch Templates permissions
    
    
    ec2:DescribeLaunchTemplateVersions
    ec2:DescribeLaunchTemplates
    ec2:RunInstances
    

### Create a Launch Template

Launch templates are region-specific, you must create a Launch Template in the same region as your AWS cluster. You can create a Launch Template in your [EC2 dashboard in the AWS console ](https://console.aws.amazon.com/ec2/), from the `Launch Templates` page under instances.

Set a name and (optionally) a description, but do not select an Amazon Machine Image.

You can then select an instance type. This is optional, if selected it will override the instance type that you specify for a node pool on Northflank. If you are using a capacity block, the instance type must match the reserved instances.

![Selecting an instance for an AWS Launch Template in the AWS console](https://assets.northflank.com/documentation/v1/application/bring-your-own-cloud/aws-on-northflank/aws-launch-template-instances.png)

You must define at least one volume in the Launch Template, which will override the disk specified for a node pool on Northflank. Add a new volume under storage, set the [device name ](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/device_naming.html), for example `/dev/xvda`. Choose the disk size and select `yes` for delete on termination. You can configure other options, such as disk encryption, as required.

![Adding a volume in an AWS Launch Template in the AWS console](https://assets.northflank.com/documentation/v1/application/bring-your-own-cloud/aws-on-northflank/aws-launch-template-storage.png)

Next, select a purchasing option. Choose `Capacity Blocks` and enter your [capacity reservation targeted ID ](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/capacity-reservations-create.html).

![Choosing a Capacity Block for an AWS Launch Template in the AWS console](https://assets.northflank.com/documentation/v1/application/bring-your-own-cloud/aws-on-northflank/aws-launch-template-capacity-blocks.png)

Do not configure the machine image, subnets, shutdown behaviour or IAM profile in the Launch Template, as these are handled by Northflank. Finally, save your Launch template.

Configuring resources not mentioned in this guide in a Launch Template may cause issues scheduling and managing nodes with Northflank. Learn more about [Launch Template configuration ](https://docs.aws.amazon.com/eks/latest/userguide/launch-templates.html), or contact [[support@northflank.com](mailto:support@northflank.com)](mailto:support@northflank.com) to discuss other use cases.

### Use a Launch Template

To use a Launch Template, select an existing AWS cluster on Northflank, or create a new one. Configure the cluster as normal with a node pools for system components, and any other required node pools.

Create a new node pool and [configure it as normal](../deploy-and-scale-node-pools), selecting the node type, disk size, availability zone. Expand the `advanced` section and update the scheduling rules, if required. In the advanced section, select your Launch Template and version (updating the Launch Template will create a new version).

![Creating a node pool with an AWS Launch Template in the Northflank application](https://assets.northflank.com/documentation/v1/application/bring-your-own-cloud/aws-on-northflank/node-pool-launch-template.png)

When you create your cluster, or add the new node pool, the Launch Template will override any configured fields.

If you are using a capacity block nodes will not join the node pool until the date and time of the capacity reservation. At the end of the reservation period nodes will be removed from the node pool, you may want to gracefully terminate workloads before this happens. If your cluster has no other node pools with nodes that these workloads can schedule on, they will remain unscheduled until the required capacity is added.

Next steps

[Configure your Kubernetes clusterManage your clusters on other cloud providers using Northflank.](/docs/v1/application/bring-your-own-cloud/configure-your-cluster)[Deploy node poolsConfigure and deploy node pools on a Kubernetes cluster with Northflank.](/docs/v1/application/bring-your-own-cloud/deploy-and-scale-node-pools)[Deploy workloads to your clusterDeploy services, jobs, and addons to your own cluster, and configure workloads to schedule on specific node pools.](/docs/v1/application/bring-your-own-cloud/deploy-workloads-to-your-cluster)[Run GPU workloadsDeploy GPU workloads on Northflank for AI, machine learning, HPC workloads, and other tasks.](/docs/v1/application/gpu-workloads/gpus-on-northflank)
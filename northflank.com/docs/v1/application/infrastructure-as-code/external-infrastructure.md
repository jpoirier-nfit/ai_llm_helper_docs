---
source_url: https://northflank.com/docs/v1/application/infrastructure-as-code/external-infrastructure
title: Manage external infrastructure | Infrastructure as Code | Northflank Application docs
crawl_date: 2025-07-29T09:26:09.856615
watsonmd_version: 0.1.0
---

Infrastructure as Code / 

# Manage external infrastructure

Northflank provides a robust mechanism for provisioning and managing external infrastructure directly within your own cloud environment through the use of OpenTofu modules. OpenTofu is an open-source Infrastructure as Code (IaC) tool, and Northflank integrates this capability by allowing OpenTofu modules to be embedded as template nodes within Northflank templates.

These OpenTofu nodes can be added to any existing or new Northflank template, enabling teams to automate the deployment of external infrastructure components—such as databases, object storage, and other cloud services—alongside application and service configuration. This infrastructure is created and managed within your own cloud accounts.

Once the OpenTofu module is added to a template and configured, Northflank takes responsibility for executing the module, managing its life cycle, and securely storing the Terraform state between runs. This allows infrastructure management integrated directly into your Northflank workflows.

The process of creating and configuring an OpenTofu node is consistent with how other template nodes are added in Northflank. This documentation will guide you through a complete example that demonstrates how to use an OpenTofu module to provision an AWS S3 bucket.

You should understand how to [create a new template](create-a-template) and [use other cloud providers](../bring-your-own-cloud/use-other-cloud-providers-with-northflank) before reading this section.

Add provider integration to Northflank

Northflank OpenTofu nodes will require credentials to access upstream providers. These are described in detail in [use other cloud providers](../bring-your-own-cloud/use-other-cloud-providers-with-northflank).

note

Northflank OpenTofu nodes currently do not support cross account roles. Make sure to setup a provider integration with direct credentials.

  1. Navigate to your Northflank account settings and open the clusters page
  2. [Create a new cloud provider integration ](https://app.northflank.com/s/account/cloud/clusters/integrations/new/aws)
  3. Select Amazon Web Services as the provider and choose the OpenTofu feature
  4. Open your [AWS IAM console ](https://console.aws.amazon.com/iam/home), open the `users` page and create a new user without console access. Skip the remaining steps and save the user.
  5. In the new user click `add permissions` and the required permissions for the resources you want to create. In our case we can allow all actions to S3 resources.
  6. Open `security credentials` in your new user and click `create access key`. Select the `third-party service` use case and click`next`. Enter a description that will help you recognise your key (e.g. `Northflank OpenTofu`) and `create access key`.
  7. Enter the `access key` and `secret key` for the user you created into the Northflank integration form and `create` the integration.



Add an OpenTofu node to a template

OpenTofu nodes are created as part of a template. [Create a new template](./create-a-template) or pick an existing one to begin. Add `example` as the Node reference so we can refer to this node later in our template.

Add a new OpenTofu node to your template, this node contains all of the details for a single OpenTofu module. We recommended keeping your modules as small as possible as larger modules take longer to apply. You can use Northflank templating system to pass variables between OpenTofu nodes, more details in the outputs section below.

Northflank offers a limited selection of providers and resources. Please contact us if there is anything you would like added.

Since we want an S3 bucket, that is available under the AWS provider. Select that and the integration credentials setup in the previous step, as well as the aws region that your resources will be created in.

The set of required fields will vary for different providers.

The providers and resources that Northflank makes available come directly from the upstream [OpenTofu registry ](https://search.opentofu.org/providers). Refer to that documentation at any time for any available attributes and descriptions of each one.

Add OpenTofu resources

The next section of the OpenTofu node is where resources are defined, the set of resources available will be different depending on the provider selected. To add a resource click the Add resource button then select the resource type from the available list. Provide a name to refer to that resource later in the node.

Select `aws_s3_bucket` as the type and name it `my_bucket`.

The Spec field is for entering this resources attributes as documented in the [ upstream providers resource documentation ](https://search.opentofu.org/provider/hashicorp/aws/latest/docs/resources/s3_bucket#argument-reference). Refer to the upstream documentation for details about which attributes are available for any resource and details about those attributes. Northflank uses the JSON configuration syntax, [ documented here ](https://opentofu.org/docs/language/syntax/json/). The syntax is similar to HCL, the main difference being that keys are quoted and the value separator is colon (:) instead of equals (=).

There are no required attributes for the `aws_s3_bucket` resource so we can leave the sepc as an empty object, alternatively we can pass a name to our bucket:
    
    
    {
      "bucket": "example-bucket-name"
    }
    

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAACXBIWXMAAAsTAAALEwEAmpwYAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAEZSURBVHgB7ZXBDYIwFIbfa030YuIIuoEj6Ml4dALZQDdwBEdwCoPhghs4giuQSMCDoRYEUkqBB8GTfklDaN57//+nDQD8FOEFXbnubXoYtdC3wZKPhVzT4AJ7ah9SC1Pn06QJwRsGYoYb8Jr6SAmeDttlw2OEgEkwoqVoTBDacjCiqwokjcQUjQkYY1t9eAw1RW2C1H3lraGkqE+A7KC+jlZRsjIoKSoFEvcgLGiAM9x9alsK6O6riFPU1RoFqO4VGcs/w5wsQHWvwjkejaP0Dd+BOY/wBh14CbEcr+Gq7pUSyOFH6MgAsZS8IKB80Izo19TA4mEX+wsC3OCgLXqK/Axi91LgBD2gnkWeoA/3GQPFKPmH8+drvAGciFlVpRD4HQAAAABJRU5ErkJggg==)

important

OpenTofu modules use the same syntax for template strings as Northflank templates `${}`. They will be interpreted as Northflank template strings, to use OpenTofu template strings you need to escape them with a backslash.

For example `${aws_s3_bucket.my_bucket.id}`will need to be written as `\${aws_s3_bucket.my_bucket.id}`.

Use outputs

Any output attribute can be exposed to subsequent template nodes, however they must be declared in the output section of the OpenTofu node.

In our example we want to access the S3 bucket domain name later in our template. To do this add a new output, give it a descriptive name, and then as the value enter
    
    
    ${aws_s3_bucket.my_bucket.bucket_domain_name}
    

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAACXBIWXMAAAsTAAALEwEAmpwYAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAEZSURBVHgB7ZXBDYIwFIbfa030YuIIuoEj6Ml4dALZQDdwBEdwCoPhghs4giuQSMCDoRYEUkqBB8GTfklDaN57//+nDQD8FOEFXbnubXoYtdC3wZKPhVzT4AJ7ah9SC1Pn06QJwRsGYoYb8Jr6SAmeDttlw2OEgEkwoqVoTBDacjCiqwokjcQUjQkYY1t9eAw1RW2C1H3lraGkqE+A7KC+jlZRsjIoKSoFEvcgLGiAM9x9alsK6O6riFPU1RoFqO4VGcs/w5wsQHWvwjkejaP0Dd+BOY/wBh14CbEcr+Gq7pUSyOFH6MgAsZS8IKB80Izo19TA4mEX+wsC3OCgLXqK/Axi91LgBD2gnkWeoA/3GQPFKPmH8+drvAGciFlVpRD4HQAAAABJRU5ErkJggg==)

important

The form editor will auto escape these strings, however the code editor will not. Make sure to escape any OpenTofu template string in the output section the same as the resource section when using the code editor.

Any outputs declared in this way will be available on the OpenTofu node after it has run. They can be accessed using Northflank template strings under the refs object. If our node has a ref of `example` and we called the output `generated_url` then the value can be referenced later in the template with the template string

`${refs.example.outputs.generated_url.value}`.

note

Outputs are not known until after the resources have been applied. Make sure`Wait for completion` is selected if you are planning on using the outputs.

Create a new secret group node and add a new variable with any name and

`${refs.example.outputs.generated_url.value}` as the value. Once this template is run you will be able to retrieve the generated url from this secret group.

Run template

Once you are happy with the template, save and run it. Northflank will provision all of the resources defined in the OpenTofu node once that node is processed.

Provisioning resources may take some time so be patient. The OpenTofu node will remain in pending state until the resources have either been successfully created or failed. Any error messages are displayed on the node that failed.

Once the template has fully completed, you can view the secret group we created to confirm that the outputs have saved as expected.

note

Northflank currently has no way to delete resources once created. If you no longer need these resources then it is up to you to clean them up.

Northflank can handle running multiple OpenTofu jobs simultaneously, however only the latest run will contain accurate information. Northflank will skip running any job for a OpenTofu node if it detects a later one has been scheduled for the same OpenTofu node.
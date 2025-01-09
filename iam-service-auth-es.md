---

copyright:
  years:  2021, 2025
lastupdated: "2025-01-09"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}

# Creating a S2S authorization to work with the {{site.data.keyword.messagehub_full}} service
{: #iam-service-auth-es}

Use {{site.data.keyword.iamlong}} (IAM) to create an authorization that grants {{site.data.keyword.atracker_full_notm}} access to the {{site.data.keyword.messagehub_full}} service.
{: shortdesc}



## Before you begin
{: #iam-service-auth-es-prereqs}

- Read about [Managing authorizations to grant access between services](/docs/atracker?topic=atracker-iam-service-auth).

- You must have access to the target service to manage authorization between services. For more information, see [Permissions to manage authorizations](/docs/atracker?topic=atracker-iam-service-auth#iam-service-auth-permissions).

- The autorization that you define for the {{site.data.keyword.atracker_full_notm}} service requires that you have `Administrator` role for the {{site.data.keyword.messagehub_full}} target.

- Make sure that you define the authorization in the account where the bucket is located.

- If you create an authorization between a service in another account and a target service in your current account, you need to have access only to the target resource. For the source account, you need only the account ID. 


## Service access roles
{: #iam-service-auth-es-roles}

You must grant `Writer` role to handle source integration with the {{site.data.keyword.messagehub_full}} service.


## Creating an authorization through the console
{: #iam-service-auth-es-create-ui}
{: ui}

Complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and select **Authorizations**.
2. Click **Create**.
3. Select a source account.

    If {{site.data.keyword.atracker_full_notm}} and the {{site.data.keyword.messagehub_full}} instance are in the same account where you are defining the authorization, select **This account**.

    If {{site.data.keyword.atracker_full_notm}} and the {{site.data.keyword.messagehub_full}} instance are in different accounts, select **Other account**. Then, enter the account ID of the source account, that is, the account where {{site.data.keyword.atracker_full_notm}} is to be configured to send data to the instance.

4. Select `Activity Tracker Event Routing` as the source service. Then, set the scope of the access to **All resources**.

5. Select **Event Streams** as the target service. Then, set the scope of the access.

    To grant access to all {{site.data.keyword.messagehub_full}} instances and resources in the account, select **All resources**.

    To grant access to a specific instance, select single instance by configuring **Resources based on selected attributes** &gt; **Service Instance**.

6. In the *Service Access* section, select the role to assign access to the source service that accesses the target service.

    Select **Writer** to authorize streaming to {{site.data.keyword.messagehub_full}}.

7. Click **Authorize**.

If you create an authorization between a service in another account and a target service in your current account, you need to have access only to the target resource. For the source account, you need only the account number. 
{: note}

## Creating an authorization by using the CLI
{: #iam-service-auth-es-create-cli-1}
{: cli}



Run the following command to create an authorization for the {{site.data.keyword.atracker_full_notm}} service.

```sh
ibmcloud iam authorization-policy-create atracker messagehub "Writer" [--target-service-instance-id TARGET_SERVICE_INSTANCE_ID]
```
{: codeblock}


For more information about all of the parameters that are available for this command, see [ibmcloud iam authorization-policy-create](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_authorization_policy_create).


## Creating an authorization cross accounts by using the CLI
{: #iam-service-auth-es-create-cli-cross}
{: cli}


Run the following command to create an authorization in the account where the target service is located when the {{site.data.keyword.atracker_full_notm}} service and the target service are in different accounts:

```sh
ibmcloud iam authorization-policy-create atracker cloud-object-storage "Object Writer"  [--target-service-instance-id TARGET_SERVICE_INSTANCE_ID] [--source-service-account SOURCE_SERVICE_ACCOUNT_GUID ]
```
{: codeblock}

Where you can set the following parameters to grant access to a single bucket:
- `TARGET_SERVICE_INSTANCE_NAME`: CRN of the {{site.data.keyword.messagehub_full}} instance.
- `SOURCE_SERVICE_ACCOUNT_GUID`: Set the account GUID where {{site.data.keyword.atracker_full_notm}} is configured to send data to the target service. Only use this option if the source service is from another account.


For more information about all of the parameters that are available for this command, see [ibmcloud iam authorization-policy-create](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_authorization_policy_create).


## Creating an authorization by using Terraform
{: #iam-service-auth-es-create-terra}
{: terraform}


Before you can create an authorization by using Terraform, make sure that you have completed the following:

- Install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. For more information, see the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud_notm}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.
- Create a Terraform configuration file that is named `main.tf`. In this file, you define resources by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.

Use the following steps to create an authorization by using Terraform:

1. Create an authorization policy between services by using the `ibm_iam_authorization_policy` resource argument in your `main.tf` file.

    The following example creates an authorization between 2 services:

    ```terraform
    resource "ibm_iam_authorization_policy" "policy" {
     source_service_name = "atracker"
     target_service_name = "messagehub"
     roles               = ["Writer"]
     description         = "Authorization Policy"
     transaction_id     = "terraformAuthorizationPolicy"
    }
    ```
    {: codeblock}

    The following example creates an authorization between 2 specific service instances:

    ```terraform
    resource "ibm_iam_authorization_policy" "policy" {
      source_service_name         = "atracker"
      source_resource_instance_id = ibm_resource_instance.instance1.guid
      target_service_name         = "messagehub"
      target_resource_instance_id = ibm_resource_instance.instance2.guid
      roles                       = ["Writer"]
    }
    ```
    {: codeblock}

    The `ibm_iam_authorization_policy` resource requires the source service, target service, and role. The source service is granted access to the target service, and the role is the level of permission that the access allows. Optionally, you can add a description for the authorization and a transaction ID.
    {: note}

    - You can provide a `target_resource_instance_id` to scope a {{site.data.keyword.messagehub_full}} target instance.

    - For more examples, see the [Terraform documentation for authorization resources](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_authorization_policy){: external}.

2. After you finish building your configuration file, initialize the Terraform CLI. For more information, see [Initializing Working Directories](https://developer.hashicorp.com/terraform/cli/init){: external}.

    ```terraform
    terraform init
    ```
    {: pre}

3. Provision the resources from the `main.tf` file. For more information, see [Provisioning Infrastructure with Terraform](https://developer.hashicorp.com/terraform/cli/run){: external}.

    1. Run `terraform plan` to generate a Terraform execution plan to preview the proposed actions.

        ```terraform
        terraform plan
        ```
        {: pre}

    2. Run `terraform apply` to create the resources that are defined in the plan.

        ```terraform
        terraform apply
        ```
        {: pre}

## Creating an authorization by using the API
{: #iam-service-auth-es-create-api}
{: api}


To authorize a source service access to a target service, use the [IAM Policy Management API](/apidocs/iam-policy-management#create-policy). See the following API example for create a policy method with the `type=authorization` specified for a `event-notifications` target.

The supported attributes for creating an authorization policy depend on what each service supports. For more information about the supported attributes for each service, see the documentation for the services that you're using.
{: note}

```bash
curl --request POST \
  --url https://iam.cloud.ibm.com/v1/policies \
  --header 'Authorization: Bearer <token>' \
  --header 'Content-Type: application/json' \
  --data '{
    "type": "authorization",
    "subjects": [
        {
            "attributes": [
                {
                    "name": "accountId",
                    "value": "<account-id>"
                },
                {
                    "name": "serviceName",
                    "value": "atracker"
                }
            ]
        }
    ],
    "roles": [
        {
            "role_id": "crn:v1:bluemix:public:iam::::serviceRole:Writer"
        }
    ],
    "resources": [
        {
            "attributes": [
                {
                   "name": "accountId",
                   "value": "CUSTOMER_ACCOUNT_ID"
               },
               {
                    "name": "serviceName",
                    "value": "messagehub"
                },
                {
                    "name": "serviceInstance",
                    "value": "IES_SERVICE_INSTANCE"
                }
            ]
        }
    ]
}'
```
{: curl}
{: codeblock}

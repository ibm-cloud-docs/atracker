---

copyright:
  years:  2021, 2025
lastupdated: "2025-01-23"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}

# Configuring {{site.data.keyword.atracker_full_notm}} in a hub and spoke mode for routing activity tracking events to a centralized {{site.data.keyword.logs_full_notm}} instance
{: #hub-spoke}

Configure {{site.data.keyword.atracker_full_notm}} in a hub and spoke architectural mode for routing activity tracking events to a centralized {{site.data.keyword.logs_full_notm}} instance.
{: shortdesc}

## Prereqs
{: #tutorial-hub-spoke-prereqs}

Throughout the tutorial, the following sample account IDs are used:
-	Hub account ID: 00000000000000000000000000000001
-	Spoke account ID: 11111111111111111111111111111111

In your setup, you must replace the account IDs with your 32 character account IDs.

The tutorial provides steps by using terraform. For more information, see [Getting started with Terraform on {{site.data.keyword.cloud_notm}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started).



## Configure the S2S authorizations in the hub account
{: #tutorial-hub-spoke-step1}
{: step}

Setup an authorization policy in the hub account for each {{site.data.keyword.atracker_full_notm}} in an spoke account.
{: important}

You must define a service to service authorization to permit {{site.data.keyword.atracker_full_notm}} in an spoke account to send activity tracking events to the {{site.data.keyword.logs_full_notm}} instance in the hub account. For more information, see [Creating a S2S authorization to grant access to the IBM Cloud Logs service](/docs/atracker?topic=atracker-iam-service-auth-logs).


For example, you can run in the hub account the following terraform to grant permission to a spoke account:

1. Create a Terraform configuration file that is named `main.tf`. In this file, you add the configuration to create the service to service authorization:

    ```terraform
    # Lookup the Cloud Logs instance that will receive the AT events
    data "ibm_resource_instance" "logs_instance" {
        name = var.cloud_logs_instance_name
        service = "logs"
    }

    resource "ibm_iam_authorization_policy" "policy" {
        source_service_name = "atracker"
        target_service_name = "logs"
        roles               = ["Sender"]
        description         = "Authorization Policy"
        transaction_id     = "terraformAuthorizationPolicy"
        source_service_account = var.spoke_account_id
        target_resource_instance_id = data.ibm_resource_instance.logs_instance.id
    }
    ```
    {: codeblock}

    Where the following terraform variables are required:

    - `var.spoke_account_id`: Variable that sets the account ID for the spoke account.

    -	`var.cloud_logs_instance_name`: Variable that sets the {{site.data.keyword.logs_full_notm}} instance that is used to perform the lookup to get the ID of the instance.

2. Initialize the Terraform CLI. Run the following command:

    ```terraform
    ./terraform init
    ```
    {: pre}

    You should see the following message: `Terraform has been successfully initialized!`.

3. Apply the terraform. Run the following command:

    ```terraform
    ./terraform apply -var region=us-south -var cloud_logs_instance_name=cloud-logs -var spoke_account_id=11111111111111111111111111111111
    ```
    {: codeblock}


## Configure {{site.data.keyword.atracker_full_notm}} in an spoke account
{: #tutorial-hub-spoke-step2}
{: step}


You must configure {{site.data.keyword.atracker_full_notm}} in each of the spoke accounts to indicate what activity tracking events are routed to the {{site.data.keyword.logs_full_notm}} instance in the hub account.
{: important}

Repeat the following steps in each spoke account:

1. Configure the {{site.data.keyword.atracker_full_notm}} settings to define where the metadata is stored.

    The metadata region must be set to the same region as your {{site.data.keyword.logs_full_notm}} instance.
    {: important}

2. Configure the {{site.data.keyword.logs_full_notm}} instance, that you have created in the hub account to receive auditing events, as a	target in the {{site.data.keyword.atracker_full_notm}} of the spoke account.

    Create a target that points to the {{site.data.keyword.logs_full_notm}} instance in the hub account. The region for the target should match the region in the {{site.data.keyword.logs_full_notm}} instance CRN.
    {: important}

3. Configure a route in the {{site.data.keyword.atracker_full_notm}} of the spoke account to define which events to send to the {{site.data.keyword.logs_full_notm}} target.

    Consider configuring a route with a wildcard (*) as location to indicate that all the activity tracking events should be sent to the {{site.data.keyword.logs_full_notm}} target.
    {: note}


Complete the following steps to configure {{site.data.keyword.atracker_full_notm}} in the spoke account:

1. Create a Terraform configuration file that is named `main.tf`. In this file, you add the configuration to configure the spoke account.

    ```terraform
    # Indicate the location for the metadata for the IBM Cloud Activity Tracker Event Routing configurations.
    # The metadata region must be set to the same region as your IBM Cloud Logs instance.
    resource "ibm_atracker_settings" "atracker_settings" {
      metadata_region_primary = "us-south"
      metadata_region_backup = "us-east"
      private_api_endpoint_only = false
      # Optional but recommended lifecycle flag to ensure target delete order is correct
      lifecycle {
        create_before_destroy = true
      }
    }

    # Create a target that points to the IBM Cloud Logs instance in the hub account.
    # The region for the target should match the region in the IBM Cloud Logs instance CRN.
    resource "ibm_atracker_target" "atracker_cloudlogs_target" {
      cloudlogs_endpoint {
        target_crn = var.cloud_logs_crn
      }
      name = "cloudlogs-hub-target"
      target_type = "cloud_logs"
      region = var.region
    }

    # Create a route that selects the events to send to the IBM Cloud Logs target
    # The route configured in this tutorial sends all of the events from the account to the target.

    resource "ibm_atracker_route" "atracker_route" {
      name = "route-to-hub"
      rules {
        target_ids = [ ibm_atracker_target.atracker_cloudlogs_target.id ]
        locations = [ "*" ]
      }
      lifecycle {
        # Recommended to ensure that if a target ID is removed here and destroyed in a plan, this is updated first
        create_before_destroy = true
      }
    }
    ```
    {: codeblock}

2. Initialize the Terraform CLI. Run the following command:

    ```terraform
    ./terraform init
    ```
    {: pre}

    You should see the following message: `Terraform has been successfully initialized!`.

3. Apply the terraform. Run the following command:

    ```terraform
    terraform apply -var region=us-south -var cloud_logs_crn=crn:v1:bluemix:public:logs:ca-tor:a/00000000000000000000000000000001:0908b3e3-b0cb-4630-a783-7a377c1cc61c::
    ```
    {: codeblock}

    Where the variables are :

    -	`cloud_logs_crn`: the CRN of the {{site.data.keyword.logs_full_notm}} instance from the hub account

    -	`region`: the region of the {{site.data.keyword.logs_full_notm}} instance from the hub account

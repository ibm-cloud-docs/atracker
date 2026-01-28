---

copyright:
  years:  2023, 2025
lastupdated: "2025-12-05"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}

# Routing activity tracker events across accounts
{: #cross-account-scenario}


Use {{site.data.keyword.atracker_full}} to configure the routing of activity tracker events from multiple source accounts to a target account.
{: shortdesc}

You can configure your source accounts to route all or a subset of activity tracker events to the target account. Source accounts are your accounts that contain Cloud resources that generate activity tracker events regardless of the Cloud resource location. Target account refers to your account that contains the {{site.data.keyword.logs_full_notm}} instance that will contain the activity tracker events.

This configuration implements a spoke–hub distribution system using the source account as the spoke and target account as the hub. Multiple spoke accounts send activity tracker events to a centralized hub account simplifying observability across the multiple spoke accounts.

This example uses terraform. However, other configuration methods can be used as well.
{: tip}

![A diagram that shows a sample {{site.data.keyword.atracker_full_notm}} cross account configuration.](/images/atracker-cross-account.svg "{{site.data.keyword.atracker_full_notm}} cross account configuration."){: caption="{{site.data.keyword.atracker_full_notm}} cross account configuration" caption-side="bottom"}

## Prerequisites
{: #cross-account-prereqs}

- You must identify the hub account that you want to receive the activity tracker events and the spoke accounts that will be sending the events to the hub account.

- You must have the Administrator role with permissions to manage {{site.data.keyword.atracker_full_notm}} in the source accounts. See [Managing access with IAM](/docs/atracker?topic=atracker-iam) and [Assigning access to {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-iam-assign-access).

## Step 1 - Create the hub account instance
{: #step-create-target-instance-terraform}
{: terraform}

Follow [Provisioning an {{site.data.keyword.logs_full_notm}} instance by using Terraform](/docs/cloud-logs?topic=cloud-logs-terraform-setup) to create the instance in the hub account. The instance will not receive activity tracker events until the spoke accounts are configured to send their events to the instance.

## Step 2 - Create hub authorization policies
{: #step-create-authorization-policy-terraform}
{: terraform}

Create an {{site.data.keyword.iamshort}} (IAM) service to service authorization policy in the hub account for each of your spoke accounts. In this example there are two spoke accounts.

```terraform
# FILE: hub/main.tf

terraform {
  required_version = ">= 0.13"
  required_providers {
    ibm = {
      source  = "ibm-cloud/ibm"
      version = "~>1.81.0"
    }
  }
}

variable "ibmcloud_api_key" {
  description = "The IBM Cloud API key."
  type        = string
  sensitive   = true
}

provider "ibm" {
  ibmcloud_api_key = var.ibmcloud_api_key
}

locals {
  source_account_a = "<INPUT_SPOKE_A_ACCOUNT_ID>"
  source_account_b = "<INPUT_SPOKE_B_ACCOUNT_ID>"
}

resource "ibm_iam_authorization_policy" "hub_policy_source_a" {
  source_service_name         = "atracker"
  source_service_account      = local.source_account_a
  target_service_name         = "logs"
  target_resource_instance_id = "<INPUT_HUB_LOGS_INSTANCE_ID>"
  roles                       = ["Sender"]
  description                 = "Authorize spoke A to the hub"
}

resource "ibm_iam_authorization_policy" "hub_policy_source_b" {
  source_service_name         = "atracker"
  source_service_account      = local.source_account_b
  target_service_name         = "logs"
  target_resource_instance_id = "<INPUT_HUB_LOGS_INSTANCE_ID>"
  roles                       = ["Sender"]
  description                 = "Authorize spoke B to the hub"
}
```
{: codeblock}

This step ensures {{site.data.keyword.atracker_full}} is authorized to route spoke A and spoke B account activity tracker events to hub account.


## Step 3 - Create spoke targets
{: #step-create-spoke-targets}
{: terraform}

Now that the hub account is fully configured, you need to create {{site.data.keyword.atracker_full_notm}} targets in each spoke account, the target destination is the hub account's {{site.data.keyword.logs_full_notm}} instance. In this example, there are only two spoke accounts, but there is no limitation to the number of spoke accounts that can be targeted to a single hub account.

```terraform
# NEW FILE: spoke_a/main.tf

terraform {
  required_version = ">= 0.13"
  required_providers {
    ibm = {
      source  = "ibm-cloud/ibm"
      version = "~>1.81.0"
    }
  }
}

variable "ibmcloud_api_key" {
  description = "The IBM Cloud API key."
  type        = string
  sensitive   = true
}

provider "ibm" {
  ibmcloud_api_key = var.ibmcloud_api_key
}

resource "ibm_atracker_target" "atracker_target" {
  cloudlogs_endpoint {
    target_crn = "<INPUT_HUB_LOGS_CRN>"
  }
  name = "spoke-a-target"
  target_type = "cloud_logs"
}
```
{: codeblock}

```terraform
# NEW FILE: spoke_b/main.tf

terraform {
  required_version = ">= 0.13"
  required_providers {
    ibm = {
      source  = "ibm-cloud/ibm"
      version = "~>1.81.0"
    }
  }
}

variable "ibmcloud_api_key" {
  description = "The IBM Cloud API key."
  type        = string
  sensitive   = true
}

provider "ibm" {
  ibmcloud_api_key = var.ibmcloud_api_key
}

resource "ibm_atracker_target" "atracker_target" {
  cloudlogs_endpoint {
    target_crn = "<INPUT_HUB_LOGS_CRN>"
  }
  name = "spoke-b-target"
  target_type = "cloud_logs"
}
```
{: codeblock}

This step creates {{site.data.keyword.atracker_full}} targets pointing to the hub {{site.data.keyword.logs_full_notm}} instance. Routing is not yet enabled.

## Step 4 - Create spoke routes
{: #step-create-spoke-routes}
{: terraform}

Create {{site.data.keyword.atracker_full_notm}} routes in each spoke account. You can route all activity tracker events to the hub or a subset of activity tracker events to the hub. In this example, spoke A will route all activity tracker events to the hub and spoke B will route activity tracker events from specific locations to the hub.

See [IBM Cloud services that generate events that are managed through {{site.data.keyword.atracker_full}}](/docs/atracker?topic=atracker-cloud_services_atracker).

```terraform
# FILE: spoke_a/main.tf

# Previous steps...

resource "ibm_atracker_route" "atracker_route" {
  lifecycle {
    create_before_destroy = true
  }
  name = "spoke-a-route"

  # Route all activity tracker events to the hub.
  rules {
    target_ids = [ ibm_atracker_target.atracker_target.id ]
    locations = [ "*" ]
  }
}
```
{: codeblock}

```terraform
# FILE: spoke_b/main.tf

# Previous steps...

resource "ibm_atracker_route" "atracker_route" {
  lifecycle {
    create_before_destroy = true
  }
  name = "spoke-b-route"

  # Route activity tracker events for a few locations.
  rules {
    target_ids = [ ibm_atracker_target.atracker_target.id ]
    locations = [ "ca-tor", "us-east", "us-south" ]
  }
}
```
{: codeblock}

This step creates the {{site.data.keyword.atracker_full}} routes. Activity tracker events will be routed to the hub {{site.data.keyword.logs_full_notm}} instance.

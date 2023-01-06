---

copyright:
  years: 2019, 2023
lastupdated: "2022-05-16"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}



# Using Terraform to migrate the account configuration
{: #atracker-tf-migration}

Migrate your {{site.data.keyword.atracker_short}} resources from V1 to V2 by using HashiCorp Configuration Language (HCL).
{: shortdesc}



## Prerequisites
{: #atracker-tf-migration-prereqs}

- Ensure that you have the [required access](/docs/atracker?topic=atracker-iam) to create and work with {{site.data.keyword.atracker_short}} resources.
- Learn how to use Terraform to automate the creation, update, and deletion of your {{site.data.keyword.atracker_short}} resources by using HashiCorp Configuration Language (HCL). [Learn more](/docs/atracker?topic=atracker-atracker-tf-config&interface=cli).


## Terraform sample to create V1 resources
{: #atracker-tf-migration-v1}

The following sample shows Terraform code to create configuration resources by using the V1 API:

```terraform
provider "ibm" {
  region = "us-south"
}


resource "ibm_atracker_target" "atracker_target-us-south" {
  name = var.cos_target_name
  target_type = "cloud_object_storage"
  cos_endpoint {
    endpoint = var.cos_endpoint
    target_crn = var.cos_target_crn
    bucket = var.cos_bucket_name
    api_key = var.cos_api_key
  }
}

resource "ibm_atracker_route" "atracker_route_instance-us-south" {
  name = var.route_name
  receive_global_events=true
  rules {
    target_ids = [ibm_atracker_target.atracker_target-us-south.id]
  }
}
data "ibm_atracker_endpoints" "atracker_endpoints" {}
```
{: codeblock}


## How to update the V1 Terraform script to migrate to V2 for 1 region
{: #atracker-tf-migration-update}

When you migrate resources from V1 to V2, make sure that you configure the account settings before migrating your account configuration. You should set the `permitted-target-regions` list with all the regions where you have currently defined targets in your account. You must set the `metadata-region-primary` and the `default-targets` target. You must set a current V1 target as a default target in the settings account configuration.
{: important}

The following code shows how to update the V1 Terraform configuration in 1 region to migrate your resources to a V2 API configuration:


```terraform
provider "ibm" {
  region = "us-south"
}


resource "ibm_atracker_target" "atracker_target-us-south" {
  name = var.cos_target_name
  target_type = "cloud_object_storage"
  cos_endpoint {
    endpoint = var.cos_endpoint
    target_crn = var.cos_target_crn
    bucket = var.cos_bucket_name
    api_key = var.cos_api_key
  }
}

# This is new in version 2.  MUST BE DEFINED before migration
resource "ibm_atracker_settings" "atracker_settings" {
  metadata_region_primary = "us-south"
  default_targets = [ibm_atracker_target.atracker_target-us-south.id]
  permitted_target_regions = ["us-south", "us-east"]
  private_api_endpoint_only = false
}


resource "ibm_atracker_route" "atracker_route_instance-us-south" {
  name = var.route_name
  receive_global_events=true
  rules {
    target_ids = [ibm_atracker_target.atracker_target-us-south.id]
  }
}

data "ibm_atracker_endpoints" "atracker_endpoints" {}
```
{: codeblock}



## How to update the V1 Terraform script to migrate to V2 for 2 regions
{: #atracker-tf-migration-update-2}

When you migrate resources from V1 to V2, make sure that you configure the account settings before migrating your account configuration. You should set the `permitted-target-regions` list with all the regions where you have currently defined targets in your account. You must set the `metadata-region-primary` and the `default-targets` target.
{: important}

The following code shows how to update the V1 Terraform configuration in 2 region2 to migrate your resources to a V2 API configuration. You must set a current V1 target as a default target in the settings account configuration.

You must run the Terraform script in bothe regions.
{: note}


```
provider "ibm" {
  region = "us-south"
}

# Since this migration would be done "inplace" or in the same folder as the current `us-south` infrastructure
# We don't need to run `terraform import -var-file="secret.tfvars" ibm_atracker_target.atracker_target-us-south <TARGET ID>` on this unless the terraform state is lost
resource "ibm_atracker_target" "atracker_target-us-south" {
  name = var.cos_target_name-us-south
  target_type = "cloud_object_storage"
  cos_endpoint {
    endpoint = var.cos_endpoint-us-south
    target_crn = var.cos_target_crn-us-south
    bucket = var.cos_bucket_name-us-south
    api_key = var.cos_api_key-us-south
  }
}

# This is moved/copied over from our examples/migration/v1-us-east project.
# Once migration is complete, we need to tell terraform to import the information for this by running
# `terraform import -var-file="secret.tfvars" ibm_atracker_target.atracker_target-us-east <TARGET ID>`
resource "ibm_atracker_target" "atracker_target-us-east" {
  name = var.cos_target_name-us-east
  target_type = "cloud_object_storage"
  cos_endpoint {
    endpoint = var.cos_endpoint-us-east
    target_crn = var.cos_target_crn-us-east
    bucket = var.cos_bucket_name-us-east
    api_key = var.cos_api_key-us-east
  }
}

resource "ibm_atracker_settings" "atracker_settings" {
  metadata_region_primary = "us-south"
  default_targets = [ibm_atracker_target.atracker_target-us-south.id]
  permitted_target_regions = ["us-south", "us-east"]
  private_api_endpoint_only = false
}


resource "ibm_atracker_route" "atracker_route_instance-us-south" {
  name = var.route_name-us-south
  rules {
    target_ids = [ibm_atracker_target.atracker_target-us-south.id]
    locations = ["global", "us-south"]
  }
}

# This is moved/copied over from our examples/migration/v1-us-east project.
# Once migration is complete, we need to tell terraform to import the information for this by running
# `terraform import -var-file="secret.tfvars" ibm_atracker_route.atracker_route_instance-us-east <ROUTE ID>`
resource "ibm_atracker_route" "atracker_route_instance-us-east" {
  name = var.route_name-us-east
  rules {
    target_ids = [ibm_atracker_target.atracker_target-us-east.id]
    locations = ["us-east"]
  }
}
```
{: codeblock}

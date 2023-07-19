---

copyright:
  years: 2019, 2023
lastupdated: "2023-07-17"

keywords:

subcollection: atracker

content-type: tutorial
services: atracker
account-plan: lite
completion-time: 1h

---

{{site.data.keyword.attribute-definition-list}}


# Configuring a Cloud Object Storage target
{: #getting-started-target-cos}
{: toc-content-type="tutorial"}
{: toc-services="atracker"}
{: toc-completion-time="1h"}


A target is an {{site.data.keyword.cloud_notm}} resource where you can collect auditing events. Use this tutorial to learn how to configure a Cloud Object Storage target in the account.
{: shortdesc}

## Scenarios
{: #getting-started-target-COS-scenarios}

You can define a Cloud Object Storage bucket as a target in any of the following situations:
- You need a solution to monitor the activity in your account that must be Financial Services Validated.
- You want to collect and store auditing events in a Cloud Object Storage bucket. You can have the bucket in the account that generates the events or in a different account from the one that generates auditing events.


## Prerequisites
{: #getting-started-target-COS-prereqs}

- Learn about {{site.data.keyword.atracker_short}}. For more information, see [About](/docs/atracker?topic=atracker-atracker-resources).

- Install the {{site.data.keyword.cloud_notm}} CLI. For more information, see [Installing the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

- Install the latest {{site.data.keyword.atracker_short}} CLI V2 plugin in your local system. See [Installing the {{site.data.keyword.atracker_short}} CLI](/docs/atracker?topic=atracker-atracker-cli-config&interface=cli).

- You need a user ID that is a member, or an owner of, an {{site.data.keyword.cloud_notm}} account. To get an {{site.data.keyword.cloud_notm}} user ID, go to: [Create an account](https://cloud.ibm.com/login){: external}.

- Every user that manages the {{site.data.keyword.atracker_short}} configuration in your account must be assigned an access policy. The policy determines what actions the user can perform. The allowable actions are customized and defined by {{site.data.keyword.atracker_short}} as operations that are allowed to be performed on the service. The actions are then mapped to IAM user roles. [Learn more](/docs/atracker?topic=atracker-iam).

    Your user ID needs **administrator platform permissions** to manage the {{site.data.keyword.atracker_full_notm}} service. Contact the account owner. The account owner can grant another user access to the account for the purposes of managing user access, and managing account resources. [Learn more](/docs/account?topic=account-userroles).


## Configure a COS bucket
{: #getting-started-routing-3-step3}
{: step}


Auditing events that are collected in your account can be stored in {{site.data.keyword.cos_full_notm}} (COS) buckets.

When you configure {{site.data.keyword.atracker_short}}, you must define a target per region. The target defines the COS bucket where auditing events in that region are collected.

Before you create a bucket, consider the following information:
- You can create the bucket in any location.
- You can only configure 1 bucket per target.
- If you have regulatory and compliance requirements, check the locations where you can create a bucket. Then, if performance is critical, consider creating the COS bucket in the same region where the auditing events are generated.

For more information, see [Managing {{site.data.keyword.cos_full_notm}} (COS) buckets](/docs/atracker?topic=atracker-cos).

You can define a bucket in the account that generates the auditing events or in a different account.
{: important}

Choose one of the following options to create a bucket:

| Action             | More info |
|--------------------|-----------|
| Create a bucket through the {{site.data.keyword.cloud_notm}} UI | [Learn more](/docs/atracker?topic=atracker-cos#cos_create_bucket_ui) |
| Create a bucket through the {{site.data.keyword.cloud_notm}} CLI | [Learn more](/docs/cloud-object-storage?topic=cloud-object-storage-cli-plugin-ic-cos-cli#ic-create-bucket) |
| Create a bucket by using cURL | [Learn more](/docs/cloud-object-storage?topic=cloud-object-storage-curl#curl-add-bucket) |
| Create a bucket by using the REST API | [Learn more](/docs/cloud-object-storage?topic=cloud-object-storage-compatibility-api-bucket-operations#compatibility-api-new-bucket) |
| Create a bucket with a different storage class by using the REST API| [Learn more](/docs/cloud-object-storage?topic=cloud-object-storage-compatibility-api-bucket-operations#compatibility-api-storage-class) |
| Create a bucket with Key Protect or Hyper Protect Crypto Services managed encryption keys (SSE-KP) by using the REST API | [Learn more](/docs/cloud-object-storage?topic=cloud-object-storage-compatibility-api-bucket-operations#compatibility-api-key-protect) |
| Create a bucket by using Terraform | [Learn more](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-object-storage-resources) |
{: caption="Table 1. Create bucket requests" caption-side="top"}


## Configure service-to-service authorization
{: #getting-started-routing-step3}
{: step}

Configure service-to-service authorization to your COS bucket so you do not need to pass an API key when writing your encrypted data to the COS bucket.

The following steps show how to define service to service authorization when the COS bucket is available in a different account from where auditing events are generated:

You must complete these steps in the account where the COS bucket is available.
{: important}

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external} as the account owner that will be configuring {{site.data.keyword.atracker_full_notm}} targets.

	After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} dashboard opens.

2. Click **Manage** &gt; **Access (IAM)**.  **Manage access and users** is displayed.

3. Click **Authorizations**.

4. Click **Create**.

5. Select the **Source account**. Choose **Other account**. Then, enter the account ID for the source service. An account ID is a 32 character, unique account identifier.

6. For **Source service** select *Activity Tracker Event Routing* and for **How do you want to scope the access?** select *All resources*.

7. For **Target service** select *Cloud Object Storage* for **How do you want to scope the access?** select *Resources based on selected attributes*.

8. Select **Service instance** and **string equals** the name of your COS instance.

9. For **Service access** select **Object writer**.

10. Click **Authorize**.  Your new service-to-service authorization will be listed in the **Manage authorizations** view.

Alternately, you can create the service-to-service policy by running the following command:

```text
ibmcloud iam authorization-policy-create atracker cloud-object-storage "Object Writer"
```
{: pre}

You will only be able to authorize to the {{site.data.keyword.cos_full_notm}} instance using the UI. If you want to limit authorization to a specific {{site.data.keyword.cos_full_notm}} bucket, you need to configure authorization using the [API](/docs/atracker?topic=atracker-target_v2_cos&interface=cli#cos_s2s_api).
{: important}


## Create a target
{: #getting-started-routing-step5}
{: step}

After you create the bucket and configure the authorizartion method, you can configure a target. The target defines the COS bucket where auditing events will be routed.

The region identifies the location from which the writing to the bucket will occur.  If you want events from all regions to flow to this one COS bucket, then you only require a single target to be defined.

To [create a target](/docs/atracker?topic=atracker-target_v2_cos&interface=cli#target-create-cli-cos), run the following command:

```text
ibmcloud atracker target create --name <TARGET_NAME> --type cloud-object-storage --endpoint <COS_ENDPOINT> --target-crn <COS_TARGET_CRN> --bucket <BUCKET> --region <REGION> --service-to-service-enabled true
```
{: pre}

Where

`--region <REGION>`
:   Name of the region that will process the events, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--name <TARGET_NAME>`
:   The name to be given to the target.

`--endpoint <COS_ENDPOINT>`
:   The {{site.data.keyword.cos_full_notm}} endpoint to be associated with the {{site.data.keyword.cos_full_notm}} bucket.

`--bucket <BUCKET>`
:    The name of the {{site.data.keyword.cos_full_notm}} bucket to be associated with the target.

`--target-crn <COS_TARGET_CRN>`
:   The CRN of the {{site.data.keyword.cos_full_notm}} instance.

`--service-to-service-enabled`
:   Indicates if [service-to-service authorization](#getting-started-routing-step3) has been enabled for the bucket.  Specify `TRUE` if service-to-service authorization is enabled and `FALSE` if service-to-service authorization is not enable.

For example, to create a target in the US-South region, you can run the following command:

```text
ibmcloud atracker target create --name  "My target" --type cloud-object-storage --endpoint "s3.private.us-south.cloud-object-storage.appdomain.cloud" --target-crn "crn:v1:bluemix:public:cloud-object-storage:global:a/<AccountID>:<COSinstanceID>::" --bucket "activity-tracking-bucket-us-south" --region "us-south" --service-to-service-enabled true
```
{: pre}

To see the target definition in a region, see [Getting information about a target using the CLI](/docs/atracker?topic=atracker-target_v2_cos&interface=cli#target-get-cli-cos).

When your target is created the target ID is returned. Make note of the target ID. You will need the target ID to configure a rule that routes events to the target in the account.
{: note}

## Next
{: #getting-started-target-cos-next}
{: step}

Define 1 or more routes in the account. For more information, see [Configuring a route](/docs/atracker?topic=atracker-route_v2&interface=cli#route-create-cli).

When you configure a route, you associate a target with the route and define which type of auditing events are collected. The route defines the rules that determine where auditing events are collected in your account. For example, you can define a route that collects auditing events from 2 different regions, and also collects global events.


You can collect [global events](/docs/atracker?topic=atracker-event_types#event_types_global) and [location-based events](/docs/atracker?topic=atracker-event_types#event_types_location).
- Global events report on activity in your account that relate to data and resources that are generally synchronized across all regions.
- Location-based events report on activity in your account that is generated by IBM Cloud services that are hosted within an IBM data center location, such as US-South or US-East.

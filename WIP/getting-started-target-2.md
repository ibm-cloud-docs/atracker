---

copyright:
  years: 2019, 2023
lastupdated: "2022-05-23"

keywords:

subcollection: atracker

content-type: tutorial
services: activity-tracker
account-plan: lite
completion-time: 1h

---

{{site.data.keyword.attribute-definition-list}}


# Configuring a Cloud Object Storage target in the same account that generates the auditing events by using the CLI (WIP)
{: #getting-started-target-2}
{: toc-content-type="tutorial"}
{: toc-services="activity-tracker"}
{: toc-completion-time="1h"}

A target is an {{site.data.keyword.cloud_notm}} resource where you can collect auditing events.
{: shortdesc}

Use this tutorial to learn how to configure an {{site.data.keyword.cos_full_notm}} bucket as a target by using the {{site.data.keyword.atracker_short}} V2 CLI and configuring service-to-service authorization between COS and {{site.data.keyword.atracker_short}}. The bucket is defined in the same account that generates the auditing events.

This information applies only if you use {{site.data.keyword.atracker_full}}.
{: important}

## Scenarios
{: #getting-started-target-2-scenarios}

You can define a Cloud Object Storage bucket as a target in any of the following situations:
- You need a solution to monitor the activity in your account that must be Financial Services Validated.
- You want to collect and store auditing events in a Cloud Object Storage bucket that is defined in the same account that also generates the auditing events.

![Diagram showing a decision flowchart to help you understand if a Cloud Object Storage bucket, or an {{site.data.keyword.atracker_full}} hosted event search (logdna) target best meets your requirements.](/images/getting-started-flow-yesFS-yesinacct.svg "Flowchart showing which target type is best for your requirements"){: caption="Figure 1. Which target type is best for your requirements" caption-side="bottom"}



## Prerequisites
{: #getting-started-target-2-prereqs}

- You need a user ID that is a member, or an owner of, an {{site.data.keyword.cloud_notm}} account. To get an {{site.data.keyword.cloud_notm}} user ID, go to: [Create an account](https://cloud.ibm.com/login){: external}.

- Install the {{site.data.keyword.cloud_notm}} CLI. For more information, see [Installing the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

- Install the latest {{site.data.keyword.atracker_short}} CLI V2 plugin in your local system. See [Installing the {{site.data.keyword.atracker_short}} CLI](/docs/atracker?topic=atracker-atracker-cli-config&interface=cli).

- Your user ID needs **administrator platform permissions** to manage the {{site.data.keyword.at_full_notm}} service. Contact the account owner. The account owner can grant another user access to the account for the purposes of managing user access, and managing account resources. [Learn more](/docs/account?topic=account-userroles).


## Manage the type of endpoints that are allowed to configure {{site.data.keyword.atracker_short}} resources
{: #getting-started-target-2-step1}
{: step}

You can use the {{site.data.keyword.atracker_short}} CLI or the {{site.data.keyword.atracker_short}} REST API to define the type of endpoints that are allowed to configure {{site.data.keyword.atracker_short}} resources in the account.

If you plan to use public endpoints to manage {{site.data.keyword.atracker_short}} resources in your account, this step is not required.
{: note}


To disable the use of public endpoints to configure {{site.data.keyword.atracker_short}} resources, see [Enforcing private endpoints to configure {{site.data.keyword.atracker_short}} resources](/docs/atracker?topic=atracker-getting-started-mng-endpoints).


## Check your IAM permissions to work with {{site.data.keyword.atracker_short}}
{: #getting-started-target-2-step2}
{: step}

**Every user that manages {{site.data.keyword.atracker_short}} configurations in your account must be assigned an access policy.** The policy determines what actions the user can perform. The allowable actions are customized and defined by {{site.data.keyword.atracker_short}} as operations that are allowed to be performed on the service. The actions are then mapped to IAM user roles. [Learn more](/docs/atracker?topic=atracker-iam).

Your user ID needs **account management permissions** to manage {{site.data.keyword.atracker_short}} configurations in the account.

Users must have the following [IAM roles](/docs/account?topic=account-assign-access-resources) to manage the {{site.data.keyword.atracker_short}} account settings.

| Role                      | Minimum scope  | Minimum required roles | Action         |
| ------------------------- | -------------- | ---------------------- | -------------- |
| `atracker.setting.get`    | Account        | `Administrator`  \n `Editor`  \n `Viewer`  \n `Operator` | Get setting information |
| `atracker.setting.update` | Account        | `Administrator`| Update settings |
{: caption="Table 1. Required IAM roles to manage the {{site.data.keyword.atracker_short}} account settings." caption-side="top"}

Users must have the following [{{site.data.keyword.atracker_full}} IAM roles](/docs/account?topic=account-assign-access-resources) to work with targets. Users with regional IAM scope will be limited to access targets in their authorized region.

| Role | Minimum scope | Minimum required roles | Action
| -------------- | -------------- | -------- | -------------- |
| `atracker.target.read` | Region | `Administrator`  \n `Editor`  \n `Viewer`  \n `Operator` | Read (view) information about a target |
| `atracker.target.create` | Region | `Administrator`  \n `Editor` | Create a target |
| `atracker.target.update` | Region | `Administrator`  \n `Editor` | Update a target |
| `atracker.target.delete` | Region | `Administrator`  \n `Editor` | Delete a target |
| `atracker.target.list` | Account | `Administrator`  \n `Editor`  \n `Viewer`  \n `Operator` | List all targets |
{: caption="Table 2. Required IAM roles}

Choose one of the following options to grant your user permissions:
- [Using the console to assign access](/docs/account?topic=account-account-services&interface=ui#api-acct-mgmt)
- [Using the CLI to assign access](/docs/account?topic=account-account-services&interface=cli#api-acct-mgmt)
- [Using the API to assign access](/docs/account?topic=account-account-services&interface=api#api-acct-mgmt). Use the **serviceName** `atracker`.


## Configure a COS bucket
{: #getting-started-target-2-step3}
{: step}

Auditing events that are collected in your account can be stored in 1 or more {{site.data.keyword.cos_full_notm}} (COS) buckets.

When you configure {{site.data.keyword.atracker_short}}, you must define at least 1 target in a region. The target defines the COS bucket where you plan to collect the auditing events that are generated in the account.

Before you create a bucket, consider the following information:
- You can create the bucket in any location.
- You can only configure 1 bucket per target.
- You can share a bucket to collect [location-based auditing events](/docs/atracker?topic=atracker-event_types#event_types_location) from multiple regions. Notice that when you share a bucket across multiple regions, you might be affected by latency and network issues between regions.
- If you have regulatory and compliance requirements, check the locations where you can create a bucket. Then, if performance is critical, consider creating the COS bucket in the same region where the auditing events are generated.

For more information, see [Managing {{site.data.keyword.cos_full_notm}} (COS) buckets](/docs/atracker?topic=atracker-cos).

Wherever possible, use a dedicated bucket per region.
{: important}

Choose one of the following options to create a bucket:

| Action             | More info |
|--------------------|-----------|
| Create a bucket through the {{site.data.keyword.cloud_notm}} UI | [Learn more](/docs/atracker?topic=atracker-cos#cos_create_bucket_ui) |
| Create a bucket through the {{site.data.keyword.cloud_notm}} CLI | [Learn more](/docs/cloud-object-storage-cli-plugin?topic=cloud-object-storage-cli-plugin-ic-cos-cli#ic-create-bucket) |
| Create a bucket by using cURL | [Learn more](/docs/cloud-object-storage?topic=cloud-object-storage-curl#curl-add-bucket) |
| Create a bucket by using the REST API | [Learn more](/docs/cloud-object-storage?topic=cloud-object-storage-compatibility-api-bucket-operations#compatibility-api-new-bucket) |
| Create a bucket with a different storage class by using the REST API| [Learn more](/docs/cloud-object-storage?topic=cloud-object-storage-compatibility-api-bucket-operations#compatibility-api-storage-class) |
| Create a bucket with Key Protect or Hyper Protect Crypto Services managed encryption keys (SSE-KP) by using the REST API | [Learn more](/docs/cloud-object-storage?topic=cloud-object-storage-compatibility-api-bucket-operations#compatibility-api-key-protect) |
| Create a bucket by using Terraform | [Learn more](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-template#storage-templates) |
{: caption="Table 1. Create bucket requests" caption-side="top"}


## Configure service-to-service authorization
{: #getting-started-target-2-step4}
{: step}

You can configure service-to-service authorization to your COS bucket so you do not need to pass an API key to the {{site.data.keyword.atracker_short}} service when writing your encrypted data to the COS bucket.

### Configuring service-to-service authorization by using the UI
{: #getting-started-target-2-step4-1}

Do the following to configure a service-to-service authorization using the {{site.data.keyword.cloud_notm}} UI.

The following steps show how to define service to service authorization when the COS bucket is available in a different account from where auditing events are generated:

You must complete these steps in the account where the COS bucket is available.
{: important}

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external} as the account owner that will be configuring {{site.data.keyword.atracker_full_notm}} targets.

	After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} dashboard opens.

2. Click **Manage** &gt; **Access (IAM)**.  **Manage access and users** is displayed.

3. Click **Authorizations**.

4. Click **Create**.

5. Select the **Source account**. Choose **This account**.

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

You will only be able to authorize to the {{site.data.keyword.cos_full_notm}} instance using the UI. If you want to limit authorization to a specific {{site.data.keyword.cos_full_notm}} bucket, you need to configure authorization using the [API](/docs/atracker?topic=atracker-target_v2_cos&interface=api#target_v2_cos_s2s_api).
{: important}



### Configuring service-to-service authorization using the API
{: #getting-started-target-2-step4-2}

Do the following to configure a service-to-service authorization using the {{site.data.keyword.cloud_notm}} API.

1. [Log in to your {{site.data.keyword.cloud_notm}} account](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login) as the account owner that will be configuring {{site.data.keyword.atracker_full_notm}} targets.

2. Create an `authorization_policy_resource.json` file defining your service-to-service authorization.

   ```json
   {
       "type": "authorization",
       "subjects": [
           {
               "attributes": [
                 {
                      "name": "accountId",
                      "value": "CUSTOMER_ACCOUNT_ID"
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
               "role_id": "crn:v1:bluemix:public:iam::::serviceRole:ObjectWriter"
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
                       "value": "cloud-object-storage"
                   },
                   {
                       "name": "serviceInstance",
                       "value": "COS_SERVICE_INSTANCE"
                   }
               ]
           }
       ]
   }
   ```
   {: codeblock}

   Where:

   `CUSTOMER_ACCOUNT_ID` is the account GUID for the account that will be configuring targets.  This can be found by using the [`ibmcloud account list`](/docs/cli?topic=cli-ibmcloud_commands_account#ibmcloud_account_list) command.

   `COS_SERVICE_INSTANCE` is the [bucket instance CRN](/docs/atracker?topic=atracker-cos#cos_bucket_details) of the COS instance to be authorized.

3. Run the following command to configure your service-to-service authorization:

   ```sh
   curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header "Authorization: Bearer $ACCESS_TOKEN" --header "X-Auth-Refresh-Token: $REFRESH_TOKEN" -d @authorization_policy_resource.json "https://iam.cloud.ibm.com/v1/policies"
   ```
   {: pre}


## Define a target
{: #getting-started-target-2-step5}
{: step}

This tutorial uses the {{site.data.keyword.atracker_full}} v2 API.
{: important}

After you create the bucket, you can configure a target in a region. The target defines the COS bucket where auditing events in that region are collected.

Complete the following steps to create a target in the US-South region in your account:

1. Get an access token.

    You need an IAM access token to authenticate in {{site.data.keyword.cloud_notm}}.

    To generate an IAM access token, run the following command:

    ```text
    export ACCESS_TOKEN=`ibmcloud iam oauth-tokens | grep IAM | cut -d \: -f 2 | sed 's/^ *//'`
    ```
    {: pre}

    The access token is only valid for 1 hour.

2. [Create a target](/docs/atracker?topic=atracker-target_v2). Run the following cURL command:

    ```shell
    curl -X POST  <ENDPOINT>/api/v1/targets   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"   -d '{
        "name": "TARGET_NAME",
        "target_type": "TARGET_TYPE",
        "cos_endpoint": {
          "endpoint": "PRIVATE_COS_ENDPOINT",
          "target_crn": "COS_CRN",
          "bucket": "BUCKET_NAME",
          "api_key": "API_KEY"
        }
      }'
    ```
    {: codeblock}

    Where

    - `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).

    - `TARGET_NAME` is the name of the target. The maximum length of the name is 256 characters.

    - `TARGET_TYPE` is the type of the target. Set this field to `cloud-object-storage`.

    - `cos_endpoint` includes information about the target. For more information on how to get the bucket details, see [Getting the bucket configuration details](/docs/atracker?topic=atracker-cos#cos_bucket_details).

| Field | Description |
|-------|-------------|
| `endpoint` | Indicates the {{site.data.keyword.atracker_short}} where to look for this bucket. Use the private endpoint. |
| `target_crn` | Indicates the [CRN](/docs/account?topic=account-crn) of the COS instance where you provisioned the bucket. |
| `bucket` | Indicates the name of the bucket. |
| `api_key`| Contains the API key that has permissions to upload objects into the bucket. |
{: caption="Table 2. Target endpoint fields" caption-side="top"}

For example, to create a target in the US-South region, you can run the following cURL command:

```shell
curl -X POST   https://private.us-south.atracker.cloud.ibm.com/api/v1/targets   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"   -d '{
"name": "My target",
"target_type": "cloud_object_storage",
"cos_endpoint": {
  "endpoint": "s3.private.us-south.cloud-object-storage.appdomain.cloud",
  "target_crn": "crn:v1:bluemix:public:cloud-object-storage:global:a/<AccountID>:<COSinstanceID>::",
  "bucket": "activity-tracking-bucket-us-south",
  "api_key": "xxxxxxxxxxxxx"
  }
}'
```
{: codeblock}

To get the target definition in a region, see [Viewing a target](/docs/atracker?topic=atracker-target#target-view).



## Next
{: #getting-started-target-2-step6}
{: step}

Define a route per region where you operate. For more information, see [Configuring a route](/docs/atracker?topic=atracker-route_v2&interface=cli).

When you configure a route, you associate a target with the route and define which type of auditing events are collected. The route defines the rules that determine where auditing events are collected in your account. For example, you can define a route that collects auditing events from 2 different regions, and also collects global events.


You can collect [global events](/docs/atracker?topic=atracker-event_types#event_types_global) and [location-based events](/docs/atracker?topic=atracker-event_types#event_types_location).
- Global events report on activity in your account that relate to data and resources that are generally synchronized across all regions.
- Location-based events report on activity in your account that is generated by IBM Cloud services that are hosted within an IBM data centre location, like US-South or US-East.

Per account, you can choose the region where global events are collected.

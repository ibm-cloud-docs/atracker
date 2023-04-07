---

copyright:
  years: 2019, 2023
lastupdated: "2022-05-23"

keywords:

subcollection: atracker

content-type: tutorial
services: atracker
account-plan: lite
completion-time: 1h

---

{{site.data.keyword.attribute-definition-list}}


# Configuring a logdna target
{: #getting-started-target-logdna}
{: toc-content-type="tutorial"}
{: toc-services="atracker"}
{: toc-completion-time="1h"}

A target is an {{site.data.keyword.cloud_notm}} resource where you can collect auditing events. Use this tutorial to learn how to configure an {{site.data.keyword.atracker_short}} hosted event search target in the account.
{: shortdesc}

This tutorial uses the {{site.data.keyword.atracker_full}} v2 API.
{: important}

## Scenarios
{: #getting-started-target-LOGDNA-scenarios}

You can define an {{site.data.keyword.at_short}} event search target in any of the following situations:
- You need a solution to monitor the activity in your account through the UI.
- You want to collect and store auditing events in an {{site.data.keyword.at_short}} hosted event search instance. You also want to choose the instance or instances where to collect and manage those events.


## Prerequisites
{: #getting-started-target-LOGDNA-prereqs}

- You need a user ID that is a member, or an owner of, an {{site.data.keyword.cloud_notm}} account. To get an {{site.data.keyword.cloud_notm}} user ID, go to: [Create an account](https://cloud.ibm.com/login){: external}.

- Your user ID needs **administrator platform permissions** to manage the {{site.data.keyword.at_full_notm}} service. Contact the account owner. The account owner can grant another user access to the account for the purposes of managing user access, and managing account resources. [Learn more](/docs/account?topic=account-userroles).

- Learn about {{site.data.keyword.atracker_short}}. For more information, see [About](/docs/atracker?topic=atracker-atracker-resources).

- Install the {{site.data.keyword.cloud_notm}} CLI. For more information, see [Installing the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

- Install the latest {{site.data.keyword.atracker_short}} CLI V2 plugin in your local system. See [Installing the {{site.data.keyword.atracker_short}} CLI](/docs/atracker?topic=atracker-atracker-cli-config&interface=cli).



## Manage the type of endpoints
{: #getting-started-target-LOGDNA-step1}
{: step}

Manage the type of endpoints that are allowed to configure {{site.data.keyword.atracker_short}} resources. You can use the {{site.data.keyword.atracker_short}} CLI, the {{site.data.keyword.atracker_short}} REST API, or a terraform script to define the type of endpoints that are allowed to configure {{site.data.keyword.atracker_short}} resources in the account.

If you plan to use public endpoints to manage {{site.data.keyword.atracker_short}} resources in your account, this step is not required.
{: note}


To disable the use of public endpoints to configure {{site.data.keyword.atracker_short}} resources, see [Enforcing private endpoints to configure {{site.data.keyword.atracker_short}} resources](/docs/atracker?topic=atracker-getting-started-mng-endpoints).


## Check your IAM permissions
{: #getting-started-target-LOGDNA-step2}
{: step}

Check your IAM permissions to work with {{site.data.keyword.atracker_short}}.

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
{: caption="Table 2. Required IAM roles"}

Choose one of the following options to grant your user permissions:
- [Using the console to assign access](/docs/account?topic=account-account-services#console-acct-mgmt)
- [Using the CLI to assign access](/docs/account?topic=account-account-services#using-the-cli-to-assign-access)
- [Using the API to assign access](/docs/account?topic=account-account-services#api-acct-mgmt). Use the **serviceName** `atracker`.


## Provision an {{site.data.keyword.at_short}} hosted event search instance
{: #getting-started-target-LOGDNA-step3}
{: step}

Complete the following steps:

1. Provision an {{site.data.keyword.at_short}} event search instance. See [Provisioning an instance](/docs/activity-tracker?topic=activity-tracker-provision).
2. [Copy the ingestion key](/docs/activity-tracker?topic=activity-tracker-ingestion_key).


## Define a target
{: #getting-started-target-LOGDNA-step4}
{: step}

After you create the instance, you can configure a target in a region. The target defines where auditing events in that region are collected.

Complete the following steps to create a target in the US-South region in your account:

1. Get an access token.

    You need an IAM access token to authenticate in {{site.data.keyword.cloud_notm}}.

    To generate an IAM access token, run the following command:

    ```text
    export ACCESS_TOKEN=`ibmcloud iam oauth-tokens | grep IAM | cut -d \: -f 2 | sed 's/^ *//'`
    ```
    {: pre}

    The access token is only valid for 1 hour.

2. [Create a target](/docs/atracker?topic=atracker-target#target-create). Run the following cURL command:

    ```shell
    curl -X POST  <ENDPOINT>/api/v1/targets   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"   -d '{
        "name": "TARGET_NAME",
        "target_type": "TARGET_TYPE",
        "logdna_endpoint": {
          "target_crn": "INSTANCE_CRN",
          "ingestion_key": "API_KEY"
        }
      }'
    ```
    {: codeblock}

    Where

    - `TARGET_NAME` is the name of the target. The maximum length of the name is 256 characters.

    - `TARGET_TYPE` is the type of the target. Set this field to `logdna`.


| Field | Description |
|-------|-------------|
| `target_crn` | Indicates the [CRN](/docs/account?topic=account-crn) of the {{site.data.keyword.atracker_short}} instance. |
| `ingestion_key`| Contains the API key that has permissions to send events to an {{site.data.keyword.atracker_short}} instance. |
{: caption="Table 2. Target endpoint fields" caption-side="top"}

For example, to create a target in the US-South region, you can run the following cURL command:

```shell
curl -X POST   https://private.us-south.atracker.cloud.ibm.com/api/v1/targets   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"   -d '{
"name": "My target",
"target_type": "logdna",
"logdna_endpoint": {
  "target_crn": "crn:v1:bluemix:public:logdnaat:global:a/<AccountID>:<COSinstanceID>::",
  "ingestion_key": "xxxxxxxxxxxxx"
  }
}'
```
{: codeblock}

To get the target definition in a region, see [Viewing a target](/docs/atracker?topic=atracker-target#target-view).



## Next
{: #getting-started-target-LOGDNA-step5}
{: step}

Define 1 or more routes in the account. For more information, see [Configuring a route](/docs/atracker?topic=atracker-route_v2&interface=cli#route-create-cli).

When you configure a route, you associate a target with the route and define which type of auditing events are collected. The route defines the rules that determine where auditing events are collected in your account. For example, you can define a route that collects auditing events from 2 different regions, and also collects global events.


You can collect [global events](/docs/atracker?topic=atracker-event_types#event_types_global) and [location-based events](/docs/atracker?topic=atracker-event_types#event_types_location).
- Global events report on activity in your account that relate to data and resources that are generally synchronized across all regions.
- Location-based events report on activity in your account that is generated by IBM Cloud services that are hosted within an IBM data center location, such as US-South or US-East.

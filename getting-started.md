---

copyright:
  years:  2021, 2025
lastupdated: "2025-04-10"

keywords: Observability

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Getting started with {{site.data.keyword.atracker_full_notm}}
{: #getting-started}

Use {{site.data.keyword.atracker_full}} to configure how to route auditing events, both [global](/docs/atracker?topic=atracker-event_types#event_types_global) and [location-based](/docs/atracker?topic=atracker-event_types#event_types_location) event data, in your {{site.data.keyword.cloud_notm}}. Auditing events are critical data for security operations and a key element for meeting compliance requirements. Control of the storage location is critical to building enterprise-grade solutions on the {{site.data.keyword.cloud_notm}}.
{: shortdesc}


You can use {{site.data.keyword.atracker_short}}, a platform service, to manage auditing events at the account-level by configuring targets and routes that define where auditing data is routed. {{site.data.keyword.atracker_short}} can route events that are generated in [supported regions](/docs/atracker?topic=atracker-regions). For more information about {{site.data.keyword.atracker_full_notm}}, see [About {{site.data.keyword.atracker_short}}](/docs/atracker?topic=atracker-about).


## Prerequisites
{: #getting-started-prereqs}

- [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

- [Install the {{site.data.keyword.atracker_full_notm}} CLI](/docs/atracker?topic=atracker-atracker-cli-config).

- You must have a user ID with permissions to manage {{site.data.keyword.atracker_full_notm}}. For more information about IAM roles and how to assign them, see [Managing access with IAM](/docs/atracker?topic=atracker-iam) and [IAM roles](/docs/account?topic=account-assign-access-resources).



## Step 1. Configure the account global settings
{: #getting-started-step1}

When you configure {{site.data.keyword.atracker_short}} in your account, you can configure the account settings such as the metadata location, type of endpoints allowed to manage the configuration, locations where targets can be defined, and default targets for collecting auditing events in regions that you have not explicitly configured. For more information, see [Configuring {{site.data.keyword.atracker_short}} account settings](/docs/atracker?topic=atracker-settings&interface=cli).

Set these settings to define where and how auditing events are collected, routed, and managed in your account. For example, to configure the primary metadata location that defines the region where all your {{site.data.keyword.atracker_short}} resource definitions are stored, run the following command:

```pre
ibmcloud atracker setting update --metadata-region-primary <REGION>
```
{: codeblock}

Where `<REGION>` you can set the region to any of the supported locations where {{site.data.keyword.atracker_short}} is available.

When you set the metadata location, check any compliance or industry regulations that apply to data location.
{: tip}

## Step 2. Configure 1 target
{: #getting-started-step2}

A target defines where auditing events are collected. For more information about targets, see [Understanding how targets work in your account](/docs/atracker?topic=atracker-target_v2&interface=cli#target_v2_behavior).

Choose 1 of the following options to configure a target in your account:
- [Configuring a Cloud Object Storage target](/docs/atracker?topic=atracker-getting-started-target-cos).
- [Configuring an {{site.data.keyword.logs_full_notm}} target](/docs/atracker?topic=atracker-target_v2_icl).
- [Configuring an {{site.data.keyword.messagehub}} target](/docs/atracker?topic=atracker-getting-started-target-event-streams).



The rest of the instructions assume that you configure a `cloud-object-storage` target.


## Step 3. Configure 1 route
{: #getting-started-step3}

A route defines the rules that indicate where auditing events that are generated in an account are routed. Routes are global under an account and are evaluated in all regions where {{site.data.keyword.atracker_short}} is deployed. For more information, see [Understanding how routes work in your account](/docs/atracker?topic=atracker-route_v2&interface=cli#route_behaviour).

In this step, you will configure a route to redirect regional and global events to a target bucket.

Run the following command to create the route:

```text
ibmcloud atracker route create --name <ROUTE_NAME> --rules
```
{: pre}

Where

`--name <ROUTE_NAME>`
:   The name to be given to the route.

`--rules <ROUTING_RULES>`
:   A JSON formatted rule definition enclosed in single quotes. For example:

    ```json
    --rules '[{"locations":["global"],"target_ids":["11111111-1111-1111-1111-111111111111"]},{"locations":["us-south","us-east"],"target_ids":["22222222-2222-2222-2222-222222222222","33333333-3333-3333-3333-333333333333"]}]'
    ```
    {: codeblock}

After you configure a route, it might take up to 1 hour for the configuration to be enabled.
{: note}

For example, to create a route to send auditing events to a target that you created in the previous step, run the following command.

```text
ibmcloud atracker route create --name "my-route" --rules '[{"locations":["global","eu-de"],"target_ids":["TARGETID"]}]'
```
{: pre}

Where `TARGETID` is the ID of the target that you created in the previous step.


## Step 4. Verify collection of events
{: #getting-started-step4}


After the target and the route is configured, you must verify that auditing events are available in your bucket.

For example, auditing events are stored in log files in the bucket.

Log files are structured and named as follows:

```text
<REGION>/<DATE>T<HOUR>/2021-02-23T15:38+05.log
```
{: codeblock}

Where

- `<REGION>` defines the region from where auditing events are collected. For example, valid values are `us-south` and `us-east`.
- `<DATE>` defines the date when auditing events are collected. The format is `YYYY-MM-DD`.
- `<HOUR>` defines the hour of the day. The value is set by using a 24-hour clock.
- `<FILENAME>` defines a timestamp. The format is `YYYY-MM-DDTHH:MM+SS`.

Each log file includes auditing events that have an `eventTime` that maps the filename timestamp. `eventTime` indicates when the auditing event was generated.

For example, a sample log file that collects auditing events in the US-South region looks as follows:

```text
us-south/2021-02-23T15/2021-02-23T15:38+05.log
```
{: screen}


You can choose any of the following methods to list objects in a bucket:
- [List objects in a given bucket by using the CLI](/docs/cloud-object-storage-cli-plugin?topic=cloud-object-storage-cli-plugin-ic-cos-cli#ic-list-objects).
- [List objects in a given bucket by using the API](/docs/cloud-object-storage?topic=cloud-object-storage-compatibility-api-bucket-operations#compatibility-api-list-objects-v2)
- [List objects in a given bucket through the {{site.data.keyword.cloud_notm}} UI](/docs/atracker?topic=atracker-cos#cos_bucket_list_objects_ui).





## Next
{: #getting-started-next}

Plan your account configuration. For more information, see [Planning the account configuration](/docs/atracker?topic=atracker-planning).

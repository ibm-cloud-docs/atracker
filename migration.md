---

copyright:
  years: 2019, 2022
lastupdated: "2022-05-24"

keywords: 

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Migrating the {{site.data.keyword.atracker_short}} account configuration from V1 to V2
{: #migration}

The {{site.data.keyword.atracker_full}} feature has been enhanced. A new version (V2) is now available. To use the new V2 features and configurations, your existing {{site.data.keyword.atracker_short}} V1 account configuration must be migrated to an {{site.data.keyword.atracker_short}} V2 account configuration.
{: shortdesc}


## Why do you need to migrate?
{: #migration-why}

In the {{site.data.keyword.atracker_short}} V1 configuration, each region is managed separately. In the {{site.data.keyword.atracker_short}} V2 configuration, all of the account configuration metadata is managed in a user-specified location. As a result, when you migrate to V2, all V1 regions are migrated at the same time so that when the migration is complete, the account as a whole will be migrated to the V2 configuration.

Once you have migrated from your existing V1 configuration to V2, you must use the V2 APIs.  After migration you will no longer be able to use the V1 APIs.
{: important}


## Planning the migration
{: #migration-ov}

When you migrate the {{site.data.keyword.atracker_short}} account configuration from V1 to V2 in your account, you must plan and decide how the account's {{site.data.keyword.atracker_short}} configuration is managed and stored:

1. Decide the location in your {{site.data.keyword.cloud_notm}} account where the {{site.data.keyword.atracker_short}} account configuration metadata is stored. 

    You can choose any of the supported locations where {{site.data.keyword.atracker_short}} is available. For more information, see [Locations](/docs/atracker?topic=atracker-regions&interface=cli).

    Take into account any corporate or industry compliance requirements such as Financial Services Validated locations, or EU-managed regions.

2. Decide whether public endpoints, private endpoints, or both are allowed to manage the {{site.data.keyword.atracker_short}} account configuration.

3. Define the locations where an account administrator can define targets to collect auditing events.

    You can choose any of the supported locations where {{site.data.keyword.atracker_short}} is available. For more information, see [Locations](/docs/atracker?topic=atracker-regions&interface=cli).

    Take into account any corporate or industry compliance requirements such as Financial Services Validated locations, or EU-managed regions.

4. Define 1 or more default targets in the account that will collect auditing events from supported {{site.data.keyword.atracker_short}} locations where you have not configured how you want to collect the auditing data.

    If you define more than 1 target, all default targets get a copy of an auditing event that does not have a clearly defined routing rule to indicate where to collect it in the account. You can define up to 2 default targets per account.
    {: note}

## IAM permissions
{: #migration-iam}

Users must have the following [IAM roles](/docs/account?topic=account-assign-access-resources) to manage the {{site.data.keyword.atracker_short}} account settings.

| Role                      | Minimum scope  | Minimum required roles | Action         |
| ------------------------- | -------------- | ---------------------- | -------------- |
| `atracker.setting.get`    | Account        | `Administrator`  \n `Editor`  \n `Viewer`  \n `Operator` | Get setting information |
| `atracker.setting.update` | Account        | `Administrator`| Update settings |
{: caption="Table 1. Required IAM roles to manage the {{site.data.keyword.atracker_short}} account settings." caption-side="top"}

Users must have the following [IAM roles](/docs/account?topic=account-assign-access-resources) to migrate the account's {{site.data.keyword.atracker_short}} configuration. 

| Role                      | Minimum scope  | Minimum required roles | Action         |
| ------------------------- | -------------- | ---------------------- | -------------- |
| `atracker.migration.post` | Account        | `Administrator`        | Start the migration of {{site.data.keyword.atracker_short}} resources in the account. | 
| `atracker.migration.get`  | Account        | `Administrator`  \n `Editor`  \n `Viewer`  \n `Operator` | Get the status of {{site.data.keyword.atracker_short}} resources that are being migrated from V1 to V2. |
| `atracker.migration.delete`  | Account        | IBM INTERNAL USE ONLY | IBM INTERNAL USE ONLY |
{: caption="Table 2. Required IAM roles to migrate the {{site.data.keyword.atracker_short}} account configuration." caption-side="top"}

## Migration steps
{: #migration-steps}

Use the following diagrams to follow the steps to migrate the {{site.data.keyword.atracker_short}} account configuration from V1 to V2 using the CLI or API:

| CLI | API | 
| -------------- | -------------- |
| [![Step 1: Configure and initialize the Activity Tracker CLI V2 in your local system](/images/mig_s1.svg)](/docs/atracker?topic=atracker-migration&interface=cli#migration-step1) |[![Step 1: Configure and initialize the Activity Tracker CLI V2 in your local system](/images/mig_s1.svg)](/docs/atracker?topic=atracker-migration&interface=api#migration-step1-api) | 
| [![Step 2: Check the Activity Tracker resources that must be migrated in the account](/images/mig_s2.svg)](/docs/atracker?topic=atracker-migration&interface=cli#migration-step2) | [![Step 2: Check the Activity Tracker resources that must be migrated in the account](/images/mig_s2.svg)](/docs/atracker?topic=atracker-migration&interface=api#migration-step2-api) |
| [![Step 3: Configure the Activity Tracker account settings](/images/mig_s3.svg)](/docs/atracker?topic=atracker-migration&interface=cli#migration-step3) | [![Step 3: Configure the Activity Tracker account settings](/images/mig_s3.svg)](/docs/atracker?topic=atracker-migration&interface=api#migration-step3-api) |
| [![Step 4: Migrate the Activity Tracker resources](/images/mig_s4.svg)](/docs/atracker?topic=atracker-migration&interface=cli#migration-step4) | [![Step 4: Migrate the Activity Tracker resources](/images/mig_s4.svg)](/docs/atracker?topic=atracker-migration&interface=api#migration-step4-api) |
| [![Step 5: Initialize the CLI in your local system to use the Activity Tracker Event](/images/mig_s5.svg)](/docs/atracker?topic=atracker-migration&interface=cli#migration-step5) | [![Step 5: Initialize the CLI in your local system to use the Activity Tracker Event](/images/mig_s5.svg)](/docs/atracker?topic=atracker-migration&interface=api#migration-step5-api) |
{: caption="Table 1. Migration steps" caption-side="bottom"}

## Step 1. Configure the CLI V2 in your local system
{: #migration-step1}
{: cli}

Complete the following prerequisites to configure and initialize the {{site.data.keyword.atracker_short}} CLI in your local system:

1. Install the latest {{site.data.keyword.atracker_short}} CLI V2 plugin in your local system. See [Installing the {{site.data.keyword.atracker_short}} CLI](/docs/atracker?topic=atracker-atracker-cli-mng&interface=cli#atracker-cli-mng-install).

2. Log in to the {{site.data.keyword.cloud_notm}}. Run the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)

3. Make sure that your account is configured to use the V1 APIs.

    Initialize the {{site.data.keyword.atracker_short}} CLI plugin to use the API version that was used to create the configuration resources in your account. Run the following command:

    ```text
    ibmcloud atracker init version
    ```
    {: pre}

    If the command indicates your system is running version 2, no migration is required.

## Step 2. Check the resources that must be migrated
{: #migration-step2}
{: cli}

Check the resources that must be migrated. Run the following command:

```text
ibmcloud atracker migration status
```
{: pre}

You will get a list of all the resources per region that must be migrated.

## Step 3. Configure the V2 account settings
{: #migration-step3}
{: cli}

Complete the following steps:

1. Check the account settings. Run the following command:

    ```text
    ibmcloud atracker setting get
    ```
    {: pre}

    You will get a response similar to the following one where no settings have been configured and only some values are displayed to indicate default values. The account settings is new in V2.

    ```text
    OK
    IBM Cloud Activity Tracker settings       
    Metadata region primary:                                
    Default targets:                                     []   
    Permitted target regions:                            []   
    Private api endpoint only:                           false   
    API version:                                         1   
    ```
    {: screen}

2. Configure the V2 account settings. Run the following command:

    ```text
    ibmcloud atracker setting update --metadata-region-primary METADATA_REGION [--default-targets TARGET] [--permitted-target-regions REGION] [--private-api-endpoint-only ( TRUE | FALSE )]
    ```
    {: pre}

    Where
    
    - `METADATA_REGION` defines the {{site.data.keyword.cloud_notm}} location where the {{site.data.keyword.atracker_short}} account metadata is stored. For more information, see [Locations](/docs/atracker?topic=atracker-regions&interface=cli).

    - `TARGET` defines 1 or more target IDs. When a supported {{site.data.keyword.atracker_short}} location is not configured to collect auditing events, these events are routed to every target that is listed in this section. 

        The target IDs that you list must be defined within the account where the auditing events are being generated.
        {: important}

    - `REGION` defines the list of supported {{site.data.keyword.atracker_short}} locations where the account administrator can define a target to collect auditing events.
    
    - `--private-api-endpoint-only` indicates whether an account administrator can only use private api endpoints to manage the {{site.data.keyword.atracker_short}} account configuration.

    Make sure that the `--permitted-target-regions` list all the regions where you have currently defined targets in your account. Also, you must have a `--metadata-region-primary` defined as well as a `--default-targets` target before [migrating your account configuration.](#migration-step4)
    {: important}

## Step 4. Migrate the account configuration from V1 to V2
{: #migration-step4}
{: cli}

Use this command to migrate the {{site.data.keyword.atracker_short}} account configuration from a V1 API configuration to a V2 API configuration. 

```text
ibmcloud atracker migration start 
```
{: pre}

The following is an example when a migration has started.

```json
Are you sure you want to migrate atracker v1 api configurations to atracker v2 api? [y/N]> y
OK
{
  "progress": 0,
  "status": "in-process",
  "migration_items": [
    {
      "resource_type": "route",
      "id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "status": "pending",
      "detailed_status": 
      [
        "migration of this resource is not started yet."
      ],
      "error" : "",
    },
    {
      "resource_type": "target",
      "id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "status": "pending",
      "detailed_status": [
        "migration of this resource is not started yet."
      ],
      "error" : "",                    
    },
  ]
}         
```
{: codeblock}


Use the following command to get the status of an in-progress migration:

```text
ibmcloud atracker migration status
```
{: pre}

The following is an example when the migration is 50% complete (`"progress": 50`).

```json
{
  "progress": 50,
  "status": "in-process",
  "migration_items": [
    {
      "resource_type": "route",
      "id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "status": "completed",
      "detailed_status": [
        "migration of this resource is successful."
      ],
      "error" : "",
    },
    {
      "resource_type": "target",
      "id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "status": "pending",
      "detailed_status": [
        "migration of this resource is not started yet."
      ],
      "error" : ""
    },
  ]
}
```
{: codeblock}


## Step 5. Initialize the CLI plugin to use the V2 API
{: #migration-step5}
{: cli}

Initialize the {{site.data.keyword.atracker_short}} CLI plugin to use the API version 2. Run the following command:

```text
ibmcloud atracker init version
```
{: pre}




## API settings and actions
{: #migrating-api}
{: api}

The following table lists the actions that you can run to migrate your accounts and find the status of an existing migration request:

| Action                     | REST API Method  | API_URL                                          | 
|----------------------------|------------------|--------------------------------------------------|
| Migrate account            | `POST`            | `<ENDPOINT>/api/v2/migration`  |
| Get migration status            | `GET`           | `<ENDPOINT>/api/v2/migration`              |
{: caption="Table 3. Migration actions by using the {{site.data.keyword.atracker_short}} REST API" caption-side="top"}

You can use private and public endpoints to migrate your configuration. For more information about the list of `ENDPOINTS` that are available, see [Endpoints](/docs/atracker?topic=atracker-endpoints).

For more information about the REST API, see [the migration API](https://{DomainName}/apidocs/atracker/atracker-v2#post-migration){: external}.
{: note}

## API prerequsites
{: #migration-prereqs-api}
{: api}

To make API calls to migrate your account, complete the following steps:

1. Get an IAM access token. For more information, see [Retrieving IAM access tokens](/docs/atracker?topic=atracker-retrieve-iam-token).

2. Identify the API endpoint in the region where you plan to migrate your account. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints#endpoints_api).


## Migrating from V1 to V2 using the API
{: #migrating-api}
{: api}

You must be logged in to the account to be migrated before running this command.  All targets and routes associated with the account will be migrated.
{: important}

To migrate using the API you will need to use a combination of the CLI and API.

## Step 1. Configure the V2 API in your local system using the CLI
{: #migration-step1-api}
{: api}

Complete the following prerequisites to configure and initialize the {{site.data.keyword.atracker_short}} API in your local system:

1. Install the latest {{site.data.keyword.atracker_short}} CLI V2 plugin in your local system. See [Installing the {{site.data.keyword.atracker_short}} CLI](/docs/atracker?topic=atracker-atracker-cli-mng&interface=cli#atracker-cli-mng-install).

2. Log in to the {{site.data.keyword.cloud_notm}}. Run the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)

3. Make sure that your account is configured to use the V1 APIs. 

    Initialize the {{site.data.keyword.atracker_short}} CLI plugin to use the API version that was used to create the configuration resources in your account. Run the following command:

    ```text
    ibmcloud atracker init version
    ```
    {: pre}

    If the command indicates your system is running version 2, no migration is required.

## Step 2. Check the resources that must be migrated using the API
{: #migration-step2-api}
{: api}

Check the resources that must be migrated. Run the following command:

```shell
curl -X GET 
  https://<ENDPOINT>/api/v2/migration 
  -H "Authorization: Bearer <IAM_TOKEN>" 
  -H 'accept: application/json'
```
{: codeblock}

Where `<ENDPOINT>` is the API endpoint in the region where you want to run the migration. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints#endpoints_api).

You will get a list of all the resources per region that must be migrated.

## Step 3. Configure the V2 account settings using the API
{: #migration-step3-api}
{: api}

Complete the following steps:

1. Check the account settings. Run the following command:

   ```shell
   curl -X GET <ENDPOINT>/api/v2/settings   -H "Authorization:  $ACCESS_TOKEN"   
   ```
   {: codeblock}

   Where:

   `<ENDPOINT>` 
   :   Is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints#endpoints_api).

   You will get a response similar to the following one where no settings have been configured and only some values are displayed to indicate default values. The account settings is new in V2.

   ```json
   {
    "default_targets": [],
    "permitted_target_regions": [],
    "metadata_region_primary": [],
    "private_api_endpoint_only": false,
    "api_version": 1
    }
   ```
   {: screen}

2. Configure the V2 account settings. Run the following command:

   ```shell
   curl -X PUT  <ENDPOINT>/api/v2/settings   
   -H "Authorization:  $ACCESS_TOKEN"   
   -H "content-type: application/json"  
   -d '{
      "default_targets": ["IDs"],
      "permitted_target_regions": ["REGIONS"],
      "metadata_region_primary": "REGION",
      "private_api_endpoint_only": false
   }'
   ```
   {: codeblock}

   Where:

   `ENDPOINT` 
   :    Is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints#endpoints_api).

   `default_targets`
   :   Is a list of target IDs.  If no routing rules cause events to be sent to other targets, these targets will received the events.

   `permitted_target_regions`
   :   Is the list of regions that can be used to define a target. A maximum of two permitted target regions can be specified.

   `metadata_region_primary`
   :   Is the region where the metadata associated with route and target definitions is stored.

   `private_api_endpoint_only`
   :   Specifies whether nor not a private endpoint can be used.  If `true` only a private endpoint can be used.

   Make sure that the `--permitted-target-regions` list all the regions where you have currently defined targets in your account. Also, you must have a `--metadata-region-primary` defined as well as a `--default-targets` target before [migrating your account configuration.](#migration-step4)
   {: important}

## Step 4. Migrate the account configuration from V1 to V2 using the API
{: #migration-step4-api}
{: api}

Use this command to migrate the {{site.data.keyword.atracker_short}} account configuration from a V1 API configuration to a V2 API configuration. 

```shell
curl -X POST 
  https://<ENDPOINT>/api/v2/migration 
  -H "Authorization: Bearer <IAM_TOKEN>" 
  -H 'accept: application/json'
```
{: codeblock}

Where `ENDPOINT` is the API endpoint in the region where you want to run the migration. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints#endpoints_api).

The following is an example when a migration has started.

```json
{
  "progress": 0,
  "status": "in-process",
  "migration_items": [
    {
      "resource_type": "route",
      "id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "status": "pending",
      "detailed_status": 
      [
        "migration of this resource is not started yet."
      ],
      "error" : "",
    },
    {
      "resource_type": "target",
      "id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "status": "pending",
      "detailed_status": [
        "migration of this resource is not started yet."
      ],
      "error" : "",
    },
  ]
}
```
{: codeblock}


Use the following command to get the status of an in-progress migration:

```shell
curl -X GET 
  https://<ENDPOINT>/api/v2/migration 
  -H "Authorization: Bearer <IAM_TOKEN>" 
  -H 'accept: application/json'
```
{: codeblock}

Where `ENDPOINT` is the API endpoint in the region where you want to run the migration. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints#endpoints_api).

The following is an example when the migration is 50% complete (`"progress": 50`).

```json
{
  "progress": 50,
  "status": "in-process",
  "migration_items": [
    {
      "resource_type": "route",
      "id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "status": "completed",
      "detailed_status": [
        "migration of this resource is successful."
      ],
      "error" : "",
    },
    {
      "resource_type": "target",
      "id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "status": "pending",
      "detailed_status": [
        "migration of this resource is not started yet."
      ],
      "error" : ""
    },
  ]
}
```
{: codeblock}

## Step 5. Initialize the CLI plugin to use the V2 API after migrating
{: #migration-step5-api}
{: api}

Initialize the {{site.data.keyword.atracker_short}} CLI plugin to use the API version 2. Run the following command:

```text
ibmcloud atracker init version
```
{: pre}

## HTTP response codes
{: #migration-rc}
{: api}

When you use the {{site.data.keyword.atracker_short}} REST API, you can get standard HTTP response codes to indicate whether a method completed successfully. 

- A 200 response always indicates success. 
- A 4xx response indicates a failure.
- A 5xx response usually indicates an internal system error.

See the following table for some HTTP response codes:

| Status code | Status | Description |
|-------------|--------|-------------|
| `200` |	OK | The request was successful. |
| `201` |	OK | The request was successful. A resource is created. |
| `400` | Bad Request |	The request was unsuccessful. You might be missing a parameter that is required. |
| `401` |	Unauthorized | The IAM token that is used in the API request is invalid or expired. |
| `403` |	Forbidden | The operation is forbidden due to insufficient permissions. |
| `404` | Not Found |	The requested resource doesn't exist or is already deleted. |
| `429` |	Too Many Requests |	Too many requests hit the API too quickly. |
| `500` |	Internal Server Error |	Something went wrong in {{site.data.keyword.atracker_short}} processing. |
{: caption="Table 4. List of HTTP response codes" caption-side="top"}



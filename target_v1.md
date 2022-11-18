---

copyright:
  years: 2019, 2022
lastupdated: "2022-05-24"

keywords: 

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Managing targets by using the V1 API
{: #target}

You can manage targets in your account by using the {{site.data.keyword.atracker_full}} CLI or the {{site.data.keyword.atracker_full_notm}} REST API. A target is a resource where you can collect auditing events. 
{: shortdesc}


The V1 API is deprecated. See [managing {{site.data.keyword.atracker_full_notm}} hosted event search offering targets by using the V2 API](/docs/atracker?topic=atracker-target_v2_at) and [managing COS targets by using the V2 API](/docs/atracker?topic=atracker-target_v2_cos) for information on using the V2 API.  Also see [migrating resources](/docs/atracker?topic=atracker-migrate-resources) for information on migrating from your V1 configuration.
{: deprecated}

The version of the API running in your account can be determined by running the [`ibmcloud atracker init version` command.](/docs/atracker?topic=atracker-v2api)
{: note}

You can define up to 16 targets in each region. 

You must define a {{site.data.keyword.cos_full_notm}} (COS) target for each region. While you can use the same COS bucket for collecting auditing events in your account across multiple regions, you should consider defining a bucket in each region to improve performance and reduce network latency. 
{: important}

The following table outlines valid target types:

| Target                                      | Type                     |
|---------------------------------------------|--------------------------|
| `{{site.data.keyword.cos_full_notm}} (COS)` | `cloud_object_storage`   |
{: caption="Table 1. List of targets" caption-side="top"}

When you define a target in {{site.data.keyword.cos_full_notm}} (COS), consider the following information:
- You can create the bucket in any location. For more information, see [Managing {{site.data.keyword.cos_full_notm}} (COS) buckets](/docs/atracker?topic=atracker-cos).
- You configure 1 bucket for each target.

If you have regulatory and compliance requirements, check the locations where you can create a bucket. Then, if performance is critical, consider creating the COS bucket in the same region where the auditing events are generated.
{: note}

## CLI prerequisites
{: #target-prereqs}
{: cli}

Before you use the CLI to manage targets, complete the following steps:

1. Identify the endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints#endpoints_api).

2. [Pre-requisite] [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

3. [Pre-requisite] [Install the {{site.data.keyword.atracker_full_notm}} CLI](/docs/atracker?topic=atracker-activity-tracking-cli#activity-tracking-cli-prereq).

4. Log in to the region in the {{site.data.keyword.cloud_notm}} where the instance is running. Run the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)

5. Set the resource group where the instance is running. Run the following command: [ibmcloud target](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_target)

    By default, the `default` resource group is set.

## Creating a target using the CLI
{: #target-create-cli}
{: cli}

Use this command to create an {{site.data.keyword.atracker_full_notm}} service target to be used to configure a destination for activity events.

```sh
 ibmcloud atracker target create --name <TARGET_NAME> --type <TARGET_TYPE> ( --file <COS_ENDPOINT_DEFINITION_JSON_FILE> |  --endpoint <COS_ENDPOINT> --bucket <COS_BUCKET> --target-crn <COS_TARGET_CRN> --api-key ( <COS_API_KEY> | <@COS_API_KEY_FILE> ) ) [--region <REGION>] [--output JSON]
```
{: pre}

### Command options 
{: #target-create-options}

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--name <TARGET_NAME>`
:   The name to be given to the target.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--type <TARGET_TYPE>`
:   Only supported value for `<TARGET_TYPE>` is `cloud-object-storage`.

`--file <@COS_ENDPOINT_DEFINITION_JSON_FILE>`
:   A file containing an endpoint definition in the following format:

    ```json
    {
      "endpoint": "aaaaa", 
      "target_crn": "yyyyy",
      "bucket": "zzzzzz", 
      "api_key": "xxxxxx"
    }
    ```
    {: codeblock}

`--endpoint <COS_ENDPOINT>`
:   The {{site.data.keyword.cos_full_notm}} endpoint to be associated with the {{site.data.keyword.cos_full_notm}} bucket.

`--bucket <BUCKET>`
:    The name of the {{site.data.keyword.cos_full_notm}} bucket to be associated with the target.

`--target-crn <COS_TARGET_CRN>`
:   The CRN of the {{site.data.keyword.cos_full_notm}} instance.

`--api-key <COS_API_KEY>` | `<@COS_API_KEY_FILE>`
:   Your [API key](/docs/account?topic=account-manapikey) value or a reference to the API Key file used when logging in.  For example, `ibmcloud login --apikey $KEYFILE`

`--output JSON`
:   If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.
  
### Example
{: #target-create-example}

The following is an example using the **`ibmcloud atracker target create --name my-target --type cloud-object-storage --endpoint s3.us-west.cloud-object-storage.appdomain.cloud --bucket cloud-object-storage-my-cos --target-crn crn:v1:staging:public:cloud-object-storage:global:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx:: --api-key yyyyyyyyyyyyyyyyyyyyyyyyyyyyy`** command.

This example shows an example successful target creation.
{: note}

```text
Target
Name:               my-target
ID:                 000000000-00000000-0000-0000-00000000
CRN:                crn:v1:staging:public:atracker:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx
Type:               cloud_object_storage
COS Endpoint:       s3.us-west.cloud-object-storage.appdomain.cloud
COS Target CRN:     crn:v1:staging:public:cloud-object-storage:global:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx:
COS Bucket:         cloud-object-my-target
COS API Key:        REDACTED
COS Write Status:   success
Created:            2021-07-21T16:04:15.174Z
Updated:            2021-07-21T16:04:15.174Z
```
{: screen}

## Updating a target using the CLI
{: #target-update-cli}
{: cli}

Use this command to update a target for an {{site.data.keyword.atracker_full_notm}} region.  Any specified value that is different from when the target was originally created will be updated to the value specified in the command.

```sh
ibmcloud atracker target update --target <TARGET> [--name <TARGET_NAME>] [ --file <COS_ENDPOINT_DEFINITION_JSON_FILE> |  [--endpoint <COS_ENDPOINT>] [--bucket <COS_BUCKET>] [--target-crn <COS_TARGET_CRN>] [--api-key ( <COS_API_KEY> | <@COS_API_KEY_FILE> )] ) ] [--region <REGION>] [--output JSON]
```
{: pre}

### Command options 
{: #target-update-options}

`--target <TARGET>`
:   The ID or current target name.

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--name <TARGET_NAME>`
:   The name to be given to the target.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--file <@COS_ENDPOINT_DEFINITION_JSON_FILE>`
:   A file containing an endpoint definition in the following format:

    ```json
    {
      "endpoint": "aaaaa", 
      "target_crn": "yyyyy",
      "bucket": "zzzzzz", 
      "api_key": "xxxxxx"
    }
    ```
    {: codeblock}

`--endpoint <COS_ENDPOINT>`
:   The {{site.data.keyword.cos_full_notm}} endpoint to be associated with the {{site.data.keyword.cos_full_notm}} bucket.

`--bucket <COS_BUCKET>`
:   The name of the {{site.data.keyword.cos_full_notm}} bucket to be associated with the target.

`--target-crn <COS_TARGET_CRN>`
:   The CRN of the {{site.data.keyword.cos_full_notm}} instance.

`--api-key <COS_API_KEY>` | `<@COS_API_KEY_FILE>`
:   Your [API key](/docs/account?topic=account-manapikey) value or a reference to the API Key file used when logging in.  For example, `ibmcloud login --apikey $KEYFILE`

`--output JSON`
:   If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.
  
### Example
{: #target-update-example}

The following is an example using the **`ibmcloud atracker target update --target my-target --name new-target-name`** command.

```text
Target
Name:               new-target-name
ID:                 xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
CRN:                crn:v1:staging:public:atracker:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx
Type:               cloud_object_storage
COS Endpoint:       s3.us-west.cloud-object-storage.appdomain.cloud
COS Target CRN:     crn:v1:staging:public:cloud-object-storage:global:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx:
COS Bucket:         cloud-object-my-target
COS API Key:        REDACTED
COS Write Status:   success
Created:            2021-07-21T16:04:15.174Z
Updated:            2021-07-21T17:49:56.452Z
```
{: screen}

## Deleting a target using the CLI
{: #target-delete-cli}
{: cli}

Use this command to delete a target for an {{site.data.keyword.atracker_full_notm}} region. 

```sh
ibmcloud atracker target rm --target <TARGET> [--region <REGION>] [--force]
```
{: pre}

### Command options 
{: #target-rm-options}

`--target <TARGET>`
:   The ID or name of the target.

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--force`
:   Will delete the target without providing the user with any additional prompt.

`help` | `--help` | `-h`
:   List options available for the command.
  
### Example
{: #target-rm-example}

The following is an example using the **`ibmcloud atracker target rm --region us-east --target xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`** command.

```text
Are you sure you want to remove the target with target ID xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx? [y/N]>y
OK
Target with target ID xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx was successfully removed.
```
{: screen}

The following is an example using the **`ibmcloud atracker target rm --region us-east --target xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -force`** command.

This example shows a failed command where the specified target could not be found.
{: note}

```text
FAILED
Something went wrong. Error: Delete "https://us-east.atracker.cloud.ibm.com/api/v1/targets/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx": dial tcp: lookup us-east.atracker.cloud.ibm.com: no such host
```
{: screen}

## Validating a target using the CLI
{: #target-validate-cli}
{: cli}

Use this command to validate that a target is correctly configured for an {{site.data.keyword.atracker_full_notm}} region. 

```sh
ibmcloud atracker target validate --target <TARGET> [--region <REGION>] [--output JSON]
```
{: pre}

### Command options 
{: #target-validate-options}

`--target <TARGET>`
:   The ID or name of the target.

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output JSON`
:   If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.
  
### Example
{: #target-validate-example}

The following is an example using the **`ibmcloud atracker target validate --target new-target-name`** command.

This example shows a successfully validated target.
{: note}

```text
Target
Name:               new-target-name
ID:                 xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
CRN:                crn:v1:staging:public:atracker:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx
Type:               cloud_object_storage
COS Endpoint:       s3.us-west.cloud-object-storage.appdomain.cloud
COS Target CRN:     crn:v1:staging:public:cloud-object-storage:global:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx:
COS Bucket:         cloud-object-my-target
COS API Key:        REDACTED
COS Write Status:   success
Created:            2021-07-21T16:04:15.174Z
Updated:            2021-07-21T17:49:56.452Z
```
{: screen}

## Getting information about a target using the CLI
{: #target-get-cli}
{: cli}

Use this command to get information about a target for an {{site.data.keyword.atracker_full_notm}} region. 

```sh
ibmcloud atracker target get --target <TARGET> [--region <REGION>] [--output JSON]
```
{: pre}

### Command options 
{: #target-get-options}

`--target <TARGET>`
:   The ID or name of the target.

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output JSON`
:   If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.
  
### Example
{: #target-get-example}

The following is an example using the **`ibmcloud atracker target get --target new-target-name`** command.

```text
Target
Name:               new-target-name
ID:                 xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
CRN:                crn:v1:staging:public:atracker:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx
Type:               cloud_object_storage
COS Endpoint:       s3.us-west.cloud-object-storage.appdomain.cloud
COS Target CRN:     crn:v1:staging:public:cloud-object-storage:global:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx:
COS Bucket:         cloud-object-my-target
COS API Key:        REDACTED
COS Write Status:   success
Created:            2021-07-21T16:04:15.174Z
Updated:            2021-07-21T17:49:56.452Z
```
{: screen}

## Listing all targets in a region
{: #target-list-cli}
{: cli}

Use this command to list the configured targets for an {{site.data.keyword.atracker_full_notm}} region.

```sh
ibmcloud atracker target ls [--region <REGION>] [--output JSON]
```
{: pre}

### Command options 
{: #target-options}

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output JSON`
:   If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.
  
### Example
{: #target-example}

The following is an example using the **`ibmcloud atracker target ls`** command.

```text
Name                       ID                                     Region     Type                     Created
target-01                  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx   us-south    cloud_object_storage     2020-11-18T03:52:08.603Z
target-02                  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx   us-south    cloud_object_storage     2020-11-18T03:52:01.592Z
target-02-backup           xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx   us-south   cloud_object_storage     2021-02-26T06:53:13.466Z
```
{: screen}


## API targets and actions
{: #target-actions-api}
{: api}

The following table lists the actions that you can run to manage targets:

| Action                     | REST API Method  | API_URL                                          | 
|----------------------------|------------------|--------------------------------------------------|
| Create a target            | `POST`           | `<ENDPOINT>/api/v1/targets`              |
| Update a target            | `PUT`            | `<ENDPOINT>/api/v1/targets/<TARGET_ID>`  |
| Delete a target            | `DELETE`         | `<ENDPOINT>/api/v1/targets/<TARGET_ID>`  |
| Read a target              | `GET`            | `<ENDPOINT>/api/v1/targets/<TARGET_ID>`  |
| List all targets           | `GET`            | `<ENDPOINT>/api/v1/targets`             |
| Validate a target          | `POST`           | `<ENDPOINT>/api/v1/targets/{id}/validate` |
{: caption="Table 2. Target actions by using the {{site.data.keyword.atracker_full_notm}} REST API" caption-side="top"}

You can use private and public endpoints to manage targets. For more information about the list of `ENDPOINTS` that are available, see [Endpoints](/docs/atracker?topic=atracker-endpoints).

* By default, you can manage targets from the private network. You must use an API endpoint with the following format: `https://private.<region>.atracker.cloud.ibm.com`

* You can also enable public endpoints in a region to manage targets. For more information, see [Managing endpoints](/docs/atracker?topic=atracker-endpoints_manage).

For more information about the REST API, see [Targets](https://{DomainName}/apidocs/atracker-v1#create-target){: external}.


## API prerequisites
{: #target-prereqs-api}
{: api}

To make API calls to manage targets, complete the following steps:
1. Get an IAM access token. For more information, see [Retrieving IAM access tokens](/docs/atracker?topic=atracker-retrieve-iam-token).
2. Identify the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints#endpoints_api).


## Creating a target using the API
{: #target-create-api}
{: api}

You can use the following cURL command to create a target:

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

- `ENDPOINT` is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints#endpoints_api).
- `TARGET_NAME` is the name of the target. The maximum length of the name is 256 characters.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

- `TARGET_TYPE` is the type of the target. The only valid type is `cloud-object-storage`.
- `cos_endpoint` includes information about the target. For more information on how to get the bucket details, see [Getting the bucket configuration details](/docs/atracker?topic=atracker-cos#cos_bucket_details).
    
    `endpoint` indicates the {{site.data.keyword.atracker_full_notm}} endpoint where to look for this bucket. Use the private endpoint. 

    `target_crn` indicates the [CRN](/docs/account?topic=account-crn) of the COS instance where you provisioned the bucket.

    `bucket` indicates the name of the bucket.

    `api_key` contains the API key that has permissions to upload objects into the bucket.


For example, you can use the following cURL request to create a target in Dallas:

```shell
curl -X POST   https://private.us-south.atracker.cloud.ibm.com/api/v1/targets   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"   -d '{
    "name": "My COS target",
    "target_type": "cloud_object_storage",
    "cos_endpoint": {
      "endpoint": "s3.private.us-south.cloud-object-storage.appdomain.cloud",
      "target_crn": "crn:v1:bluemix:public:cloud-object-storage:global:a/<account-id>:<instance-id>::",
      "bucket": "my-activity-tracking-bucket",
      "api_key": "xxxxxxxxxxxxxxxxxx"
    }
  }'
```
{: screen}

In the response, you get information about the target such as the `id`, that indicates the GUID of the target, and the `crn`, that indicates the CRN of the target.
 



## Updating a target using the API
{: #target-update-api}
{: api}

When you update a target, you must include the target information in the data section of the request. 
- You must pass all fields.
- Update the fields that need changing.

You can use the following cURL command to update a target:

```shell
curl -X PUT  <ENDPOINT>/api/v1/targets/<target_ID>   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"   -d '{
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

- `<target_ID>` is the ID of the target.
- `TARGET_NAME` is the name of the target. The maximum length of the name is 256 characters.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}
    
- `TARGET_TYPE` is the type of the target. The only valid type is `cloud-object-storage`.
- `cos_endpoint` includes information about the target. For more information on how to get the bucket details, see [Getting the bucket configuration details](/docs/atracker?topic=atracker-cos#cos_bucket_details).
    
    `endpoint` indicates the {{site.data.keyword.atracker_full_notm}} endpoint where to look for this bucket. Use the private endpoint. 

    `target_crn` indicates the [CRN](/docs/account?topic=account-crn) of the COS instance where you provisioned the bucket.

    `bucket` indicates the name of the bucket.

    `api_key` contains the API key that has permissions to upload objects into the bucket.


For example, you can use the following cURL request to create a target in Dallas:

```shell
curl -X PUT   https://private.us-south.atracker.cloud.ibm.com/api/v1/targets   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"   -d '{
    "name": "My COS target",
    "target_type": "cloud_object_storage",
    "cos_endpoint": {
      "endpoint": "s3.private.us-south.cloud-object-storage.appdomain.cloud",
      "target_crn": "crn:v1:bluemix:public:cloud-object-storage:global:a/<account-id>:<instance-id>::",
      "bucket": "my-activity-tracking-bucket",
      "api_key": "xxxxxxxxxxxxxxxxxx"
    }
  }'
```
{: screen}

## Deleting a target using the API
{: #target-delete-api}
{: api}

You can use the following cURL command to delete a target:

```text
curl -X DELETE   <ENDPOINT>/api/v1/targets/<target_ID>   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"
```
{: codeblock}

Where

- `ENDPOINT` is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints#endpoints_api).
- `<target_ID>` is the ID of the target.


## Validating a target using the API
{: #target-validate-api}
{: api}

You can use the following cURL command to validate a target by checking the credentials to write to the bucket. 

```shell
curl -X POST  <ENDPOINT>/api/v1/targets/<target_ID>/validate   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json" 
```
{: codeblock}

Where

- `ENDPOINT` is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints#endpoints_api).
- `<target_ID>` is the ID of the target.

For example, you can use the following cURL request to validate a target in US-South:

```shell
curl -X POST   https://private.us-south.atracker.cloud.ibm.com/api/v1/targets/<TARGETID>/validate   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json" 
```
{: screen}

In the response, you get information in the section `cos_write_status`, for example:

```json
"cos_write_status": {
    "status": "success"
  },
```
{: screen}
 

## Viewing a target using the API
{: #target-view-api}
{: api}

You can use the following cURL command to view the configuration details of 1 target:

```shell
curl -X GET   <ENDPOINT>/api/v1/targets/<target_ID>   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"
```
{: codeblock}

Where

- `ENDPOINT` is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints#endpoints_api).
- `<target_ID>` is the ID of the target.


For example, you can run the following cURL request to get informatiomn about a target with ID `7faa6ea6-e564-4fef-93b0-4317a0d27c34`:

```shell
curl -X GET   https://private.us-south.atracker.cloud.ibm.com/api/v1/targets/7faa6ea6-e564-4fef-93b0-4317a0d27c34    -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"
```
{: screen}



## Listing all targets
{: #target-list-api}
{: api}

You can use the following cURL command to view all targets:

```shell
curl -X GET   <ENDPOINT>/api/v1/targets   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"
```
{: codeblock}

Where `ENDPOINT` is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints#endpoints_api).




For example, you can run the following cURL request to get informatiomn about the targets that are defined in Dallas:

```shell
curl -X GET   https://private.us-south.atracker.cloud.ibm.com/api/v1/targets    -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"
```
{: screen}


## HTTP response codes
{: #target-rc-api}
{: api}

When you use the {{site.data.keyword.atracker_full_notm}} REST API, you can get standard HTTP response codes to indicate whether a method completed successfully. 

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
| `500` |	Internal Server Error |	Something went wrong in {{site.data.keyword.atracker_full_notm}} processing. |
{: caption="Table 3. List of HTTP response codes" caption-side="top"}







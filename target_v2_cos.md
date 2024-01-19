---

copyright:
  years: 2022, 2024
lastupdated: "2024-01-19"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Managing COS targets
{: #target_v2_cos}

You can manage {{site.data.keyword.cos_full_notm}} (COS) targets in your account by using the {{site.data.keyword.atracker_full_notm}} CLI, the {{site.data.keyword.atracker_full_notm}} REST API, and Terraform scripts. A target is a resource where you can collect auditing events.
{: shortdesc}

For more information on {{site.data.keyword.atracker_full_notm}} targets, see [Targets](/docs/atracker?topic=atracker-target_v2).



## About COS targets
{: #target_v2_cos_targets}

If you are using an {{site.data.keyword.cos_full_notm}} (COS) target, you can use the same COS bucket for collecting auditing events in your account across multiple regions.  In that scenario events are forwarded to the target region before being written to the COS bucket.  You may consider defining a bucket in each region to improve performance and reduce network latency.
{: important}

When you define a target in {{site.data.keyword.cos_full_notm}} (COS), consider the following information:

* You can create the bucket in any location. For more information, see [Managing {{site.data.keyword.cos_full_notm}} (COS) buckets](/docs/atracker?topic=atracker-cos).

* You can only configure 1 bucket for a target.

* If you have regulatory and compliance requirements, check the locations where you can create a bucket. Then, if performance is critical, consider creating the COS bucket in the same region where the auditing events are generated.

## IAM Access
{: #target_v2_iam_access_cos}

You must grant users IAM permissions to manage targets. For more information, see [Assign access to resources](/docs/account?topic=account-assign-access-resources).

When you define a policy, you can indicate the scope of the permissions. You can choose from granting permissions for a specific region or for the entire account.

Users with regional scope will be limited to access targets in their authorized region.
{: note}



| IAM action               | IAM Policy scope  | IAM Roles                          | Description         |
| ------------------------ | ----------------- | ---------------------------------- | -------------- |
| `atracker.target.read`   | Region            | `Administrator`  \n `Editor`  \n `Viewer`  \n `Operator` | Read (view) information about a target |
| `atracker.target.create` | Region            | `Administrator`  \n `Editor` | Create a target |
| `atracker.target.update` | Region            | `Administrator`  \n `Editor` | Update a target |
| `atracker.target.delete` | Region            | `Administrator`  \n `Editor` | Delete a target |
| `atracker.target.list`   | Account           | `Administrator`  \n `Editor`  \n `Viewer`  \n `Operator` | List all targets |
{: caption="Table 1. IAM actions and the IAM roles that include them."}

## Authentication options
{: #target_v2_cos_auth_opts}

When writing to a COS target you can use the following options to authenticate to an {{site.data.keyword.cos_full_notm}} (COS) bucket.

* By configuring service-to-service (S2S) authorization (recommended).
* By providing an API key when configuring the target.


You can configure service-to-service authorization to your COS bucket so you do not need to pass an [API key](#target_v2_cos_apikey) when writing your encrypted data to the COS bucket.
{: note}


## CLI prerequisites
{: #target_prereqs_cos}
{: cli}

Before you use the CLI to manage targets, complete the following steps:

1. [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

2. [Install the {{site.data.keyword.atracker_full_notm}} CLI](/docs/atracker?topic=atracker-atracker-cli-config).

3. Log in to {{site.data.keyword.cloud_notm}}. Run the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)


## Obtaining your COS bucket API key
{: #target_v2_cos_apikey}

For information on obtaining your COS bucket API key, see [generating an API key to access a bucket](/docs/atracker?topic=atracker-cos#cos_bucket_access).


## Configuring S2S authorization using the UI witihin the same account
{: #target_v2_cos_s2s_ui}
{: ui}

Do the following to configure a service-to-service authorization using the {{site.data.keyword.cloud_notm}} UI.

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external} as the account owner that will be configuring {{site.data.keyword.atracker_full_notm}} targets.

	After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} dashboard opens.

2. Click **Manage** &gt; **Access (IAM)**.  **Manage access and users** is displayed.

3. Click **Authorizations**.

4. Click **Create**.

5. For **Source service** select *Activity Tracker* and for **How do you want to scope the access?** select *All resources*.

6. For **Target service** select *Cloud Object Storage* for **How do you want to scope the access?** select *Resources based on selected attributes*.

7. Select **Service instance** and **string equals** the name of your COS instance.

8. For **Service access** select **Object writer**.

9. Click **Authorize**.  Your new service-to-service authorization will be listed in the **Manage authorizations** view.

You will only be able to authorize to the {{site.data.keyword.cos_full_notm}} instance using the UI. If you want to limit authorization to a specific {{site.data.keyword.cos_full_notm}} bucket, you need to configure authorization using the [API](/docs/atracker?topic=atracker-target_v2_cos&interface=api#target_v2_cos_s2s_api).
{: important}


## Configuring S2S authorization using the CLI
{: #target_v2_cos_s2s_cli}
{: cli}

Do the following to configure a service-to-service authorization using the {{site.data.keyword.cloud_notm}} CLI.

1. [Log in to your {{site.data.keyword.cloud_notm}} account] (/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login) as the account owner that will be configuring {{site.data.keyword.atracker_full_notm}} authorization.

2. Create an authorization policy defining your service-to-service authorization.

   ```sh
   ibmcloud iam authorization-policy-create atracker cloud-object-storage "Object Writer" [--target-service-instance-id <COS_SERVICE_INSTANCE>
   ```
   {: pre}

   Where:

   `COS_SERVICE_INSTANCE` is the [bucket instance CRN](/docs/atracker?topic=atracker-cos#cos_bucket_details) of the COS instance to be authorized.


## Configuring S2S authorization using the API
{: #target_v2_cos_s2s_api}
{: api}

Do the following to configure a service-to-service authorization using the {{site.data.keyword.cloud_notm}} API.

1. [Log in to your {{site.data.keyword.cloud_notm}} account](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login) as the account owner that will be configuring {{site.data.keyword.atracker_full_notm}} IAM authorization.

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

3. Get an IAM access token. For more information, see [Retrieving IAM access tokens](/docs/atracker?topic=atracker-retrieve-iam-token).

4. Run the following command to configure your service-to-service authorization:

   ```sh
   curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header "Authorization: $ACCESS_TOKEN" -d @authorization_policy_resource.json "https://iam.cloud.ibm.com/v1/policies"
   ```
   {: pre}



## Creating a COS target using the CLI
{: #target-create-cli-cos}
{: cli}

Use this command to create a {{site.data.keyword.cos_full_notm}} target to be used to configure a destination for activity events.

```sh
 ibmcloud atracker target create --name TARGET_NAME --type TARGET_TYPE ( [--file COS_ENDPOINT_DEFINITION_JSON_FILE] |  ( [--endpoint COS_ENDPOINT] [--bucket COS_BUCKET] [--target-crn COS_TARGET_CRN] ( [--api-key ( COS_API_KEY | @COS_API_KEY_FILE )] |  [--service-to-service-enabled ( TRUE | FALSE )] ) ) ) [--region REGION] [--output FORMAT]
```
{: pre}

### Command options
{: #target-create-options-cos}

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--name TARGET_NAME`
:   The name to be given to the target.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--type TARGET_TYPE`
:   Set the `TARGET_TYPE` to `cloud_object_storage` for a COS target.

`--file @COS_ENDPOINT_DEFINITION_JSON_FILE`
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

`--endpoint COS_ENDPOINT`
:   The {{site.data.keyword.cos_full_notm}} endpoint to be associated with the {{site.data.keyword.cos_full_notm}} bucket.

`--bucket BUCKET`
:    The name of the {{site.data.keyword.cos_full_notm}} bucket to be associated with the target.

`--target-crn COS_TARGET_CRN`
:   The CRN of the {{site.data.keyword.cos_full_notm}} instance.

`--api-key COS_API_KEY` | `@COS_API_KEY_FILE`
:   Your [API key](/docs/account?topic=account-manapikey) value or a reference to the API Key file used to gain access.  For example, `ibmcloud login --apikey $KEYFILE`

`--service-to-service-enabled`
:   Indicates if [service-to-service authorization](/docs/atracker?topic=atracker-target_v2_cos&interface=ui#target_v2_cos_s2s_ui) has been enabled for the bucket.  Specify `TRUE` if service-to-service authorization is enabled and `FALSE` if service-to-service authorization is not enable.  By default, `service_to_service_enabled` is `FALSE`.

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-create-example-cos}

The following is an example using the **`ibmcloud atracker target create --name my-target --type cloud_object_storage --endpoint s3.us-west.cloud-object-storage.appdomain.cloud --bucket cloud-object-storage-my-cos --target-crn crn:v1:staging:public:cloud-object-storage:global:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx:: --api-key yyyyyyyyyyyyyyyyyyyyyyyyyyyyy`** command.

This example shows an example successful target creation.
{: note}

```text
Target
Name:               		my-target
ID:                 		000000000-00000000-0000-0000-00000000
CRN:                		crn:v1:staging:public:atracker:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx
Type:               		cloud_object_storage
COS Endpoint:       		s3.us-west.cloud-object-storage.appdomain.cloud
COS Target CRN:     		crn:v1:staging:public:cloud-object-storage:global:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx:
COS Bucket:         		cloud-object-my-target
Service to Service Enabled:	true
Write Status:   		success
Created:            		2021-07-21T16:04:15.174Z
Updated:            		2021-07-21T16:04:15.174Z
```
{: screen}



## Updating a COS target using the CLI
{: #target-update-cli-cos}
{: cli}

Use this command to update a COS target for an {{site.data.keyword.atracker_full_notm}} region.  Any specified value that is different from when the target was originally created will be updated to the value specified in the command.

```sh
ibmcloud atracker target update --target TARGET [--name TARGET_NAME] [ [--file COS_ENDPOINT_DEFINITION_JSON_FILE] |  ( [--endpoint COS_ENDPOINT] [--bucket COS_BUCKET] [--target-crn COS_TARGET_CRN] ( [--api-key ( COS_API_KEY | @COS_API_KEY_FILE )] | [--service-to-service-enabled ( TRUE | FALSE )]))] [--output FORMAT]
```
{: pre}

### Command options
{: #target-update-options-cos}

`--target TARGET`
:   The ID or current target name.

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--name TARGET_NAME`
:   The name to be given to the target.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--file @COS_ENDPOINT_DEFINITION_JSON_FILE`
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

    or for a scenario where service-to-service authentication is enabled:

    ```json
    {
      "endpoint": "aaaaa",
      "target_crn": "yyyyy",
      "bucket": "zzzzzz",
      "service_to_service_enabled": true
    }
    ```
    {: codeblock}


`--endpoint COS_ENDPOINT`
:   The {{site.data.keyword.cos_full_notm}} endpoint to be associated with the {{site.data.keyword.cos_full_notm}} bucket.

`--bucket COS_BUCKET`
:   The name of the {{site.data.keyword.cos_full_notm}} bucket to be associated with the target.

`--target-crn COS_TARGET_CRN`
:   The CRN of the {{site.data.keyword.cos_full_notm}} instance.

`--api-key COS_API_KEY` | `@COS_API_KEY_FILE`
:   Your [API key](/docs/account?topic=account-manapikey) value or a reference to the API Key file used to gain access.  For example, `ibmcloud login --apikey $KEYFILE`

`--service-to-service-enabled (TRUE | FALSE)`
:   Indicates if [service-to-service authorization](/docs/atracker?topic=atracker-target_v2_cos&interface=cli#target_v2_cos_s2s_cli) has been enabled for the bucket.  Specify `TRUE` if service-to-service authorization is enabled and `FALSE` if service-to-service authorization is not enable.  By default, service-to-service authorization is `FALSE`.

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-update-example-cos}

The following is an example using the **`ibmcloud atracker target update --target my-target --name new-target-name`** command.

```text
Target
Name:               		new-target-name
ID:                 		xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
CRN:               		crn:v1:staging:public:atracker:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx
Type:               		cloud_object_storage
COS Endpoint:       		s3.us-west.cloud-object-storage.appdomain.cloud
COS Target CRN:    		crn:v1:staging:public:cloud-object-storage:global:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx:
COS Bucket:         		cloud-object-my-target
Service to Service Enabled:	true
Write Status:   		success
Created:            		2021-07-21T16:04:15.174Z
Updated:           		2021-07-21T17:49:56.452Z
```
{: screen}


## Deleting a target using the CLI
{: #target-delete-cli-cos}
{: cli}

Use this command to delete a target.

```sh
ibmcloud atracker target rm --target TARGET [--force]
```
{: pre}

### Command options
{: #target-rm-options-cos}

`--target TARGET`
:   The ID or name of the target.

`--force` | `-f`
:   Will delete the target without providing the user with any additional prompt.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-rm-example-cos}

The following is an example using the **`ibmcloud atracker target rm --target xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`** command.

```text
Are you sure you want to remove the target with target ID xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx? [y/N]>y
OK
Target with target ID xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx was successfully removed.
```
{: screen}

The following is an example using the **`ibmcloud atracker target rm --target xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -force`** command.

This example shows a failed command where the specified target could not be found.
{: note}

```text
Are you sure you want to remove the Target bearing Target ID 33333333-3333-3333-3333-333333333333? [y/N]> y
FAILED
Something went wrong. Error:
 Status Code:  404
 Incident ID:  67a33257-d5a4-46ec-94d9-14eb70e94f3d
 Code:         not_found
 Message:      The target id specified in `target_id` field is not found.
```
{: screen}

## Validating a target using the CLI
{: #target-validate-cli-cos}
{: cli}

Use this command to validate that a target is correctly configured for an {{site.data.keyword.atracker_full_notm}} region.

```sh
ibmcloud atracker target validate --target TARGET [--region REGION] [--output FORMAT]
```
{: pre}

### Command options
{: #target-validate-options-cos}

`--target TARGET`
:   The ID or name of the target.

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-validate-example-cos}

The following is an example using the **`ibmcloud atracker target validate --target new-target-name`** command.

This example shows a successfully validated COS target.
{: note}

```text
Target
Name:               		new-target-name
ID:                 		xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
CRN:               		crn:v1:staging:public:atracker:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx
Type:               		cloud_object_storage
COS Endpoint:       		s3.us-west.cloud-object-storage.appdomain.cloud
COS Target CRN:     		crn:v1:staging:public:cloud-object-storage:global:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx:
COS Bucket:         		cloud-object-my-target
Service to Service Enabled:	true
Write Status:   		success
Created:            		2021-07-21T16:04:15.174Z
Updated:           		2021-07-21T17:49:56.452Z
```
{: screen}

## Getting information about a target using the CLI
{: #target-get-cli-cos}
{: cli}

Use this command to get information about a target for an {{site.data.keyword.atracker_full_notm}} region.

```sh
ibmcloud atracker target get --target TARGET [--output FORMAT]
```
{: pre}

### Command options
{: #target-get-options-cos}

`--target TARGET`
:   The ID or name of the target.

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-get-example-cos}

The following is an example using the **`ibmcloud atracker target get --target new-target-name`** command showing a COS target.

```text
Target
Name:               		new-target-name
ID:                 		xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
CRN:               		crn:v1:staging:public:atracker:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx
Type:               		cloud_object_storage
COS Endpoint:      		s3.us-west.cloud-object-storage.appdomain.cloud
COS Target CRN:     		crn:v1:staging:public:cloud-object-storage:global:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx:
COS Bucket:         		cloud-object-my-target
Service to Service Enabled:	true
Write Status:   		success
Created:           		2021-07-21T16:04:15.174Z
Updated:            		2021-07-21T17:49:56.452Z
```
{: screen}

## Listing all targets in a region
{: #target-list-cli-cos}
{: cli}

Use this command to list the configured targets for an {{site.data.keyword.atracker_full_notm}} region.

```sh
ibmcloud atracker target ls [--output FORMAT]
```
{: pre}

### Command options
{: #target-options-cos}

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-example-cos}

The following is an example using the **`ibmcloud atracker target ls`** command.

```text
Name                       ID                                     Region     Type                     Service to Service Enabled	Created
target-01                  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx   us-south    cloud_object_storage    true				2020-11-18T03:52:08.603Z
target-02                  yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy   us-south    cloud_object_storage    true				2020-11-18T03:52:01.592Z
target-02-backup           zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz   us-east     cloud_object_storage    false				2021-02-26T06:53:13.466Z
```
{: screen}


## API targets and actions
{: #target-actions-api-cos}
{: api}

The following table lists the actions that you can run to manage targets:

| Action                     | REST API Method  | API_URL                                          |
|----------------------------|------------------|--------------------------------------------------|
| Create a target            | `POST`           | `<ENDPOINT>/api/v2/targets`              |
| Update a target            | `PUT`            | `<ENDPOINT>/api/v2/targets/<TARGET_ID>`  |
| Delete a target            | `DELETE`         | `<ENDPOINT>/api/v2/targets/<TARGET_ID>`  |
| Read a target              | `GET`            | `<ENDPOINT>/api/v2/targets/<TARGET_ID>`  |
| List all targets           | `GET`            | `<ENDPOINT>/api/v2/targets`             |
| Validate a target          | `POST`           | `<ENDPOINT>/api/v2/targets/{id}/validate` |
{: caption="Table 2. Target actions by using the {{site.data.keyword.atracker_full_notm}} REST API" caption-side="top"}

You can use private and public endpoints to manage targets. For more information about the list of `ENDPOINTS` that are available, see [Endpoints](/docs/atracker?topic=atracker-endpoints).


* You can manage targets from the private network using an API endpoint with the following format: `https://private.REGION.atracker.cloud.ibm.com`
* You can manage targets from the public network using an API endpoint with the following format: `https://REGION.atracker.cloud.ibm.com`

* You can disable the public endpoints by updating the account settings. For more information, see [Configuring target and region settings](/docs/atracker?topic=atracker-settings).

For more information about the REST API, see [Targets](https://{DomainName}/apidocs/atracker/atracker-v2#create-target){: external}.
{: note}


## API prerequisites
{: #target-prereqs-api-cos}
{: api}

To make API calls to manage targets, complete the following steps:
1. Get an IAM access token. For more information, see [Retrieving IAM access tokens](/docs/atracker?topic=atracker-retrieve-iam-token).
2. Identify the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).



## Creating a COS target using the API
{: #target-create-api-cos}
{: api}

You can use the following cURL command to create a {{site.data.keyword.cos_full_notm}} (COS) target:

```shell
curl -X POST  <ENDPOINT>/api/v2/targets   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"   -d '{
    "name": "TARGET_NAME",
    "target_type": "cloud_object_storage",
    "cos_endpoint": {
      "endpoint": "PRIVATE_COS_ENDPOINT",
      "target_crn": "COS_CRN",
      "bucket": "BUCKET_NAME",
      "api_key": "API_KEY",
      "service_to_service_enabled": SERVICE_TO_SERVICE
    }
  }'
```
{: codeblock}

Where

- `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).
- `TARGET_NAME` is the name of the target. The maximum length of the name is 256 characters.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

- `TARGET_TYPE` is the type of the target. The valid type is `cloud_object_storage`.
- `cos_endpoint` includes information about the target. For more information on how to get the bucket details, see [Getting the bucket configuration details](/docs/atracker?topic=atracker-cos#cos_bucket_details).

    `PRIVATE_COS_ENDPOINT` indicates the {{site.data.keyword.atracker_full_notm}} endpoint to look for this bucket. Use the private endpoint.

    `COS_CRN` indicates the [CRN](/docs/account?topic=account-crn) of the COS instance where you provisioned the bucket.

    `BUCKET_NAME` indicates the name of the bucket.

    `API_KEY` contains the API key that has permissions to upload objects into the bucket.  This value is ignore if `service_to_service_enabled` is `true`.

    `SERVICE_TO_SERVICE` indicates if [service-to-service authorization](/docs/atracker?topic=atracker-target_v2_cos&interface=cli#target_v2_cos_s2s_cli) has been enabled for the bucket.  Specify `true` if service-to-service authorization is enabled and `false` if service-to-service authorization is not enable.  By default, service-to-service authorization is `false`.


For example, you can use the following cURL request to create a target in Dallas:

```shell
curl -X POST   https://private.us-south.atracker.cloud.ibm.com/api/v2/targets   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"   -d '{
    "name": "My COS target",
    "target_type": "cloud_object_storage",
    "cos_endpoint": {
      "endpoint": "s3.private.us-south.cloud-object-storage.appdomain.cloud",
      "target_crn": "crn:v1:bluemix:public:cloud-object-storage:global:a/<account-id>:<instance-id>::",
      "bucket": "my-activity-tracking-bucket",
      "api_key": "xxxxxxxxxxxxxxxxxx",
      "service_to_service_enabled": false
    }
  }'
```
{: screen}

In the response, you get information about the target such as the `id`, that indicates the GUID of the target, and the `crn`, that indicates the CRN of the target.


## Updating a COS target using the API
{: #target-update-api-cos}
{: api}

When you update an {{site.data.keyword.cos_full_notm}} (COS) target, you must include the target information in the data section of the request.
- You must pass all fields.
- Update the fields that need to be changed.
- You cannot change the `target_type` of a target once created.

You can use the following cURL command to update a target:

```shell
curl -X PUT  <ENDPOINT>/api/v2/targets/TARGET_ID  -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"   -d '{
    "name": "TARGET_NAME",
    "target_type": "TARGET_TYPE",
    "cos_endpoint": {
      "endpoint": "PRIVATE_COS_ENDPOINT",
      "target_crn": "COS_CRN",
      "bucket": "BUCKET_NAME",
      "api_key": "API_KEY",
      "service_to_service_enabled": SERVICE_TO_SERVICE
    }
  }'
```
{: codeblock}

Where

- `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).
- `TARGET_ID` is the ID of the target.
- `TARGET_NAME` is the name of the target. The maximum length of the name is 256 characters.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

- `TARGET_TYPE` is the type of the target. Set the value to `cloud_object_storage` for a COS target.
- `cos_endpoint` includes information about the target. For more information on how to get the bucket details, see [Getting the bucket configuration details](/docs/atracker?topic=atracker-cos#cos_bucket_details).

    `PRIVATE_COS_ENDPOINT` indicates the {{site.data.keyword.atracker_full_notm}} endpoint to look for this bucket. Use the private endpoint.

    `COS_CRN` indicates the [CRN](/docs/account?topic=account-crn) of the COS instance where you provisioned the bucket.

    `BUCKET_NAME` indicates the name of the bucket.

    `API_KEY` contains the API key that has permissions to upload objects into the bucket.  This value is ignore if `service_to_service_enabled` is `true`.

    `SERVICE_TO_SERVICE` indicates if [service-to-service authorization](/docs/atracker?topic=atracker-target_v2_cos&interface=cli#target_v2_cos_s2s_cli) has been enabled for the bucket.  Specify `true` if service-to-service authorization is enabled and `false` if service-to-service authorization is not enable.  By default, service-to-service authorization is `false`.


For example, you can use the following cURL request to create a target in Dallas:

```shell
curl -X PUT   https://private.us-south.atracker.cloud.ibm.com/api/v2/targets   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"   -d '{
    "name": "My COS target",
    "target_type": "cloud_object_storage",
    "cos_endpoint": {
      "endpoint": "s3.private.us-south.cloud-object-storage.appdomain.cloud",
      "target_crn": "crn:v1:bluemix:public:cloud-object-storage:global:a/<account-id>:<instance-id>::",
      "bucket": "my-activity-tracking-bucket",
      "service_to_service_enabled": true
    }
  }'
```
{: screen}



## Deleting a target using the API
{: #target-delete-api-cos}
{: api}

You can use the following cURL command to delete a target:

```text
curl -X DELETE <ENDPOINT>/api/v2/targets/<TARGET_ID> -H "Authorization:  $ACCESS_TOKEN" -H "content-type: application/json"
```
{: codeblock}

Where

- `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).
- `<TARGET_ID>` is the ID of the target.


For example, you can use the following cURL request to delete a target in US-South with the ID `00000000-0000-0000-0000-000000000000`:

```shell
curl -X DELETE https://private.us-south.atracker.cloud.ibm.com/api/v2/targets/00000000-0000-0000-0000-000000000000 -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json"
```
{: screen}

In the response, you get an empty result if the deletion was successful:

```json
{}
```
{: screen}


## Validating a target using the API
{: #target-validate-api-cos}
{: api}

You can use the following cURL command to validate a target by checking the credentials to write to the target.

```shell
curl -X POST <ENDPOINT>/api/v2/targets/<TARGET_ID>/validate -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json"
```
{: codeblock}

Where

- `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).
- `<TARGET_ID>` is the ID of the target.

For example, you can use the following cURL request to validate a target in US-South with the ID `00000000-0000-0000-0000-000000000000`:

```shell
curl -X POST https://private.us-south.atracker.cloud.ibm.com/api/v2/targets/<TARGETID>/validate -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json"
```
{: screen}

In the response, you get information in the section `cos_write_status`, for example:

```json
"write_status": {
    "status": "success"
  },
```
{: screen}


## Viewing a target using the API
{: #target-view-api-cos}
{: api}

You can use the following cURL command to view the configuration details of 1 target:

```shell
curl -X GET <ENDPOINT>/api/v2/targets/<TARGET_ID> -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json"
```
{: codeblock}

Where

- `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).
- `<TARGET_ID>` is the ID of the target.


For example, you can run the following cURL request to get information about a target with the ID `00000000-0000-0000-0000-000000000000`:

```shell
curl -X GET https://private.us-south.atracker.cloud.ibm.com/api/v2/targets/00000000-0000-0000-0000-000000000000 -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json"
```
{: screen}

Results will show if the target is COS (`"target_type": "cloud_object_storage"`) or an {{site.data.keyword.atracker_full_notm}} hosted event search offering (`"target_type": "logdna"`).

## Listing all targets using the API
{: #target-list-targets-cos}
{: api}

You can use the following cURL command to view all targets:

```shell
curl -X GET <ENDPOINT>/api/v2/targets -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json"
```
{: codeblock}

Where

- `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).


For example, you can run the following cURL request to get information about the targets that are defined in Dallas:

```shell
curl -X GET https://private.us-south.atracker.cloud.ibm.com/api/v2/targets -H "Authorization:  $ACCESS_TOKEN" -H "content-type: application/json"
```
{: screen}

Results will show if the target is a COS (`"target_type": "cloud_object_storage"`) target or an [{{site.data.keyword.atracker_full_notm}} hosted event search offering (`"target_type": "logdna"`) target}](/docs/atracker?topic=atracker-target_v2_at) target.


## HTTP response codes
{: #target-rc-api-cos}
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

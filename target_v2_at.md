---

copyright:
  years: 2022, 2024
lastupdated: "2024-01-18"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Managing {{site.data.keyword.at_full_notm}} hosted event search targets
{: #target_v2_at}

You can manage {{site.data.keyword.atracker_full}} hosted event search targets in your account by using the {{site.data.keyword.atracker_full_notm}} CLI, the {{site.data.keyword.atracker_full_notm}} REST API, and Terraform scripts. A target is a resource where you can collect auditing events.
{: shortdesc}


For more information on {{site.data.keyword.atracker_full_notm}} targets, see [Targets](/docs/atracker?topic=atracker-target_v2).


## IAM Access
{: #target_v2_iam_access_at}

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



## CLI prerequisites
{: #target_prereqs_at}
{: cli}

Before you use the CLI to manage targets, complete the following steps:

1. [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

2. [Install the {{site.data.keyword.atracker_full_notm}} CLI](/docs/atracker?topic=atracker-atracker-cli-config).

3. Log in to {{site.data.keyword.cloud_notm}}. Run the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)


## Creating an {{site.data.keyword.at_full_notm}} hosted event search offering target using the CLI
{: #target-create-cli-at}
{: cli}

Use this command to create an {{site.data.keyword.at_full_notm}} hosted event search offering target to be used to configure a destination for activity events.

```sh
ibmcloud atracker target create --name TARGET_NAME --type TARGET_TYPE ( [--file LOGDNA_ENDPOINT_DEFINITION_JSON_FILE] | ( [--target-crn LOGDNA_TARGET_CRN] [--ingestion-key LOGDNA_INGESTION_KEY] ) ) [--region REGION] [--output FORMAT]
```
{: pre}

### Command options
{: #target-create-options-at}

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--name TARGET_NAME`
:   The name to be given to the target.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--type TARGET_TYPE`
:   Set the `TARGET_TYPE` to `logdna` for an IBM Cloud Activity Tracker hosted event search offering target.

`--file @LOGDNA_ENDPOINT_DEFINITION_JSON_FILE`
:   A file containing an endpoint definition in the following format:

    ```json
    {
      "target_crn": "yyyyy",
      "ingestion_key": "xxxxxx"
    }
    ```
    {: codeblock}

`--target-crn LOGDNA_TARGET_CRN`
:   The CRN of the {{site.data.keyword.at_full_notm}} hosted event search offering instance.

`--ingestion-key LOGDNA_INGESTION_KEY`
:   `LOGDNA_INGESTION_KEY` is the ingestion key that will be used to gain access to the {{site.data.keyword.atracker_full_notm}} instance.

`--output FORMAT`
:   Currently support format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-create-example-at}

The following is an example using the **`ibmcloud atracker target create --name eu-de-logdna-target --type logdna --target-crn "crn:v1:bluemix:public:logdna:eu-de:a/11111111111111111111111111111111:22222222-2222-2222-2222-222222222222::" --ingestion-key xxxxxx`** command.

This example shows an example successful target creation.
{: note}

```text
OK
Target
Name:                eu-de-logdna-target
ID:                  cccccccc-cccc-cccc-cccc-cccccccccccc
CRN:                 crn:v1:bluemix:public:atracker:eu-de:a/11111111111111111111111111111111::target:cccccccc-cccc-cccc-cccc-cccccccccccc
Type:                logdna
LogDNA Target CRN:   crn:v1:bluemix:public:logdna:eu-de:a/11111111111111111111111111111111:22222222-2222-2222-2222-222222222222::
CreatedAt:           2022-05-06T18:59:26.760Z
UpdatedAt:           2022-05-06T18:59:26.760Z
```
{: screen}


## Updating an {{site.data.keyword.at_full_notm}} hosted event search offering target using the CLI
{: #target-update-cli-at}
{: cli}

Use this command to update an {{site.data.keyword.at_full_notm}} hosted event search offering target to be used to configure a destination for activity events.

```sh
ibmcloud atracker target update --target TARGET [--name TARGET_NAME] ( --file @LOGDNA_ENDPOINT_DEFINITION_JSON_FILE ) | (--target-crn LOGDNA_TARGET_CRN --ingestion-key LOGDNA_INGESTION_KEY )  [--region REGION] [--output FORMAT]
```
{: pre}

### Command options
{: #target-update-options-at}

`--target TARGET`
:   The ID or current target name.

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--name TARGET_NAME`
:   The name to be given to the target.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--file @LOGDNA_ENDPOINT_DEFINITION_JSON_FILE`
:   A file containing an endpoint definition in the following format:

    ```json
    {
      "target_crn": "yyyyy",
      "ingestion_key": "xxxxxx"
    }
    ```
    {: codeblock}

`--target-crn LOGDNA_TARGET_CRN`
:   The CRN of the {{site.data.keyword.at_full_notm}} hosted event search offering instance.

`--ingestion-key LOGDNA_INGESTION_KEY`
:   `LOGDNA_INGESTION_KEY` is the ingestion key for the {{site.data.keyword.atracker_full_notm}} instance.

`--output FORMAT`
:   Currently support format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-update-example-at}

The following is an example using the **`ibmcloud atracker target update --name eu-de-logdna-target --target-crn "crn:v1:bluemix:public:logdna:eu-de:a/11111111111111111111111111111111:22222222-2222-2222-2222-222222222222::" --ingestion-key xxxxxx`** command.

This example shows an example successful target update.
{: note}

```text
OK
Target
Name:                eu-de-logdna-target
ID:                  cccccccc-cccc-cccc-cccc-cccccccccccc
CRN:                 crn:v1:bluemix:public:atracker:eu-de:a/11111111111111111111111111111111::target:cccccccc-cccc-cccc-cccc-cccccccccccc
Type:                logdna
LogDNA Target CRN:   crn:v1:bluemix:public:logdna:eu-de:a/11111111111111111111111111111111:22222222-2222-2222-2222-222222222222::
CreatedAt:           2022-05-06T18:59:26.760Z
UpdatedAt:           2022-05-06T19:16:50.090Z
```
{: screen}

## Deleting a target using the CLI
{: #target-delete-cli-at}
{: cli}

Use this command to delete a target.

```sh
ibmcloud atracker target rm --target TARGET [--force]
```
{: pre}

### Command options
{: #target-rm-options-at}

`--target TARGET`
:   The ID or name of the target.

`--force` | `-f`
:   Will delete the target without providing the user with any additional prompt.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-rm-example-at}

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
{: #target-validate-cli-at}
{: cli}

Use this command to validate that a target is correctly configured for an {{site.data.keyword.atracker_full_notm}} region.

```sh
ibmcloud atracker target validate --target TARGET [--region REGION] [--output FORMAT]
```
{: pre}

### Command options
{: #target-validate-options-at}

`--target TARGET`
:   The ID or name of the target.

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output FORMAT`
:   Currently support format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-validate-example-at}

The following is an example using the **`ibmcloud atracker target validate --target new-target-name`** command.

This example shows a successfully validated {{site.data.keyword.at_full_notm}} hosted event search target.
{: note}

```text
TBD
```
{: screen}

## Getting information about a target using the CLI
{: #target-get-cli-at}
{: cli}

Use this command to get information about a target for an {{site.data.keyword.atracker_full_notm}} region.

```sh
ibmcloud atracker target get --target TARGET [--output FORMAT]
```
{: pre}

### Command options
{: #target-get-options-at}

`--target TARGET`
:   The ID or name of the target.

`--output FORMAT`
:   Currently support format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-get-example-at}

The following is an example using the **`ibmcloud atracker target get --target new-target-name`** command showing an {{site.data.keyword.at_full_notm}} hosted event search target.

```text
OK
Target
Name:                new-target-name
ID:                  cccccccc-cccc-cccc-cccc-cccccccccccc
CRN:                 crn:v1:bluemix:public:atracker:eu-de:a/11111111111111111111111111111111::target:cccccccc-cccc-cccc-cccc-cccccccccccc
Type:                logdna
LogDNA Target CRN:   crn:v1:bluemix:public:logdna:eu-de:a/11111111111111111111111111111111:22222222-2222-2222-2222-222222222222::
CreatedAt:           2022-05-06T18:59:26.760Z
UpdatedAt:           2022-05-06T19:16:50.090Z
```
{: screen}

## Listing all targets in a region
{: #target-list-cli-at}
{: cli}

Use this command to list the configured targets for an {{site.data.keyword.atracker_full_notm}} region.

```sh
ibmcloud atracker target ls [--output FORMAT]
```
{: pre}

### Command options
{: #target-options-at}

`--output FORMAT`
:   Currently support format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-example-at}

The following is an example using the **`ibmcloud atracker target ls`** command.

```text
Name                       ID                                     Region     Type                     Created
test-eu-de-target           xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx   eu-de   logdna     2022-02-26T06:53:13.466Z
```
{: screen}


## API targets and actions
{: #target-actions-api-at}
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

For more information about the REST API, see [Targets](/apidocs/atracker#create-target){: external}.
{: note}


## API prerequisites
{: #target-prereqs-api-at}
{: api}

To make API calls to manage targets, complete the following steps:
1. Get an IAM access token. For more information, see [Retrieving IAM access tokens](/docs/atracker?topic=atracker-retrieve-iam-token).
2. Identify the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).





## Creating an {{site.data.keyword.at_full_notm}} hosted event search offering target using the API
{: #target-create-api-at-at}
{: api}

You can use the following cURL command to create an {{site.data.keyword.at_full_notm}} hosted event search offering target:

```shell
curl -X POST <ENDPOINT>/api/v2/targets
  -H "Authorization: Bearer IAM_TOKEN"
  -H 'content-type: application/json'
  -d '{
       "name": "TARGET_NAME",
       "target_type": "TARGET_TYPE",
       "logdna_endpoint": {
         "target_crn": "TARGET_CRN",
         "ingestion_key": "TARGET_KEY"
        }
      }
```
{: codeblock}

Where

- `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).
- `TARGET_NAME` is the name of the target. The maximum length of the name is 256 characters.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

- `TARGET_TYPE` is the type of the target. The valid type is `logdna`.
- `logdna_endpoint` includes information about the target. This includes the CRN of the {{site.data.keyword.at_full_notm}} hosted event search offering instance and the ingestion key of the instance.

    `TARGET_CRN` indicates the [CRN](/docs/account?topic=account-crn) of the {{site.data.keyword.atracker_full_notm}} instance.

    `TARGET_KEY` is the ingestion key for the {{site.data.keyword.atracker_full_notm}} instance.


For example, you can use the following cURL request to create a target in Dallas:

```shell
curl -X POST https://private.us-south.atracker.cloud.ibm.com/api/v2/targets -H "Authorization:  $ACCESS_TOKEN" -H "content-type: application/json" -d '{
     "name": "a-target-us-south",
       "target_type": "logdna",
         "logdna_endpoint": {
           "target_crn": "crn:v1:staging:public:logdna:us-south:a/11111111111111111111111111111111:22222222-2222-2222-2222-222222222222::",
           "ingestion_key": "xxxxxxxxxxxxxxxxxx"
    }
  }'
```
{: screen}

In the response, you get information about the target such as the `id`, that indicates the GUID of the target, and the `crn`, that indicates the CRN of the target.




## Updating an {{site.data.keyword.at_full_notm}} hosted event search offering target
{: #target-update-at-api-at}
{: api}

When you update an {{site.data.keyword.at_full_notm}} hosted event search offering target, you must include the target information in the data section of the request.
- You must pass all fields.
- Update the fields that need to be changed.

You can use the following cURL command to update an {{site.data.keyword.at_full_notm}} hosted event search offering target:

```shell
curl -X PUT <ENDPOINT>/api/v2/targets
  -H "Authorization: Bearer IAM_TOKEN"
  -H 'content-type: application/json'
  -d '{
       "name": "TARGET_NAME",
       "target_type": "TARGET_TYPE",
       "logdna_endpoint": {
         "target_crn": "TARGET_CRN",
         "ingestion_key": "TARGET_KEY"
        }
      }'
```
{: codeblock}

Where

- `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).
- `TARGET_NAME` is the name of the target. The maximum length of the name is 256 characters.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

- `TARGET_TYPE` is the type of the target. The valid type is `logdna`.
- `logdna_endpoint` includes information about the target. This includes the CRN of the {{site.data.keyword.at_full_notm}} hosted event search offering instance and the ingestion key of the instance.

    `TARGET_CRN` indicates the [CRN](/docs/account?topic=account-crn) of the {{site.data.keyword.atracker_full_notm}} instance.

    `TARGET_KEY` is the ingestion key for the {{site.data.keyword.atracker_full_notm}} instance.


For example, you can use the following cURL request to update a target in Dallas:

```shell
curl -X PUT https://private.us-south.atracker.cloud.ibm.com/api/v2/targets -H "Authorization:  $ACCESS_TOKEN" -H "content-type: application/json" -d '{
     "name": "a-target-us-south",
       "target_type": "logdna",
         "logdna_endpoint": {
           "target_crn": "crn:v1:staging:public:logdna:us-south:a/11111111111111111111111111111111:22222222-2222-2222-2222-222222222222::",
           "ingestion_key": "xxxxxxxxxxxxxxxxxx"
    }
  }'
```
{: screen}


## Deleting a target using the API
{: #target-delete-api-at}
{: api}

You can use the following cURL command to delete a target:

```text
curl -X DELETE <ENDPOINT>/api/v2/targets/TARGET_ID -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json"
```
{: codeblock}

Where

- `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).
- `TARGET_ID` is the ID of the target.


## Validating a target using the API
{: #target-validate-api-at}
{: api}

You can use the following cURL command to validate a target by checking the credentials to write to the target.

```shell
curl -X POST <ENDPOINT>/api/v2/targets/TARGET_ID/validate -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json"
```
{: codeblock}

Where

- `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).
- `TARGET_ID` is the ID of the target.

For example, you can use the following cURL request to validate a target in US-South:

```shell
curl -X POST https://private.us-south.atracker.cloud.ibm.com/api/v2/targets/<TARGET_ID>/validate   -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json"
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
{: #target-view-api-at}
{: api}

You can use the following cURL command to view the configuration details of 1 target:

```shell
curl -X GET <ENDPOINT>/api/v2/targets/TARGET_ID -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json"
```
{: codeblock}

Where

- `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).
- `TARGET_ID` is the ID of the target.


For example, you can run the following cURL request to get information about a target with the ID `00000000-0000-0000-0000-000000000000`:

```shell
curl -X GET https://private.us-south.atracker.cloud.ibm.com/api/v2/targets/00000000-0000-0000-0000-000000000000 -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json"
```
{: screen}

Results will show if the target is a [COS (`"target_type": "cloud_object_storage"`)](/docs/atracker?topic=atracker-target_v2_cos) target or an {{site.data.keyword.at_full_notm}} hosted event search offering (`"target_type": "logdna"`) target.

## Listing all targets using the API
{: #target-list-targets-at}
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
curl -X GET https://private.us-south.atracker.cloud.ibm.com/api/v2/targets -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json"
```
{: screen}

Results will show if the target is COS (`"target_type": "cloud_object_storage"`) or an {{site.data.keyword.at_full_notm}} hosted event search offering (`"target_type": "logdna"`).


## HTTP response codes
{: #target-rc-api-at}
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


## Creating an {{site.data.keyword.at_full_notm}} hosted event search offering target using the UI
{: #target-create-ui-at}
{: ui}

Only resources in your account are listed and selectable. To specify a resource in a different account, select **Specify CRN** under **Choose destination**.
{: important}

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.
2. Click the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg) &gt; **Observability**.
3. Select **Activity Tracker**.
4. Select **Routing**.
5. Select **Targets**.
6. Click **Create** to open the create panel.
7. **Choose type**: Click **Activity Tracker**.
8. **Choose destination**: Pick **Search by instance** or **Specify CRN**
    - **Search by instance**: Select an {{site.data.keyword.at_full_notm}} hosted event search instance from the table or click **Create** to create a new {{site.data.keyword.at_full_notm}} hosted event search instance.
    - **Specify CRN**: Enter the Cloud Resource Name (CRN) of the {{site.data.keyword.at_full_notm}} hosted event search instance. If you want to target an instance in a different account, you must specify the CRN.
9. **Ingestion key**: Select or enter the ingestion key for the targeted {{site.data.keyword.at_full_notm}} hosted event search instance.
10. **Target name**: Enter a meaningful name for the target.
11. **Target region**: Select the region that will process the event data.
12. Toggle **Set as default target** to automatically set your new target as a default target in your {{site.data.keyword.atracker_full_notm}} settings. See [the default targets documentation](/docs/atracker?topic=atracker-planning#planning-4) for more details.
13. Click **Create target**.


## Updating an {{site.data.keyword.at_full_notm}} hosted event search offering target using the UI
{: #target-update-ui-at}
{: ui}

Only resources in your account are listed and selectable. To specify a resource in a different account, select **Specify CRN** under **Choose destination**.
{: important}

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.
2. Click the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg) &gt; **Observability**.
3. Select **Activity Tracker**.
4. Select **Routing**.
5. Select **Targets**.
6. Determine which target to update and click the ![Actions icon](../icons/action-menu-icon.svg "Actions").
7. Click **Unset as default** to remove your target as a default target in your {{site.data.keyword.atracker_full_notm}} settings. See [the default targets documentation](/docs/atracker?topic=atracker-planning#planning-4) for more details.
8. Click **Edit** to open the update panel.
9. **Details**: Click **Edit** to update your target's name or region. You can also toggle **Default target** to add or remove your target as a default target in your {{site.data.keyword.atracker_full_notm}} settings.
10. Click **Save** to update your target.
11. **Destination**: Click **Edit** to change the {{site.data.keyword.at_full_notm}} hosted event search instance and ingestion key associated with your target.
12. Click **Save** to update your target.

## Deleting a target using the UI
{: #target-delete-ui-at}
{: ui}

You cannot delete an {{site.data.keyword.atracker_full_notm}} target if it is used in a route or as a default target setting.
{: important}

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.
2. Click the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg) &gt; **Observability**.
3. Select **Activity Tracker**.
4. Select **Routing**.
5. Select **Targets**.
6. Determine which target to delete and click the ![Actions icon](../icons/action-menu-icon.svg "Actions").
7. Click **Delete** and then click **Delete** in the confirmation panel.


## Listing all targets in a region
{: #target-list-ui-at}
{: ui}

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.
2. Click the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg) &gt; **Observability**.
3. Select **Activity Tracker**.
4. Select **Routing**.
5. Select **Targets**.

The table details:
- Target type
- Destination name
- Destination region
- **Routes**: If it is used in any routes
- **Target status**:
    - **Active**: The target is working as expected
    - **Error**: The target is misconfigured and events will not be routed to the destination. Update your target details or destination to fix the target configuration or delete the target if it is no longer needed

---

copyright:
  years:  2021, 2025
lastupdated: "2025-07-23"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Managing {{site.data.keyword.logs_full_notm}} targets
{: #target_v2_icl}

You can manage {{site.data.keyword.logs_full_notm}} targets in your account by using the {{site.data.keyword.atracker_full_notm}} CLI, the {{site.data.keyword.atracker_full_notm}} REST API, and Terraform scripts. A target is a resource where you can collect auditing events.
{: shortdesc}

For more information on {{site.data.keyword.atracker_full_notm}} targets, see [Targets](/docs/atracker?topic=atracker-target_v2).



## About {{site.data.keyword.logs_full_notm}} targets
{: #target_v2_icl_targets}

If you are using an {{site.data.keyword.logs_full_notm}} target, you can use the same {{site.data.keyword.logs_full_notm}} instance for collecting auditing events in your account across multiple regions.  In that scenario events are forwarded to the target region before being routed to the {{site.data.keyword.logs_full_notm}} instance.  You may consider defining a {{site.data.keyword.logs_full_notm}} instance in each region to improve performance and reduce network latency.
{: important}

## IAM Access
{: #target_v2_iam_access_icl}

You must grant users IAM permissions to manage targets. For more information, see [Assign access to resources](/docs/account?topic=account-assign-access-resources).

When you define a policy, you can indicate the scope of the permissions. You can choose from granting permissions for a specific region or for the entire account.

If you have the IAM permission to create policies and authorizations, you can grant only the level of access that you have as a user of the target service. For example, if you have viewer access for the target service, you can assign only the viewer role for the authorization. If you attempt to assign a higher permission such as administrator, it might appear that permission is granted, however, only the highest level permission you have for the target service, that is viewer, will be assigned. 
{: important}

Users with regional scope will be limited to access targets in their authorized region.
{: note}



| IAM action               | IAM Policy scope  | IAM Roles                          | Description         |
| ------------------------ | ----------------- | ---------------------------------- | -------------- |
| `atracker.target.read`   | Region            | `Administrator`  \n `Editor`  \n `Viewer`  \n `Operator` | Read (view) information about a target |
| `atracker.target.create` | Region            | `Administrator`  \n `Editor` | Create a target |
| `atracker.target.update` | Region            | `Administrator`  \n `Editor` | Update a target |
| `atracker.target.delete` | Region            | `Administrator`  \n `Editor` | Delete a target |
| `atracker.target.list`   | Account           | `Administrator`  \n `Editor`  \n `Viewer`  \n `Operator` | List all targets |
{: caption="IAM actions and the IAM roles that include them."}

## Authentication
{: #target_v2_icl_auth_opts}

When writing to a {{site.data.keyword.logs_full_notm}} target you can use the following options to authenticate to an {{site.data.keyword.logs_full_notm}} you must configure service-to-service (S2S) authorization between {{site.data.keyword.atracker_full_notm}} and {{site.data.keyword.logs_full_notm}}.

## CLI prerequisites
{: #target_prereqs_icl}
{: cli}

Before you use the CLI to manage targets, complete the following steps:

1. [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

2. [Install the {{site.data.keyword.atracker_full_notm}} CLI](/docs/atracker?topic=atracker-atracker-cli-config).

3. Log in to {{site.data.keyword.cloud_notm}}. Run the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)

## Configuring S2S authorization using the UI witihin the same account
{: #target_v2_icl_s2s_ui}
{: ui}

Do the following to configure a service-to-service authorization using the {{site.data.keyword.cloud_notm}} UI.

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external} as the account owner that will be configuring {{site.data.keyword.atracker_full_notm}} targets.

	After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} dashboard opens.

2. Click **Manage** &gt; **Access (IAM)**.  **Manage access and users** is displayed.

3. Click **Authorizations**.

4. Click **Create**.

5. For **Source service** select *Activity Tracker* and for **How do you want to scope the access?** select *All resources*.

6. For **Target service** select *{{site.data.keyword.logs_full_notm}}* for **How do you want to scope the access?** select *Resources based on selected attributes*.

7. Select **Service instance** and **string equals** the name of your {{site.data.keyword.logs_full_notm}} instance.

8. For **Service access** select **Sender**.

9. Click **Authorize**.  Your new service-to-service authorization will be listed in the **Manage authorizations** view.

## Configuring S2S authorization using the CLI
{: #target_v2_icl_s2s_cli}
{: cli}

Do the following to configure a service-to-service authorization using the {{site.data.keyword.cloud_notm}} CLI.

1. [Log in to your {{site.data.keyword.cloud_notm}} account](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login) as the account owner that will be configuring {{site.data.keyword.atracker_full_notm}} authorization.

2. Create an authorization policy defining your service-to-service authorization.

   ```sh
   ibmcloud iam authorization-policy-create atracker cloud-logs "Sender" [--target-service-instance-id <CLOUD_LOGS_SERVICE_INSTANCE>
   ```
   {: pre}

## Configuring S2S authorization using the API
{: #target_v2_icl_s2s_api}
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
               "role_id": "crn:v1:bluemix:public:iam::::serviceRole:Sender"
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
                       "value": "cloud-logs"
                   },
                   {
                       "name": "serviceInstance",
                       "value": "CLOUD_LOGS_SERVICE_INSTANCE"
                   }
               ]
           }
       ]
   }
   ```
   {: codeblock}

   Where:

   `CUSTOMER_ACCOUNT_ID` is the account GUID for the account that will be configuring targets.  This can be found by using the [`ibmcloud account list`](/docs/cli?topic=cli-ibmcloud_commands_account#ibmcloud_account_list) command.

   `CLOUD_LOGS_SERVICE_INSTANCE` is the instance ID of the {{site.data.keyword.logs_full_notm}} instance.

3. Get an IAM access token. For more information, see [Retrieving IAM access tokens](/docs/atracker?topic=atracker-retrieve-iam-token).

4. Run the following command to configure your service-to-service authorization:

   ```sh
   curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header "Authorization: $ACCESS_TOKEN" -d @authorization_policy_resource.json "https://iam.cloud.ibm.com/v1/policies"
   ```
   {: pre}



## Creating a {{site.data.keyword.logs_full_notm}} target using the CLI
{: #target-create-cli-icl}
{: cli}

Use this command to create a {{site.data.keyword.logs_full_notm}} target to be used to configure a destination for activity events.

```sh
 ibmcloud atracker target create --name TARGET_NAME --type TARGET_TYPE ( [--file CLOUD_LOGS_ENDPOINT_DEFINITION_JSON_FILE] |  ( [--target-crn CLOUD_LOGS_TARGET_CRN] [--region REGION] [--output FORMAT]
```
{: pre}

### Command options
{: #target-create-options-icl}

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--name TARGET_NAME`
:   The name to be given to the target.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--type TARGET_TYPE`
:   Set the `TARGET_TYPE` to `cloud_logs` for a {{site.data.keyword.logs_full_notm}} target.

`--file @CLOUD_LOGS_ENDPOINT_DEFINITION_JSON_FILE`
:   A file containing an endpoint definition in the following format:

    ```json
    {
      "target_crn": "yyyyy",
    }
    ```
    {: codeblock}

`--target-crn CLOUD_LOGS_TARGET_CRN`
:   The CRN of the {{site.data.keyword.logs_full_notm}} instance.



`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-create-example-icl}

The following is an example using the **`ibmcloud atracker target create --name my-target --type cloud_logs --target-crn crn:v1:staging:public:logs:global:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx::`** command.

This example shows an example successful target creation.
{: note}

```text
OK
Target
Name:                    my-target
ID:                      000000000-00000000-0000-0000-00000000
CRN:                     crn:v1:staging:public:atracker:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx
Region:                  us-south
Type:                    cloud_logs
Cloud Logs Target CRN:   crn:v1:staging:public:logs:global:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx:
Write Status:            success
CreatedAt:               2024-05-31T19:03:35.427Z
UpdatedAt:               2024-05-31T19:03:35.427Z
```
{: screen}


## Updating a {{site.data.keyword.logs_full_notm}} target using the CLI
{: #target-update-cli-icl}
{: cli}

Use this command to update a {{site.data.keyword.logs_full_notm}} target for an {{site.data.keyword.atracker_full_notm}} region.  Any specified value that is different from when the target was originally created will be updated to the value specified in the command.

```sh
ibmcloud atracker target update --target TARGET [--name TARGET_NAME] [ [--file CLOUD_LOGS_ENDPOINT_DEFINITION_JSON_FILE] |  [--target-crn CLOUD_LOGS_TARGET_CRN]]] [--output FORMAT]
```
{: pre}

### Command options
{: #target-update-options-icl}

`--target TARGET`
:   The ID or current target name.

`--name TARGET_NAME`
:   The name to be given to the target.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--file @CLOUD_LOGS_ENDPOINT_DEFINITION_JSON_FILE`
:   A file containing an endpoint definition in the following format:

    ```json
    {
      "target_crn": "yyyyy",
    }
    ```
    {: codeblock}

`--target-crn CLOUD_LOGS_TARGET_CRN`
:   The CRN of the {{site.data.keyword.logs_full_notm}} instance.



`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-update-example-icl}

The following is an example using the **`ibmcloud atracker target update --target my-target --name new-target-name`** command.

```text
OK
Target
Name:                    new-target-name
ID:                      000000000-00000000-0000-0000-00000000
CRN:                     crn:v1:staging:public:atracker:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx
Region:                  us-south
Type:                    cloud_logs
Cloud Logs Target CRN:   crn:v1:staging:public:logs:global:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx:
Write Status:            success
Created:                 2024-05-31T19:03:35.427Z
Updated:                 2024-05-31T19:03:35.427Z
```
{: screen}

## Deleting a target using the CLI
{: #target-delete-cli-icl}
{: cli}

Use this command to delete a target.

```sh
ibmcloud atracker target rm --target TARGET [--force]
```
{: pre}

### Command options
{: #target-rm-options-icl}

`--target TARGET`
:   The ID or name of the target.

`--force` | `-f`
:   Will delete the target without providing the user with any additional prompt.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-rm-example-icl}

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
{: #target-validate-cli-icl}
{: cli}

Use this command to validate that a target is correctly configured for an {{site.data.keyword.atracker_full_notm}} region.

```sh
ibmcloud atracker target validate --target TARGET [--region REGION] [--output FORMAT]
```
{: pre}

### Command options
{: #target-validate-options-icl}

`--target TARGET`
:   The ID or name of the target.

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-validate-example-icl}

The following is an example using the **`ibmcloud atracker target validate --target new-target-name`** command.

This example shows a successfully validated ICL target.
{: note}

```text
Target
Name:                       new-target-name
ID:                         xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
CRN:                        crn:v1:staging:public:atracker:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx
Type:                       cloud_logs
Cloud Logs Target CRN:      crn:v1:staging:public:logs:global:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx:
Service to Service Enabled:	true
Write Status:               success
Created:                    2021-07-21T16:04:15.174Z
Updated:                    2021-07-21T17:49:56.452Z
```
{: screen}

## Getting information about a target using the CLI
{: #target-get-cli-icl}
{: cli}

Use this command to get information about a target for an {{site.data.keyword.atracker_full_notm}} region.

```sh
ibmcloud atracker target get --target TARGET [--output FORMAT]
```
{: pre}

### Command options
{: #target-get-options-icl}

`--target TARGET`
:   The ID or name of the target.

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-get-example-icl}

The following is an example using the **`ibmcloud atracker target get --target new-target-name`** command showing a {{site.data.keyword.logs_full_notm}} target.

```text
Target
Name:                       new-target-name
ID:                         xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
CRN:                        crn:v1:staging:public:atracker:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx
Type:                       cloud_logs
Cloud Logs Target CRN:      crn:v1:staging:public:logs:global:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx:
Service to Service Enabled: true
Write Status:               success
Created:                    2024-06-02T16:04:15.174Z
Updated:                    2024-06-05T17:49:56.452Z
```
{: screen}

## Listing all targets in a region
{: #target-list-cli-icl}
{: cli}

Use this command to list the configured targets for an {{site.data.keyword.atracker_full_notm}} region.

```sh
ibmcloud atracker target ls [--output FORMAT]
```
{: pre}

### Command options
{: #target-options-icl}

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-example-icl}

The following is an example using the **`ibmcloud atracker target ls`** command.

```text
Name                       ID                                     Region     Type                Created
target-01                  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx   us-south   cloud_logs          2020-11-18T03:52:08.603Z
```
{: screen}


## API targets and actions
{: #target-actions-api-icl}
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
{: caption="Target actions by using the {{site.data.keyword.atracker_full_notm}} REST API" caption-side="top"}

You can use private and public endpoints to manage targets. For more information about the list of `ENDPOINTS` that are available, see [Endpoints](/docs/atracker?topic=atracker-endpoints).


* You can manage targets from the private network using an API endpoint with the following format: `https://private.REGION.atracker.cloud.ibm.com`
* You can manage targets from the public network using an API endpoint with the following format: `https://REGION.atracker.cloud.ibm.com`

* You can disable the public endpoints by updating the account settings. For more information, see [Configuring target and region settings](/docs/atracker?topic=atracker-settings).

For more information about the REST API, see [Targets](/apidocs/atracker#create-target).
{: note}


## API prerequisites
{: #target-prereqs-api-icl}
{: api}

To make API calls to manage targets, complete the following steps:
1. Get an IAM access token. For more information, see [Retrieving IAM access tokens](/docs/atracker?topic=atracker-retrieve-iam-token).
2. Identify the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).

## Creating a {{site.data.keyword.logs_full_notm}} target using the API
{: #target-create-api-icl}
{: api}

You can use the following cURL command to create a {{site.data.keyword.logs_full_notm}} target:

```shell
curl -X POST  <ENDPOINT>/api/v2/targets   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"   -d '{
    "name": "TARGET_NAME",
    "target_type": "cloud_logs",
    "cloudlogs_endpoint": {
      "target_crn": "CLOUD_LOGS_CRN"
    }
  }'
```
{: codeblock}

Where

- `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).
- `TARGET_NAME` is the name of the target. The maximum length of the name is 256 characters.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

- `TARGET_TYPE` is the type of the target.
- `cloudlogs_endpoint` includes information about the target.

    `CLOUD_LOGS_CRN` indicates the [CRN](/docs/account?topic=account-crn) of the {{site.data.keyword.logs_full_notm}} instance.

    

For example, you can use the following cURL request to create a target in Dallas:

```shell
curl -X POST   https://private.us-south.atracker.cloud.ibm.com/api/v2/targets   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"   -d '{
    "name": "My CLOUD LOGS target",
    "target_type": "cloud_logs",
    "cloudlogs_endpoint": {
      "target_crn": "crn:v1:bluemix:public:logs:us-south:a/<account-id>:<instance-id>::"
    }
  }'
```
{: screen}

In the response, you get information about the target such as the `id`, that indicates the GUID of the target, and the `crn`, that indicates the CRN of the target.


## Updating a {{site.data.keyword.logs_full_notm}} target using the API
{: #target-update-api-icl}
{: api}

When you update an {{site.data.keyword.logs_full_notm}} target, you must include the target information in the data section of the request.
- You must pass all fields.
- Update the fields that need to be changed.
- You cannot change the `target_type` of a target once created.

You can use the following cURL command to update a target:

```shell
curl -X PUT  <ENDPOINT>/api/v2/targets/TARGET_ID  -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"   -d '{
    "name": "TARGET_NAME",
    "target_type": "cloud_logs",
    "cloudlogs_endpoint": {
      "target_crn": "CLOUD_LOGS_CRN"
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

- `TARGET_TYPE` is the type of the target. Set the value to `cloud_logs` for a {{site.data.keyword.logs_full_notm}} target.
- `cloudlogs_endpoint` includes information about the target. 

    `CLOUD_LOGS_CRN` indicates the [CRN](/docs/account?topic=account-crn) of the {{site.data.keyword.logs_full_notm}} instance.




For example, you can use the following cURL request to update a target in Dallas:

```shell
curl -X PUT   https://private.us-south.atracker.cloud.ibm.com/api/v2/targets/TARGET_ID   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"   -d '{
    "name": "My new CLOUD LOGS target name",
    "target_type": "cloud_logs",
    "cloudlogs_endpoint": {
      "target_crn": "crn:v1:bluemix:public:logs:us-south:a/<account-id>:<instance-id>::"
    }
  }'
```
{: screen}



## Deleting a target using the API
{: #target-delete-api-icl}
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
{: #target-validate-api-icl}
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

In the response, you get information in the section `write_status`, for example:

```json
"write_status": {
    "status": "success"
  },
```
{: screen}


## Viewing a target using the API
{: #target-view-api-icl}
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

Results will show if the target is COS (`"target_type": "cloud_object_storage"`), or {{site.data.keyword.logs_full_notm}} offering (`"target_type": "cloud_logs"`)

## Listing all targets using the API
{: #target-list-targets-icl}
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

Results will show if the target is COS (`"target_type": "cloud_object_storage"`), or {{site.data.keyword.logs_full_notm}} offering (`"target_type": "cloud_logs"`)


## HTTP response codes
{: #target-rc-api-icl}
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
{: caption="List of HTTP response codes" caption-side="top"}


## Creating a {{site.data.keyword.logs_full_notm}} target using the UI
{: #target-create-ui-icl}
{: ui}

Only resources in your account are listed and selectable. To specify a resource in a different account, select **Specify CRN** under **Choose destination**.
{: important}

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.
2. Click the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg) &gt; **Observability**.
3. Select **Activity Tracker**.
4. Select **Routing**.
5. Select **Targets**.
6. Click **Create** to open the create panel.
7. **Choose type**: Click **Cloud Logs**.
8. **Service authorization required**: Service authorization is required to allow {{site.data.keyword.atracker_full_notm}} to communicate with {{site.data.keyword.logs_full_notm}}. Click **Authorize now** to create the policy automatically or click **Grant access in IAM**.
9.  **Choose destination**: Pick **Search by instance** or **Specify CRN**
    - **Search by instance**: Select an {{site.data.keyword.logs_full_notm}} instance from the table or click **Create** to create a new {{site.data.keyword.logs_full_notm}} instance.


- **Target name**: Enter a meaningful name for the target.
- **Target region**: Select the region that will process the event data.
- Toggle **Set as default target** to automatically set your new target as a default target in your {{site.data.keyword.atracker_full_notm}} settings. See [the default targets documentation](/docs/atracker?topic=atracker-planning#planning-4) for more details.
- Click **Create target**.


## Updating a {{site.data.keyword.logs_full_notm}} target using the UI
{: #target-update-ui-icl}
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
9.  **Details**: Click **Edit** to update your target's name or region. You can also toggle **Default target** to add or remove your target as a default target in your {{site.data.keyword.atracker_full_notm}} settings.
10. Click **Save** to update your target.
11. **Destination**: Click **Edit** to change the {{site.data.keyword.logs_full_notm}} instance associated with your target.


12. Click **Save** to update your target.

## Deleting a target using the UI
{: #target-delete-ui-icl}
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


## Listing all targets in a region using the UI
{: #target-list-ui-icl}
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
    - **Error**: The target is miscosfigured and events will not be routed to the destination. Update your target details or destination to fix the target configuration or delete the target if it is no longer needed

---

copyright:
  years:  2021, 2026
lastupdated: "2026-06-30"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Managing {{site.data.keyword.appconfig_notm}} targets
{: #target_v2_appconf}

You can manage {{site.data.keyword.appconfig_notm}} targets in your account by using the {{site.data.keyword.atracker_full_notm}} CLI, the {{site.data.keyword.atracker_full_notm}} REST API, and Terraform scripts. A target is a resource where you can collect auditing events.
{: shortdesc}

For more information on {{site.data.keyword.atracker_full_notm}} targets, see [Targets](/docs/atracker?topic=atracker-target_v2).



## About {{site.data.keyword.appconfig_notm}} targets
{: #target_v2_appconf_targets}

If you are using an {{site.data.keyword.appconfig_notm}} target, you can use the same {{site.data.keyword.appconfig_notm}} instance for collecting auditing events in your account across multiple regions.  In that scenario events are directly sent to the {{site.data.keyword.appconfig_notm}} instance from source regions.

You may consider defining an {{site.data.keyword.appconfig_notm}} instance in each region to improve performance and reduce network latency.
{: important}

{{site.data.keyword.appconfig_notm}} targets cannot be configured as default targets in settings. Use routes and rules to configure a {{site.data.keyword.appconfig_notm}} type of target as the destination.
{: important}

## IAM Access
{: #target_v2_iam_access_appconf}

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
{: #target_v2_appconf_auth_opts}

When writing to an {{site.data.keyword.appconfig_notm}} target, you must configure service-to-service (S2S) authorization between {{site.data.keyword.atracker_full_notm}} and {{site.data.keyword.appconfig_notm}}.

You must grant the `Configuration Update Reporter` role for the {{site.data.keyword.appconfig_notm}} instance.

## CLI prerequisites
{: #target_prereqs_appconf}
{: cli}

Before you use the CLI to manage targets, complete the following steps:

1. [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

2. [Install the {{site.data.keyword.atracker_full_notm}} CLI](/docs/atracker?topic=atracker-atracker-cli-config).

3. Log in to {{site.data.keyword.cloud_notm}}. Run the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)

## Configuring S2S authorization using the UI within the same account
{: #target_v2_appconf_s2s_ui}
{: ui}

Do the following to configure a service-to-service authorization using the {{site.data.keyword.cloud_notm}} UI.

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external} as the account owner that will be configuring {{site.data.keyword.atracker_full_notm}} targets.

	After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} dashboard opens.

2. Select **Manage** > **Access (IAM) > Authorizations**.

3. Click **Create**.

4. For **Source service**, select *Activity Tracker* and for **How do you want to scope the access?**, select *All resources*.

5. For **Target service** select *App Configuration* and for **How do you want to scope the access?**, select *Resources based on selected attributes*.

6. Select **Service instance** and **string equals**. Set the name of your {{site.data.keyword.appconfig_notm}} instance.

7. For **Service access**, select the **Manager** and **Configuration Update Reporter** roles.

8. Click **Authorize**.  Your new service-to-service authorization will be listed in the **Manage authorizations** view.



## Configuring S2S authorization using the CLI
{: #target_v2_appconf_s2s_cli}
{: cli}

Do the following to configure a service-to-service authorization using the {{site.data.keyword.cloud_notm}} CLI.

1. [Log in to your {{site.data.keyword.cloud_notm}} account](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login) as the account owner that will be configuring {{site.data.keyword.atracker_full_notm}} authorization.

2. Create an authorization policy defining your service-to-service authorization.

   ```sh
   ibmcloud iam authorization-policy-create atracker apprapp "ConfigurationUpdateReporter" [--target-service-instance-id <APPCONFIG_SERVICE_INSTANCE>
   ```
   {: pre}

## Configuring S2S authorization using the API
{: #target_v2_appconf_s2s_api}
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
               "role_id": "crn:v1:bluemix:public:iam::::serviceRole:ConfigurationUpdateReporter"
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
                       "value": "apprapp"
                   },
                   {
                       "name": "serviceInstance",
                       "value": "APPCONFIG_SERVICE_INSTANCE"
                   }
               ]
           }
       ]
   }
   ```
   {: codeblock}

   Where:

   `CUSTOMER_ACCOUNT_ID` is the account GUID for the account that will be configuring targets.  This can be found by using the [`ibmcloud account list`](/docs/cli?topic=cli-ibmcloud_commands_account#ibmcloud_account_list) command.

   `APPCONFIG_SERVICE_INSTANCE` is the instance ID of the {{site.data.keyword.appconfig_notm}} instance.

3. Get an IAM access token. For more information, see [Retrieving IAM access tokens](/docs/atracker?topic=atracker-retrieve-iam-token).

4. Run the following command to configure your service-to-service authorization:

   ```sh
   curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header "Authorization: $ACCESS_TOKEN" -d @authorization_policy_resource.json "https://iam.cloud.ibm.com/v1/policies"
   ```
   {: pre}



## Creating an {{site.data.keyword.appconfig_notm}} target using the CLI
{: #target-create-cli-appconf}
{: cli}

Use this command to create an {{site.data.keyword.appconfig_notm}} target to be used to configure a destination for activity events.

```sh
 ibmcloud atracker target create --name TARGET_NAME --type TARGET_TYPE ( [--file APPCONFIG_ENDPOINT_DEFINITION_JSON_FILE] | ( [--target-crn APPCONFIG_TARGET_CRN] ) ) [--region REGION] [--output FORMAT]
```
{: pre}

### Command options
{: #target-create-options-appconf}

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--name TARGET_NAME`
:   The name to be given to the target.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--type TARGET_TYPE`
:   Set the `TARGET_TYPE` to `app_config` for an {{site.data.keyword.appconfig_notm}} target.

`--file @APPCONFIG_ENDPOINT_DEFINITION_JSON_FILE`
:   A file containing an endpoint definition in the following format:

    ```json
    {
      "target_crn": "yyyyy"
    }
    ```
    {: codeblock}

`--target-crn APPCONFIG_TARGET_CRN`
:   The CRN of the {{site.data.keyword.appconfig_notm}} instance.

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-create-example-appconf}

The following is an example using the **`ibmcloud atracker target create --name my-target --type app_config --target-crn crn:v1:bluemix:public:apprapp:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx::`** command.

This example shows an example successful target creation.
{: note}

```text
OK
Target
Name:                         my-target
ID:                           000000000-00000000-0000-0000-00000000
CRN:                          crn:v1:bluemix:public:atracker:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx
Region:                       us-south
Type:                         app_config
App Configuration Target CRN: crn:v1:bluemix:public:apprapp:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx::
Write Status:                 success
CreatedAt:                    2024-05-31T19:03:35.427Z
UpdatedAt:                    2024-05-31T19:03:35.427Z
```
{: screen}


## Updating an {{site.data.keyword.appconfig_notm}} target using the CLI
{: #target-update-cli-appconf}
{: cli}

Use this command to update an {{site.data.keyword.appconfig_notm}} target for an {{site.data.keyword.atracker_full_notm}} region.  Any specified value that is different from when the target was originally created will be updated to the value specified in the command.

```sh
ibmcloud atracker target update --target TARGET [--name TARGET_NAME] [ [--file APPCONFIG_ENDPOINT_DEFINITION_JSON_FILE] | [--target-crn APPCONFIG_TARGET_CRN]] [--output FORMAT]
```
{: pre}

### Command options
{: #target-update-options-appconf}

`--target TARGET`
:   The ID or current target name.

`--name TARGET_NAME`
:   The name to be given to the target.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--file @APPCONFIG_ENDPOINT_DEFINITION_JSON_FILE`
:   A file containing an endpoint definition in the following format:

    ```json
    {
      "target_crn": "yyyyy"
    }
    ```
    {: codeblock}

`--target-crn APPCONFIG_TARGET_CRN`
:   The CRN of the {{site.data.keyword.appconfig_notm}} instance.

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-update-example-appconf}

The following is an example using the **`ibmcloud atracker target update --target my-target --name new-target-name`** command.

```text
OK
Target
Name:                         new-target-name
ID:                           000000000-00000000-0000-0000-00000000
CRN:                          crn:v1:bluemix:public:atracker:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx
Region:                       us-south
Type:                         app_config
App Configuration Target CRN: crn:v1:bluemix:public:apprapp:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx::
Write Status:                 success
Created:                      2024-05-31T19:03:35.427Z
Updated:                      2024-05-31T19:03:35.427Z
```
{: screen}

## Deleting a target using the CLI
{: #target-delete-cli-appconf}
{: cli}

Use this command to delete a target.

```sh
ibmcloud atracker target rm --target TARGET [--force]
```
{: pre}

### Command options
{: #target-rm-options-appconf}

`--target TARGET`
:   The ID or name of the target.

`--force` | `-f`
:   Will delete the target without providing the user with any additional prompt.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-rm-example-appconf}

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
{: #target-validate-cli-appconf}
{: cli}

Use this command to validate that a target is correctly configured for an {{site.data.keyword.atracker_full_notm}} region.

```sh
ibmcloud atracker target validate --target TARGET [--region REGION] [--output FORMAT]
```
{: pre}

### Command options
{: #target-validate-options-appconf}

`--target TARGET`
:   The ID or name of the target.

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-validate-example-appconf}

The following is an example using the **`ibmcloud atracker target validate --target new-target-name`** command.

This example shows a successfully validated App Configuration target.
{: note}

```text
Target
Name:                            new-target-name
ID:                              xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
CRN:                             crn:v1:bluemix:public:atracker:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx
Type:                            app_config
App Configuration Target CRN:    crn:v1:bluemix:public:apprapp:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx::
Service to Service Enabled:      true
Write Status:                    success
Created:                         2021-07-21T16:04:15.174Z
Updated:                         2021-07-21T17:49:56.452Z
```
{: screen}

## Getting information about a target using the CLI
{: #target-get-cli-appconf}
{: cli}

Use this command to get information about a target for an {{site.data.keyword.atracker_full_notm}} region.

```sh
ibmcloud atracker target get --target TARGET [--output FORMAT]
```
{: pre}

### Command options
{: #target-get-options-appconf}

`--target TARGET`
:   The ID or name of the target.

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-get-example-appconf}

The following is an example using the **`ibmcloud atracker target get --target new-target-name`** command showing an {{site.data.keyword.appconfig_notm}} target.

```text
Target
Name:                            new-target-name
ID:                              xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
CRN:                             crn:v1:bluemix:public:atracker:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx
Region:                          us-east
Type:                            app_config
App Configuration Target CRN:    crn:v1:bluemix:public:apprapp:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx::
Write Status:                    success
Created:                         2024-06-02T16:04:15.174Z
Updated:                         2024-06-05T17:49:56.452Z
```
{: screen}

## Listing all targets in a region
{: #target-list-cli-appconf}
{: cli}

Use this command to list the configured targets for an {{site.data.keyword.atracker_full_notm}} region.

```sh
ibmcloud atracker target ls [--output FORMAT]
```
{: pre}

### Command options
{: #target-options-appconf}

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-example-appconf}

The following is an example using the **`ibmcloud atracker target ls`** command.

```text
Name                       ID                                     Region     Type                Created
target-01                  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx   us-south   app_config   2020-11-18T03:52:08.603Z
```
{: screen}


## API targets and actions
{: #target-actions-api-appconf}
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
{: #target-prereqs-api-appconf}
{: api}

To make API calls to manage targets, complete the following steps:
1. Get an IAM access token. For more information, see [Retrieving IAM access tokens](/docs/atracker?topic=atracker-retrieve-iam-token).
2. Identify the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).

## Creating an {{site.data.keyword.appconfig_notm}} target using the API
{: #target-create-api-appconf}
{: api}

You can use the following cURL command to create an {{site.data.keyword.appconfig_notm}} target:

```shell
curl -X POST  <ENDPOINT>/api/v2/targets   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"   -d '{
    "name": "TARGET_NAME",
    "target_type": "app_config",
    "app_config_endpoint": {
      "target_crn": "APPCONFIG_CRN"
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
- `app_config_endpoint` includes information about the target.

    `APPCONFIG_CRN` indicates the [CRN](/docs/account?topic=account-crn) of the {{site.data.keyword.appconfig_notm}} instance.

For example, you can use the following cURL request to create a target in Dallas:

```shell
curl -X POST   https://private.us-south.atracker.cloud.ibm.com/api/v2/targets   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"   -d '{
    "name": "My App Configuration target",
    "target_type": "app_config",
    "app_config_endpoint": {
      "target_crn": "crn:v1:bluemix:public:apprapp:us-south:a/<account-id>:<instance-id>::"
    }
  }'
```
{: screen}

In the response, you get information about the target such as the `id`, that indicates the GUID of the target, and the `crn`, that indicates the CRN of the target.


## Updating an {{site.data.keyword.appconfig_notm}} target using the API
{: #target-update-api-appconf}
{: api}

When you update an {{site.data.keyword.appconfig_notm}} target, you must include the target information in the data section of the request.
- You must pass all fields.
- Update the fields that need to be changed.
- You cannot change the `target_type` of a target once created.

You can use the following cURL command to update a target:

```shell
curl -X PUT  <ENDPOINT>/api/v2/targets/TARGET_ID  -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"   -d '{
    "name": "TARGET_NAME",
    "target_type": "app_config",
    "app_config_endpoint": {
      "target_crn": "APPCONFIG_CRN"
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

- `TARGET_TYPE` is the type of the target. Set the value to `app_config` for an {{site.data.keyword.appconfig_notm}} target.
- `app_config_endpoint` includes information about the target.

    `APPCONFIG_CRN` indicates the [CRN](/docs/account?topic=account-crn) of the {{site.data.keyword.appconfig_notm}} instance.


For example, you can use the following cURL request to update a target in Dallas:

```shell
curl -X PUT   https://private.us-south.atracker.cloud.ibm.com/api/v2/targets/TARGET_ID   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"   -d '{
    "name": "My new App Configuration target name",
    "target_type": "app_config",
    "app_config_endpoint": {
      "target_crn": "crn:v1:bluemix:public:apprapp:us-south:a/<account-id>:<instance-id>::"
    }
  }'
```
{: screen}



## Deleting a target using the API
{: #target-delete-api-appconf}
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
{: #target-validate-api-appconf}
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
{: #target-view-api-appconf}
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

Results will show if the target is COS (`"target_type": "cloud_object_storage"`), {{site.data.keyword.logs_full_notm}} offering (`"target_type": "cloud_logs"`), or {{site.data.keyword.appconfig_notm}} (`"target_type": "app_config"`)

## Listing all targets using the API
{: #target-list-targets-appconf}
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

Results will show if the target is COS (`"target_type": "cloud_object_storage"`), {{site.data.keyword.logs_full_notm}} offering (`"target_type": "cloud_logs"`), or {{site.data.keyword.appconfig_notm}} (`"target_type": "app_config"`)


## HTTP response codes
{: #target-rc-api-appconf}
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

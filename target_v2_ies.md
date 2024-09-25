---

copyright:
  years:  2021, 2024
lastupdated: "2024-09-25"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Managing {{site.data.keyword.messagehub}} targets
{: #target_v2_ies}

You can manage {{site.data.keyword.messagehub_full}} (Event Streams) targets in your account by using the {{site.data.keyword.atracker_full_notm}} CLI, the {{site.data.keyword.atracker_full_notm}} REST API, and Terraform scripts. A target is a resource where you can collect auditing events.
{: shortdesc}

For more information on {{site.data.keyword.atracker_full_notm}} targets, see [Targets](/docs/atracker?topic=atracker-target_v2).

## IAM access
{: #target_v2_iam_access_ies}

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

### IAM access for {{site.data.keyword.messagehub}}
{: #target_es}

If you need to restrict access to a single {{site.data.keyword.messagehub}} topic, you will need to create two policies:

* A policy for the topic with the writer role and the `resource ID` with the name of the topic.
* A policy for the cluster with the reader role.

For more information, see the [{{site.data.keyword.messagehub_full}} documentation.](/docs/EventStreams?topic=EventStreams-security)

## Authentication options
{: #target_v2_ies_auth_opts}

When writing to an {{site.data.keyword.messagehub}} target you can use one of the following options to authenticate to an {{site.data.keyword.messagehub_full}} topic.

* By configuring service-to-service (S2S) authorization (recommended).
* By providing an API key when configuring the target.


You can configure service-to-service authorization to your {{site.data.keyword.messagehub}} topic so you do not need to pass an [API key](#target_v2_ies_apikey) when writing your data to the {{site.data.keyword.messagehub}} topic.
{: note}


## CLI prerequisites
{: #target_prereqs_ies}
{: cli}

Before you use the CLI to manage targets, complete the following steps:

1. [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

2. [Install the {{site.data.keyword.atracker_full_notm}} CLI](/docs/atracker?topic=atracker-atracker-cli-config).

   The `atracker` CLI 0.3.2 or higher is required to run {{site.data.keyword.messagehub}} CLI commands. If you have previously installed the `atracker` CLI, you might need to upgrade the `atracker` CLI plug-in by running `ibmcloud plugin update atracker`.
   {: note}

3. Log in to {{site.data.keyword.cloud_notm}}. Run the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)

## Obtaining your {{site.data.keyword.messagehub}} Instance API key
{: #target_v2_ies_apikey}

For information on obtaining your {{site.data.keyword.messagehub}} Instance API key, see [generating an API key to access a topic](/docs/EventStreams?topic=EventStreams-connecting).

## Configuring S2S authorization using the UI within the same account
{: #target_v2_ies_s2s_ui}
{: ui}

Do the following to configure a service-to-service authorization using the {{site.data.keyword.cloud_notm}} UI.

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external} as the account owner that will be configuring {{site.data.keyword.atracker_full_notm}} targets.

	After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} dashboard opens.

2. Click **Manage** &gt; **Access (IAM)**.  **Manage access and users** is displayed.

3. Click **Authorizations**.

4. Click **Create**.

5. For **Source service** select *Activity Tracker* and for **How do you want to scope the access?** select *All resources*.

6. For **Target service** select *Message Hub* for **How do you want to scope the access?** select *Resources based on selected attributes*.

7. Select **Service instance** and **string equals** the name of your {{site.data.keyword.messagehub}} instance.

8. For **Service access** select **Writer**.

9. Click **Authorize**.  Your new service-to-service authorization will be listed in the **Manage authorizations** view.

## Configuring S2S authorization using the CLI
{: #target_v2_ies_s2s_cli}
{: cli}

Do the following to configure a service-to-service authorization using the {{site.data.keyword.cloud_notm}} CLI.

1. [Log in to your {{site.data.keyword.cloud_notm}} account](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login) as the account owner that will be configuring {{site.data.keyword.atracker_full_notm}} authorization.

2. Create an authorization policy defining your service-to-service authorization.

   ```sh
   ibmcloud iam authorization-policy-create atracker messagehub "Writer" [--target-service-instance-id <IES_SERVICE_INSTANCE>
   ```
   {: pre}

   Where:

   `IES_SERVICE_INSTANCE` is the CRN of the {{site.data.keyword.messagehub}} instance to be authorized.


## Configuring S2S authorization using the API
{: #target_v2_ies_s2s_api}
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
               "role_id": "crn:v1:bluemix:public:iam::::serviceRole:Writer"
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
                       "value": "messagehub"
                   },
                   {
                       "name": "serviceInstance",
                       "value": "IES_SERVICE_INSTANCE"
                   }
               ]
           }
       ]
   }
   ```
   {: codeblock}

   Where:

   `CUSTOMER_ACCOUNT_ID` is the account GUID for the account that will be configuring targets.  This can be found by using the [`ibmcloud account list`](/docs/cli?topic=cli-ibmcloud_commands_account#ibmcloud_account_list) command.

   `IES_SERVICE_INSTANCE` is the CRN of the IES instance to be authorized.

3. Get an IAM access token. For more information, see [Retrieving IAM access tokens](/docs/atracker?topic=atracker-retrieve-iam-token).

4. Run the following command to configure your service-to-service authorization:

   ```sh
   curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header "Authorization: $ACCESS_TOKEN" -d @authorization_policy_resource.json "https://iam.cloud.ibm.com/v1/policies"
   ```
   {: pre}


## Creating an {{site.data.keyword.messagehub}} target using the CLI
{: #target-create-cli-ies}
{: cli}

Use this command to create a {{site.data.keyword.messagehub_full}} target to be used to configure a destination for activity events.

```sh
 ibmcloud atracker target create --name TARGET_NAME --type TARGET_TYPE ( [--file EVENTSTREAMS_ENDPOINT_DEFINITION_JSON_FILE] | ( [--target-crn EVENTSTREAMS_TARGET_CRN] [--brokers BROKER_LIST] [--topic TOPIC] [--api-key ( EVENTSTREAMS_API_KEY | @EVENTSTREAMS_API_KEY_FILE )] | [--service-to-service-enabled ( TRUE | FALSE )]) ) [--region REGION] [--output FORMAT]
```
{: pre}

### Command options
{: #target-create-options-ies}

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--name TARGET_NAME`
:   The name to be given to the target.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--type TARGET_TYPE`
:   Set the `TARGET_TYPE` to `event_streams` for an {{site.data.keyword.messagehub}} target.

`--file @EVENTSTREAMS_ENDPOINT_DEFINITION_JSON_FILE`
:   A file containing an endpoint definition in the following format:

    ```json
    {
      "target_crn": "yyyyy",
      "brokers": ["broker-1:9093","broker-2:9093"],
      "topic": "my-topic",
      "api_key": "xxxxxxxxxxxxxx"
    }
    ```
    {: codeblock}

`--target-crn` [EVENTSTREAMS_TARGET_CRN](/docs/EventStreams?topic=EventStreams-connecting)
:   The CRN of the {{site.data.keyword.messagehub_full}} instance. You can get the source crn from the service credentials.

`--brokers BROKER_LIST`
:   The list of {{site.data.keyword.messagehub}} brokers (endpoints). This is the value of the `kafka_brokers_sasl` in the service credentials.

`--topic TOPIC`
:   {{site.data.keyword.messagehub}} topic name to where the events are sent. This is the name of the topic created for an {{site.data.keyword.messagehub}} instance.

`--api-key EVENTSTREAMS_API_KEY` | `@EVENTSTREAMS_API_KEY_FILE`
:   The password value found in the {{site.data.keyword.messagehub}} service credential. This is the IAM API key.

`--service-to-service-enabled`
:   Determines if  {{site.data.keyword.atracker_full_notm}} has service to service authentication enabled. Set this flag to true if service to service is enabled and do not supply an apikey.

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-create-example-ies}

The following is an example using the **`ibmcloud atracker target create --name new-target-name --type event-streams --target-crn "crn:v1:bluemix:public:messagehub:eu-de:a/11111111111111111111111111111111:22222222-2222-2222-2222-222222222222::" --brokers "broker-1:9093,broker-2:9093" --topic "topic-name" --api-key xxxxx`** command.

This example shows an example successful target creation.
{: note}

```text
Target
Name:                     my-target
ID:                       000000000-00000000-0000-0000-00000000
CRN:                      crn:v1:staging:public:atracker:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx
Region:                   us-south
Type:                     event_streams
Event Streams Target CRN: crn:v1:bluemix:public:messagehub:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx::
Event Streams Topic:      my-topic
Event Streams Brokers:    [broker-1:9093,broker-2:9093]
Write Status:             success
CreatedAt:                2022-10-20T19:20:38.888Z
UpdatedAt:                2022-10-20T19:20:38.888Z
```
{: screen}


## Updating an {{site.data.keyword.messagehub}} target using the CLI
{: #target-update-cli-ies}
{: cli}

Use this command to update an {{site.data.keyword.messagehub}} target for an {{site.data.keyword.atracker_full_notm}} region.  Any specified value that is different from when the target was originally created will be updated to the value specified in the command.

```sh
ibmcloud atracker target update --target TARGET [--name TARGET_NAME] [ [--file EVENTSTREAMS_ENDPOINT_DEFINITION_JSON_FILE] | ( [--brokers BROKER_LIST] [--target-crn EVENTSTREAMS_TARGET_CRN] [--topic TOPIC] ( [--api-key ( EVENTSTREAMS_API_KEY | @EVENTSTREAMS_API_KEY_FILE )] | [--service-to-service-enabled ( TRUE | FALSE )]))] [--output FORMAT]
```
{: pre}

### Command options
{: #target-update-options-ies}

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--target TARGET`
:   The ID or current target name.

`--name TARGET_NAME`
:   The name to be given to the target.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--file @EVENTSTREAMS_ENDPOINT_DEFINITION_JSON_FILE`
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
      "target_crn": "yyyyy",
      "brokers": ["broker-1:9093","broker-2:9093"],
      "topic": "my-topic",
      "api_key": "xxxxxxxxxxxxxx"
    }
    ```
    {: codeblock}

`--target-crn` [EVENTSTREAMS_TARGET_CRN](/docs/EventStreams?topic=EventStreams-connecting)
:   The CRN of the {{site.data.keyword.messagehub_full}} instance. You can get the source crn from the service credentials.

`--brokers BROKER_LIST`
:   The list of {{site.data.keyword.messagehub}} brokers (endpoints). This is the value of the `kafka_brokers_sasl` in the service credentials.

`--topic TOPIC`
:   {{site.data.keyword.messagehub}} topic name to where the events are sent. This is the name of the topic created for an {{site.data.keyword.messagehub}} instance

`--api-key EVENTSTREAMS_API_KEY` | `@EVENTSTREAMS_API_KEY_FILE`
:   The password value found in the {{site.data.keyword.messagehub}} service credential. This is the IAM API key

`--service-to-service-enabled`
:   Determines if  {{site.data.keyword.atracker_full_notm}} has service to service authentication enabled. Set this flag to true if service to service is enabled and do not supply an apikey.

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-update-example-ies}

The following is an example using the **`ibmcloud atracker target update --target my-target --name new-target-name`** command.

```text
Target
Name:                     my-new-target
ID:                       000000000-00000000-0000-0000-00000000
CRN:                      crn:v1:staging:public:atracker:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx
Region:                   us-south
Type:                     event_streams
Event Streams Target CRN: crn:v1:bluemix:public:messagehub:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx::
Event Streams Topic:      my-topic
Event Streams Brokers:    [broker-1:9093,broker-2:9093]
Write Status:             success
CreatedAt:                2022-10-20T19:20:38.888Z
UpdatedAt:                2022-10-20T19:20:38.888Z
```
{: screen}


## Deleting a target using the CLI
{: #target-delete-cli-ies}
{: cli}

Use this command to delete a target.

```sh
ibmcloud atracker target rm --target TARGET [--force]
```
{: pre}

### Command options
{: #target-rm-options-ies}

`--target TARGET`
:   The ID or name of the target.

`--force` | `-f`
:   Will delete the target without providing the user with any additional prompt.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-rm-example-ies}

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
{: #target-validate-cli-ies}
{: cli}

Use this command to validate that a target is correctly configured for an {{site.data.keyword.atracker_full_notm}} region.

```sh
ibmcloud atracker target validate --target TARGET [--region REGION] [--output FORMAT]
```
{: pre}

### Command options
{: #target-validate-options-ies}

`--target TARGET`
:   The ID or name of the target.

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-validate-example-ies}

The following is an example using the **`ibmcloud atracker target validate --target new-target-name`** command.

This example shows a successfully validated {{site.data.keyword.messagehub}} target.
{: note}

```text
Target
Name:               		    new-target-name
ID:                 		    xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
CRN:               		      crn:v1:staging:public:atracker:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx
Region:                     us-south
Type:                       event_streams
Event Streams Target CRN:   crn:v1:bluemix:public:messagehub:us-south:a/a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx::
Event Streams Topic:        my-test-topic
Event Streams Brokers:      [broker-1:9093,broker-2:9093]
Write Status:               success
CreatedAt:                  2022-10-20T19:20:38.888Z
UpdatedAt:                  2022-10-20T19:20:38.888Z
```
{: screen}

## Getting information about a target using the CLI
{: #target-get-cli-ies}
{: cli}

Use this command to get information about a target for an {{site.data.keyword.atracker_full_notm}} region.

```sh
ibmcloud atracker target get --target TARGET [--output FORMAT]
```
{: pre}

### Command options
{: #target-get-options-ies}

`--target TARGET`
:   The ID or name of the target.

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-get-example-ies}

The following is an example using the **`ibmcloud atracker target get --target new-target-name`** command showing a {{site.data.keyword.messagehub}} target.

```text
Target
Name:               		    updated-target-name
ID:                 		    xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
CRN:               		      crn:v1:staging:public:atracker:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx
Region:                     us-south
Type:                       event_streams
Event Streams Target CRN:   crn:v1:bluemix:public:messagehub:us-south:a/a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx::
Event Streams Topic:        my-test-topic
Event Streams Brokers:      [broker-1:9093,broker-2:9093]
Write Status:               success
CreatedAt:                  2022-10-20T19:20:38.888Z
UpdatedAt:                  2022-10-20T19:20:38.888Z
```
{: screen}

## Listing all targets in a region
{: #target-list-cli-ies}
{: cli}

Use this command to list the configured targets for an {{site.data.keyword.atracker_full_notm}} region.

```sh
ibmcloud atracker target ls [--output FORMAT]
```
{: pre}

### Command options
{: #target-options-ies}

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-example-ies}

The following is an example using the **`ibmcloud atracker target ls`** command.

```text
Name                       ID                                     Region     Type             Service to Service Enabled Created
target-01                  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx   us-south    event_streams   -				                     2020-11-18T03:52:08.603Z
target-02                  yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy   us-south    event_streams   -				                     2020-11-18T03:52:01.592Z
target-02-backup           zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz   us-east     event_streams   -				                     2021-02-26T06:53:13.466Z
```
{: screen}


## API targets and actions
{: #target-actions-api-ies}
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

For more information about the REST API, see [Targets](/apidocs/atracker#create-target).
{: note}


## API prerequisites
{: #target-prereqs-api-ies}
{: api}

To make API calls to manage targets, complete the following steps:
1. Get an IAM access token. For more information, see [Retrieving IAM access tokens](/docs/atracker?topic=atracker-retrieve-iam-token).
2. Identify the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).



## Creating an {{site.data.keyword.messagehub}} target using the API
{: #target-create-api-ies}
{: api}

You can use the following curl command to create an {{site.data.keyword.messagehub_full}} (Event Streams) target:

```shell
curl -X POST  <ENDPOINT>/api/v2/targets   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"   -d '{
    "name": "TARGET_NAME",
    "target_type": "TARGET_TYPE",
    "eventstreams_endpoint": {
        "target_crn": "EVENTSTREAMS_CRN",
        "brokers": "BROKER_LIST",
        "topic”: "TOPIC_NAME",
        "password": "API_KEY",
        "service_to_service_enabled": false}
    }
  }'
```
{: codeblock}

Where

- `TARGET_NAME` is the name of the target. The maximum length of the name is 256 characters.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

- `TARGET_TYPE` is the type of the target. Set the value to `event_streams` for an {{site.data.keyword.messagehub}} target.

- `BROKER_LIST` is the list of {{site.data.keyword.messagehub}} brokers (endpoints).

- `TOPIC_NAME` is the name of an {{site.data.keyword.messagehub}} topic name where the events are sent.

- `API_KEY` is the password value found in the {{site.data.keyword.messagehub}} service credential. This is the IAM API key.

- `service_to_service_enabled` determines if  {{site.data.keyword.atracker_full_notm}} has service to service authentication enabled. Set this flag to true if service to service is enabled and do not supply an apikey.

In the response, you get information about the target such as the `id`, that indicates the GUID of the target, and the `crn`, that indicates the CRN of the target.


## Updating an {{site.data.keyword.messagehub}} target using the API
{: #target-update-api-ies}
{: api}

When you update an {{site.data.keyword.messagehub_full}} (Event Streams) target, you must include the target information in the data section of the request.
- You must pass all fields.
- Update the fields that need to be changed.
- You cannot change the `target_type` of a target once created.

You can use the following curl command to update a target:

```shell
curl -X PUT  <ENDPOINT>/api/v2/targets/TARGET_ID  -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"   -d '{
    "name": "TARGET_NAME",
    "target_type": "TARGET_TYPE",
    "eventstreams_endpoint": {
      "target_crn": "EVENTSTREAMS_CRN",
      "brokers": "BROKER_LIST",
      "topic”: "TOPIC_NAME",
      "password": "API_KEY",
      "service_to_service_enabled": false}
    }
  }'
```
{: codeblock}

Where

- `TARGET_ID` is the ID of the target.

- `TARGET_NAME` is the name of the target. The maximum length of the name is 256 characters.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

- `TARGET_TYPE` is the type of the target. Set the value to `event_streams` for an {{site.data.keyword.messagehub}} target.

- `BROKER_LIST` is the list of {{site.data.keyword.messagehub}} brokers (endpoints).

- `TOPIC_NAME` is the name of an {{site.data.keyword.messagehub}} topic where the events are sent.

- `API_KEY` is the password value found in the {{site.data.keyword.messagehub}} service credential. This is the IAM API key.

- `service_to_service_enabled` determines if {{site.data.keyword.atracker_full_notm}} has service to service authentication enabled. Set this flag to true if service to service is enabled and do not supply an apikey.

## Deleting a target using the API
{: #target-delete-api-ies}
{: api}

You can use the following curl command to delete a target:

```text
curl -X DELETE <ENDPOINT>/api/v2/targets/<TARGET_ID> -H "Authorization:  $ACCESS_TOKEN" -H "content-type: application/json"
```
{: codeblock}

Where

- `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).
- `<TARGET_ID>` is the ID of the target.


For example, you can use the following curl request to delete a target in US-South with the ID `00000000-0000-0000-0000-000000000000`:

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
{: #target-validate-api-ies}
{: api}

You can use the following curl command to validate a target by checking the credentials to write to the target.

```shell
curl -X POST <ENDPOINT>/api/v2/targets/<TARGET_ID>/validate -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json"
```
{: codeblock}

Where

- `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).
- `<TARGET_ID>` is the ID of the target.

For example, you can use the following curl request to validate a target in US-South with the ID `00000000-0000-0000-0000-000000000000`:

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
{: #target-view-api-ies}
{: api}

You can use the following curl command to view the configuration details of 1 target:

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

Results will show if the target is COS (`"target_type": "cloud_object_storage"`) or AT (`"target_type": "logdna"`) or {{site.data.keyword.messagehub}} (`"target_type": "event_streams"`) or an {{site.data.keyword.at_full_notm}} hosted event search offering.

## Listing all targets using the API
{: #target-list-targets-ies}
{: api}

You can use the following curl command to view all targets:

```shell
curl -X GET <ENDPOINT>/api/v2/targets -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json"
```
{: codeblock}

Where

- `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).


For example, you can run the following curl request to get information about the targets that are defined in Dallas:

```shell
curl -X GET https://private.us-south.atracker.cloud.ibm.com/api/v2/targets -H "Authorization:  $ACCESS_TOKEN" -H "content-type: application/json"
```
{: screen}

Results will show if the target is COS (`"target_type": "cloud_object_storage"`) or AT (`"target_type": "logdna"`) or {{site.data.keyword.messagehub}} (`"target_type": "event_streams"`) or an {{site.data.keyword.at_full_notm}} hosted event search offering.


## HTTP response codes
{: #target-rc-api-ies}
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


## Creating a {{site.data.keyword.messagehub}} target using the UI
{: #target-create-ui-ies}
{: ui}

Only resources in your account are listed and selectable. To specify a resource in a different account, select **Specify CRN** under **Choose destination**.
{: important}

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.
2. Click the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg) &gt; **Observability**.
3. Select **Activity Tracker**.
4. Select **Routing**.
5. Select **Targets**.
6. Click **Create** to open the create panel.
7. **Choose type**: Click **Event Streams**.
8. **Choose destination**: Pick **Search by instance** or **Specify CRN**
    - **Search by instance**: Select an {{site.data.keyword.messagehub}} instance from the table or click **Create** to create a new {{site.data.keyword.messagehub}} instance.
    - **Specify CRN**: Enter the Cloud Resource Name (CRN) of the {{site.data.keyword.messagehub}} instance. This enables you to enter a CRN from a different account.
- **Service credentials**: Select one of the service credentials, it contains the brokers list username, and api_key or password.
- **Event Streams topic**: Select an existing topic.
- **Target name**: Enter a meaningful name for the target.
- **Target region**: Select the region that will process the event data.
- Toggle **Set as default target** to automatically set your new target as a default target in your {{site.data.keyword.atracker_full_notm}} settings. See [the default targets documentation](/docs/atracker?topic=atracker-planning#planning-4) for more details.
- Click **Create target**.


## Updating a {{site.data.keyword.messagehub}} target using the UI
{: #target-update-ui-ies}
{: ui}

Only resources in your account are listed and selectable. To specify a resource in a different account, select **Specify CRN** under **Choose destination**.
{: important}

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.
2. Click the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg) &gt; **Observability**.
3. Select **Activity Tracker**.
4. Select **Routing**.
5. Select **Targets**.
6. Determine which target to update and click the ![Actions icon](../icons/action-menu-icon.svg "Actions").
7. You can click **Unset as default** to remove your target as a default target in your {{site.data.keyword.atracker_full_notm}} settings. See [Default targets documentation](/docs/atracker?topic=atracker-planning#planning-4) for more details.
8. Click **Edit** to open the update panel.
9. **Details**: Click **Edit** to update your target's name or region. You can also toggle **Default target** to add or remove your target as a default target in your {{site.data.keyword.atracker_full_notm}} settings.
10. Click **Save** to update your target.
11. **Destination**: Click **Edit** to change the {{site.data.keyword.messagehub}} instance, service credential, or topic associated with your target.
12. Click **Save** to update your target.

## Deleting a target using the UI
{: #target-delete-ui-ies}
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
{: #target-list-ui-ies}
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

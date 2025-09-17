---

copyright:
  years: 2021, 2025
lastupdated: "2025-09-17"

subcollection: atracker

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Activity Tracker Event Routing CLI
{: #atracker-v2-cli}

The {{site.data.keyword.cloud}} command-line interface (CLI) provides extra capabilities for service offerings. This information describes how you can use the CLI to define and manage settings for your {{site.data.keyword.atracker_full}} instance using the CLI.
{: shortdesc}



## Prerequisites
{: #atracker-v2-cli-prereq}

* Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).
* Install the CLI by running the following command:

   ```sh
   ibmcloud plugin install atracker
   ```
   {: pre}

You're notified on the command line when updates to the {{site.data.keyword.cloud_notm}} CLI and plug-ins are available. Be sure to keep your CLI up to date so that you can use the latest commands. You can view the current version of all installed plug-ins by running `ibmcloud plugin list`.
{: tip}

## `ibmcloud atracker route create`
{: #route-create-v2-cli}

Use this command to create a new route for an {{site.data.keyword.atracker_short}} target.

```sh
ibmcloud atracker route create --name ROUTE_NAME  ( --target-ids TARGETS  [--locations REGIONS] | --rules RULES | --file RULES_DEFINITION_JSON_FILE ) [--output FORMAT]
```
{: pre}

### Command options
{: #route-create-options}

`--name ROUTE_NAME`
:   The name to be given to the route.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--file RULES_DEFINITION_JSON_FILE`
:   A JSON file containing the definition of the rules for route.  The file needs to be formatted as follows:

    ```json
    [
      {
        "locations": ["LOCATION1","LOCATION2"],
        "target_ids": ["TARGET_ID1","TARGET_ID2"]
      }
    ]
    ```
    {: codeblock}

`--rules RULES`
:   A JSON formatted rule definition enclosed in single quotes. For example:

    ```json
    --rules '[{"locations":["global"],"target_ids":["11111111-1111-1111-1111-111111111111"]},{"locations":["us-south","us-east"],"target_ids":["22222222-2222-2222-2222-222222222222","33333333-3333-3333-3333-333333333333"]}]'
    ```
    {: codeblock}

`--locations LOCATIONS`
:   List of locations associated with the route.  Specify `global` to include global events. To include all locations specify `*`.  If you have multiple rules, along with a rule with a `*` location, then the other rules will route events to the specified targets with any events not matching any other rule routing the remaining events to the target specified by the rule with the `*` location.

`--target-ids TARGET_ID`
:   A comma-separated list of target IDs.

`--output FORMAT`
:   If `JSON` is specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

## `ibmcloud atracker route update`
{: #route-update-v2-cli}


Use this command to update a route for an {{site.data.keyword.atracker_short}} target. Any specified value that is different from when the route was originally created will be updated to the value specified in the command.

```sh
ibmcloud atracker route update --route ROUTE [--name ROUTE_NAME] [--force] ( [--target-ids TARGETS]  [--locations REGIONS] | [--rules RULES] | [--file RULES_DEFINITION_JSON_FILE] ) [--output FORMAT] [--output FORMAT]
```
{: pre}

### Command options
{: #route-update-options}

`--route ROUTE`
:   The existing name or ID of the route.

`--name ROUTE_NAME`
:   The updated name to be given to the route (optional).

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--file RULES_DEFINITION_JSON_FILE`
:   A JSON file containing the definition of the rules for route.  The file needs to be formatted as follows:

    ```json
    [
      {
        "location": ["LOCATIONS"],
        "target_ids": ["TARGET_ID"]
      }
    ]
    ```
    {: codeblock}

`--rules RULES`
:   A JSON formatted rule definition enclosed in single quotes. For example:

    ```json
    --rules '[{"locations":["global"],"target_ids":["11111111-1111-1111-1111-111111111111"]},{"locations":["us-south","us-east"],"target_ids":["22222222-2222-2222-2222-222222222222","33333333-3333-3333-3333-333333333333"]}]'
    ```
    {: codeblock}

`--locations LOCATIONS`
:   List of locations associated with the route.  Specify `global` to include global events. To include all locations specify `*`.  If you have multiple rules, along with a rule with a `*` location, then the other rules will route events to the specified targets with any events not matching any other rule routing the remaining events to the target specified by the rule with the `*` location.

`--target-ids TARGET_ID`
:   A comma-separated list of target IDs.

`--output FORMAT`
:   If `JSON` is specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`--force`
:   Will delete the route without providing the user with any additional prompt.

`help` | `--help` | `-h`
:   List options available for the command.

## `ibmcloud atracker route rm`
{: #route-delete-v2-cli}

Use this command to delete an {{site.data.keyword.atracker_short}} route.

```sh
ibmcloud atracker route rm --route ROUTE [--force]
```
{: pre}

### Command options
{: #route-rm-v2-options}

`--route ROUTE`
:   The name or ID of the route to be deleted.

`--force`
:   Will delete the route without providing the user with any additional prompt.

`help` | `--help` | `-h`
:   List options available for the command.

## `ibmcloud atracker route get`
{: #route-view-v2-cli}

Use this command to get information about an {{site.data.keyword.atracker_short}} route.

```sh
ibmcloud atracker route get --route ROUTE [--output FORMAT]
```
{: pre}

### Command options
{: #route-get-v2-options}

`--route <ROUTE_ID>`
:   The name or ID of the route.

`--output FORMAT`
:   If `JSON` is specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

## `ibmcloud atracker route ls`
{: #route-list-v2-cli}

Use this command to list all the configured routes for {{site.data.keyword.atracker_short}} .

```sh
ibmcloud atracker route ls [--output FORMAT]
```
{: pre}

### Command options
{: #route-ls-v2-options}

`--output FORMAT`
:   If `JSON` is specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

## `ibmcloud atracker target create` (COS)
{: #target-create-cli-v2-cos}

Use this command to create a {{site.data.keyword.cos_full_notm}} target to be used to configure a destination for activity events.

```sh
 ibmcloud atracker target create --name TARGET_NAME --type TARGET_TYPE ( [--file COS_ENDPOINT_DEFINITION_JSON_FILE] |  ( [--endpoint COS_ENDPOINT] [--bucket COS_BUCKET] [--target-crn COS_TARGET_CRN] ( [--api-key ( COS_API_KEY | @COS_API_KEY_FILE )] |  [--service-to-service-enabled ( TRUE | FALSE )] ) ) ) [--region REGION] [--output FORMAT]
```
{: pre}

### Command options
{: #target-create-options-v2-cos}

`--region REGION` | `-r REGION`
:   Name of the region that determines the {{site.data.keyword.atracker_full_notm}} API endpoint for the request, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

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
:   Indicates if [service-to-service authorization](/docs/atracker?topic=atracker-iam-service-auth-cos&interface=ui) has been enabled for the bucket.  Specify `TRUE` if service-to-service authorization is enabled and `FALSE` if service-to-service authorization is not enable.  By default, `service_to_service_enabled` is `FALSE`.

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.



## `ibmcloud atracker target create` (Event Streams)
{: #target-create-cli-ies}

Use this command to create a {{site.data.keyword.messagehub_full}} target to be used to configure a destination for activity events.

```sh
 ibmcloud atracker target create --name TARGET_NAME --type TARGET_TYPE ( [--file EVENTSTREAMS_ENDPOINT_DEFINITION_JSON_FILE] | ( [--target-crn EVENTSTREAMS_TARGET_CRN] [--brokers BROKER_LIST] [--topic TOPIC] [--api-key ( EVENTSTREAMS_API_KEY | @EVENTSTREAMS_API_KEY_FILE )] | [--service-to-service-enabled ( TRUE | FALSE )]) ) [--region REGION] [--output FORMAT]
```
{: pre}

### Command options
{: #target-create-options-ies}

`--region REGION` | `-r REGION`
:   Name of the region that determines the {{site.data.keyword.atracker_full_notm}} API endpoint for the request, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

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

`--target-crn` [EVENTSTREAMS_TARGET_CRN](/docs/EventStreams?topic=EventStreams-connecting)[
:   The CRN of the {{site.data.keyword.messagehub_full}} instance. You can get the source crn from the service credentials.

`--brokers BROKER_LIST`
:   The list of {{site.data.keyword.messagehub}} brokers (endpoints). This is the value of the `kafka_brokers_sasl` in the service credentials.

`--topic TOPIC`
:   {{site.data.keyword.messagehub}} topic name to where the events are sent. This is the name of the topic created for an {{site.data.keyword.messagehub}} instance.

`--api-key EVENTSTREAMS_API_KEY` | `@EVENTSTREAMS_API_KEY_FILE`
:   The password value found in the {{site.data.keyword.messagehub}} service credential. This is the IAM API key.

`--service-to-service-enabled`
:   Determines if {{site.data.keyword.atracker_full_notm}} has service to service authentication enabled. Set this flag to `true` if service to service is enabled and do not supply an apikey.

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.## ibmcloud atracker target create (COS).

Use this command to create a {{site.data.keyword.messagehub_full}} target to be used to configure a destination for activity events.

```sh
 ibmcloud atracker target create --name new-target-name --type event-streams --target-crn "crn:v1:bluemix:public:messagehub:eu-de:a/11111111111111111111111111111111:22222222-2222-2222-2222-222222222222::" --brokers "broker-1:9093,broker-2:9093" --topic "topic-name" --api-key xxxxx
```
{: pre}

## `ibmcloud atracker target create` ({{site.data.keyword.logs_full_notm}})
{: #target-create-cli-icl}

Use this command to create a {{site.data.keyword.messagehub_full}} target to be used to configure a destination for activity events.

```sh
 ibmcloud atracker target create --name TARGET_NAME --type TARGET_TYPE ( [--file CLOUD_LOGS_ENDPOINT_DEFINITION_JSON_FILE] | ( [--target-crn CLOUD_LOGS_TARGET_CRN] ) ) [--region REGION] [--output FORMAT]
```
{: pre}

### Command options
{: #target-create-options-icl}

`--region REGION` | `-r REGION`
:   Name of the region that determines the {{site.data.keyword.atracker_full_notm}} API endpoint for the request, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--name TARGET_NAME`
:   The name to be given to the target.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--type TARGET_TYPE`
:   Set the `TARGET_TYPE` to `cloud_logs` for an {{site.data.keyword.logs_full_notm}} target.

`--file @CLOUD_LOGS_ENDPOINT_DEFINITION_JSON_FILE`
:   A file containing an endpoint definition in the following format:

    ```json
    {
      "target_crn": "yyyyy"
    }
    ```
    {: codeblock}

`--target-crn CLOUD_LOGS_TARGET_CRN`
:   The CRN of the {{site.data.keyword.logs_full_notm}} instance.

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.## ibmcloud atracker target create.

Use this command to create a {{site.data.keyword.logs_full_notm}} target to be used to configure a destination for activity events.

```sh
 ibmcloud atracker target create --name new-target-name --type cloud-logs --target-crn "crn:v1:bluemix:public:logs:eu-de:a/11111111111111111111111111111111:22222222-2222-2222-2222-222222222222::"
```
{: pre}

## `ibmcloud atracker target update` (COS)
{: #target-update-v2-cli-cos}

Use this command to update a COS target for an {{site.data.keyword.atracker_full_notm}} region.  Any specified value that is different from when the target was originally created will be updated to the value specified in the command.

```text
ibmcloud atracker target update --target TARGET [--name TARGET_NAME] [ [--file COS_ENDPOINT_DEFINITION_JSON_FILE] |  ( [--endpoint COS_ENDPOINT] [--bucket COS_BUCKET] [--target-crn COS_TARGET_CRN] ( [--api-key ( COS_API_KEY | @COS_API_KEY_FILE )] | [--service-to-service-enabled ( TRUE | FALSE )]))] [--output FORMAT]
```
{: pre}

### Command options
{: #target-update-options-cos}

`--target TARGET`
:   The ID or current target name.

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
:   Indicates if [service-to-service authorization](/docs/atracker?topic=atracker-iam-service-auth-cos&interface=ui) has been enabled for the bucket.  Specify `TRUE` if service-to-service authorization is enabled and `FALSE` if service-to-service authorization is not enable.  By default, service-to-service authorization is `FALSE`.

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.



## `ibmcloud atracker target update` (Event Streams)
{: #target-update-cli-ies}

Use this command to update an {{site.data.keyword.messagehub}} target for an {{site.data.keyword.atracker_full_notm}} region.  Any specified value that is different from when the target was originally created will be updated to the value specified in the command.

```text
ibmcloud atracker target update --target TARGET [--name TARGET_NAME] [ [--file EVENTSTREAMS_ENDPOINT_DEFINITION_JSON_FILE] | ( [--brokers BROKER_LIST] [--target-crn EVENTSTREAMS_TARGET_CRN] [--topic TOPIC] ( [--api-key ( EVENTSTREAMS_API_KEY | @EVENTSTREAMS_API_KEY_FILE )] | [--service-to-service-enabled ( TRUE | FALSE )]))] [--output FORMAT]
```
{: pre}

### Command options
{: #target-update-options-ies}

`--name TARGET_NAME`
:   The name to be given to the target.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--type TARGET_TYPE`
:   Set the `TARGET_TYPE` to `cloud_object_storage` for a COS target.

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

`--target-crn` [EVENTSTREAMS_TARGET_CRN](/docs/EventStreams?topic=EventStreams-connecting)[
:   The CRN of the {{site.data.keyword.messagehub_full}} instance. You can get the source crn from the service credentials.

`--brokers BROKER_LIST`
:   The list of {{site.data.keyword.messagehub}} brokers (endpoints). This is the value of the `kafka_brokers_sasl` in the service credentials.

`--topic TOPIC`
:   {{site.data.keyword.messagehub}} topic name to where the events are sent. This is the name of the topic created for an {{site.data.keyword.messagehub}} instance.

`--api-key EVENTSTREAMS_API_KEY` | `@EVENTSTREAMS_API_KEY_FILE`
:   The password value found in the {{site.data.keyword.messagehub}} service credential. This is the IAM API key.

`--service-to-service-enabled`
:   Determines if {{site.data.keyword.atracker_full_notm}} has service to service authentication enabled. Set this flag to `true` if service to service is enabled and do not supply an apikey.

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

## `ibmcloud atracker target update` ({{site.data.keyword.logs_full_notm}})
{: #target-update-cli-icl}

Use this command to update an {{site.data.keyword.logs_full_notm}} target to be used to configure a destination for activity events.

```sh
ibmcloud atracker target update --target TARGET [--name TARGET_NAME] ( --file @CLOUD_LOGS_ENDPOINT_DEFINITION_JSON_FILE ) | (--target-crn CLOUD_LOGS_TARGET_CRN) [--output FORMAT]
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
:   Currently support format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

## `ibmcloud atracker target rm`
{: #target-delete-v2-cli}

Use this command to delete a target.

```sh
ibmcloud atracker target rm --target TARGET [--force]
```
{: pre}

### Command options
{: #target-rm-v2-options-cos}

`--target TARGET`
:   The ID or name of the target.

`--force` | `-f`
:   Will delete the target without providing the user with any additional prompt.

`help` | `--help` | `-h`
:   List options available for the command.

## `ibmcloud atracker target validate`
{: #target-validate-v2-cli}

Use this command to validate that a target is correctly configured for an {{site.data.keyword.atracker_full_notm}} region.

```sh
ibmcloud atracker target validate --target TARGET [--region REGION] [--output FORMAT]
```
{: pre}

### Command options
{: #target-validate-v2-options-cos}

`--target TARGET`
:   The ID or name of the target.

`--region REGION` | `-r REGION`
:   Name of the region that determines the {{site.data.keyword.atracker_full_notm}} API endpoint for the request, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

## `ibmcloud atracker target get`
{: #target-get-v2-cli-cos}

Use this command to get information about a target for an {{site.data.keyword.atracker_full_notm}} region.

```sh
ibmcloud atracker target get --target TARGET [--output FORMAT]
```
{: pre}

### Command options
{: #target-get-v2-options-cos}

`--target TARGET`
:   The ID or name of the target.

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

## `ibmcloud atracker target ls`
{: #target-list-v2-cli-cos}

Use this command to list the configured targets for an {{site.data.keyword.atracker_full_notm}} region.

```sh
ibmcloud atracker target ls [--output FORMAT]
```
{: pre}

### Command options
{: #target-v2-options-cos}

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

## `ibmcloud atracker setting get`
{: #settings-get-v2-cli}

Use this command to get the settings for the {{site.data.keyword.atracker_full_notm}} account configurations.

```sh
ibmcloud atracker setting get [--output FORMAT]
```
{: pre}

### Command options
{: #settings-get-v2-options}

`--output FORMAT`
:   If `JSON` is specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

## `ibmcloud atracker setting update`
{: #settings-update-v2-cli}

Use this command to modify current settings such as the default targets, permitted target regions, primary and secondary metadata regions in {{site.data.keyword.atracker_full_notm}}. Any value that is different from when the target was originally created will be updated to the value specified in the command.

Before disabling a public endpoint (`--private-api-endpoint-only TRUE`), make sure your account has access to the private endpoint.  You can do this by running the command `bx account show`.  If `VRF Enabled` is `true` and `Service Endpoint Enabled` is `true` then you have access to the private endpoint.  If you do not have access to the private endpoint, you will be unable to re-enable the public endpoint since private endpoint access is required to re-enable the public endpoint.
{: important}

```text
ibmcloud atracker setting update [--metadata-region-primary REGION] [--metadata-region-backup REGION] [--default-targets TARGET] [--permitted-target-regions REGIONS] [--private-api-endpoint-only ( TRUE | FALSE )] [--output FORMAT] [--force]
```
{: pre}

### Command options
{: #settings-update-v2-options}

`default-targets`
:   Is a list of target IDs.  If no routing rules cause events to be sent to other targets, these targets will received the events.  TARGETS is a comma-separated list of target IDs.

`permitted-target-regions`
:   Is the list of regions that can be used to define a target. REGIONS is a comma-separated list of regions. A maximum of two permitted target regions can be specified.

`metadata-region-primary`
:   Specify the REGION where the metadata associated with route and target definitions is stored.

`metadata_region_backup`
:   Is the region where the metadata associated with route and target definitions is stored as a backup location.

`private-api-endpoint-only`
:   Specifies whether nor not a private endpoint can be used.  If `true` only a private endpoint can be used.

`--output FORMAT`
:   If `JSON` specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

 `help` | `--help` | `-h`
:   List options available for the command.

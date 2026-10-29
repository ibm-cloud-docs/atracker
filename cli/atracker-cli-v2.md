---

copyright:
  years: 2021, 2026
lastupdated: "2026-10-29"

subcollection: atracker

keywords:

content-type: cli-docs

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

Use this command to create an {{site.data.keyword.atracker_short}} route that sends activity events from one or more locations to one or more targets. A route contains rules that define which events are sent to which targets. 

```sh
ibmcloud atracker route create --name ROUTE_NAME [--force] ( --target-ids TARGETS [--locations REGIONS] | --rules RULES | --file RULES_DEFINITION_JSON_FILE ) [--output FORMAT]
```
{: pre}

### Command options
{: #route-create-options}

`--name ROUTE_NAME`
:   The name to be given to the route.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--target-ids TARGETS`
:   A comma-separated list of target IDs. All events are sent to all targets that are listed in the rule. You can include targets from other regions.

`--locations REGIONS`
:   List of locations associated with the route.  Specify `global` to include global events. To include all locations specify `*`.  If you have multiple rules, along with a rule with a `*` location, then the other rules will route events to the specified targets with any events not matching any other rule routing the remaining events to the target specified by the rule with the `*` location.

`--rules RULES`
:   A JSON formatted rule definition enclosed in single quotes. For example:

    ```json
    --rules '[{"locations":["global"],"target_ids":["11111111-1111-1111-1111-111111111111"]},{"locations":["us-south","us-east"],"target_ids":["22222222-2222-2222-2222-222222222222","33333333-3333-3333-3333-333333333333"]}]'
    ```
    {: codeblock}

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

`--managed-by MANAGED_BY`
:   The owner of the route to be created. Valid values are `account` or `enterprise`.

`--force`
:   Runs the command without prompting you to confirm that you want to continue. This option is used only when the resulting route discards events.

`--output FORMAT`
:   If `JSON` is specified, the output is returned in JSON format. If `JSON` is not specified, the output is returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Examples
{: #route-create-examples}

Send events from all locations to two targets.

```sh
ibmcloud atracker route create --name ROUTE_NAME --target-ids 11111111-1111-1111-1111-111111111111,22222222-2222-2222-2222-222222222222 --locations "*"
```
{: pre}

Send events from the `us-south` location to a target.

```sh
ibmcloud atracker route create --name ROUTE_NAME --target-ids 11111111-1111-1111-1111-111111111111 --locations us-south
```
{: pre}

Use rules to create a route.

```sh
ibmcloud atracker route create --name ROUTE_NAME --rules '[{"locations":["global"],"target_ids":["11111111-1111-1111-1111-111111111111"]},{"locations":["us-south","us-east"],"target_ids":["11111111-1111-1111-1111-111111111111","22222222-2222-2222-2222-222222222222"]}]'
```
{: pre}

Use a rules definition JSON file to create a route.

```sh
ibmcloud atracker route create --name ROUTE_NAME --file RULES_DEFINITION_JSON_FILE
```
{: pre}

Create an enterprise route that sends events from the `us-south` location to an enterprise target.

```sh
ibmcloud atracker route create --name ROUTE_NAME --target-ids 33333333-3333-3333-3333-333333333333 --locations us-south --managed-by enterprise
```
{: pre}

## `ibmcloud atracker route update`
{: #route-update-v2-cli}

Use this command to update an {{site.data.keyword.atracker_short}} route. Any specified value that is different from when the route was originally created will be updated to the value specified in the command.

```sh
ibmcloud atracker route update --route ROUTE [--name ROUTE_NAME] [--force] ( [--target-ids TARGETS] [--locations REGIONS] | [--rules RULES] | [--file RULES_DEFINITION_JSON_FILE] ) [--output FORMAT]
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

`--target-ids TARGETS`
:   A comma-separated list of target IDs. All events are sent to all targets that are listed in the rule. You can include targets from other regions.

`--locations REGIONS`
:   List of locations associated with the route.  Specify `global` to include global events. To include all locations specify `*`.  If you have multiple rules, along with a rule with a `*` location, then the other rules will route events to the specified targets with any events not matching any other rule routing the remaining events to the target specified by the rule with the `*` location.

`--rules RULES`
:   A JSON formatted rule definition enclosed in single quotes. For example:

    ```json
    --rules '[{"locations":["global"],"target_ids":["11111111-1111-1111-1111-111111111111"]},{"locations":["us-south","us-east"],"target_ids":["22222222-2222-2222-2222-222222222222","33333333-3333-3333-3333-333333333333"]}]'
    ```
    {: codeblock}

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

`--force`
:   Runs the command without prompting you to confirm that you want to continue. This option is used only when the resulting route discards events.

`--output FORMAT`
:   If `JSON` is specified, the output is returned in JSON format. If `JSON` is not specified, the output is returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Examples
{: #route-update-examples}

Update a route to send events from all locations to two targets.

```sh
ibmcloud atracker route update --route ROUTE --name ROUTE_NAME --target-ids 11111111-1111-1111-1111-111111111111,22222222-2222-2222-2222-222222222222 --locations "*"
```
{: pre}

Update a route to send events from the `us-south` location to a target.

```sh
ibmcloud atracker route update --route ROUTE --name ROUTE_NAME --target-ids 11111111-1111-1111-1111-111111111111 --locations us-south
```
{: pre}

Use rules to update a route.

```sh
ibmcloud atracker route update --route ROUTE --name ROUTE_NAME --rules '[{"locations":["global"],"target_ids":["11111111-1111-1111-1111-111111111111"]},{"locations":["us-south","us-east"],"target_ids":["11111111-1111-1111-1111-111111111111","22222222-2222-2222-2222-222222222222"]}]'
```
{: pre}

Use a rules definition JSON file to update a route.

```sh
ibmcloud atracker route update --route ROUTE --name ROUTE_NAME --file RULES_DEFINITION_JSON_FILE
```
{: pre}

## `ibmcloud atracker route rm`
{: #route-delete-v2-cli}

Use this command to delete an {{site.data.keyword.atracker_short}} route. Events are no longer routed to the targets that are defined in the route. 

```sh
ibmcloud atracker route rm --route ROUTE [--force]
```
{: pre}

### Command options
{: #route-rm-v2-options}

`--route ROUTE`
:   The name or ID of the route to be deleted.

`--force`
:   Runs the command without prompting you to confirm that you want to continue.

`help` | `--help` | `-h`
:   List options available for the command.

### Examples
{: #route-rm-examples}


Delete a route.

```sh
ibmcloud atracker route rm --route ROUTE
```
{: pre}

Delete a route without being prompted to confirm.

```sh
ibmcloud atracker route rm --route ROUTE --force
```
{: pre}

## `ibmcloud atracker route get`
{: #route-view-v2-cli}

Use this command to get detailed information about an {{site.data.keyword.atracker_short}} route, such as its rules, locations, and targets. 

```sh
ibmcloud atracker route get --route ROUTE [--output FORMAT]
```
{: pre}

### Command options
{: #route-get-v2-options}

`--route ROUTE`
:   The name or ID of the route.

`--output FORMAT`
:   If `JSON` is specified, the output is returned in JSON format. If `JSON` is not specified, the output is returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Examples
{: #route-get-examples}


Get information about a route.

```sh
ibmcloud atracker route get --route ROUTE
```
{: pre}

Get information about a route in JSON format.

```sh
ibmcloud atracker route get --route ROUTE --output JSON
```
{: pre}

## `ibmcloud atracker route ls`
{: #route-list-v2-cli}

Use this command to list all the configured routes for {{site.data.keyword.atracker_short}}.

```sh
ibmcloud atracker route ls [--output FORMAT]
```
{: pre}

### Command options
{: #route-ls-v2-options}

`--output FORMAT`
:   If `JSON` is specified, the output is returned in JSON format. If `JSON` is not specified, the output is returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Examples
{: #route-ls-examples}


List all routes.

```sh
ibmcloud atracker route ls
```
{: pre}

List all routes in JSON format.

```sh
ibmcloud atracker route ls --output JSON
```
{: pre}

## `ibmcloud atracker target create`
{: #target-create-v2-cli}

Use this command to create an {{site.data.keyword.atracker_short}} target to be used to configure a destination for activity events. The options that you specify depend on the type of target that you create. Use the `--type` option to specify the target type.

### Create a {{site.data.keyword.cos_full_notm}} target
{: #target-create-cli-v2-cos}

Use this command to create a {{site.data.keyword.cos_full_notm}} target to be used to configure a destination for activity events.

```sh
ibmcloud atracker target create --name TARGET_NAME --type TARGET_TYPE ( [--file COS_ENDPOINT_DEFINITION_JSON_FILE] | ( [--endpoint COS_ENDPOINT] [--bucket COS_BUCKET] [--target-crn COS_TARGET_CRN] ( [--api-key ( COS_API_KEY | @COS_API_KEY_FILE )] | [--service-to-service-enabled ( TRUE | FALSE )] ) ) ) [--region REGION] [--output FORMAT]
```
{: pre}

#### Command options
{: #target-create-options-v2-cos}

`--region REGION` | `-r REGION`
:   Name of the region that determines the {{site.data.keyword.atracker_full_notm}} API endpoint for the request, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--name TARGET_NAME`
:   The name to be given to the target.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--type TARGET_TYPE`
:   Set the `TARGET_TYPE` to `cloud-object-storage` for a COS target. 

`--file COS_ENDPOINT_DEFINITION_JSON_FILE`
:   A file containing an endpoint definition in the following format:

    ```json
    {
      "endpoint": "ENDPOINT",
      "target_crn": "TARGET_CRN",
      "bucket": "BUCKET",
      "api_key": "API_KEY"
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
:   Your [API key](/docs/iam?topic=iam-manapikey) value or a reference to the API Key file used to gain access.  For example, `ibmcloud login --apikey $KEYFILE`

`--service-to-service-enabled (TRUE | FALSE)`
:   Indicates if [service-to-service authorization](/docs/atracker?topic=atracker-iam-service-auth-cos&interface=ui) has been enabled for the bucket.  Specify `TRUE` if service-to-service authorization is enabled and `FALSE` if service-to-service authorization is not enabled.  By default, `service_to_service_enabled` is `FALSE`.

`--output FORMAT`
:   The only supported format is JSON. If specified, the output is returned in JSON format. If `JSON` is not specified, the output is returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

#### Examples
{: #target-create-examples-cos}

Create a COS target by using an endpoint definition JSON file.

```sh
ibmcloud atracker target create --name TARGET_NAME --type cloud-object-storage --file COS_ENDPOINT_DEFINITION_JSON_FILE
```
{: pre}

Create a COS target that uses a customer-provided API key for authentication.

```sh
ibmcloud atracker target create --name TARGET_NAME --type cloud-object-storage --endpoint s3.private.us-east.cloud-object-storage.appdomain.cloud --target-crn "crn:v1:bluemix:public:cloud-object-storage:global:a/11111111111111111111111111111111:22222222-2222-2222-2222-222222222222::" --bucket "COS_BUCKET" --api-key COS_API_KEY --service-to-service-enabled false
```
{: pre}

Create a COS target that uses service-to-service authentication.

```sh
ibmcloud atracker target create --name TARGET_NAME --type cloud-object-storage --endpoint s3.private.us-east.cloud-object-storage.appdomain.cloud --target-crn "crn:v1:bluemix:public:cloud-object-storage:global:a/11111111111111111111111111111111:22222222-2222-2222-2222-222222222222::" --bucket "COS_BUCKET" --service-to-service-enabled true
```
{: pre}

### Create an {{site.data.keyword.messagehub_full}} target
{: #target-create-cli-ies}

Use this command to create a {{site.data.keyword.messagehub_full}} target to be used to configure a destination for activity events.

```sh
ibmcloud atracker target create --name TARGET_NAME --type TARGET_TYPE ( [--file EVENTSTREAMS_ENDPOINT_DEFINITION_JSON_FILE] | ( [--target-crn EVENTSTREAMS_TARGET_CRN] [--brokers BROKER_LIST] [--topic TOPIC] ( [--api-key ( EVENTSTREAMS_API_KEY | @EVENTSTREAMS_API_KEY_FILE )] | [--service-to-service-enabled ( TRUE | FALSE )] ) ) ) [--region REGION] [--output FORMAT]
```
{: pre}

#### Command options
{: #target-create-options-ies}

`--region REGION` | `-r REGION`
:   Name of the region that determines the {{site.data.keyword.atracker_full_notm}} API endpoint for the request, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--name TARGET_NAME`
:   The name to be given to the target.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--type TARGET_TYPE`
:   Set the `TARGET_TYPE` to `event-streams` for an {{site.data.keyword.messagehub}} target.

`--file EVENTSTREAMS_ENDPOINT_DEFINITION_JSON_FILE`
:   A file containing an endpoint definition in the following format:

    ```json
    {
      "target_crn": "TARGET_CRN",
      "brokers": ["broker-1:9093","broker-2:9093"],
      "topic": "my-topic",
      "api_key": "API_KEY"
    }
    ```
    {: codeblock}

`--target-crn EVENTSTREAMS_TARGET_CRN`
:   The CRN of the {{site.data.keyword.messagehub_full}} instance. You can get the [CRN](/docs/EventStreams?topic=EventStreams-connecting) from the service credentials.

`--brokers BROKER_LIST`
:   The list of {{site.data.keyword.messagehub}} brokers (endpoints). This is the value of the `kafka_brokers_sasl` in the service credentials.

`--topic TOPIC`
:   {{site.data.keyword.messagehub}} topic name to where the events are sent. This is the name of the topic created for an {{site.data.keyword.messagehub}} instance.

`--api-key EVENTSTREAMS_API_KEY` | `@EVENTSTREAMS_API_KEY_FILE`
:   The password value found in the {{site.data.keyword.messagehub}} service credential. This is the IAM API key.

`--service-to-service-enabled (TRUE | FALSE)`
:   Determines if {{site.data.keyword.atracker_full_notm}} has service to service authentication enabled. Set this option to `TRUE` if service to service is enabled and do not supply an API key.

`--output FORMAT`
:   The only supported format is JSON. If specified, the output is returned in JSON format. If `JSON` is not specified, the output is returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

#### Examples
{: #target-create-examples-ies}

Create an {{site.data.keyword.messagehub}} target that uses a customer-provided API key for authentication.

```sh
ibmcloud atracker target create --name TARGET_NAME --type event-streams --target-crn "crn:v1:bluemix:public:messagehub:eu-de:a/11111111111111111111111111111111:22222222-2222-2222-2222-222222222222::" --brokers "broker-1.kafka.svc11.region.eventstreams.cloud.ibm.com:9093,broker-2.kafka.svc11.region.eventstreams.cloud.ibm.com:9093" --topic "TOPIC" --api-key EVENTSTREAMS_API_KEY --service-to-service-enabled false
```
{: pre}

Create an {{site.data.keyword.messagehub}} target that uses service-to-service authentication.

```sh
ibmcloud atracker target create --name TARGET_NAME --type event-streams --target-crn "crn:v1:bluemix:public:messagehub:eu-de:a/11111111111111111111111111111111:22222222-2222-2222-2222-222222222222::" --brokers "broker-1.kafka.svc11.region.eventstreams.cloud.ibm.com:9093,broker-2.kafka.svc11.region.eventstreams.cloud.ibm.com:9093" --topic "TOPIC" --service-to-service-enabled true
```
{: pre}

### Create an {{site.data.keyword.logs_full_notm}} target
{: #target-create-cli-icl}

Use this command to create an {{site.data.keyword.logs_full_notm}} target to be used to configure a destination for activity events.

```sh
ibmcloud atracker target create --name TARGET_NAME --type TARGET_TYPE ( [--file CLOUDLOGS_ENDPOINT_DEFINITION_JSON_FILE] | ( [--target-crn CLOUDLOGS_TARGET_CRN] ) ) [--region REGION] [--output FORMAT]
```
{: pre}

#### Command options
{: #target-create-options-icl}

`--region REGION` | `-r REGION`
:   Name of the region that determines the {{site.data.keyword.atracker_full_notm}} API endpoint for the request, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--name TARGET_NAME`
:   The name to be given to the target.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--type TARGET_TYPE`
:   Set the `TARGET_TYPE` to `cloud-logs` for an {{site.data.keyword.logs_full_notm}} target.

`--file CLOUDLOGS_ENDPOINT_DEFINITION_JSON_FILE`
:   A file containing an endpoint definition in the following format:

    ```json
    {
      "target_crn": "TARGET_CRN"
    }
    ```
    {: codeblock}

`--target-crn CLOUDLOGS_TARGET_CRN`
:   The CRN of the {{site.data.keyword.logs_full_notm}} instance.

`--managed-by MANAGED_BY`
:   The owner of the target to be created. Valid values are `account` or `enterprise`.

`--output FORMAT`
:   The only supported format is JSON. If specified, the output is returned in JSON format. If `JSON` is not specified, the output is returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

#### Examples
{: #target-create-examples-icl}

Create an {{site.data.keyword.logs_full_notm}} target.

```sh
ibmcloud atracker target create --name TARGET_NAME --type cloud-logs --target-crn "crn:v1:bluemix:public:logs:eu-es:a/11111111111111111111111111111111:22222222-2222-2222-2222-222222222222::"
```
{: pre}

Create an {{site.data.keyword.logs_full_notm}} target that is managed by the enterprise.

```sh
ibmcloud atracker target create --name TARGET_NAME --type cloud-logs --target-crn "crn:v1:bluemix:public:logs:eu-es:a/11111111111111111111111111111111:22222222-2222-2222-2222-222222222222::" --managed-by enterprise
```
{: pre}



### Create an {{site.data.keyword.appconfig_full}} target
{: #target-create-cli-appconfig}

Use this command to create an {{site.data.keyword.appconfig_full}} target to be used to configure a destination for activity events.

```sh
ibmcloud atracker target create --name TARGET_NAME --type TARGET_TYPE ( [--target-crn APPCONFIG_TARGET_CRN] ) [--region REGION] [--output FORMAT]
```
{: pre}

#### Command options
{: #target-create-options-appconfig}

`--region REGION` | `-r REGION`
:   Name of the region that determines the {{site.data.keyword.atracker_full_notm}} API endpoint for the request, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--name TARGET_NAME`
:   The name to be given to the target.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--type TARGET_TYPE`
:   Set the `TARGET_TYPE` to `app-config` for an {{site.data.keyword.appconfig_notm}} target.

`--target-crn APPCONFIG_TARGET_CRN`
:   The CRN of the {{site.data.keyword.appconfig_notm}} instance.

`--managed-by MANAGED_BY`
:   The owner of the target to be created. Valid values are `account` or `enterprise`.

`--output FORMAT`
:   The only supported format is JSON. If specified, the output is returned in JSON format. If `JSON` is not specified, the output is returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

#### Examples
{: #target-create-examples-appconfig}

Create an {{site.data.keyword.appconfig_notm}} target.

```sh
ibmcloud atracker target create --name TARGET_NAME --type app-config --target-crn "crn:v1:bluemix:public:apprapp:us-south:a/11111111111111111111111111111111:22222222-2222-2222-2222-222222222222::"
```
{: pre}

Create an {{site.data.keyword.appconfig_notm}} target that is managed by the enterprise.

```sh
ibmcloud atracker target create --name TARGET_NAME --type app-config --target-crn "crn:v1:bluemix:public:apprapp:us-south:a/11111111111111111111111111111111:22222222-2222-2222-2222-222222222222::" --managed-by enterprise
```
{: pre}



## `ibmcloud atracker target update`
{: #target-update-v2-cli}

Use this command to update the properties of an {{site.data.keyword.atracker_short}} target. Any specified value that is different from when the target was originally created will be updated to the value specified in the command. The options that you specify depend on the type of target that you update.

### Update a {{site.data.keyword.cos_full_notm}} target
{: #target-update-v2-cli-cos}

Use this command to update a {{site.data.keyword.cos_full_notm}} target.

```text
ibmcloud atracker target update --target TARGET [--name TARGET_NAME] [ [--file COS_ENDPOINT_DEFINITION_JSON_FILE] | ( [--endpoint COS_ENDPOINT] [--bucket COS_BUCKET] [--target-crn COS_TARGET_CRN] ( [--api-key ( COS_API_KEY | @COS_API_KEY_FILE )] | [--service-to-service-enabled ( TRUE | FALSE )] ) ) ] [--output FORMAT]
```
{: pre}

#### Command options
{: #target-update-options-cos}

`--target TARGET`
:   The ID or current target name.

`--name TARGET_NAME`
:   The name to be given to the target.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--file COS_ENDPOINT_DEFINITION_JSON_FILE`
:   A file containing an endpoint definition in the following format:

    ```json
    {
      "endpoint": "ENDPOINT",
      "target_crn": "TARGET_CRN",
      "bucket": "BUCKET",
      "api_key": "API_KEY"
    }
    ```
    {: codeblock}

    or for a scenario where service-to-service authentication is enabled:

    ```json
    {
      "endpoint": "ENDPOINT",
      "target_crn": "TARGET_CRN",
      "bucket": "BUCKET",
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
:   Your [API key](/docs/iam?topic=iam-manapikey) value or a reference to the API Key file used to gain access.  For example, `ibmcloud login --apikey $KEYFILE`

`--service-to-service-enabled (TRUE | FALSE)`
:   Indicates if [service-to-service authorization](/docs/atracker?topic=atracker-iam-service-auth-cos&interface=ui) has been enabled for the bucket.  Specify `TRUE` if service-to-service authorization is enabled and `FALSE` if service-to-service authorization is not enabled.  By default, service-to-service authorization is `FALSE`.

`--output FORMAT`
:   The only supported format is JSON. If specified, the output is returned in JSON format. If `JSON` is not specified, the output is returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

#### Examples
{: #target-update-examples-cos}

Update a COS target by using an endpoint definition JSON file.

```sh
ibmcloud atracker target update --target TARGET --name TARGET_NAME --file COS_ENDPOINT_DEFINITION_JSON_FILE
```
{: pre}

Update a COS target that uses a customer-provided API key for authentication.

```sh
ibmcloud atracker target update --target TARGET --name TARGET_NAME --endpoint s3.private.us-east.cloud-object-storage.appdomain.cloud --target-crn "crn:v1:bluemix:public:cloud-object-storage:global:a/11111111111111111111111111111111:22222222-2222-2222-2222-222222222222::" --bucket "COS_BUCKET" --api-key @COS_API_KEY_FILE --service-to-service-enabled false
```
{: pre}

Update a COS target that uses service-to-service authentication.

```sh
ibmcloud atracker target update --target TARGET --name TARGET_NAME --endpoint s3.private.us-east.cloud-object-storage.appdomain.cloud --target-crn "crn:v1:bluemix:public:cloud-object-storage:global:a/11111111111111111111111111111111:22222222-2222-2222-2222-222222222222::" --bucket "COS_BUCKET" --service-to-service-enabled true
```
{: pre}

### Update an {{site.data.keyword.messagehub_full}} target
{: #target-update-cli-ies}

Use this command to update an {{site.data.keyword.messagehub}} target.

```text
ibmcloud atracker target update --target TARGET [--name TARGET_NAME] [ [--file EVENTSTREAMS_ENDPOINT_DEFINITION_JSON_FILE] | ( [--brokers BROKER_LIST] [--target-crn EVENTSTREAMS_TARGET_CRN] [--topic TOPIC] ( [--api-key ( EVENTSTREAMS_API_KEY | @EVENTSTREAMS_API_KEY_FILE )] | [--service-to-service-enabled ( TRUE | FALSE )] ) ) ] [--output FORMAT]
```
{: pre}

#### Command options
{: #target-update-options-ies}

`--target TARGET`
:   The ID or current target name.

`--name TARGET_NAME`
:   The name to be given to the target.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--file EVENTSTREAMS_ENDPOINT_DEFINITION_JSON_FILE`
:   A file containing an endpoint definition in the following format:

    ```json
    {
      "target_crn": "TARGET_CRN",
      "brokers": ["broker-1:9093","broker-2:9093"],
      "topic": "my-topic",
      "api_key": "API_KEY"
    }
    ```
    {: codeblock}

`--target-crn EVENTSTREAMS_TARGET_CRN`
:   The CRN of the {{site.data.keyword.messagehub_full}} instance. You can get the [CRN](/docs/EventStreams?topic=EventStreams-connecting) from the service credentials.

`--brokers BROKER_LIST`
:   The list of {{site.data.keyword.messagehub}} brokers (endpoints). This is the value of the `kafka_brokers_sasl` in the service credentials.

`--topic TOPIC`
:   {{site.data.keyword.messagehub}} topic name to where the events are sent. This is the name of the topic created for an {{site.data.keyword.messagehub}} instance.

`--api-key EVENTSTREAMS_API_KEY` | `@EVENTSTREAMS_API_KEY_FILE`
:   The password value found in the {{site.data.keyword.messagehub}} service credential. This is the IAM API key.

`--service-to-service-enabled (TRUE | FALSE)`
:   Determines if {{site.data.keyword.atracker_full_notm}} has service to service authentication enabled. Set this option to `TRUE` if service to service is enabled and do not supply an API key.

`--output FORMAT`
:   The only supported format is JSON. If specified, the output is returned in JSON format. If `JSON` is not specified, the output is returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

#### Examples
{: #target-update-examples-ies}

Update an {{site.data.keyword.messagehub}} target that uses a customer-provided API key for authentication.

```sh
ibmcloud atracker target update --target TARGET --name TARGET_NAME --target-crn "crn:v1:bluemix:public:messagehub:eu-de:a/11111111111111111111111111111111:22222222-2222-2222-2222-222222222222::" --brokers "broker-1.kafka.svc11.region.eventstreams.cloud.ibm.com:9093,broker-2.kafka.svc11.region.eventstreams.cloud.ibm.com:9093" --topic "TOPIC" --api-key EVENTSTREAMS_API_KEY --service-to-service-enabled false
```
{: pre}

Update an {{site.data.keyword.messagehub}} target that uses service-to-service authentication.

```sh
ibmcloud atracker target update --target TARGET --name TARGET_NAME --target-crn "crn:v1:bluemix:public:messagehub:eu-de:a/11111111111111111111111111111111:22222222-2222-2222-2222-222222222222::" --brokers "broker-1.kafka.svc11.region.eventstreams.cloud.ibm.com:9093,broker-2.kafka.svc11.region.eventstreams.cloud.ibm.com:9093" --topic "TOPIC" --service-to-service-enabled true
```
{: pre}

### Update an {{site.data.keyword.logs_full_notm}} target
{: #target-update-cli-icl}

Use this command to update an {{site.data.keyword.logs_full_notm}} target.

```sh
ibmcloud atracker target update --target TARGET [--name TARGET_NAME] [ [--file CLOUDLOGS_ENDPOINT_DEFINITION_JSON_FILE] | ( [--target-crn CLOUDLOGS_TARGET_CRN] ) ] [--output FORMAT]
```
{: pre}

#### Command options
{: #target-update-options-icl}

`--target TARGET`
:   The ID or current target name.

`--name TARGET_NAME`
:   The name to be given to the target.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--file CLOUDLOGS_ENDPOINT_DEFINITION_JSON_FILE`
:   A file containing an endpoint definition in the following format:

    ```json
    {
      "target_crn": "TARGET_CRN"
    }
    ```
    {: codeblock}

`--target-crn CLOUDLOGS_TARGET_CRN`
:   The CRN of the {{site.data.keyword.logs_full_notm}} instance.

`--output FORMAT`
:   The only supported format is JSON. If specified, the output is returned in JSON format. If `JSON` is not specified, the output is returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

#### Examples
{: #target-update-examples-icl}

Update an {{site.data.keyword.logs_full_notm}} target.

```sh
ibmcloud atracker target update --target TARGET --name TARGET_NAME --target-crn "crn:v1:bluemix:public:logs:eu-es:a/11111111111111111111111111111111:22222222-2222-2222-2222-222222222222::"
```
{: pre}



### Update an {{site.data.keyword.appconfig_full}} target
{: #target-update-cli-appconfig}

Use this command to update an {{site.data.keyword.appconfig_full}} target.

```sh
ibmcloud atracker target update --target TARGET [--name TARGET_NAME] [ [--target-crn APPCONFIG_TARGET_CRN] ] [--output FORMAT]
```
{: pre}

#### Command options
{: #target-update-options-appconfig}

`--target TARGET`
:   The ID or current target name.

`--name TARGET_NAME`
:   The name to be given to the target.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--target-crn APPCONFIG_TARGET_CRN`
:   The CRN of the {{site.data.keyword.appconfig_notm}} instance.

`--output FORMAT`
:   The only supported format is JSON. If specified, the output is returned in JSON format. If `JSON` is not specified, the output is returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

#### Examples
{: #target-update-examples-appconfig}

Update an {{site.data.keyword.appconfig_notm}} target.

```sh
ibmcloud atracker target update --target TARGET --name TARGET_NAME --target-crn "crn:v1:bluemix:public:apprapp:us-south:a/11111111111111111111111111111111:22222222-2222-2222-2222-222222222222::"
```
{: pre}



## `ibmcloud atracker target rm`
{: #target-delete-v2-cli}

Use this command to delete an {{site.data.keyword.atracker_short}} target. Events are no longer sent to the deleted target. 

```sh
ibmcloud atracker target rm --target TARGET [--force]
```
{: pre}

### Command options
{: #target-rm-v2-options-cos}

`--target TARGET`
:   The ID or name of the target.

`--force`
:   Runs the command without prompting you to confirm that you want to continue.

`help` | `--help` | `-h`
:   List options available for the command.

### Examples
{: #target-rm-examples}


Delete a target.

```sh
ibmcloud atracker target rm --target TARGET
```
{: pre}

Delete a target without being prompted to confirm.

```sh
ibmcloud atracker target rm --target TARGET --force
```
{: pre}

## `ibmcloud atracker target validate`
{: #target-validate-v2-cli}

Use this command to validate an {{site.data.keyword.atracker_short}} target with its destination service, such as {{site.data.keyword.cos_full_notm}}. Validation confirms that the target is correctly configured. 

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
:   The only supported format is JSON. If specified, the output is returned in JSON format. If `JSON` is not specified, the output is returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Examples
{: #target-validate-examples}


Validate a target.

```sh
ibmcloud atracker target validate --target TARGET
```
{: pre}

Validate a target by using the {{site.data.keyword.atracker_short}} API endpoint of a specific region.

```sh
ibmcloud atracker target validate --target TARGET --region us-south
```
{: pre}

## `ibmcloud atracker target get`
{: #target-get-v2-cli-cos}

Use this command to get detailed information about an {{site.data.keyword.atracker_short}} target, such as its type and configuration. 

```sh
ibmcloud atracker target get --target TARGET [--output FORMAT]
```
{: pre}

### Command options
{: #target-get-v2-options-cos}

`--target TARGET`
:   The ID or name of the target.

`--output FORMAT`
:   The only supported format is JSON. If specified, the output is returned in JSON format. If `JSON` is not specified, the output is returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Examples
{: #target-get-examples}


Get information about a target.

```sh
ibmcloud atracker target get --target TARGET
```
{: pre}

Get information about a target in JSON format.

```sh
ibmcloud atracker target get --target TARGET --output JSON
```
{: pre}

## `ibmcloud atracker target ls`
{: #target-list-v2-cli-cos}

Use this command to list the {{site.data.keyword.atracker_short}} targets that are configured for your account in a region. A target is a destination to which activity events are sent. 

```sh
ibmcloud atracker target ls [--output FORMAT]
```
{: pre}

### Command options
{: #target-v2-options-cos}

`--output FORMAT`
:   The only supported format is JSON. If specified, the output is returned in JSON format. If `JSON` is not specified, the output is returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Examples
{: #target-ls-examples}


List all targets.

```sh
ibmcloud atracker target ls
```
{: pre}

List all targets in JSON format.

```sh
ibmcloud atracker target ls --output JSON
```
{: pre}

## `ibmcloud atracker setting get`
{: #settings-get-v2-cli}

Use this command to get the current {{site.data.keyword.atracker_short}} settings for your account, such as the default targets, permitted target regions, and metadata regions. 

```sh
ibmcloud atracker setting get [--output FORMAT]
```
{: pre}

### Command options
{: #settings-get-v2-options}

`--output FORMAT`
:   If `JSON` is specified, the output is returned in JSON format. If `JSON` is not specified, the output is returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Examples
{: #settings-get-examples}


Get the settings for your account.

```sh
ibmcloud atracker setting get
```
{: pre}

Get the settings for your account in JSON format.

```sh
ibmcloud atracker setting get --output JSON
```
{: pre}

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

`--default-targets TARGET`
:   A comma-separated list of target IDs. If no routing rules cause events to be sent to other targets, these targets receive the events.

`--permitted-target-regions REGIONS`
:   A comma-separated list of regions that can be used to define a target. A maximum of two permitted target regions can be specified.

`--metadata-region-primary REGION`
:   The region where the metadata associated with route and target definitions is stored.

`--metadata-region-backup REGION`
:   The region where the metadata associated with route and target definitions is stored as a backup location.

`--private-api-endpoint-only (TRUE | FALSE)`
:   Specifies whether a private endpoint can be used.  If `TRUE`, only a private endpoint can be used.

`--force`
:   Runs the command without prompting you to confirm that you want to continue.

`--output FORMAT`
:   If `JSON` is specified, the output is returned in JSON format. If `JSON` is not specified, the output is returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Examples
{: #settings-update-examples}


Set the primary and backup metadata regions.

```sh
ibmcloud atracker setting update --metadata-region-primary us-south --metadata-region-backup us-east
```
{: pre}

Set the default targets.

```sh
ibmcloud atracker setting update --default-targets 11111111-1111-1111-1111-111111111111,22222222-2222-2222-2222-222222222222
```
{: pre}

Restrict the regions that can be used to define a target.

```sh
ibmcloud atracker setting update --permitted-target-regions us-south,us-east
```
{: pre}

## `ibmcloud atracker help`
{: #atracker-help-v2-cli}

Alias: `h`

Use this command to display help for {{site.data.keyword.atracker_short}} CLI commands.

```sh
ibmcloud atracker help [COMMAND]
```
{: pre}

### Command options
{: #atracker-help-v2-options}

`COMMAND`
:   The name of the command for which to display help. If not specified, help for all available {{site.data.keyword.atracker_short}} commands is displayed.

`help` | `--help` | `-h`
:   List options available for the command.

### Examples
{: #atracker-help-examples}


Display help for all {{site.data.keyword.atracker_short}} commands.

```sh
ibmcloud atracker help
```
{: pre}

## `ibmcloud atracker route help`
{: #route-help-v2-cli}

Alias: `h`

Use this command to display help for `ibmcloud atracker route` subcommands.

```sh
ibmcloud atracker route help [COMMAND]
```
{: pre}

### Command options
{: #route-help-v2-options}

`COMMAND`
:   The name of the route subcommand for which to display help. If not specified, help for all available `ibmcloud atracker route` subcommands is displayed.

`help` | `--help` | `-h`
:   List options available for the command.

### Examples
{: #route-help-examples}


Display help for all `ibmcloud atracker route` subcommands.

```sh
ibmcloud atracker route help
```
{: pre}

## `ibmcloud atracker setting help`
{: #setting-help-v2-cli}

Alias: `h`

Use this command to display help for `ibmcloud atracker setting` subcommands.

```sh
ibmcloud atracker setting help [COMMAND]
```
{: pre}

### Command options
{: #setting-help-v2-options}

`COMMAND`
:   The name of the setting subcommand for which to display help. If not specified, help for all available `ibmcloud atracker setting` subcommands is displayed.

`help` | `--help` | `-h`
:   List options available for the command.

### Examples
{: #setting-help-examples}


Display help for all `ibmcloud atracker setting` subcommands.

```sh
ibmcloud atracker setting help
```
{: pre}

## `ibmcloud atracker target help`
{: #target-help-v2-cli}

Alias: `h`

Use this command to display help for `ibmcloud atracker target` subcommands.

```sh
ibmcloud atracker target help [COMMAND]
```
{: pre}

### Command options
{: #target-help-v2-options}

`COMMAND`
:   The name of the target subcommand for which to display help. If not specified, help for all available `ibmcloud atracker target` subcommands is displayed.

`help` | `--help` | `-h`
:   List options available for the command.

### Examples
{: #target-help-examples}


Display help for all `ibmcloud atracker target` subcommands.

```sh
ibmcloud atracker target help
```
{: pre}

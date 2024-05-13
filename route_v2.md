---

copyright:
  years: 2022, 2024
lastupdated: "2024-05-06"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Managing routes
{: #route_v2}

You can manage routes in your account by using the {{site.data.keyword.atracker_full}} CLI, {{site.data.keyword.atracker_short}} REST API, and Terraform scripts. A route defines the rules that indicate what auditing events are routed in a region and where to route them.
{: shortdesc}

## Understanding how routes work in your account
{: #route_behaviour}

Note the following information about routes:

* Routes are global under an account and are evaluated in all regions where {{site.data.keyword.atracker_full}} is deployed.

* Routes may be accessed from any regional {{site.data.keyword.atracker_short}} API endpoint.

* You can define up to 10 routes for an account.

* By default, the account has 0 routes configured.

* You can configure up to 30 rules for each route.

* You can configure up to 8 locations for each rule.

* You can configure up to 3 targets (`target_ids`) for each rule.

* Routes are processed independently.  If you have multiple routes with rules that match the same event, that event will be sent to multiple targets.

* Rules are processed in order.  The first matching rule (for example,  `location`) an event matches will be used to process the event.  Once an event has been processed it will not be processed by a subsequent rule within that route's definition. If you want to specify a default rule for all events that were not processed by other rules you would specify the rule (`"locations" : ["*"]`) as the final rule in your `rules` definition for the `route`.

* If an event doesn't match any rule and no default target is configured, the event will be dropped and not routed to any target.

* Any update to a `rules` configuration must include all `location` rules.  An update will discard the existing rule set and replace it with the specified configuration.

After you configure a route, it might take up to 1 hour for the configuration to be enabled.
{: note}

The target defines where auditing events are collected. The target can be an [{{site.data.keyword.cos_full_notm}} (COS) target](/docs/atracker?topic=atracker-target_v2_cos), an [{{site.data.keyword.at_short}} hosted event search target](/docs/atracker?topic=atracker-target_v2_at) or an [{{site.data.keyword.messagehub_full}} target](/docs/atracker?topic=atracker-target_v2_ies&interface=cli).  The route defines what auditing events are routed to a target.

The following sample route definition will:
- send all `us-south`, `us-east` and `global` events to the target identified by the ID `281f78a2-3333-4444-5555-e896f03cb403`
- drop events for all other regions unless there is a default target defined in the settings

```json
{
    "id": "959ceeaf-9999-9999-9999-b7ad27a3e109",
    "name": "my-route",
    "crn": "crn:v1:bluemix:public:atracker:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx:route:959ceeaf-9999-9999-9999-b7ad27a3e109",
    "version": 0,
    "rules": [
        {
            "locations": ["us-south", "us-east", "global"],
            "target_ids": [
                "281f78a2-3333-4444-5555-e896f03cb403"
            ]
        }
    ],
    "created": "0001-01-01T00:00:00Z"
}
```
{: screen}

There are 2 types of auditing events:
- [Global events](/docs/atracker?topic=atracker-event_types#event_types_global)
- [Location-based events](/docs/atracker?topic=atracker-event_types#event_types_location)

To include global events in a route, specify `global` in the list of `locations`.

## IAM Access
{: #route_access}

You must grant users IAM permissions to manage routes. For more information, see [Assign access to resources](/docs/account?topic=account-assign-access-resources).

When you define a policy, you can must set the scope of the policy to the account. A route is a global resource that is not bound to a specific region.
{: note}


| IAM action               | IAM Policy scope  | IAM Roles                          | Description         |
| ------------------------ | ----------------- | ---------------------------------- | ------------------- |
| `atracker.route.read` | Account | `Administrator`  \n `Editor`  \n `Viewer`  \n `Operator` | Read (view) information about a route |
| `atracker.route.create` | Account | `Administrator`  \n `Editor` | Create a route |
| `atracker.route.update` | Account | `Administrator`  \n `Editor` | Update a route |
| `atracker.route.delete` | Account | `Administrator`  \n `Editor` | Delete a route |
| `atracker.route.list` | Account | `Administrator`  \n `Editor`  \n `Viewer`  \n `Operator` | List all routes |
{: caption="Table 1. Required IAM roles}

## CLI prerequisites
{: #route-prereqs-cli}
{: cli}

Before you use the the CLI to manage routes, install the latest {{site.data.keyword.atracker_short}} CLI V2 plugin in your local system. See [Installing the {{site.data.keyword.atracker_short}} CLI](/docs/atracker?topic=atracker-atracker-cli-config&interface=cli).

Next, log in to the {{site.data.keyword.cloud_notm}}. Run the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)



## Creating a route using the CLI
{: #route-create-cli}
{: cli}

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

### Example
{: #route-create-example}

The following is an example using the **`ibmcloud atracker route create --name dev-eu-de-route --target_ids 33333333-3333-3333-3333-333333333333 --locations us-south`** command to create a route with 1 routing rule.

```text
OK
Route
Name:                    dev-eu-de-route
ID:                      44444444-4444-4444-4444-444444444444
CRN:                     crn:v1:staging:public:atracker:eu-de:a/11111111111111111111111111111111::route:44444444-4444-4444-4444-444444444444
Version:                 0
Rules:                   [locations: [us-south], target_ids: [33333333-3333-3333-3333-333333333333]]
Created:                 2022-02-24T21:10:09.996Z
Updated:                 2022-02-24T21:10:09.996Z
```
{: screen}

## Updating a route using the CLI
{: #route-update-cli}
{: cli}

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

### Example
{: #route-update-example}

The following is an example using the **`ibmcloud atracker route update --route dev-eu-de-route --target_ids 55555555-5555-5555-5555-555555555555 --locations *`** command.

```text
OK
Route
Name:                    dev-eu-de-route
ID:                      44444444-4444-4444-4444-444444444444
CRN:                     crn:v1:staging:public:atracker:eu-de:a/11111111111111111111111111111111::route:44444444-4444-4444-4444-444444444444
Version:                 1
Rules:                   [locations: [*], target_ids: [55555555-5555-5555-5555-555555555555]]
Created:                 2022-02-24T21:10:09.996Z
Updated:                 2022-02-24T21:13:37.218Z
```
{: screen}

## Deleting a route using the CLI
{: #route-delete-cli}
{: cli}

Use this command to delete an {{site.data.keyword.atracker_short}} route.

```sh
ibmcloud atracker route rm --route ROUTE [--force]
```
{: pre}

### Command options
{: #route-rm-options}

`--route ROUTE`
:   The name or ID of the route to be deleted.

`--force`
:   Will delete the route without providing the user with any additional prompt.

`help` | `--help` | `-h`
:   List options available for the command.


### Example
{: #route-rm-example}

The following is an example using the **`ibmcloud atracker route rm --route 44444444-4444-4444-4444-444444444444`** command.

```text
Are you sure you want to remove the route with the Route ID 44444444-4444-4444-4444-444444444444? [y/N]> y
OK
Route with route ID 44444444-4444-4444-4444-444444444444 was successfully removed.
```
{: screen}

The following is an example using the **`ibmcloud atracker route rm --route 33333333-3333-3333-3333-333333333333`** command.

This example shows a failed command where the specified route could not be found.
{: note}

```text
FAILED
No route found with route name - 33333333-3333-3333-3333-333333333333
```
{: screen}

## Viewing a route using the CLI
{: #route-view-cli}
{: cli}

Use this command to get information about an {{site.data.keyword.atracker_short}} route.

```sh
ibmcloud atracker route get --route ROUTE [--output FORMAT]
```
{: pre}

### Command options
{: #route-get-options}

`--route <ROUTE_ID>`
:   The name or ID of the route.

`--output FORMAT`
:   If `JSON` is specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #route-get-example}

The following is an example using the **`ibmcloud atracker route get --route 44444444-4444-4444-4444-444444444444`** command.

```text
OK
Route
Name:                    dev-eu-de-route-0
ID:                      44444444-4444-4444-4444-444444444444
CRN:                     crn:v1:staging:public:atracker:eu-de:a/11111111111111111111111111111111::route:44444444-4444-4444-4444-444444444444
Version:                 2
Rules:                   [locations: [us-south], target_ids: [55555555-5555-5555-5555-555555555555]]
Created:                 2022-02-24T21:10:09.996Z
Updated:                 2022-02-24T21:15:07.281Z
```
{: screen}

## Listing all routes using the CLI
{: #route-list-cli}
{: cli}

Use this command to list all the configured routes for {{site.data.keyword.atracker_short}} .

```sh
ibmcloud atracker route ls [--output FORMAT]
```
{: pre}

### Command options
{: #route-ls-options}

`--output FORMAT`
:   If `JSON` is specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.


### Example
{: #route-ls-example}

The following is an example using the **`ibmcloud atracker route ls`** command which returns the routes for all regions.

```text
Name                      ID                                     Rules                                              Route Version   API version   CreatedAt                  UpdatedAt
my-global-route           aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa   [[11111111-1111-1111-1111-111111111111],[global]]  5               2             2022-05-04T20:18:00.595Z   2022-05-05T19:04:58.374Z
send-all-to-us-east       bbbbbbbb-bbbb-bbbb-bbbb-bbbbbbbbbbbb   [[22222222-2222-2222-2222-222222222222],[*]]       0               2             2022-05-06T12:02:47.832Z   2022-05-06T12:02:47.832Z
```
{: screen}



## API routes and actions
{: #target-actions-api}
{: api}

The following table lists the actions that you can run to manage routes:

| Action                     | REST API Method  | API_URL                                          |
|----------------------------|------------------|--------------------------------------------------|
| Create a route            | `POST`           | `<ENDPOINT>/api/v2/routes`              |
| Update a route            | `PUT`            | `<ENDPOINT>/api/v2/routes/<ROUTE_ID>`  |
| Delete a route            | `DELETE`         | `<ENDPOINT>/api/v2/routes/<ROUTE_ID>`  |
| Get information about a route             | `GET`            | `<ENDPOINT>/api/v2/routes/<ROUTE_ID>`  |
| List all routes           | `GET`            | `<ENDPOINT>/api/v2/routes`             |
{: caption="Table 1. Target actions by using the {{site.data.keyword.atracker_short}} REST API" caption-side="top"}

You can use private and public endpoints to manage routes. For more information about the list of `ENDPOINTS` that are available, see [Endpoints](/docs/atracker?topic=atracker-endpoints).

* You can manage routes from the private network using an API endpoint with the following format: `https://private.REGION.atracker.cloud.ibm.com`.
* You can manage routes from the public network using an API endpoint with the following format: `https://REGION.atracker.cloud.ibm.com`.
* Since the routes are global configurations, you can use any regional endpoint to manage the routes for the account.

* You can disable the public endpoints by updating the account settings. For more information, see [Configuring target and region settings](/docs/atracker?topic=atracker-settings).

For more information about the REST API, see [Routes](/apidocs/atracker#create-route).
{: note}

## API prerequsites
{: #route-target-prereqs-api}
{: api}

To make API calls to manage routes, complete the following steps:
1. Get an IAM access token. For more information, see [Retrieving IAM access tokens](/docs/atracker?topic=atracker-retrieve-iam-token).
2. Identify the API endpoint in the region where you plan to configure or manage a route. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).


## Creating a route using the API
{: #route-create-api}
{: api}

You must [create a target](/docs/atracker?topic=atracker-target_v2) before you create a route.

You can use the following cURL command to create a route:

```shell
curl -X POST  <ENDPOINT>/api/v2/routes   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"  -d '{
    "name": "ROUTE_NAME",
    "rules": [
      {
        "locations": ["LOCATIONS"],
        "target_ids": ["TARGET_ID"]
      }
    ]
  }'
```
{: codeblock}

Where

- `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a route. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).
- `ROUTE_NAME` is the name of the route. The maximum length of the name is 180 characters and cannot include any of the following special characters:`-`, `.`, `_`, `:`.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

- `LOCATIONS` is a list of locations associated with the route.  Specify `global` to include global events. To include all locations specify `*`.  If you have multiple rules, along with a rule with a `*` location, then the other rules will route events to the specified targets with any events not matching any other rule routing the remaining events to the target specified by the rule with the `*` location.
- `TARGET_ID` is the GUID of the target that defines where auditing events are routed and collected. This can include GUIDs of targets in other regions. If `TARGET_ID` is empty, any events matching the rule will be discarded.

For example, you can use the following cURL request to create a route that defines how global and US-South location-based events are collected and routed in the account:

```shell
curl -X POST   https://private.us-south.atracker.cloud.ibm.com/api/v2/routes   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"  -d '{
    "name": "my-route",
    "rules": [
      {
        "locations": ["us-south", "global"],
        "target_ids": ["22222222-2222-2222-2222-222222222222"]
      }
    ]
  }'
```
{: screen}

In the response, you get information about the route such as the `id`, that indicates the GUID of the route, and the `crn`, that indicates the CRN of the route.


## Updating a route using the API
{: #route-update-api}
{: api}

When you update a route, you must include the route information in the data section of the request.
- You must pass all fields.
- Update the fields that need changing.

You can use the following cURL command to update a route:

```shell
curl -X PUT  <ENDPOINT>/api/v2/routes/<ROUTE_ID>   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"  -d '{
    "name": "ROUTE_NAME",
    "rules": [
      {
        "locations": ["LOCATIONS"],
        "target_ids": ["TARGET_ID"]
      }
    ]
  }'
```
{: codeblock}

Where
- `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a route. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).
- `<ROUTE_ID>` is the ID of the route to be updated
- `ROUTE_NAME` is the name of the route. The maximum length of the name is 180 characters and cannot include any of the following special characters:`-`, `.`, `_`, `:`.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

- `LOCATIONS` is a list of locations associated with the route.  Specify `global` to include global events. To include all locations specify `*`.  If you have multiple rules, along with a rule with a `*` location, then the other rules will route events to the specified targets with any events not matching any other rule routing the remaining events to the target specified by the rule with the `*` location.
- `TARGET_ID` is the GUID of the target that defines where auditing events are routed and collected. This can include GUIDs of targets in other regions.  If `TARGET_ID` is empty, any events matching the rule will be discarded.


For example, you can use the following cURL request to update a route that defines how global and US-South and US-East location-based events are collected and routed in the account:

```shell
curl -X PUT https://private.us-south.atracker.cloud.ibm.com/api/v2/routes/aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"  -d '{
    "name": "my-route",
    "rules": [
      {
        "locations": ["us-south", "global", "us-east],
        "target_ids": ["22222222-2222-2222-2222-222222222222"]
      }
    ]
  }'
```
{: screen}



## Deleting a route using the API
{: #route-delete-api}
{: api}

You can use the following cURL command to delete a route:

```text
curl -X DELETE   <ENDPOINT>/api/v2/routes/<ROUTE_ID>   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"
```
{: codeblock}

Where
- `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a route. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).
- `<ROUTE_ID>` is the ID of the route to be deleted

For example, you can run the following cURL request to delete the route with the ID `aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa`:

```shell
curl -X DELETE  https://private.us-south.atracker.cloud.ibm.com/api/v2/routes/aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"
```


## Viewing a route using the API
{: #route-view-api}
{: api}

You can use the following cURL command to view 1 route:

```text
curl -X GET   <ENDPOINT>/api/v2/routes/<ROUTE_ID>   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"
```
{: codeblock}

Where
- `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a route. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).
- `<ROUTE_ID>` is the ID of the route to be fetched

For example, you can run the following cURL request to get information about a route with the ID `aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa`:

```shell
curl -X GET   https://private.us-south.atracker.cloud.ibm.com/api/v2/routes/aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa    -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"
```
{: screen}


## Listing all routes in a region using the API
{: #route-list-api}
{: api}

You can use the following cURL command to view all routes:

```text
curl -X GET   <ENDPOINT>/api/v2/routes   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"
```
{: codeblock}

Where
- `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a route. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).

For example, you can run the following cURL request to get information about the routes that are defined in US South:

```shell
curl -X GET   https://private.us-south.atracker.cloud.ibm.com/api/v2/routes    -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"
```
{: screen}


## HTTP response codes
{: #route-target-rc}
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
{: caption="Table 2. List of HTTP response codes" caption-side="top"}

---

copyright:
  years: 2019, 2023
lastupdated: "2022-05-24"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Managing routes using the V1 API
{: #route}

You can manage routes in your account by using the {{site.data.keyword.atracker_full}} CLI or {{site.data.keyword.atracker_full_notm}} REST API. A route defines the rules that indicate what auditing events are collected in a region and where to store them.
{: shortdesc}

The V1 API is deprecated. See [managing routes using the V2 API](/docs/atracker?topic=atracker-route_v2) for information on using the V2 API.  Also see [migrating resources](/docs/atracker?topic=atracker-migrate-resources) for information on migrating from your V1 configuration.
{: deprecated}

The version of the API running in your account can be determined by running the [`ibmcloud atracker init version` command.](/docs/atracker?topic=atracker-v2api)
{: note}

## Understanding how routes work in your account
{: #route_behaviour}

Note the following information about routes:
- You can define 1 route per region.
- By default, the account has 0 routes configured.
- You can configure 1 or more rules for each route.
- You can configure 1 target for each rule.
- If you plan to share a target across multiple regions, you must define the target in each region. You can only configure a route with a target that is defined in the same region.
- For each rule, you must specify what auditing events are affected by the rule. In additon, you must define the target where you want the auditing events to be collected.
- You can only configure 1 route for each account to collect global events.

After you configure a route, it takes over 1 hour for the configuration to be enabled in that region.
{: note}

The target defines where auditing events are collected. The route defines what auditing events are collected in a target.

A route definition is similar to the follows:

```json
{
    "id": "959ceeaf-9999-9999-9999-b7ad27a3e109",
    "name": "my-route",
    "instance_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "receive_global_events": true,
    "crn": "crn:v1:bluemix:public:atracker:us-south:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx:route:959ceeaf-9999-9999-9999-b7ad27a3e109",
    "version": 0,
    "rules": [
        {
            "target_ids": [
                "281f78a2-3333-4444-5555-e896f03cb403"
            ]
        }
    ],
    "updated": "0001-01-01T00:00:00Z"
}
```
{: screen}

There are 2 types of auditing events:
- [Global events](/docs/atracker?topic=atracker-event_types#event_types_global)
- [Location-based events](/docs/atracker?topic=atracker-event_types#event_types_location)

When you configure a route in a region, you must specify the type of event. When you set `receive_global_events` to true or false, you are indicating the type of events that are collected in the region:
* When you set `receive_global_events` to true, you are indicating that you want global events and location-based events to go to the target that is configured in the rule that is defined in the route.
* When you set `receive_global_events` to false, you are indicating that you want location-based events to go to the target that is configured in the rule that is defined in the route.

If you operate in different regions, you must define 1 route for each region. In addition, you must choose the region where you want to collect global events, and configure that region to collect both types of events.
{: important}

The following table outlines different scenarios that explain where auditing events are collected in your account:

| Event Type              | Scenario                           | Outcome         |
|-------------------------|------------------------------------|-----------------|
| Location-based events   | No routes defined                  | Events are routed to {{site.data.keyword.at_full_notm}}. |
| Location-based events   | 1 route is defined for 1 region with `receive_global_events = false`    | Events, that are generated in the region where the route is defined, are sent to the bucket that is configured. Auditing events that are generated in other regions, where there is no route defined, are routed to {{site.data.keyword.at_full_notm}}. |
| Location-based events   | Routes defined for multiple regions with `receive_global_events = false` | Events, that are generated in the regions where routes are defined, are sent to the bucket that is configured per region. Auditing events that are generated in other regions, where there is no route defined, are routed to {{site.data.keyword.at_full_notm}}. |
| Global events           | No route in the account is defined with `receive_global_events = true` | Global events are sent to {{site.data.keyword.at_full_notm}}. |
| Global events           | 1 route in the account is defined with `receive_global_events = true` | Location-based events, that are generated in the region where the route is defined to collect global events, and global events are sent to the bucket that is configured in the route. Events, that are generated in other regions where routes are defined, are sent to the bucket that is configured per region. Auditing events that are generated in other regions, where there is no route defined, are routed to {{site.data.keyword.at_full_notm}}. |
| Global events           | Multiple routes defined with `receive_global_events = true` | This configuration is not supported. |
{: caption="Table 1. Auditing events collection scenarios" caption-side="top"}


## CLI prerequisites
{: #route-prereqs-cli}
{: cli}

Before you use the the CLI to manage routes, complete the following steps:

1. Identify the endpoint in the region where you plan to configure or manage a route.  For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints#endpoints_api).

2. [Pre-requisite] [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

3. [Pre-requisite] [Install the {{site.data.keyword.atracker_full_notm}} CLI](/docs/atracker?topic=atracker-activity-tracking-cli#activity-tracking-cli-prereq).

4. Log in to the region in the {{site.data.keyword.cloud_notm}} where the instance is running. Run the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)

5. Set the resource group where the instance is running. Run the following command: [ibmcloud target](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_target)

    By default, the `default` resource group is set.

## Creating a route using the CLI
{: #route-create-cli}
{: cli}

Use this command to create a new route for an {{site.data.keyword.atracker_full_notm}} target in a region.

```sh
ibmcloud atracker route create --name <ROUTE_NAME> --target <TARGET> [--receive-global-events] [--region <REGION>] [--output JSON]
```
{: pre}

### Command options
{: #route-create-options}

`--target <TARGET_ID>`
:   The ID or name of the target.

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--name <ROUTE_NAME>`
:   The name to be given to the route.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--receive-global-events`
:   Specifies that the route will receive [global events](/docs/atracker?topic=atracker-event_types#event_types_global).  If not specified, global events will not be sent on the route

`--output JSON`
:   If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #route-create-example}

The following is an example using the **`ibmcloud atracker route create --name my_route --target xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx --receive-global-events`** command.

```text
Route
Name:                    my_route
ID:                      xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
CRN:                     crn:v1:staging:public:atracker:us-south:a/xxxxxxxxxxxxxxxxxxxxxxxxxxxxx::route:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
Receive Global Events:   true
Version:                 0
Rules:                   [*: [b1ea1ad9-71ac-493e-abb1-1261f9110b07]]
Created:                 2021-07-21T18:10:44.456Z
Updated:                 2021-07-21T18:10:44.456Z
```
{: screen}

## Updating a route using the CLI
{: #route-update-cli}
{: cli}

Use this command to update a route for an {{site.data.keyword.atracker_full_notm}} target in a region.  Any specified value that is different from when the route was originally created will be updated to the value specified in the command.

```sh
ibmcloud atracker route update --route <ROUTE> [--name <ROUTE_NAME>] [--receive-global-events ( TRUE | FALSE )] [--target <TARGET>] [--region <REGION>] [--output JSON]
```
{: pre}

### Command options
{: #route-update-options}

`--route <ROUTE>`
:   The name or ID of the route to be updated.

`--target <TARGET>`
:   The ID or name of the target.

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--name <ROUTE_NAME>`
:   The name to be given to the route.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--receive-global-events (TRUE | FALSE)`
:   Specifies that the route will receive [global events](/docs/atracker?topic=atracker-event_types#event_types_global).  If not specified, global events will not be sent on the route

`--output JSON`
:   If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #route-update-example}

The following is an example using the **`ibmcloud atracker route update --route my_route --receive-global-events false`** command.

```text
Route
Name:                    my_route
ID:                      xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
CRN:                     crn:v1:staging:public:atracker:us-south:a/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx::route:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
Receive Global Events:   false
Version:                 1
Rules:                   [*: [b1ea1ad9-71ac-493e-abb1-1261f9110b07]]
Created:                 2021-07-21T18:10:44.456Z
Updated:                 2021-07-21T18:33:48.898Z
```
{: screen}

## Deleting a route using the CLI
{: #route-delete-cli}
{: cli}

Use this command to delete a route for an {{site.data.keyword.atracker_full_notm}} region.

```sh
ibmcloud atracker route rm --route <ROUTE> [--region <REGION>] [--force]
```
{: pre}

### Command options
{: #route-rm-options}

`--route <ROUTE>`
:   The name or ID of the route to be deleted.

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--force`
:   Will delete the route without providing the user with any additional prompt.

`help` | `--help` | `-h`
:   List options available for the command.


### Example
{: #route-rm-example}

The following is an example using the **`ibmcloud atracker route rm --route my_route`** command.

```text
Are you sure you want to remove the route with the route ID xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx [y/N]> y
OK
Route with route ID xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx was successfully removed.
```
{: screen}

The following is an example using the **`ibmcloud atracker route rm --route my_route --force`** command.

This example shows a failed command where the specified route could not be found.
{: note}

```text
FAILED
Something went wrong. Error: No route found with route name - my_route.
```
{: screen}

## Viewing a route using the CLI
{: #route-view-cli}
{: cli}

Use this command to get information about a route for an {{site.data.keyword.atracker_full_notm}} region.

```sh
ibmcloud atracker route get --route [ <ROUTE_ID> | <ROUTE_NAME> ] [--region <REGION>] [--output JSON]
```
{: pre}

### Command options
{: #route-get-options}

`--route <ROUTE_ID>` | `<ROUTE_NAME>`
:   The route ID or name of the route.

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output JSON`
:   If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #route-get-example}

The following is an example using the **`ibmcloud atracker route get --route my_route --output json`** command.

```json
{
  "id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "name": "my_route",
  "crn": "crn:v1:staging:public:atracker:us-south:a/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx::route:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "version": 1,
  "receive_global_events": false,
  "rules": [
    {
      "target_ids": [
        "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
      ]
    }
  ],
  "created": "2021-07-21T18:10:44.456Z",
  "updated": "2021-07-21T18:33:48.898Z"
}
```
{: screen}

## Listing all routes in a region using the CLI
{: #route-list-cli}
{: cli}

Use this command to list all the configured routes for a specific {{site.data.keyword.atracker_full_notm}} region or all {{site.data.keyword.atracker_full_notm}} regions.

```sh
ibmcloud atracker route ls [--region <REGION> | --all-regions ] [--output JSON]
```
{: pre}

### Command options
{: #route-ls-options}

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--all-regions`
:   Specifies the routes for all regions should be listed.  This option cannot be specified if `--region` is specified.

`--output JSON`
:   If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.


### Example
{: #route-ls-example}

The following is an example using the **`ibmcloud atracker route ls --region us-south`** command which returns the routes for all regions.

```text
Name       ID                                     Region     Receive Global Events   Version   Created                    Updated
my_route   xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx   us-south   true                    0         2021-07-21T18:10:44.456Z   2021-07-21T18:10:44.456Z
```
{: screen}


## API routes and actions
{: #target-actions-api}
{: api}

The following table lists the actions that you can run to manage routes:

| Action                     | REST API Method  | API_URL                                          |
|----------------------------|------------------|--------------------------------------------------|
| Create a route            | `POST`           | `<ENDPOINT>/api/v1/routes`              |
| Update a route            | `PUT`            | `<ENDPOINT>/api/v1/routes/<ROUTE_ID>`  |
| Delete a route            | `DELETE`         | `<ENDPOINT>/api/v1/routes/<ROUTE_ID>`  |
| Read a route             | `GET`            | `<ENDPOINT>/api/v1/routes/<ROUTE_ID>`  |
| List all route           | `GET`            | `<ENDPOINT>/api/v1/routes`             |
{: caption="Table 2. Target actions by using the {{site.data.keyword.atracker_full_notm}} REST API" caption-side="top"}

You can use private and public endpoints to manage routes. For more information about the list of `ENDPOINTS` that are available, see [Endpoints](/docs/atracker?topic=atracker-endpoints).

* By default, you can manage routes from the private network. You must use an API endpoint with the following format: `https://private.<region>.atracker.cloud.ibm.com`

* You can also enable public endpoints in a region to manage routes. For more information, see [Managing endpoints](/docs/atracker?topic=atracker-endpoints_manage).

For more information about the REST API, see [Routes](https://{DomainName}/apidocs/atracker-v1#create-route){: external}.
{: note}

## API prerequisites
{: #route-target-prereqs-api}
{: api}

To make API calls to manage routes, complete the following steps:
1. Get an IAM access token. For more information, see [Retrieving IAM access tokens](/docs/atracker?topic=atracker-retrieve-iam-token).
2. Identify the API endpoint in the region where you plan to confige or manage a route. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints#endpoints_api).


## Creating a route using the API
{: #route-create-api}
{: api}

You must [create a target](/docs/atracker?topic=atracker-target#target-create) before you create a route.

You can use the following cURL command to create a route:

```shell
curl -X POST  <ENDPOINT>/api/v1/routes   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"  -d '{
    "name": "ROUTE_NAME",
    "receive_global_events": true,
    "rules": [
      {
        "target_ids": ["TARGET_ID"]
      }
    ]
  }'
```
{: codeblock}

Where

- `ENDPOINT` is the API endpoint in the region where you plan to configure or manage a route. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints#endpoints_api).
- `ROUTE_NAME` is the name of the route. The maximum length of the name is 180 characters and cannot include any of the following special characters:`-`, `.`, `_`, `:`.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

- `TARGET_ID` is the GUID of the target that defines the bucket where auditing events are routed and collected.
- `receive_global_events` indicate the type of events that are collected in the region. When you set `receive_global_events` to true, you are indicating that you want global events and location-based events to go to the target that is configured in the rule that is defined in the route. When you set `receive_global_events` to false, you are indicating that you want location-based events to go to the target that is configured in the rule that is defined in the route.

For example, you can use the following cURL request to create a route in US South that defines how global and US South-location-based events are collected and routed in the account:

```shell
curl -X POST   https://private.us-south.atracker.cloud.ibm.com/api/v1/routes   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"  -d '{
    "name": "my-route",
    "receive_global_events": true,
    "rules": [
      {
        "target_ids": ["281f78a2-d83f-430a-905e-e896f03cb403"]
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
curl -X POST  <ENDPOINT>/api/v1/routes/<route_ID>   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"  -d '{
    "name": "ROUTE_NAME",
    "receive_global_events": true,
    "rules": [
      {
        "target_ids": ["TARGET_ID"]
      }
    ]
  }'
```
{: codeblock}

Where

- `ROUTE_NAME` is the name of the route. The maximum length of the name is 180 characters and cannot include any of the following special characters:`-`, `.`, `_`, `:`.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

- `TARGET_ID` is the GUID of the target that defines the bucket where auditing events are routed and collected.
- `receive_global_events` indicate the type of events that are collected in the region. When you set `receive_global_events` to true, you are indicating that you want global events and location-based events to go to the target that is configured in the rule that is defined in the route. When you set `receive_global_events` to false, you are indicating that you want location-based events to go to the target that is configured in the rule that is defined in the route.


## Deleting a route using the API
{: #route-delete-api}
{: api}

You can use the following cURL command to delete a route:

```text
curl -X DELETE   <ENDPOINT>/api/v1/routes/<ROUTE_ID>   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"
```
{: codeblock}


## Viewing a route using the API
{: #route-view-api}
{: api}

You can use the following cURL command to view 1 route:

```text
curl -X GET   <ENDPOINT>/api/v1/routes/<ROUTE_ID>   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"
```
{: codeblock}

For example, you can run the following cURL request to get informatiomn about a route with ID `7faa6ea6-e564-4fef-93b0-4317a0d27c34`:

```text
curl -X GET   https://private.us-south.atracker.cloud.ibm.com/api/v1/targets/7faa6ea6-e564-4fef-93b0-4317a0d27c34    -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"
```
{: screen}


## Listing all routes in a region using the API
{: #route-list-api}
{: api}

You can use the following cURL command to view all routes:

```text
curl -X GET   <ENDPOINT>/api/v1/routes   -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"
```
{: codeblock}

For example, you can run the following cURL request to get informatiomn about the routes that are defined in US South:

```text
curl -X GET   https://private.us-south.atracker.cloud.ibm.com/api/v1/routes    -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"
```
{: screen}


## HTTP response codes
{: #route-target-rc}
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

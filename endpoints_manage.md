---

copyright:
  years: 2019, 2022
lastupdated: "2022-05-05"

keywords: 

subcollection: atracker
---

{{site.data.keyword.attribute-definition-list}}

# Managing endpoints (API V1)
{: #endpoints_manage}

You can use the the {{site.data.keyword.atracker_full}} CLI or {{site.data.keyword.atracker_full_notm}} REST API to manage private and public endpoints in your account.
{: shortdesc}

The V1 API is deprecated. This CLI and API can only be used while using the {{site.data.keyword.atracker_full_notm}} V1 API.  Once you have [migrated to the V2 API](/docs/atracker?topic=atracker-migrate-resources) this CLI and API can no longer be used.
{: deprecated}

By default, private endpoints are enabled. 

* You cannot disable private endpoints.

* The private endpoint format is as follows:

    ```text
    https://private.<region>.atracker.cloud.ibm.com/api/v1
    ```
    {: codeblock}

* For more information about the list of `ENDPOINTS` that are available, see [Private endpoints](/docs/atracker?topic=atracker-endpoints#endpoints_api-private).

By default, public endpoints are enabled. 

* You can disable public endpoints per region in your account. 

* The public endpoint format is as follows:

    ```text
    https://<region>.atracker.cloud.ibm.com/api/v1
    ```
    {: codeblock}
 
If public and private endpoints are enabled, you can disable a public endpoint by using private or public endpoints.
    
If public endpoints have been disabled, you can only enable public endpoints by using the private endpoint.
{: important}

For more information about the list of `ENDPOINTS` that are available, see [Public endpoints](/docs/atracker?topic=atracker-endpoints#endpoints_api-public).


## API actions
{: #endpoint-actions-api}
{: api}

The following table lists the actions that you can run to manage endpoints:

| Action                     | REST API Method  | API_URL                                          | 
|----------------------------|------------------|--------------------------------------------------|
| Get endpoints that are enabled in a region    | `GET`            | `<ENDPOINT>/api/v1/endpoints`              |
| Update an endpoint in a region                | `PATCH`          | `<ENDPOINT>/api/v1/endpoints`  |
{: caption="Table 1. Endpoints actions by using the {{site.data.keyword.atracker_full_notm}} REST API" caption-side="top"}

For more information on the API, see the [{{site.data.keyword.atracker_full_notm}} reference](https://{DomainName}/apidocs/atracker/atracker-v1){: external}
{: note}

## Prereqs
{: #endpoint-prereqs-cli}
{: cli}

Before you use the the CLI to manage endpoints,complete the following steps:

1. Identify the endpoint in the region you plan to configure.  For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints#endpoints_api).

2. [Pre-requisite] [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

3. [Pre-requisite] [Install the {{site.data.keyword.atracker_full_notm}} CLI](/docs/atracker?topic=atracker-activity-tracking-cli#activity-tracking-cli-prereq).

4. Log in to the region in the {{site.data.keyword.cloud_notm}} where the instance is running. Run the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)

5. Set the resource group where the instance is running. Run the following command: [ibmcloud target](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_target)

    By default, the `default` resource group is set.

## Listing the available endpoints using the CLI
{: #endpoints-manage-list-cli}
{: cli}

Use the following command to list the {{site.data.keyword.atracker_full_notm}} service API endpoints.

```sh
ibmcloud atracker endpoint api ls [--output JSON]
```
{: pre}

### Command options 
{: #endpoint-ls-options}

`--output JSON`
:   If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.
  
### Example
{: #endpoint-ls-example}

The following is an example using the **`ibmcloud atracker endpoint api ls`** command.

```text
Listing the IBM Cloud Activity Tracking service API endpoints....
OK
Region     Public Endpoint                           Private Endpoint
eu-gb      https://eu-gb.atracker.cloud.ibm.com      https://private.eu-gb.atracker.cloud.ibm.com
eu-de      https://eu-de.atracker.cloud.ibm.com      https://private.eu-de.atracker.cloud.ibm.com
us-south   https://us-south.atracker.cloud.ibm.com   https://private.us-south.atracker.cloud.ibm.com
```
{: screen}


## Getting the status of endpoints using the CLI
{: #endpoints-manage-get-cli}
{: cli}

You can use the following command to get information about the public and private endpoints that are enabled in a region when you use the {{site.data.keyword.atracker_full_notm}}:

```sh
ibmcloud atracker endpoint api get [--region <REGION>] [--output JSON]
```
{: pre}

### Command options 
{: #endpoint-get-options}

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output JSON`
:   If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.
  
### Example
{: #endpoint-get-example}

The following is an example using the **`ibmcloud atracker endpoint api get --region us-south`** command.

```text
API endpoints for region us-south
Public URL:                         https://us-south.atracker.cloud.ibm.com
Public Enabled:                     true
Private URL:                        https://private.us-south.atracker.cloud.ibm.com
Private Enabled:                    true

```
{: screen}

## Disabling public endpoints using the CLI
{: #endpoints-manage-disable-cli}
{: cli}

You can disable public endpoints per region in your account.

You can use the following command to disable a public endpoint in a region:

```sh
ibmcloud atracker endpoint api update --public-enabled FALSE [--region <REGION>] [--output JSON] [--force]
```
{: pre}

Before disabling a public endpoint (`--public-enabled FALSE`), make sure your account has access to the private endpoint.  You can do this by running the command `bx account show`.  If `VRF Enabled` is `true` and `Service Endpoint Enabled` is `true` then you have access to the private endpoint.  If you do not have access to the private endpoint, you will be unable to re-enable the public endpoint since private endpoint access is required to re-enable the public endpoint.
{: important}

### Command options 
{: #endpoint-update-disable}

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output JSON`
:   If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`--force`
:   The command will be run without prompting the user whether or not to continue with the command.

`help` | `--help` | `-h`
:   List options available for the command.
  
### Example
{: #endpoint-update-example-false}

The following is an example using the **`ibmcloud atracker endpoint api update --public-enabled false`** command.

```text
Are you sure you want to update the IBM Cloud Activity Tracking service endpoint settings for your account? [y/N]> y
OK
API endpoints for region us-south
Public URL:                         https://us-south.atracker.cloud.ibm.com
Public Enabled:                     false
Private URL:                        https://private.us-south.atracker.cloud.ibm.com
Private Enabled:                    true
```
{: screen}

## Enabling public endpoints using the CLI
{: #endpoints-manage-enable-cli}
{: cli}

You can configure for each region the availability of public endpoints so that you can configure {{site.data.keyword.atracker_full_notm}} resources in your account.

You can use the following command to enable a public endpoint in a region:

```sh
ibmcloud atracker endpoint api update --public-enabled TRUE [--region <REGION>] [--output JSON] [--force]
```
{: pre}

You must have access to a private endpoint to enable a public endpoint. 
{: important}

### Command options 
{: #endpoint-update-enable}

`--region <REGION>` | `-r <REGION>`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--output JSON`
:   If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`--force`
:   The command will be run without prompting the user whether or not to continue with the command.

`help` | `--help` | `-h`
:   List options available for the command.
  
### Example
{: #endpoint-update-example-true}

The following is an example using the **`ibmcloud atracker endpoint api update --public-enabled true`** command.

```text
Are you sure you want to update the IBM Cloud Activity Tracking service endpoint settings for your account? [y/N]> y
OK
API endpoints for region us-south
Public URL:                         https://us-south.atracker.cloud.ibm.com
Public Enabled:                     true
Private URL:                        https://private.us-south.atracker.cloud.ibm.com
Private Enabled:                    true
```
{: screen}

## Getting the status of endpoints using the API
{: #endpoints-manage-get-api}
{: api}

You can use the following cURL command to get information about the public and private endpoints that are enabled in a region when you use the {{site.data.keyword.atracker_full_notm}}:

```shell
curl -X GET <ENDPOINT>/api/v1/endpoints -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json" 
```
{: codeblock}

Where `ENDPOINT` is the API endpoint in the region where you plan to manage {{site.data.keyword.atracker_full_notm}} resources through public endpoints. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints#endpoints_api).



In the response, you get information about all the endpoints in the region:

```json
{
  "api_endpoint": {
    "public_url": "https://us-south.atracker.cloud.ibm.com",
    "public_enabled": true,
    "private_url": "https://private.us-south.atracker.cloud.ibm.com",
    "private_enabled": true
  }
}
```
{: screen}




## Disabling public endpoints using the API
{: #endpoints-manage-disable-api}
{: api}

You can disable public endpoints per region in your account.

You can use the following cURL command to disable a public endpoint in a region:

```text
curl -X PATCH <ENDPOINT>/api/v1/endpoints -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"  -d '{
    "api_endpoint": 
    {
      "public_enabled": false
    }
  }'
```
{: codeblock}

Where 

- `ENDPOINT` is the API endpoint in the region where you plan to manage {{site.data.keyword.atracker_full_notm}} resources through public endpoints. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints#endpoints_api).
- `public_enabled` indicates how to set on or off the availability of public endpoints in the region that is specified in the endpoint URL.


In the response, you get information about all the endpoints in the region:

```json
{
  "api_endpoint": {
    "public_url": "https://us-south.atracker.cloud.ibm.com",
    "public_enabled": false,
    "private_url": "https://private.us-south.atracker.cloud.ibm.com",
    "private_enabled": true
  }
}
```
{: screen}




## Enabling public endpoints using the API
{: #endpoints-manage-enable-api}
{: api}

You can configure for each region the availability of public endpoints so that you can configure {{site.data.keyword.atracker_full_notm}} resources in your account.

You can use the following cURL command to enable a public endpoint in a region:

```shell
curl -X PATCH <ENDPOINT>/api/v1/endpoints -H "Authorization:  $ACCESS_TOKEN"   -H "content-type: application/json"  -d '{
    "api_endpoint": 
    {
      "public_enabled": true
    }
  }'
```
{: codeblock}

Where 

- `ENDPOINT` is the API endpoint in the region where you plan to manage {{site.data.keyword.atracker_full_notm}} resources through public endpoints. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints#endpoints_api).
- `public_enabled` indicates how to set on or off the availability of public endpoints in the region that is specified in the endpoint URL.


In the response, you get information about all the endpoints in the region:

```json
{
  "api_endpoint": {
    "public_url": "https://us-south.atracker.cloud.ibm.com",
    "public_enabled": true,
    "private_url": "https://private.us-south.atracker.cloud.ibm.com",
    "private_enabled": true
  }
}
```
{: screen}



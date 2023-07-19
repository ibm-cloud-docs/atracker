---

copyright:
  years: 2019, 2023
lastupdated: "2023-07-17"

keywords:

subcollection: atracker
---

{{site.data.keyword.attribute-definition-list}}

# Managing endpoints
{: #endpoints_manage_v2}

You can use the the {{site.data.keyword.atracker_full}} CLI or {{site.data.keyword.atracker_full_notm}} REST API to manage private and public endpoints in your account.
{: shortdesc}

You can view the type of endpoints that are available in the account to manage {{site.data.keyword.atracker_short}} by using the [settings API](/docs/atracker?topic=atracker-settings).
{: tip}

## Private endpoints
{: #endpoints_manage_v2_private}

By default, private endpoints are enabled.

- You cannot disable private endpoints.

- The private endpoint format is as follows:

    ```text
    https://private.<region>.atracker.cloud.ibm.com/api/v2
    ```
    {: codeblock}

- For more information about the list of `ENDPOINTS` that are available, see [Private endpoints](/docs/atracker?topic=atracker-endpoints#endpoints_api-private).


## Public endpoints
{: #endpoints_manage_v2_public}

By default, public endpoints are enabled.

- You can disable public endpoints per region in your account.

- The public endpoint format is as follows:

    ```text
    https://<region>.atracker.cloud.ibm.com/api/v2
    ```
    {: codeblock}

For more information about the list of `ENDPOINTS` that are available, see [Public endpoints](/docs/atracker?topic=atracker-endpoints#endpoints_api-public).


## Disabling public endpoints
{: #endpoints_manage_v2_public_disable}

If public and private endpoints are enabled, you can disable a public endpoint by using private or public endpoints.

If public endpoints have been disabled, you can only enable public endpoints by using the private endpoint.
{: important}

See [Enforcing private endpoints to configure Activity Tracker resources](/docs/atracker?topic=atracker-getting-started-mng-endpoints).

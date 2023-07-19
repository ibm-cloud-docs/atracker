---

copyright:
  years: 2019, 2023
lastupdated: "2023-07-17"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Configuring the CLI to manage the {{site.data.keyword.atracker_short}} account configuration
{: #atracker-cli-config}

You must configure your local {{site.data.keyword.atracker_short}} CLI so that you can manage the {{site.data.keyword.atracker_short}} account configuration by using CLI commands.
{: shortdesc}

You must install the latest version of the {{site.data.keyword.atracker_full_notm}} CLI in order to pick up the latest CLI features.

## Step 1. Installing the {{site.data.keyword.atracker_short}} CLI
{: #atracker-cli-config-install}

Complete the following steps to install the {{site.data.keyword.atracker_short}} CLI:

1. [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

2. Get the versions that are available for the `atracker` CLI plugin. Run the following command:

    ```text
    ibmcloud plugin repo-plugins
    ```
    {: pre}

    For example, to get the versions of the {{site.data.keyword.atracker_short}} CLI plugin, run the following command:

    ```text
    ibmcloud plugin repo-plugins | grep atracker
    ```
    {: pre}

    The output of the command will list the versions that are available.

3. Install the CLI plugin in your local system. Run the following command:

    ```text
    ibmcloud plugin install atracker [-v VERSION]
    ```
    {: pre}

    Where `VERSION` is the value of a listed version that is available for the plugin.

    If you already have the {{site.data.keyword.atracker_short}} CLI plugin installed in your local system and you want to update the version of the plugin, run the following command: `ibmcloud plugin update atracker`.


If you want to delete the {{site.data.keyword.atracker_short}} CLI plugin from your local system, run the following command: `ibmcloud plugin delete atracker`.
{: tip}

---

copyright:
  years: 2019, 2022
lastupdated: "2021-09-23"

keywords: 

subcollection: atracker

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Are you getting an error when you try to install the CLI?
{: #troubleshoot-03}
{: troubleshoot}
{: support} 

You cannot install the {{site.data.keyword.atracker_short}} CLI.
{: shortdesc}


Your request fails with an error message that indicates that the plug-in being installed is already used.
{: tsSymptoms}

When you try to install the {{site.data.keyword.atracker_short}} CLI, you get an error in your response:
{: tsCauses}

```text
Namespace name/alias 'at' in the plug-in being installed is already used by a command/alias in the installed plug-in 'activity-tracker'.
```
{: screen}


To resolve the problem, complete the following steps:
{: tsResolve}

1. List the plugins that are available in your local environment.

    Run the following command:

    ```text
    ibmcloud plugin list
    ```
    {: pre}

2. Look for the `activity-tracker` plugin. Then, run the following command to remove it:

    ```text
    ibmcloud plugin uninstall activity-tracker
    ```
    {: pre}

3. Install the {{site.data.keyword.atracker_short}} CLI. Run the following command:

    ```text
    ibmcloud plugin install atracker
    ```
    {: pre}









---

copyright:
  years: 2022, 2024
lastupdated: "2024-01-19"

keywords:

subcollection: atracker


---

{{site.data.keyword.attribute-definition-list}}



# Streaming events to QRadar
{: #qradar-integration}

Stream data from an {{site.data.keyword.at_full_notm}} instance to other corporate tools such as Security Information and Event Management (SIEM) tools like QRadar.
{: shortdesc}

IBM® QRadar® is a network security management platform that provides situational awareness and compliance support. QRadar uses a combination of flow-based network knowledge, security event correlation, and asset-based vulnerability assessment.

When you stream data to QRadar, you can add additional capabilities to the ones provided by the {{site.data.keyword.at_full_notm}} service:
- You can gain visibility into enterprise data across on-premises and cloud-based environments.
- You can identify and prioritize security threats that might affect your organization.
- You can detect vulnerabilities by using Artificial Intelligence (AI) to investigate threats and incidents.

When you enable streaming on an {{site.data.keyword.at_full_notm}} instance, you configure {{site.data.keyword.at_short}} to send data to an {{site.data.keyword.messagehub}} instance. Then, you can configure Kafka Connect to consume the data and forward it to your destination tool. Once the data is persisted within {{site.data.keyword.messagehub}}, you can configure Qradar to create a subscription and take action on log data being streamed.

![QRadar integartion overview](/images/at_qradar.svg "QRadar integration overview"){: caption="QRadar integration" caption-side="bottom"}

Currently, you can only stream up to 1TB of data per day.  ?????
{: note}

IBM QRadar can collect events from multiple log sources by using plug-in files called Device Support Module (DSM).
- A DSM is a code module that parses received events from multiple log sources and converts them to a standard taxonomy format that can be displayed as output. Each type of log source has a corresponding DSM.
- {{site.data.keyword.at_short}} is a log source that you can configure in QRadar by using the [IBM Cloud Activity Tracker DSM](https://www.ibm.com/docs/en/qradar-on-cloud?topic=cloud-activity-tracker){: external} to normalize auditing events into QRadar. The DSM contains the event patterns that are required to identify and parse auditing events from the original format of the event log to the format that QRadar can use.

If you have any regulatory requirement for data residency and compliance needs, you must control the location where {{site.data.keyword.at_short}}, {{site.data.keyword.messagehub}}, Kafka Connect and QRadar are available.
{: important}



## Requirements
{: #qradar-integration-reqs}

- The {{site.data.keyword.at_short}} instance and the {{site.data.keyword.messagehub}} instance must be provisioned in the same account.

- You need 2 service credentials to configure the integration with QRadar:

    - 1 service credential is used by {{site.data.keyword.at_short}} to publish events to the ES topic.

    - 1 service credential is used by QRadar to read events from the topic.

Depending on your license limits, QRadar can read and interpret events from more than 300 log sources. DO WE NEED A SPECIAL LICENSE?
{: important}


## Step 1. Configure a topic in {{site.data.keyword.messagehub}}
{: #qradar-integration-step1}

Consider the following information before you configure a topic in {{site.data.keyword.messagehub}}:
- [Create an {{site.data.keyword.messagehub}} instance](/docs/EventStreams?topic=EventStreams-getting-started).

- Check the limitations of {{site.data.keyword.messagehub}} service plans. For more information, see [Limits and quotas](https://cloud.ibm.com/docs/EventStreams?topic=EventStreams-kafka_quotas).

- To create a topic in {{site.data.keyword.messagehub}}, you must have **manager** role. This role includes the **messagehub.topic.manage** IAM action role that allows an app or user to create or delete topic.

- The credential that {{site.data.keyword.at_short}} uses to publish data in {{site.data.keyword.messagehub}} must have **writer** role. This role includes the **messagehub.topic.write** IAM action role that allows an app or service to write data to 1 or more topics.


Complete the following steps to create an {{site.data.keyword.messagehub}} topic:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

	After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} dashboard opens.

2. Click the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg) &gt; **Resource list**.

3. Look for the {{site.data.keyword.messagehub}} instance that you plan to use, and select it.

4. Select **Topics**.

5. Click **Create a topic**.

    ![Create a topic.](/images/streaming-topic.png "Create a topic"){: caption="Create a topic" caption-side="bottom"}

6. Enter a topic name and click **Next**.

    ![Create a topic name](/images/streaming-topic-1.png "Create a topic name"){: caption="Create a topic name" caption-side="bottom"}

7. Enter the number of partitions and click **Next**.

    One or more partitions make up a topic. A partition is an ordered list of messages. Partitions are distributed across the brokers in order to increase the scalability of your topic. You can also use them to distribute messages across the members of a consumer group.
    {: note}

    ![Enter number of partitions](/images/streaming-topic-2.png "Enter number of partitions"){: caption="Enter number of partitions" caption-side="bottom"}

8.  Select a **Message retention** and click **Create Topic**.

    **Message retention** defines how long messages are retained before they are deleted. If your messages are not read by a consumer within this time, they will be missed.
    {: important}


## Step 2. Create service credentials
{: #qradar-integration-step2}

You need 2 service credentials to configure the integration with QRadar:

    - 1 service credential is used by {{site.data.keyword.at_short}} to publish events to the ES topic.

    - 1 service credential is used by QRadar to read events from the topic.


### Step 2.1. Create the credential to publish events to the ES topic
{: #qradar-integration-step2-1}

Complete the following steps to create 1 service credential that the {{site.data.keyword.at_full_notm}} instance needs to communicate with the {{site.data.keyword.messagehub}} instance:

1. In the {{site.data.keyword.cloud_notm}}, click the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg) &gt; **Resource list**.

2. Look for the {{site.data.keyword.messagehub}} instance that you plan to use, and select it.

3. In the {{site.data.keyword.messagehub}} console, click **Service credentials**.

4. Select **New credential**.

5. Enter a name such as *at-es-integration*, and select the **writer** role.

    ![Create a credential.](/images/streaming-credentials.png "Create a credential"){: caption="Create a credential" caption-side="bottom"}

6. Click **Add**.

To restrict access to 1 topic, complete the following steps:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Service IDS**.

    ![Service IDs](/images/streaming-credentials2.png "Service IDs"){: caption="Service IDs" caption-side="bottom"}

2. Select the service ID.
3. Select **Access policies**.
4. Select the policy and modify it to specify the topic.

    ![Edit Policy](/images/streaming-credentials-2.png "Edit Policy"){: caption="Edit policy" caption-side="bottom"}

    ![Select Role](/images/streaming-credentials-3.png "Select Role"){: caption="Select role" caption-side="bottom"}



### Step 2.2. Create the credential for QRadar to read events from the topic
{: #qradar-integration-step2-2}

Complete the following steps to create 1 service credential that the {{site.data.keyword.at_full_notm}} instance needs to communicate with the {{site.data.keyword.messagehub}} instance:

1. In the {{site.data.keyword.cloud_notm}}, click the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg) &gt; **Resource list**.

2. Look for the {{site.data.keyword.messagehub}} instance that you plan to use, and select it.

3. In the {{site.data.keyword.messagehub}} console, click **Service credentials**.

4. Select **New credential**.

5. Enter a name such as *qradar-es-integration*, and select the **read** role.

    ![Create a credential.](/images/streaming-credentials.png "Create a credential"){: caption="Create a credential" caption-side="bottom"}

6. Click **Add**.

To restrict access to 1 topic, complete the following steps:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Service IDS**.

    ![Service IDs](/images/streaming-credentials2.png "Service IDs"){: caption="Service IDs" caption-side="bottom"}

2. Select the service ID.
3. Select **Access policies**.
4. Select the policy and modify it to specify the topic.

    ![Edit Policy](/images/streaming-credentials-2.png "Edit Policy"){: caption="Edit policy" caption-side="bottom"}

    ![Select Role](/images/streaming-credentials-3.png "Select Role"){: caption="Select role" caption-side="bottom"}



## Step 3. Configure {{site.data.keyword.at_short}} to send events to {{site.data.keyword.messagehub}}
{: #qradar-integration-step3}

### Step 3.1. {{site.data.keyword.at_full_notm}} hosted event search offering
{: #qradar-integration-step3-1}

This information applies only if you use an {{site.data.keyword.at_full_notm}} [hosted event search offering](/docs/activity-tracker?topic=activity-tracker-service_plan).
{: important}

[Configure the connection in Activity Tracker to {{site.data.keyword.messagehub}}](/docs/activity-tracker?topic=activity-tracker-streaming-configure).

### Step 3.2. {{site.data.keyword.at_full_notm}}
{: #qradar-integration-step3-2}

TO BE ADDED ????????




## Step 4. Configure QRadar
{: #qradar-integration-step4}

Complete the following steps:

### Step 4.1. Get the latest DSM
{: #qradar-integration-step4-1}

Download and install a device support module (DSM) that supports the log source.

If automatic updates are not enabled, download the most recent versions of the RPMs from the [IBM support website](https://www.ibm.com/mysupport/s/?language=en_US){: external}:
- Kafka Protocol RPM
- DSM Common RPM
- IBM Cloud® Activity Tracker DSM RPM

Complete the following steps to add the {{site.data.keyword.at_short}} DSM into QRadar:
1. Download the DSM RPM file from the [IBM support website](https://www.ibm.com/mysupport/s/?language=en_US){: external}.
2. Copy the RPM file to QRadar.
3. Using SSH, log in to the QRadar host as the root user.
4. Go to the directory that includes the downloaded file.
5. Type the following command:

    ```text
    yum -y install <rpm_filename>
    ```
    {: pre}

6. Restart the following services so the DSM is picked by QRadar:

    This step must be done in a controlled window to avoid disruption of Qradar.
    {: important}

    ```text
    systemctl restart ecs-ec
    ```
    {: pre}

    ```text
    systemctl restart ecs-ec-ingress
    ```
    {: pre}

    ```text
    systemctl restart tomcat
    ```
    {: pre}

7. Log in to QRadar.

8. On the Admin tab, click **Deploy Changes**.

Uninstalling a Device Support Module (DSM) is not supported in QRadar.
{: important}


### Step 4.2. Add the {{site.data.keyword.at_short}} log source
{: #qradar-integration-step4-2}

If automatic discovery is supported for the DSM, wait for QRadar to automatically add the log source to your list of configured log sources.

If automatic discovery is not supported for the DSM, manually create the {{site.data.keyword.at_short}} log source configuration on the QRadar Console. Complete the following steps:


Complete the following steps to add manually the {{site.data.keyword.at_short}} log source in QRadar:

1. Login to QRadar.
2. From the **Menu**, select **Admin**. The *Admin* UI opens.
3. In the *Data Sources* section, select **Log Sources**. The Log Source management App opens.

    ![Log Sources](/images/qradar-1.png "Log Sources"){: caption="Log sources" caption-side="bottom"}

    If you get the message that `you must use the QRadar Log Source Management app`, click **Launch** to continue.

    ![QRadar Log Source Management app message](/images/qradar-2.png "QRadar Log Source Management app message"){: caption="Example message" caption-side="bottom"}

4. In the *Log Source management App*, select **Log Sources**.

    ![QRadar Log Source Management app](/images/qradar-3.png "QRadar Log Source Management app"){: caption="Select Log Sources" caption-side="bottom"}

5. Click **Add New Log Source**. Then, select **Single Log Source** to add {{site.data.keyword.at_short}}.

    ![Add log source](/images/qradar-4.png "Add log source"){: caption="Add a log source" caption-side="bottom"}

6. Select the *Log Source Type*. In the search bar, enter **{{site.data.keyword.at_short}}**. Then, select **Step 2: Select Protocol Type**.

    ![Select log source type](/images/qradar-5.png "Select log source type"){: caption="Select the type of log source" caption-side="bottom"}

7. Select **Apache Kafka** as the protocol type. Then, select **Step 3: Configure Log Source Parameters**.

    ![Select the protocol type](/images/qradar-6.png "Select the protocol type"){: caption="Select the protocol type" caption-side="bottom"}

8. Configure the log source parameters.

    - Enter a name and a description for the logs source.

    - Enable the log source in QRadar.

    - Choose the groups that this logs source belongs too. Choose **UBA: Trusted Log Source**. IBM QRadar User Behavior Analytics (UBA) analyzes user activity to detect malicious insiders and determine if a user's credentials have been compromised.

    - Change the *Credibility* to 8.

    - Disable **Coalescing events**.

    - Enable **Store Event Payloads**.

    - Select **Step 4: Configure Protocol Parameters**.

    ![Select log source type](/images/qradar-7.png "Select log source type"){: caption="Select the log source type" caption-side="bottom"}

    ![Select log source type](/images/qradar-8.png "Select log source type"){: caption="Select the log source type" caption-side="bottom"}

9. Configure the protocol parameters.

    -  In the field *Log Source Identifier*, enter a name. The name must be unique. The name can be the same as the log source name. However, if you configure multiple {{site.data.keyword.at_short}} log sources, identify the first log source as `ibmactivitytracker1` and the second log source as `ibmactivitytracker2`, for example.

    - In the field *Bootstrap Server List*, enter the list of bootstrap servers that you can get from the `kafka_brokers_sasl` property in the QRadar service credential. The format of 1 host is `<hostname/ip>:<port>`. You can specify multiple servers by using a comma separated list, such as `kafka-1.mh-xxxx-0000.eu-de.containers.appdomain.cloud:9093,kafka-0.mh-xxxx-0000.eu-de.containers.appdomain.cloud:9093,kafka-2.mh-xxxx-0000.eu-de.containers.appdomain.cloud:9093`.

    - Enter the *Consumer group* for the log source. For example, enter `auditing-events`.

    - Select **List Topics** for the *Topic Subscription Method*.

    - Enter the topic name in the *Topic List* parameter.

    - Enable **Use SASL Authentication** so you can enter the user ID and password. When you use SASL authentication without Client Authentication, a copy of the server's certificate is required to be placed in `/opt/qradar/conf/trusted_certificates/`.

    - Enter **token** for the *SASL Username*.

    - Enter the value of the *password* property from the QRadar service credential for the *SASL Password*.

     ![Configure protocol parameters part1](/images/qradar-9.png "Configure protocol parameters part1"){: caption="Step 1: Configure protocol parameters" caption-side="bottom"}

      ![Configure protocol parameters part2](/images/qradar-10.png "Configure protocol parameters part2"){: caption="Step 2: Configure protocol parameters" caption-side="bottom"}

10. Click **Finish**.

    You should see your {{site.data.keyword.at_short}} log source listed and enabled.

    ![Log source enabled](/images/qradar-11.png "Log source enabled"){: caption="Enable log source" caption-side="bottom"}

11. Return to the QRadar console. You will find that there are undeployed changes.

    Click **View details** to see what is pending to deploy.

    Click **Deploy changes** to update QRadar qith the new log source.

    ![Undeployed changes](/images/qradar-12.png "Undeployed changes"){: caption="Undeployed changes" caption-side="bottom"}




### Log source groups
{: #log_source_groups}

You can categorize your log sources into groups to efficiently view and track your log sources. For example, you might group your log sources by functional purpose, physical location, or business unit association.
You can also use log source groups in searches and rules, instead of listing the log sources to which the search or rule applies.
You must have administrative access to create, edit, or delete groups. For more information about user
roles, see the IBM QRadar Administration Guide.
Creating a log source group
When you create log source groups, you can drag groups in the navigation tree to change the organization
of the tree items.
Procedure
1. Click the Admin tab.
2. In the Data Sources section, click Log Source Groups.
3. From the navigation tree, select the group where you want to create a new group, and then click New Group.
4. In the Group Properties window, enter a name and description. The name can be up to 255 characters in length and is case-sensitive. The description can be up to 255 characters in length.
5. Click OK.
6. To change the location of the new group, click the group and drag the folder to your chosen location in the navigation tree.
7. To edit the group name or description, select the log source group and then click Edit.

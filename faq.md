---

copyright:
  years: 2019, 2024
lastupdated: "2024-01-19"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}

# FAQs
{: #faq}

Frequently asked questions about {{site.data.keyword.atracker_short}}.
{: shortdesc}

## What are the different ways to manage auditing events?
{: #faq_0}
{: faq}

{{site.data.keyword.atracker_short}} offers 2 different ways to manage auditing events in an {{site.data.keyword.cloud_notm}} account. You can use {{site.data.keyword.at_short}}, an IAM enabled service, to manage auditing events through instances that you provision in each {{site.data.keyword.cloud_notm}} region where you operate. Alternatively, you can use {{site.data.keyword.atracker_short}}, a platform service, to manage auditing events at the account-level by configuring targets and routes that define where auditing data is routed. {{site.data.keyword.atracker_short}} can only route events that are generated in [supported regions](/docs/atracker?topic=atracker-regions). Other regions, where {{site.data.keyword.atracker_short}} is not available, continue to manage events by using {{site.data.keyword.atracker_short}} hosted event search.

{{site.data.keyword.at_short}} routes location-based auditing events to an {{site.data.keyword.at_short}} instance in the region where they are generated and routes global auditing events to the {{site.data.keyword.at_short}} instance that is provisioned in Frankfurt.

{{site.data.keyword.atracker_short}} routes events based on the location that is specified in the `logSourceCRN` field included in the event. You can define a target, the resource where events are routed to, in any {{site.data.keyword.atracker_short}} supported region. However, the target resource can be located in any region where that type of target is supported, in the same account or in a different account. You can define rules to determine where auditing events are to be routed by configuring 1 or more routes in the account. You can define rules for managing global events and location-based events that are generated in regions where {{site.data.keyword.atracker_short}} is supported.

The following table outlines the options to configure {{site.data.keyword.atracker_short}} per region:

| Geo                   | Region                   | {{site.data.keyword.atracker_short}} hosted event search | {{site.data.keyword.atracker_short}} |
|-----------------------|--------------------------|----------------------------------------------|--------------------------------|
| `Asia Pacific`        | `Chennai (in-che)`       | ![Checkmark icon](images/checkmark-icon.svg) | |
| `Asia Pacific`        | `Tokyo (jp-tok)`         | ![Checkmark icon](images/checkmark-icon.svg) | |
| `Asia Pacific`        | `Sydney (au-syd)`        | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) |
| `Asia Pacific`        | `Osaka (jp-osa)`         | ![Checkmark icon](images/checkmark-icon.svg) | |
| `Europe`              | `Frankfurt (eu-de)`      | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) |
| `Europe`              | `London (eu-gb)`         | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) |
| `North America`       | `Dallas (us-south)`      | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) |
| `North America`       | `Washington (us-east)`   | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) |
| `North America`       | `Toronto (ca-tor)`       | ![Checkmark icon](images/checkmark-icon.svg) | |
| `South America`       | `Sao Paulo (br-sao)`     | ![Checkmark icon](images/checkmark-icon.svg) | |
{: caption="Table 1. Configuration options" caption-side="bottom"}


## What targets should I use based on my compliance needs?
{: #faq_1}
{: faq}

There are two options available depending on your compliance needs:

* If you require Financial Services Validation.
* If you required PCI, SOC2, Privacy Shield and HIPAA compliance.

### Financial Services Validated status
{: #faq_1_finserv}

If you're the account owner, you can enable your {{site.data.keyword.cloud}} account to be Financial Services Validated, which means your account stores and manages regulated financial services information. Services that are designated as *{{site.data.keyword.cloud_notm}} for Financial Services Validated* leverage the industry’s highest levels of encryption certification, provide preventive and compensatory controls for financial services regulatory workloads, multi-architecture support and proactive, and automated security. For more information on how to enable your account, see [Enabling your account to use Finantial Services Validated products](/docs/account?topic=account-enabling-fs-validated).

The *{{site.data.keyword.cloud_notm}} for Financial Services Validated* designation is available for services that are operating in the Dallas (`us-south`), Washington DC (`us-east`), Frankfurt (`eu-de`), and London (`eu-gb`) [multizone regions](#x9774820){: term}.

Use {{site.data.keyword.atracker_short}} to manage auditing events in your account whe requiring Financial Services Validated status.
{: tip}

### PCI, SOC2, Privacy Shield and HIPAA compliance
{: #faq_1_nonfinserv}

{{site.data.keyword.at_short}} offers ready to run event search offerings that you can use to expedite your time to greater insights. You can choose to retain your events for 7, 14, or 30 days. In addition, a 30 day HIPAA compliant offering is also available. For more information about these offerings, see [Service plans](/docs/activity-tracker?topic=activity-tracker-service_plan).

Use {{site.data.keyword.at_short}} hosted event search offerings to manage events using a UI or to manage auditing events that are not routed by {{site.data.keyword.atracker_short}}.
{: tip}

## What are the different options to collect and monitor auditing events in my account?
{: #faq_2}
{: faq}

To collect and monitor activity in your account, you must configure the {{site.data.keyword.atracker_short}} service in your account by using any of the following methods:

- You can [configure {{site.data.keyword.atracker_short}}](/docs/atracker?topic=atracker-getting-started) to manage auditing events in your account while maintaining Financial Services Validated status.

    The target resource must be an {{site.data.keyword.cos_full}} bucket that is available in the same account where the auditing events are generated.

    You can also use a bucket that is available in a different account from where auditing events are generated.

    You must follow and comply with the Financial Services Validated requirements for buckets to maintain Financial Services Validated status.
    {: important}

- You can [configure the {{site.data.keyword.atracker_short}} hosted event search offering](/docs/activity-tracker?topic=activity-tracker-getting-started) to manage auditing events through the UI, or if you need PCI, SOC2, Privacy Shield or HIPAA compliance.

- You can configure {{site.data.keyword.atracker_short}} to define the {{site.data.keyword.atracker_short}} hosted event search instances where auditing events are routed.

    The {{site.data.keyword.atracker_short}} hosted event search instances can be located in the same account where auditing events are generated or in a different account.


## Where can I find the list of Cloud services that generate {{site.data.keyword.atracker_short}} events?
{: #faq_3}
{: faq}

You can find information about the services that generate audit events and send those to {{site.data.keyword.atracker_short}} in the following documentation topic: [Cloud services](/docs/atracker?topic=atracker-cloud_services_atracker).

## Where can I find the actions that a service generates?
{: #faq_4}
{: faq}

You can link to the list of events that each service generates from the following documentation topic: [Cloud services](/docs/atracker?topic=atracker-cloud_services_atracker).

## Where can I find the events that a service generates?
{: #faq_5}
{: faq}

In {{site.data.keyword.atracker_short}}, you can differentiate events by scope as [global events](/docs/atracker?topic=atracker-event_types#event_types_global) or [location-based events](/docs/atracker?topic=atracker-event_types#event_types_location), and by operational impact as management or data events.

First, you need to check if you need to configure your service, upgrade your plan, or both to be able to collect {{site.data.keyword.at_short}} events.

* Management events are collected automatically for most services except Watson services that require a paid plan.

    If you are looking for Watson {{site.data.keyword.atracker_short}} events, check your plan and make sure you have a service plan that includes them.

* Data events are collected automatically for most services except the following ones:

    AppID requires a paid plan and you opting in.

    Cloud Object Storage requires that you enable them by bucket.

    Cloudant Database requires that you enable them per service instance.

Then, you need to determine the location of the events based on scope.

For {{site.data.keyword.at_short}} event viewing, global events are available through the {{site.data.keyword.at_short}} instance in Frankfurt. To view global events, you must provision an instance of the {{site.data.keyword.at_full_notm}} service in Frankfurt.

For {{site.data.keyword.atracker_short}}, global events are collected in the region that you configure. To find those events, you must find the route that is configured in 1 region of your account to collect global events.

For location-based events, you need to check the following scenarios to determine the {{site.data.keyword.atracker_short}} instance where the events are available for analysis:

* Scenario 1: The service is provisioned in a location where the {{site.data.keyword.atracker_short}} service is available.

    1. Identify the location where your service is provisioned.

    2. Check whether the {{site.data.keyword.atracker_short}} service is available in that region. See [Locations](/docs/atracker?topic=atracker-regions).

    3. For {{site.data.keyword.at_short}} event viewing, check that you have an {{site.data.keyword.atracker_short}} instance provisioned in the same location where your service is provisioned. For {{site.data.keyword.atracker_short}}, check that you have a target and a route defined in that region.

* Scenario 2: The service is provisioned in a location where the {{site.data.keyword.at_full_notm}} service is not available.

    1. Identify the location where your service is provisioned.

    2. Check the [Cloud services locations](/docs/atracker?topic=atracker-regions) to identify the {{site.data.keyword.atracker_short}} instance where events are available.




## Can I choose the region where global events are collected?
{: #faq_6}
{: faq}


With {{site.data.keyword.atracker_short}} you can configure a route to send your global events to a target that sends the events to any supported destination:

* [An {{site.data.keyword.cos_full_notm}} bucket](/docs/atracker?topic=atracker-getting-started-target-cos)

* [An {{site.data.keyword.at_full_notm}} instance](/docs/atracker?topic=atracker-getting-started-target-logdna)

* [An {{site.data.keyword.messagehub_full}} topic](/docs/atracker?topic=atracker-getting-started-target-event-streams)



## I cannot find auditing events in my account. Where can I find them?
{: #faq_7}
{: faq}

In {{site.data.keyword.cloud_notm}}, auditing events are generated automatically with the exception of some services that require additional configuration or a specific service plan. For more information about these services, see [Enabling Activity Tracker events](/docs/atracker?topic=atracker-events-opt-in).

There are 2 ways by which you can access the auditing events in your account. For more information see [Collecting events.](/docs/atracker?topic=atracker-events_collect)

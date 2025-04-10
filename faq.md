---

copyright:
  years:  2021, 2025
lastupdated: "2025-04-10"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}

# FAQ for {{site.data.keyword.atracker_full_notm}}
{: #faq}

Frequently asked questions about {{site.data.keyword.atracker_full}}.
{: shortdesc}



## What targets should I use based on my compliance needs?
{: #faq_1}
{: faq}



### Financial Services Validated status
{: #faq_1_finserv}

If you're the account owner, you can enable your {{site.data.keyword.cloud}} account to be Financial Services Validated, which means your account stores and manages regulated financial services information. Services that are designated as *{{site.data.keyword.cloud_notm}} for Financial Services Validated* leverage the industry’s highest levels of encryption certification, provide preventive and compensatory controls for financial services regulatory workloads, multi-architecture support and proactive, and automated security. For more information on how to enable your account, see [Enabling your account to use Finantial Services Validated products](/docs/account?topic=account-enabling-fs-validated).

The *{{site.data.keyword.cloud_notm}} for Financial Services Validated* designation is available for services that are operating in the Dallas (`us-south`), Washington DC (`us-east`), Frankfurt (`eu-de`), and London (`eu-gb`) [multizone regions](#x9774820){: term}.

Use {{site.data.keyword.atracker_short}} to manage auditing events in your account whe requiring Financial Services Validated status.
{: tip}





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

First, you need to check if you need to configure your service, upgrade your plan, or both to be able to collect activity tracking events.

* Management events are collected automatically for most services except Watson services that require a paid plan.

    If you are looking for Watson activity tracking events, check your plan and make sure you have a service plan that includes them.

* Data events are collected automatically for most services except the following ones:

    AppID requires a paid plan and you opting in.

    Cloud Object Storage requires that you enable them by bucket.

    Cloudant Database requires that you enable them per service instance.




## Can I choose the region where global events are collected?
{: #faq_6}
{: faq}


With {{site.data.keyword.atracker_short}} you can configure a route to send your global events to a target that sends the events to any supported destination:

* [An {{site.data.keyword.cos_full_notm}} bucket](/docs/atracker?topic=atracker-getting-started-target-cos)



* [An {{site.data.keyword.logs_full_notm}} instance](/docs/atracker?topic=atracker-getting-started-target-cloud-logs&interface=ui)

* [An {{site.data.keyword.messagehub_full}} topic](/docs/atracker?topic=atracker-getting-started-target-event-streams)



## I cannot find auditing events in my account. Where can I find them?
{: #faq_7}
{: faq}

In {{site.data.keyword.cloud_notm}}, auditing events are generated automatically with the exception of some services that require additional configuration or a specific service plan. For more information about these services, see [Enabling Activity Tracker events](/docs/atracker?topic=atracker-events-opt-in).

There are 2 ways by which you can access the auditing events in your account. For more information see [Collecting events.](/docs/atracker?topic=atracker-events_collect)

---

copyright:
  years: 2021, 2024
lastupdated: "2024-11-08"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}

# Understanding data portability for {{site.data.keyword.atracker_full_notm}}
{: #data-portability}

Data portability involves a set of tools and procedures that enable customers to export the digital artifacts that are needed to implement similar workload and data processing on different service providers or on-premises software. It includes procedures for copying and storing the service customer content, including the related configuration that is used by the service to store and process the data, on the customer's own location.
{: shortdesc}

## Responsibilities
{: #data-portability-responsibilities}

{{site.data.keyword.cloud_notm}} services provide interfaces and instructions to guide the customer to copy and store the service customer content, including the related configuration, on their own selected location.

The customer is responsible for the use of the exported data and configuration for data portability to other infrastructures, which includes:

- The planning and execution for setting up alternative infrastructure on different cloud providers or on-premises software that provide similar capabilities to the {{site.data.keyword.IBM_notm}} services.
- The planning and execution for the porting of the required application code on the alternative infrastructure, including the adaptation of customer's application code, deployment automation, and so on.
- The conversion of the exported data and configuration to the format that's required by the alternative infrastructure and adapted applications.

For more information about your responsibilities for {{site.data.keyword.atracker_full_notm}}, see [Understanding your responsibilities when using {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-shared-responsibilities).

## Exporting data
{: #data-portability-export}

The {{site.data.keyword.atracker_full_notm}} service is an {{site.data.keyword.cloud_notm}} service that routes activity tracking event data. It does not retain this data so no data can be exported from the {{site.data.keyword.atracker_full_notm}} service itself.

Export of data routed through {{site.data.keyword.atracker_full_notm}} might be possible through the configured [target services](/docs/atracker?topic=atracker-about#about-locations) receiving the activity tracking event data.



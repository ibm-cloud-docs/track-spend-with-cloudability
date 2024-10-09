---

copyright:
  years: 2020
lastupdated: "2024-10-09"

keywords:

subcollection: track-spend-with-cloudability

content-type: faq

---



{{site.data.keyword.attribute-definition-list}}



# FAQs for {{site.data.keyword.IBM_notm}} Cloudability Enablement
{: #ibm-cloud-enablement-faqs}



Review the FAQs for {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture. To view all FAQs for {{site.data.keyword.cloud}}, see our [FAQ library](/docs/faqs).
{: shortdesc}

## What is {{site.data.keyword.IBM_notm}} Cloudability?
{: #what-is-ibm-cloudability}
{: faq}

{{site.data.keyword.IBM_notm}} Cloudability (formerly Apptio Cloudability) is a cloud financial management platform designed to help organizations optimize their cloud spending and usage across multiple cloud providers. It provides visibility into cloud costs, resource utilization, and performance metrics, allowing businesses to track, analyze, and forecast their cloud expenditures. The tool offers features such as cost allocation, budget management, rightsizing recommendations, and customizable reporting to help companies maximize their cloud investments and align cloud usage with business objectives. To learn more visit the [{{site.data.keyword.IBM_notm}} Cloudability product page](https://www.apptio.com/products/cloudability/)

## How does the Cloudability access the my billing data?
{: #how-does-cloudability-access-my-billing-data}
{: faq}

{{site.data.keyword.IBM_notm}} Cloudability accesses your account billing data through the use of [billing exports](/docs/billing-usage?topic=billing-usage-exporting-your-usage) to a Cloud Object Storage bucket. This deployable architecture creates the access policies to an IBM Cloudability owned service id to be able to read the data in this bucket. Only the bare minimum access is granted to IBM Cloudability.

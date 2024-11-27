---

copyright:
  years: 2024
lastupdated: "2024-11-27"

keywords:

subcollection: track-spend-with-cloudability

---

{{site.data.keyword.attribute-definition-list}}

# Overview
{: #overview}

The {{site.data.keyword.IBM_notm}} Cloudability Enablement [deployable architecture](#x10293733){: term} is the easiest way to add your {{site.data.keyword.cloud_notm}} account or [enterprise](/docs/enterprise-management?topic=enterprise-management-what-is-enterprise) to {{site.data.keyword.IBM_notm}} Cloudability (formally Apptio Cloudability). With your {{site.data.keyword.cloud_notm}} account added to Cloudability, you can use it to track and analyze your {{site.data.keyword.cloud_notm}} expenses.
{: shortdesc}

## What is {{site.data.keyword.IBM_notm}} Cloudability?
{: #what-is-cloudability}

{{site.data.keyword.IBM_notm}} Cloudability is a cloud financial management platform that provides visibility and optimization capabilities across all major cloud providers. The tool offers features such as cost allocation, budget management, rightsizing recommendations, and customizable reporting. With the help of {{site.data.keyword.IBM_notm}} Cloudability, you can help maximize your companies cloud investments and align cloud usage with business objectives.
Visit the [{{site.data.keyword.IBM_notm}} Cloudability product page](https://www.apptio.com/products/cloudability/) to learn more.

## Why use the Cloudability Enablement deployable architecture (DA)?
{: #why-use}

The {{site.data.keyword.IBM_notm}} Cloudability Enablement DA performs the necessary steps to start tracking your {{site.data.keyword.cloud_notm}} expenditure within Cloudability. These are some of the key benefits:

1. **Faster and more consistent deployment**: DA's run as a pre-configured template using terraform. This ensures that the necessary steps are performed to synchronize configuration between the different components, which reduces configuration errors.

2. **Reduced complexity**: By abstracting away many infrastructure details, this DA reduces the number of inputs. This means that less of your time is spent gathering information and synchronizing information between the two services. Instead, your {{site.data.keyword.cloud_notm}} connection to {{site.data.keyword.IBM_notm}} Cloudability can be managed in a central place.

3. **Security and Compliance**: Follows {{site.data.keyword.cloud_notm}}'s recommended best practices, which are maintained through regular version updates to help ensure that your workloads are secure and compliant.

4. **Customization**: The DA inputs default to the recommended best practices, however, using the various [configuration options](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-configure) the deployment can be adjusted to meet your business needs.

## What actions does this deployable architecture (DA) perform?
{: #what-actions}

![Architectural Diagram](../deployable-reference-architectures/terraform-ibm-cloudability-onboarding/cloudability-all-inclusive-onboarding.svg){: caption="Figure 1. Architecture Diagram" caption-side="bottom"}

The {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture performs the following steps to add your {{site.data.keyword.cloud_notm}} account to Cloudability:

1. Creates or uses an existing [resource group](/docs/account?topic=account-rgs&interface=ui) in the target {{site.data.keyword.cloud_notm}} account
2. Creates the following services in the target resource group and location:
    - {{site.data.keyword.cos_full_notm}} Bucket in a newly created or existing {{site.data.keyword.cos_full_notm}} Instance
    - {{site.data.keyword.keymanagementserviceshort}} encryption key is used for [encrypting the Object Storage bucket](/docs/cloud-object-storage?topic=cloud-object-storage-encryption) with your own key by using a newly created or existing {{site.data.keyword.keymanagementserviceshort}} instance
3. [Enables daily billing report exports](/docs/account?topic=account-exporting-your-usage&interface=ui#enable-export-usage) to the newly created storage bucket
4. Grants Cloudability access to read the billing reports from the {{site.data.keyword.cos_full_notm}} bucket
    - *If the account is an enterprise*: Grants Cloudability access to read the list of child accounts in the enterprise
    - Cloudability access is controlled with a custom role so only the minimum access is given.
5. Adds the {{site.data.keyword.cloud_notm}} account or enterprise to {{site.data.keyword.IBM_notm}} Cloudability

## Getting started
{: #getting-started}

If you don't have access to an {{site.data.keyword.IBM_notm}} Cloudability account then you will need to [create one](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-accessing-cloudability). Once you have access to a Cloudability account, then [configure access to run the deployable architecture](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-planning), and [deploy the cloud resources](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-deploy-cloud).

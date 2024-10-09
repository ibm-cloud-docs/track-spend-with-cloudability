---

copyright:
  years: 2024
lastupdated: "2024-10-09"

keywords:

subcollection: track-spend-with-cloudability

---


{{site.data.keyword.attribute-definition-list}}

# Overview
{: #overview}

The {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture is the easiest way to add your {{site.data.keyword.Bluemix_notm}} account or enterprise to {{site.data.keyword.IBM_notm}} Cloudability (formally Apptio Cloudability). Once enabled your {{site.data.keyword.Bluemix_notm}} billing data will be imported into {{site.data.keyword.IBM_notm}} Cloudability within 24 hours where you will be able to aggregate your cloud spend across multiple {{site.data.keyword.Bluemix_notm}} accounts or Cloud providers.
{: shortdesc}

## What is {{site.data.keyword.IBM_notm}} Cloudability?
{: #what-is-cloudability}

{{site.data.keyword.IBM_notm}} Cloudability is a cloud financial management platform that provides visibility and optimization capabilities across all major cloud providers. It supports FinOps practices with three tiers:

- **Cloudability Essentials**: Establishes FinOps fundamentals, like multi-cloud visibility and rightsizing.
- **Cloudability Standard**: Adds features like unit economics, cost allocation, and forecasting.
- **Cloudability Premium**: Includes full features and {{site.data.keyword.IBM_notm}} Turbonomic capabilities for advanced optimization.

Visit the [{{site.data.keyword.IBM_notm}} Cloudability product page](https://www.apptio.com/products/cloudability/) to learn more.

Before the {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture can add your {{site.data.keyword.Bluemix_notm}} account to {{site.data.keyword.IBM_notm}} Cloudability, you will first need to have access to a Cloudability account. If you do not have a Cloudability account you can [request a demo or pricing quote](https://www.apptio.com/cloudability-demo-pricing-request/) or [start a free trial](https://www.apptio.com/cloudability-free-trial-request/) to get started.

## What actions does this deployable architecture (DA) perform?
{: #what-actions}

A [deployable architecture](/docs/secure-enterprise?topic=secure-enterprise-understand-module-da#what-is-da)(DA) is cloud automation for deploying a common architectural pattern that combines one or more cloud resources. The {{site.data.keyword.IBM_notm}} Cloudability Enablement DA performs the cloud resources and configurations necessary to add an {{site.data.keyword.Bluemix_notm}} account to {{site.data.keyword.IBM_notm}} Cloudability location. This DA performs the following steps:

1. Creates or uses an existing resource group in the target {{site.data.keyword.Bluemix_notm}} account
2. Creates the following services in the target resource group and location:
    - Cloud Object Storage Bucket in a newly created or existing Cloud Object Storage Instance
    - Key Protect Key (Used for encryption of a Cloud Object Storage bucket) in a newly created or existing Key Protect instance
3. [Enables daily billing reports exports](https://cloud.ibm.com/docs/billing-usage?topic=billing-usage-exporting-your-usage&interface=ui#enable-export-usage) to the newly created storage bucket
4. Grants Cloudability access to read the billing reports from the Cloud Object Storage bucket
    - *If the account is an enterprise*: Grants cloudability access to read the list of child accounts in the enterprise
    - Cloudability access is controlled with a custom role so only the minimum access is given.
5. Adds the {{site.data.keyword.Bluemix_notm}} account/enterprise to {{site.data.keyword.IBM_notm}} Cloudability

## Why should you use this deployable architecture (DA)?
{: #why-use}

The {{site.data.keyword.IBM_notm}} Cloudability Enablement DA is the fastest and best option for adding your {{site.data.keyword.Bluemix_notm}} account to {{site.data.keyword.IBM_notm}} Cloudability. Below are some of the key benefits:

1. **Faster more consistent deployment**: DA's run as a pre-configured template performing all of required steps to synchronize configuration between the different components which reduces configuration errors.

2. **Reduced complexity**: By abstracting away many infrastructure details, this DA reduces the number of required inputs. This means less of your time is spent gathering information and it allows you to manage configuration from a central place.

3. **Security and Compliance**: Follows {{site.data.keyword.Bluemix_notm}}'s recommended best practices for security and compliance and allows you to easily update the configuration template as new best practices become available.

4. **Customization**: While providing a standardized starting point, there are many [configuration options](#configuration) possible, to allow for specific business needs customization.

## Next Steps
{: #next-steps}

Start by creating your [IAM credentials to run your DA](#plan) to run the DA and gathering your [{{site.data.keyword.IBM_notm}} Cloudability api key](#plan) for the {{site.data.keyword.IBM_notm}} Cloudability Enablement DA to enable your account.

---

copyright:
  years: 2024
lastupdated: "2024-11-15"

keywords:

subcollection: track-spend-with-cloudability

content-type: faq

---



{{site.data.keyword.attribute-definition-list}}



# FAQs for {{site.data.keyword.IBM_notm}} Cloudability Enablement
{: #ibm-cloud-enablement-faqs}



Review the FAQs for {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture. To view all FAQs for {{site.data.keyword.cloud}}, see the [FAQ library](/docs/faqs).
{: shortdesc}

## How does the Cloudability access {{site.data.keyword.cloud_notm}} billing data?
{: #how-does-cloudability-access-my-billing-data}
{: faq}

{{site.data.keyword.IBM_notm}} Cloudability accesses your account billing data by using [billing exports](https://test.cloud.ibm.com/docs/account?topic=account-exporting-your-usage&interface=ui) to a Object Storage bucket. This deployable architecture creates the access policies to an {{site.data.keyword.IBM_notm}} Cloudability owned service ID to be able to read the data in this bucket. Only the bare minimum access is granted to {{site.data.keyword.IBM_notm}} Cloudability.

## How long until {{site.data.keyword.cloud_notm}} billing data is visible in Cloudability?
{: #how-long-until-I-see-my-data}
{: faq}

Once the deployable architecture has been deployed your {{site.data.keyword.cloud_notm}} billing data should be imported into {{site.data.keyword.IBM_notm}} Cloudability within 24 hours.

## How to import historical {{site.data.keyword.cloud_notm}} billing data into Cloudability?
{: #adding-historical-data}
{: faq}

Open a support case to request that as much as a year of [historical billing data be added to your bucket](/docs/account?topic=account-exporting-your-usage&interface=ui#access-historical-data).

## Why is there no option configuration option to enable immutable storage on the {{site.data.keyword.cos_full_notm}} bucket?
{: #why-no-immutable-storage}

{{site.data.keyword.cos_full_notm}} supports the [immutable storage](/docs/cloud-object-storage?topic=cloud-object-storage-immutable) of objects in your bucket. However, the manifest files, which are added as part of [billing exports](https://test.cloud.ibm.com/docs/account?topic=account-exporting-your-usage&interface=ui) are not immutable and are updated daily even if the configuration parameter [`overwrite_existing_reports`](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-configure#cos-billing-exports-config) is set to `false`.


## How to use an existing {{site.data.keyword.cos_full_notm}} instance?
{: #existing-object-storage-instance}
{: faq}

[Configure the deployable architecture](/docs/secure-enterprise?topic=secure-enterprise-config-project&interface=ui#project-input-values) to use an existing {{site.data.keyword.cos_short}} instance by entering the {{site.data.keyword.cos_full_notm}} [CRN](#x9494304){: term} in the input field `existing_cos_instance_id` and set `create_cos_instance` to `false`. See the [{{site.data.keyword.cos_short}} configuration reference](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-configure#cos-billing-exports-config) for more details.

## How to use an existing Key Protect instance?
{: #existing-key-protect-instance}
{: faq}

[Configure the deployable architecture](/docs/secure-enterprise?topic=secure-enterprise-config-project&interface=ui#project-input-values) to use an existing Key Protect instance by entering the instance ID in the input field `existing_kms_instance_guid` and set `create_key_protect_instance` to `false`. See the [configuration reference](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-configure#cos-bucket-encryption-config) for more details.

## What permissions does Cloudability need to integrate with my account?
{: #what-access-for-cloudability}
{: faq}

Only the minimum required access is granted to Cloudability to access the billing data within the account. This is controlled using [iam custom roles](/docs/account?topic=account-custom-roles&interface=ui&q=iam+custom+roles&tags=account). The privileges granted to these custom roles include:


| Service Name | Permissions | Reason |
|------|-------------|-------------|
| {{site.data.keyword.cos_full_notm}} | * iam.policy.read \n * cloud-object-storage.object.head \n * cloud-object-storage.object.get_uploads \n * cloud-object-storage.object.get \n * cloud-object-storage.bucket.list_bucket_crn \n * cloud-object-storage.bucket.head \n * cloud-object-storage.bucket.get | To list the objects in the bucket and to read the contents of the billing report files.|
| IBM Enterprise | * iam.policy.read \n * enterprise.account.retrieve \n * enterprise.account-group.retrieve | For enterprise accounts only. Used to read the names of the child accounts and account groups within the enterprise account. |
{: caption="Table 1. Cloudability access permissions" caption-side="bottom"}

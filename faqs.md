---

copyright:
  years: 2024
lastupdated: "2024-11-27"

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

Once the deployable architecture is deployed, your {{site.data.keyword.cloud_notm}} billing data should be imported into {{site.data.keyword.IBM_notm}} Cloudability within 24 hours.

## Once my {{site.data.keyword.cloud_notm}} account is added to Cloudability, how many months of data is ingested into Cloudability?
{: #adding-historical-data}
{: faq}

By default, the current month of IBM Cloud billing reports is added to Cloudability. If additional months of data are need, then [open a support case with IBM Cloud Billing](/docs/account?topic=account-exporting-your-usage&interface=ui#access-historical-data) to request that the historical cost data be sent to your billing reports Object Storage bucket. You can request up to 12 months of historical data. Once the files are in the bucket, [contact the Cloudability Support team](https://www.ibm.com/mysupport/s/createrecord/NewCase) for your historical data to be ingested into Cloudability.

## Can I configure immutable storage on the {{site.data.keyword.cos_full_notm}} bucket?
{: #why-no-immutable-storage}

No, [immutable storage](/docs/cloud-object-storage?topic=cloud-object-storage-immutable) of objects is not a supported feature of [billing exports](https://test.cloud.ibm.com/docs/account?topic=account-exporting-your-usage&interface=ui) to Object Storage. Billing exports updates a manifest file, which is what Cloudability reads. The updating of objects is not allowed when immutable storage is enabled.


## How to use an existing {{site.data.keyword.cos_full_notm}} instance?
{: #existing-object-storage-instance}
{: faq}

[Configure the deployable architecture](/docs/secure-enterprise?topic=secure-enterprise-config-project&interface=ui#project-input-values) to use an existing {{site.data.keyword.cos_short}} instance by entering the {{site.data.keyword.cos_full_notm}} [CRN](#x9494304){: term} in the input field `existing_cos_instance_id` and set `create_cos_instance` to `false`. See the [{{site.data.keyword.cos_short}} configuration reference](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-configure#cos-billing-exports-config) for more details.

## Can I use an existing Key Protect instance with the DA?
{: #existing-key-protect-instance}
{: faq}

Yes, you can [configure the deployable architecture](/docs/secure-enterprise?topic=secure-enterprise-config-project&interface=ui#project-input-values) to use an existing Key Protect instance by entering the instance ID in the input field `existing_kms_instance_guid` and set `create_key_protect_instance` to `false`. To avoid a conflict, it may also be necessary to skip the creation of the authorization policy between Key Protect and Object Storage using the variable `skip_iam_authorization_policy` if an authorization policy exists. See the [configuration reference](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-configure#cos-bucket-encryption-config) for more details.

## How often does Cloudability fetch/ingest new Cost and Usage data?
{: #how-often}
{: faq}

The billing reports are updated in the Object Storage bucket by IBM Cloud Billing once a day. Cloudability fetches the data from the bucket in the same day.

## What permissions does Cloudability need to integrate with my account?
{: #what-access-for-cloudability}
{: faq}

Only the minimum required access is granted to Cloudability to access the billing data within the account. This access is controlled by using [iam custom roles](/docs/account?topic=account-custom-roles&interface=ui&q=iam+custom+roles&tags=account). The privileges granted to these custom roles include:


| Service Name | Permissions | Reason |
|------|-------------|-------------|
| {{site.data.keyword.cos_full_notm}} | * iam.policy.read \n * cloud-object-storage.object.head \n * cloud-object-storage.object.get_uploads \n * cloud-object-storage.object.get \n * cloud-object-storage.bucket.list_bucket_crn \n * cloud-object-storage.bucket.head \n * cloud-object-storage.bucket.get | To list the objects in the bucket and to read the contents of the billing report files.|
| IBM Enterprise | * iam.policy.read \n * enterprise.account.retrieve \n * enterprise.account-group.retrieve | For enterprise accounts only. Needed for reading the names of the child accounts and account groups within the enterprise account. |
{: caption="Table 1. Cloudability access permissions" caption-side="bottom"}


## Why does my costs in Cloudability not match my invoice for months before June 2024?
{: #cost-mismatch-prior-to-june-2024}
{: faq}

There may be a discrepancy between your invoiced amount from IBM Cloud and what appears in Cloudability for the data before June 2024. This discrepancy is because the tiered pricing amount on your invoice is for all instances in your account, while the [resource instance usage](/docs/billing-usage?topic=billing-usage-exporting-your-usage&interface=ui#instances-CSV-version-1-2) file, that is read by Cloudability, did not share the tiered pricing for multiple instances. This issue applies only to [data added historically](#adding-historical-data) before the fix was applied on June 1st, 2024.

## Why don't my costs in Cloudability match my IBM Cloud invoiced amount?
{: #cost-mismatch-invoice}
{: faq}

The IBM Cloud billing data used by Cloudability is from the [usage reports](https://cloud.ibm.com/docs/account?topic=account-viewingusage), which may not reflect your [invoiced amount](/docs/account?topic=account-managing-invoices). To learn more, see the tutorial, "[how to reconcile usage and invoice files?](/docs/enterprise-management?topic=enterprise-management-tutorial-reconcile-invoice)" or visit the [FAQ for invoices page](/docs/account?topic=account-invoice-faq) to review the following topics:

* [Why does my usage not match my invoice?](/docs/account?topic=account-invoice-faq#usage-not-match-invoice)
* [Can my usage differ from what's reflected on my invoice?](/docs/account?topic=account-invoice-faq#invoice-usage-differ)

## Why does the cost for a past month in Cloudability not match a usage report that I recently downloaded?
{: #cost-mismatch-usage}
{: faq}

Sometimes, the costs that are viewed in Cloudability for a previous month may not match a recently downloaded [Resource Instance Usage report](/docs/billing-usage?topic=billing-usage-exporting-your-usage&interface=ui#instances-CSV-version-1-2). The main reason for the mismatch is because usage for a service was submitted after the billing month closed. As an example, usage was submitted on the 1st of the month for the previous month. In this case, the billing report that is submitted to Cloudability for the last day of the month does not include this usage amount. However, a recently downloaded usage report for a past month includes the updated amount.

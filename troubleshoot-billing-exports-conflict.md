---

copyright:
  years: 2025
lastupdated: "2025-01-09"

keywords: question about {{site.data.keyword.IBM_notm}} Cloudability Enablement

subcollection: track-spend-with-cloudability

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do I see a `billing_report_snapshot_instance` conflict in the deployment logs of the DA?
{: #troubleshoot-billing_report_snapshot_instance-conflict}
{: troubleshoot}

You can only [export your account's usage data](/docs/account?topic=account-exporting-your-usage&interface=ui) to a single Cloud Object Storage bucket. If your account is already configured to export usage data to a Cloud Object Storage bucket then deployment of the Cloudability Enablement deployable architecture will fail.
{: shortdesc}

The Schematics or Project logs from the {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture contains an error message similar to the following:
{: tsSymptoms}

```log
Error: ---
id: terraform-3a35498d
summary: 'CreateReportsSnapshotConfigWithContext failed: Duplicate config'
severity: error
resource: ibm_billing_report_snapshot
operation: create
component:
 name: github.com/IBM-Cloud/terraform-provider-ibm
 version: 1.71.3
---

 with module.billing_exports[0].ibm_billing_report_snapshot.billing_report_snapshot_instance,
 on modules/billing-exports/main.tf line 78, in resource "ibm_billing_report_snapshot" "billing_report_snapshot_instance":
 78: resource "ibm_billing_report_snapshot" "billing_report_snapshot_instance" {
```
{: pre}

[Billing exports](/billing/settings) is already enabled in the account corresponding to the [IAM authorization](https://cloud.ibm.com/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-planning#cloudability-iam-prereqs). This could be from a separate deployment of the Cloudability Enablement deployable architecture, the Cloudability provided terraform script, or created manually by a member in the account.
{: tsCauses}


If there is an existing Project configuration that created the billing exports and this is not desired then the recommended approach is to [undeploy](/docs/secure-enterprise?topic=secure-enterprise-remove-resources&interface=ui#delete-resource-without-project) the resources from the existing Project configuration and redeploy the newly created configuration of the Cloudability Enablement deployable architecture.
{: tsResolve}

If the billing exports were manually created, then the recommended approach is to [disconnect the Object Storage bucket](/docs/account?topic=account-exporting-your-usage&interface=ui#disconnect-exporting-your-usage) and remove the corresponding Billing to Object Storage [service authorization](/docs/account?topic=account-serviceauth&interface=ui#remove-auth). Once removed, [re-run the Cloudability deployable architecture](/docs/secure-enterprise?topic=secure-enterprise-deploy-project&interface=ui#deploy-config-copy) to re-create the service authorization and re-enable billing exports.

---

copyright:
  years: 2025
lastupdated: "2025-06-27"

keywords: question about {{site.data.keyword.IBM_notm}} Cloudability Enablement

subcollection: track-spend-with-cloudability

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why are `ibm_cbr_rule` failing to be created by terraform?
{: #troubleshoot-cbr-rule-fail-to-create}
{: troubleshoot}

The IBM Projects validation or deployment is failing and after viewing the schematics logs there are errors related to the `ibm_cbr_rule` rule failing to be created. This is typically caused by access permissions or conflicts in the cbr name.
{: shortdesc}

The deployment of the {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture failed with a similar error message in the schematics logs:
{: tsSymptoms}

```log
| Error: ---
| id: terraform-a84dad64
| summary: 'CreateZoneWithContext failed: The request could not be authorized.'
| severity: error
| resource: ibm_cbr_zone
| operation: create
| component:
|   name: github.com/IBM-Cloud/terraform-provider-ibm
|   version: 1.79.2
| ---
|
|
|   with module.cbr_zone_cloudability.ibm_cbr_zone.cbr_zone[0],
|   on .terraform/modules/cbr_zone_cloudability/modules/cbr-zone-module/main.tf line 14, in resource "ibm_cbr_zone" "cbr_zone":
|   14: resource "ibm_cbr_zone" "cbr_zone" {
```
{: pre}

This error is due to Schematics not being authorized to perform the creation of the cbr_zone.
{: tsCauses}

The recommended approach is to add the necessary access policies to the User, Trusted Profile or Service ID associated with the Project to create the cbr zones.
{: tsResolve}

The following access roles are required to create the necessary CBR zones:

* Schematics - Administrator
* Context-based Restrictions - Editor
* Key Protect - Administrator
* Object Storage - Administrator

Review the planning section for the complete list of [required access policies](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-planning#required-policies).

Once access has been granted, re-deploy the project to have schematics create the context-based restrictions. If the issue continues, [open a case](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-help-and-support) in the {{site.data.keyword.cloud_notm}} support center.

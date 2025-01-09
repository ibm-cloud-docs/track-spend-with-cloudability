---

copyright:
  years: 2025
lastupdated: "2025-01-09"

keywords: question about {{site.data.keyword.IBM_notm}} Cloudability Enablement

subcollection: track-spend-with-cloudability

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is Cloudability account verification failing?
{: #troubleshoot-cldy-verification-failed}
{: troubleshoot}

The IBM Cloud account is added to Cloudability by the deployable architecture (DA), but verification is failing. Verification may take a little longer or it may need to be skipped when running the DA.
{: shortdesc}

Running verification on the IBM Cloud account on the [IBM Cloud vendor credentials page](https://app.apptio.com/cloudability#/credentials/ibm){: external} shows an error. Additionally, the schematics logs within IBM Cloud from the deployment of the {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture contains an error message similar to the following:
{: tsSymptoms}

```log
Error: after 20 attempts, last error: verification was not successful: [error] - Permission to pull cost data is missing

  with module.cloudability_onboarding[0].data.cloudability_account_verification.ibm_account[0],
  on ../../modules/cloudability-onboarding/main.tf line 94, in data "cloudability_account_verification" "ibm_account":
  94: data "cloudability_account_verification" "ibm_account" {
```
{: pre}


Despite the error message indicating missing permissions, if the deployment reached this step then the permissions to pull the cost data are in place. The most likely cause of this error is that the billing files are not in place yet. This issue occurs more commonly when an account is removed from Cloudability and then re-added.
{: tsCauses}

The issue can often be resolved by performing the account verification at a later time. Account verification can be done manually within the [Cloudability vendor credentials](https://app.apptio.com/cloudability#/credentials/ibm){: external} or by redeploying the configuration.
{: tsResolve}

Alternatively, account verification is not an essential step for the deployment and can be disabled in the DA configuration so that the DA runs cleanly.  To disable verification visit the **Optional** tab of the DA configuration settings and set `skip_verification` to **true** and then re-run the deployment.

If it takes more than 24 hours and the account cannot be verified then [request help](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-help-and-support).



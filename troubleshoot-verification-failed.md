---

copyright:
  years: 2024
lastupdated: "2024-12-03"

keywords: question about {{site.data.keyword.IBM_notm}} Cloudability Enablement

subcollection: track-spend-with-cloudability

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why did Cloudability account verification fail?
{: #troubleshoot-cldy-verification-failed}
{: troubleshoot}

The account may still be configured correctly, but verification may have to be skipped or tried again later.
{: shortdesc}

The deployment of the {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture failed with the following error message in the schematics logs:
{: tsSymptoms}

```log
Error: after 20 attempts, last error: verification was not successful: [error] - Permission to pull cost data is missing

  with module.cloudability_onboarding[0].data.cloudability_account_verification.ibm_account[0],
  on ../../modules/cloudability-onboarding/main.tf line 94, in data "cloudability_account_verification" "ibm_account":
  94: data "cloudability_account_verification" "ibm_account" {
```
{: pre}


Despite what the error message indicates, if the deployment reached this step then the permissions to pull the cost data are in place. The most likely cause of this error is that the billing files are not in place yet. This issue occurs more commonly when an account is removed from Cloudability and then re-added.
{: tsCauses}

The issue can often be resolved by performing the account verification later. Account verification can be done manually within the [Cloudability vendor credentials](https://app.apptio.com/cloudability#/credentials/ibm) or by redeploying the configuration.
{: tsResolve}

Alternatively, account verification can be disabled in the DA configuration since it is not an essential step for the deployment. In the `Optional` settings of the configuration, set `skip_verification` to `true` and then re-run the deployment.

If it takes more than 24 hours and the account cannot be verified then [request help](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-help-and-support).

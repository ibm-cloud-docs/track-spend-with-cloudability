---

copyright:
  years: 2025
lastupdated: "2025-01-09"

keywords: question about {{site.data.keyword.IBM_notm}} Cloudability Enablement

subcollection: track-spend-with-cloudability

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do I see an internal server error in the deployment logs of the Cloudability Enablement DA?
{: #troubleshoot-cldy-internal_server_error}
{: troubleshoot}

Communication to {{site.data.keyword.IBM_notm}} Cloudability could be unavailable or an error occurred within Cloudability.
{: shortdesc}

The deployment of the {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture failed with a similar error message in the schematics logs:
{: tsSymptoms}

```log
module.cloudability_onboarding[0].restapi_object.cloudability_ibm_account: Creating...
Error: unexpected response code '500': {"error":{"status":500,"code":"internal_server_error","messages":["Our technical team has been notified"],"uniqueid":"e570ffbf-a773-11ef-aa33-f2f915150f75","typeid":"40726d7ff9191c93c01453fd11566d75","traceid":"e547fc0a-a773-11ef-aa33-f2f915150f75"}}


  with module.cloudability_onboarding[0].restapi_object.cloudability_ibm_account,
  on modules/cloudability-onboarding/main.tf line 38, in resource "restapi_object" "cloudability_ibm_account":
  38: resource "restapi_object" "cloudability_ibm_account" {
```
{: pre}


This error is often because of an issue in the handling of the request to add the {{site.data.keyword.cloud_notm}} account to Cloudability.
{: tsCauses}

Sometimes the {{site.data.keyword.cloud_notm}} account is successfully added to Cloudability even though an error was returned. So, first check whether the account was added within Cloudability on the [{{site.data.keyword.IBM_notm}} vendor credentials page](https://app.apptio.com/cloudability#/credentials/ibm){: external}.
{: tsResolve}

If the account does exist, then the recommended approach is to delete the {{site.data.keyword.cloud_notm}} account from Cloudability and redeploy the DA configuration to add the account. Deploying through the DA ensures that the vendor configurations  are set correctly within Cloudability.

If the deployment does not add the {{site.data.keyword.cloud_notm}} account to Cloudability then the terraform state for adding the Cloudability account may exist and needs to be removed. You can remove the state by using the following {{site.data.keyword.cloud_notm}} CLI command:

```bash
ibmcloud schematics workspace state rm --id $WORKSPACE_ID --address 'module.cloudability_onboarding[0].restapi_object.cloudability_ibm_account'
```
{: pre}

The `$WORKSPACE_ID` is the ID of the workspace, which can be viewed by using `ibmcloud schematics workspace list`.

If the error still occurs, then the adding of the {{site.data.keyword.cloud_notm}} account to Cloudability through the deployable architecture can be disabled.
Before version `1.0.21` disabling the connection to Cloudability is done by setting the `cloudability_api_key` parameter in the **Required** tab to `__NULL__`. After version `1.1.0`, set the `cloudability_auth_type` parameter in the **Required** tab to `Manual`. Next, redeploy the deployable architecture, which skips the adding of the account to Cloudability since it was added in the previous run. If the issue continues, [open a case](/docs/track-spend-with-cloudability?topic=track-spend-with-cloudability-help-and-support) in the {{site.data.keyword.cloud_notm}} support center.

If the {{site.data.keyword.cloud_notm}} account is not visible within Cloudability, then [open a support case](https://www.ibm.com/mysupport/s/createrecord/NewCase) in [{{site.data.keyword.IBM_notm}} Support](https://www.ibm.com/mysupport/s/).

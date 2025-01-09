---

copyright:
  years: 2025
lastupdated: "2025-01-09"

keywords: question about {{site.data.keyword.IBM_notm}} Cloudability Enablement

subcollection: track-spend-with-cloudability

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do I see a Cloudability account conflict in the deployment logs of the DA?
{: #troubleshoot-cldy-account-conflict}
{: troubleshoot}

The conflict is because the {{site.data.keyword.cloud_notm}} account exists in the Cloudability account before deployment.
{: shortdesc}

The deployment of the {{site.data.keyword.IBM_notm}} Cloudability Enablement deployable architecture failed with a similar error message in the schematics logs:
{: tsSymptoms}

```log
Error: unexpected response code '409': {"error":{"status":409,"code":"conflict","messages":["Conflict","A credential for this organization and account already exists."],"uniqueid":"3d36e9d8-90a9-11ef-b8df-9624b4132c80","typeid":"317197432da0a6add4fa95c86d8f35d5","traceid":"3d056f28-90a9-11ef-b8df-9624b4132c80"}}

  with module.cloudability_onboarding[0].restapi_object.cloudability_ibm_account,
  on modules/cloudability-onboarding/main.tf line 38, in resource "restapi_object" "cloudability_ibm_account":
  38: resource "restapi_object" "cloudability_ibm_account" {
```
{: pre}


This error is often because the {{site.data.keyword.cloud_notm}} account exists in Cloudability. The existing integration could have been added manually or by another deployment of the DA.
{: tsCauses}

The recommended approach is to delete the existing {{site.data.keyword.cloud_notm}} account from {{site.data.keyword.IBM_notm}} Cloudability and re-run the DA configuration to add the account. Deploying through the DA ensures that the vendor configurations  are set correctly within Cloudability.
{: tsResolve}

Alternatively, the existing configuration can be manually updated within Cloudability to match the configuration outputs and the adding of the {{site.data.keyword.cloud_notm}} account to Cloudability through the deployable architecture can be disabled.
Before version `1.0.21` this is done by setting the `cloudability_api_key` parameter in the **Required** tab to `__NULL__`. After version `1.1.0` set the `cloudability_auth_type` parameter in the **Required** tab to `Manual`. Next, redeploy the deployable architecture, which skips the adding of the account to Cloudability since it was added in the previous run.
Next, redeploy the deployable architecture, which skips the adding of the account to Cloudability since it was already added from the previous run.
